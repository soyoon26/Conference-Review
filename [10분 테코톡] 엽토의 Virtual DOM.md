[엽토의 Virtual DOM](https://www.youtube.com/watch?v=Bdk7QzbbcEI)

### 1. 브라우저 렌더링 과정

![](https://velog.velcdn.com/images/for24ng/post/c3a1640e-2198-4396-afba-c200bd750b49/image.png)

각 과정마다 연산비용도 많이 듦, 탐색비용과 reflow과정도 발생하게 됨

업데이트가 빈번하게 발생하며 비용이 큰 reflow과정을 거치며 성능이 좋지 않게 됨 => virtual DOM이 탄생하게 됨

### 2. Virtual DOM의 등장

- DOM트리를 **복제**하여 메모리에 저장시킨 Js 객체
- DOM의 정보는 가지고 있지만 DOM 조작 메서드는 없음. 즉, Real DOM을 **경량화**했다고 표현하기도 함
- 브라우저에서 DOM을 조작하면 렌더링과 리플로우같은 비용이 발생하는 반면, VirtualDOM은 Js 객체로써 브라우저에서 직접 수정되지 않아 위와 같은 비용이 발생되지 않음
- 메모리 상에서 **변경 사항을 계산하고 필요한 경우에만 DOM Update**를 하기 때문에 굉장히 효율적

![](https://velog.velcdn.com/images/for24ng/post/07d70c58-b9f9-4821-b786-408bf150259b/image.png)

모든 정보를 표현하고 있음

예시 업데이트 방법 : 변경 5개를 Virtual DOM을 통해 식별 - DOM Update 한 번 - reflow 한 번

하지만, 무조건 효율적인 것은 아님 ! DOM 업데이트가 많이 일어나는 경우만 효율적. **정적 페이지** 같은 경우 직접 DOM 업데이트하는 것이 효율적일 수 있음

### 3. React에서의 Virtual DOM

: Virtual DOM(VDOM)은 UI의 이상적인 또는 **"가상"적인 표현**을 메모리에 저장하고 ReactDOM과 같은 라이브러리에 의해 **"실제"DOM과 동기화**하는 프로그래밍 개념임. 이 과정을 **"재조정"**이라 함

업데이트 전 Virtul DOM과 업데이트 후 Virtual DOM을 비교

![](https://velog.velcdn.com/images/for24ng/post/9da4be91-88c3-4c2d-a990-28f7b70803e5/image.png)

예시)
![](https://velog.velcdn.com/images/for24ng/post/afab7405-a901-4916-b3f1-1ffa135d43ed/image.png)
동일한 것은 유지를 하고 변경된 것만 반영

🥞이상의 느낀 점
: 오늘 렌더링과정에 대한 컨퍼런스를 봐서 이 영상도 선택하게 되었는데 반복해서 보니 더 이해가 잘 된다. Virtual DOM이 만들어진 과정도 확실하게 알게 되었고 정적 페이지의 경우는 React를 거치지 않아도 된다는 것을 기억하기 !
