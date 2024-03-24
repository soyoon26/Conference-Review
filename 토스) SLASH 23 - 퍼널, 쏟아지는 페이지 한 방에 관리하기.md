[퍼널:쏟아지는 페이지 한 방에 관리하기](https://www.youtube.com/watch?v=NwLWX2RNVcw&list=PL1DJtS1Hv1PiGXmgruP1_gM2TSvQiOsFL&index=5)

[코드](https://github.com/toss/slash/tree/main/packages/react/use-funnel)

1.  목록 페이지와 상세 페이지의 조합으로 이루어진 상태
2.  단일 페이지 - 한 화면 내에서 상호작용(지도)
3.  설문조사 - 여러 페이지들을 통해 상태를 수집하고 결과 페이지를 보여주는 형태(mbti검사)

퍼널 : 유저가 서비스에 들어와 최종 목표지점에 이르기까지 조금씩 이탈해 '깔대기'를 비롯한 말

---

응집도, 추상화, 시각화로 개선

1.여러가지 파일을 만든 후 router.push로 다음 페이지로 이동시킴
세 페이지로 떨어져있으니 전역상태를 이용하기

```
const [registerData, updateRegisterData] = useGlobalSate(registerData)
```

- 아쉬운점
  1. 페이지 흐름이 흩어져 있음 : 3개의 파일을 넘나들며 router.push 코드를 따라가야 함
  2. 한가지 목적을 위한 상태가 흩어져 있음 : 집주소에서 호출하는 '고객등록 API'에서 쓰이는 데이터는 서로 다른 페이지에서 전역 상태를 통해 수집하고 있음 -> 상태를 사용하는 곳과 수집하는 곳이 다름 , 수정해야 할때는 앱 전체를 대상으로 디버깅을 해야 함

### 응집도 개선하기

: 연관된 코드는 가까운 곳에 배치하자

#### RegisterData 지역 상태 만들기

```
const [registerData, setRegisterData] = useState()
```

먼저 가입퍼널 페이지 만들고 registerData라는 상태 만들기
전역 상태가 아닌 지역상태 !!

```
const [step,setStep] = useState<"가입방식"|"주민번호"|"집주소"|"가입성공">("가입방식")
```

step이라는 상태 만들어 어느 UI로 보여줘야 하는지 저장

```
const [registerData, setRegisterData] = useState()
const [step,setStep] = useState<"가입방식"|"주민번호"|"집주소"|"가입성공">("가입방식")

return (
	<main>
    	<가입방식/>}
        <주민번호/>}
        <집주소/>}
        <가입성공step/>}
    <main/>
)
```

-> 각각 컴포넌트로 만들어 가입 퍼널에 모두 넣기

```
const [registerData, setRegisterData] = useState()
const [step,setStep] = useState<"가입방식"|"주민번호"|"집주소"|"가입성공">("가입방식")

return (
	<main>
    	{step === "가입방식" && <가입방식 onNext={(data) => setStep("주민번호") />}
        {step === "주민번호" && <주민번호 onNext={() => setStep("집주소") />}
        {step === "집주소" && <집주소 onNext={async() => setStep("가입성공") />}
        {step === "가입성공" && <가입성공Step />}
        }
    <main/>
)

```

step상태에 따라 각 UI컴포넌트를 조건부 렌더링함, 각 UI에서 "다음"버튼을 누를 때 step상태를 원하는 UI로 업데이트해줌
즉, step의 이동은 상위에서 관리해 UI의 흐름을 한 곳에서 관리

![](https://velog.velcdn.com/images/for24ng/post/84ed7a4b-bcc0-469e-ab17-8eda09e8efc8/image.png)

![](https://velog.velcdn.com/images/for24ng/post/0a634c80-82f6-43a4-b66e-82aa18b51e3c/image.png)

다른 퍼널에서도 재사용 => 가능한 라이브러리로 묶어 보내기

### 라이브러리로 추상화하기

step과 관련된 코드 묶어내기

```
<Step if={step === "가입방식}>
	<가입방식 onNext={()=> setStep("주민번호")} />
<Show/>

//구현
function Show({if, children}) {
	if (if === true) {
    	return children
    }
     return null
  }
```

-> 조건에 맞으면 이 컴포넌트를 보여줘라
if로 조건문 넘겨주고 퍼널스텝이니 Step으로 명명함

```
return (
	<main>
    	<Step if = {step === "가입방식"}>
        	<가입방식 onNext={() => setStep("주민번호")}/>
        <Step/>
        <Step if = {step === "주민번호"}>
        	<가입방식 onNext={() => setStep("집주소")}/>
        <Step/>
    </main>
    )
```

![](https://velog.velcdn.com/images/for24ng/post/161001fb-9116-4086-be1e-40a6eeb572d9/image.png)

if도 내부로 옮기면 name만 남음
하지만 step컴포넌트가 현재 퍼널의 step을 알고 있어야 함
=> 가입 퍼널에서 관리하던 step상태도 내부 로직으로 옮기기

#### useFunnel 훅 생성

![](https://velog.velcdn.com/images/for24ng/post/0bdce98d-43f9-4e5d-8068-43cb63ddd4e3/image.png)

상태를 담은 함수를 만들기 위해 커스텀 훅을 만들어 줌- 퍼널 관리
: 훅 내부로 step상태를 옮기고 Step컴포넌트로 받은 name프로퍼티와 현재 Step이 동일하면 Step컴포넌트 렌더링함

![](https://velog.velcdn.com/images/for24ng/post/24732b02-b7f1-4a2b-964d-10a3c09252ba/image.png)

원본 코드에 적용

토스 라이브러리에 useFunnel에 공개되어있다 !!
또한, - mermaid라이브러리 사용 => Funnel Debugger로 흐름을 체크할 수 있음 이후 공개될 예정 ..

1초만에 파악할 수 없는 페이지 흐름

#### 발표 내용 정리

1. 퍼널
2. 페이지 흐름, 상태를 응집시켜놓으면 유지보수에 편리
3. 라이브러리로 추상화하면 생산성이 높아지고 기능 추가가 편함
4. 개발자 경험 개선 가능

느낀 점 🧂
: 지금 하고 있는 프로젝트에 적용해야겠다는 생각이 계속 들었다! 열시미 영상을 멈추고 코드 보고 그러고 있었는데 깃에 공개되어있다니 좀 더 코드를 뜯어 볼 생각이다. 유지보수가 굉장히 중요한데 개발자에게 좀 더 적합하게 바뀌니까 역시 많이 배워야 겠다는 생각이 든다!! 보면서 계속 놀랐던 컨퍼런스〰
