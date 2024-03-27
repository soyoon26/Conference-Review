[솔로스타의 React렌더링](https://youtu.be/eBDj0B0HbEQ?si=PaYzVib_7cqpqqDi)

보고 좋아서 정리 ㅋㅋ

### 렌더링이란

![](https://velog.velcdn.com/images/for24ng/post/c1f39517-a2d2-444d-a66b-ff68dc0b0d98/image.png)

Render: 함수가 호출되는 것
만약 함수가 3번 호출된다면: 렌더링이 3번 된다.

개발자는 함수만 짜면 됨 ! 트리모양으로 구조화 가능

![](https://velog.velcdn.com/images/for24ng/post/17274408-7450-41b8-a389-ad01c98dbc0c/image.png)

Fiber Node: 저장하는 공간
이렇게 렌더링된 결과는 Virtual Dom(객체)임
Real Dom에 반영이 되면 웹 페이지에 그려짐

### 리-렌더링

App 컴포넌트에 useState를 추가
초기값을 Fiber Node에 저장함
나머지는 렌더링이 완료됨
![](https://velog.velcdn.com/images/for24ng/post/7e628173-202f-4aa9-9de2-4754901975aa/image.png)

버튼을 누르면 emotion이 변경되고 리렌더링이 일어남

즉, setEmotion은

- 상태를 변경
- 리-렌더링

App을 다시 호출 -> Fiber Node에 저장했던 값을 가지고 와서 재사용함

### 리-렌더링 최적화

무거운 컴포넌트가 생긴다면?
상태를 변경하더라도 모두 리렌더링해야 함 : 부담스러움

따라서, React.memo를 사용해야 함 : 메모이제이션 활용
재사용 가능

조건에 따라 리렌더링하기도 함

#### 메모이제이션 방법

![](https://velog.velcdn.com/images/for24ng/post/1a610f38-535e-4d84-b735-badf0af585a1/image.png)

React.memo를 씌우면 됨

하지만 count값을 다르게 주면 리렌더링하게 됨
who와 handleClick을 prop으로 넘겨준다면?
: 이전에 주었던 who와 다르다면? - 참조가 다르기 때문에 다르다고 판단

#### useMemo와 useCallback을 같이 활용하면 해결

![](https://velog.velcdn.com/images/for24ng/post/727cebba-6bac-4577-9fbd-2505b97ab44b/image.png)

who와 handleClick은 FiberNode에서 가지고 옴
하지만 count를 다르게 준다면 리렌더링됨

### 재조정

: 이전 렌더링 결과와 현재 렌더링 결과를 비교하고 변경된 부분을 갱신하는 작업

- Case1 : 리-렌더링 후 엘리먼트가 달라졌을 때
- Case2 : 리-렌더링 후 동일한 엘리먼트들의 순서가 달라졌을 때

![](https://velog.velcdn.com/images/for24ng/post/dc2a9fe3-732b-473c-83db-ab3705d0ae41/image.png)
![](https://velog.velcdn.com/images/for24ng/post/9cf4c4d2-8ace-48ad-a5a3-ffe7de3749f5/image.png)

Case1: 버튼을 추가한다면 변경 - 다시 App 호출

댓글목록 component추가
안녕하세요에 좋아요를 누르더라도 다른 댓글의 Fiber Node에 좋아요가 되지 않음 => key로 해결 \_ 매핑
![](https://velog.velcdn.com/images/for24ng/post/c2e340fc-5cc3-4ab7-861d-63779c0172d3/image.png)

![](https://velog.velcdn.com/images/for24ng/post/097b782e-7e1d-4ca0-a8ab-44f5a59493cd/image.png)

Case2 : 리-렌더링 후 동일한 엘리먼트들의 순서가 달라졌을 때

---

🥨 :
하고 있는 프로젝트의 렌더링이 너무 무거워지는 느낌이라 useMemo에 대한 이해가 더 필요해서 찾아보다가 발견한 영상 !
보고나니 이해가 너무 잘 된다.
useCallback도 같이 사용해봐야겠다.
