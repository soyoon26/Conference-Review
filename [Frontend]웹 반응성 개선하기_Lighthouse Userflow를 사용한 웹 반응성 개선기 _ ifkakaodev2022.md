1. 웹 성능이란?
   성능측정도구 필요, 성능 개선 가이드 제공
   하지만 Load -> Interaction
2. 웹 반응성
   Interface가 빠르게 반응하는지
   ![](https://velog.velcdn.com/images/for24ng/post/17c447ad-a65f-45e6-87d3-c3f425755caf/image.png)

3. 웹 반응성 지표
   TBT(Total Blocking Time), INP(Interaction to Next Paint), CLS(Cumulative Layout Shift)

![](https://velog.velcdn.com/images/for24ng/post/2e36a383-e929-4289-ac8c-f4c25daa58a7/image.png)

![](https://velog.velcdn.com/images/for24ng/post/8e00b173-560e-4918-9e11-f996b6d31880/image.png)

![](https://velog.velcdn.com/images/for24ng/post/efc81a9b-eae7-4e04-bba6-11a7f10df27f/image.png)

4. 웹 반응성 측정 방법

![](https://velog.velcdn.com/images/for24ng/post/01ba0d7b-976a-4a56-b770-94942c7205a1/image.png)

Navigation : 단일 페이지의 로드 성능 측정
![](https://velog.velcdn.com/images/for24ng/post/94782539-0a4f-4ae7-9c88-b03d9b295859/image.png)

Snapshot : 사용자 인터렉션 후 페이지의 상태 측정
![](https://velog.velcdn.com/images/for24ng/post/cbe65236-2db5-4d2d-be77-a1008983f0df/image.png)

Timespan : 임의의 시간동안 사용자 인터렉션 측정
![](https://velog.velcdn.com/images/for24ng/post/5218c0b7-bc72-4f3d-9cd8-9ea2875be9a6/image.png)

5. 웹 반응성 개선 사례

Reflow(Critical Rendering Path)
JavaScript - Style - Layout - Paint - Composite(실제 반영)

WPM(Web Performance Monitoring): 카카오에서 제공하는 성능 측정

- 블로킹 타임 발생시 강제 리플로우 확인,전체 화면 업데이트 발생시 중요한 부분 우선 업데이트 진행, 레이아웃 시프트는 간단한 작업만으로 쉽게 개선 가능

---

#### 로드 성능은 중요하지만 반응성도 중요 => Lighthouse userflow로 측정

이상개발자의 느낀점🧂:
역시 웹 반응성이 아주 중요하다 ! 반응성 측정해서 객관적인 지수를 따져보는게 필요하다. 요즘 들을 때마다 내가 하고 있는 프로젝트에 어떻게 적응할지 고민이 되는데 새로운 생각을 주는 컨퍼런스였다. 항상 개선하며 개발해나가기 🔥
