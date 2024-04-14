[React.js의 렌더링 방식 살펴보기](https://www.youtube.com/watch?v=N7qlk_GQRJU)

작성한 컴포넌트는 어떤 과정을 거쳐 렌더링 되는가?
이런 특징으로 인해 갖게 되는 장점은 무엇인가?

### 웹 브라우저는 어떻게 동작할까?

- 브라우저는 HTML, CSS로 작성한 웹 페이지를 어떤 과정을 거쳐 화면에 렌더링하는 걸까?
  ![](https://velog.velcdn.com/images/for24ng/post/423ca45d-943d-4bb8-8d24-ab4ff6b0a901/image.png)

![](https://velog.velcdn.com/images/for24ng/post/1524d31f-036b-4ef3-9df9-37cc3353058a/image.png)

1. 트리모양으로 변환이 됨
2. Render Tree 생성 : 웹페이지의 '청사진'으로 볼 수 있음(배치와 모양, 스타일에 대해 모든 것을 가지고 있음)
3. Layout : Render Tree를 기반으로 실제 웹 페이지에 요소들의 배치를 결정하는 작업
4. Painting : 실제로 요소들을 화면에 그려내는 과정

#### 그렇다면 업데이트는 어떻게 이루어질까?

업데이트 : 이벤트에 따라 화면이 실시간으로 변화하는 것 (좋아요 버튼 등)

![](https://velog.velcdn.com/images/for24ng/post/3d79faad-4bdf-4f98-8237-33cbefd5f376/image.png)
하지만 Layout, Painting은 매우 비싼 과정임(시간이 오래 걸림)

![](https://velog.velcdn.com/images/for24ng/post/d9d3cc8a-c14a-4ea6-bba2-c9730133ce83/image.png)

![](https://velog.velcdn.com/images/for24ng/post/799970f3-2480-4c68-8523-eec313169784/image.png)
클릭하면 리스트가 추가됨 -> 3000번 수정이 됨

![](https://velog.velcdn.com/images/for24ng/post/5c748d96-98c9-4bb4-9fa0-6df0d4ec7207/image.png)

리스트를 저장해두고 DOM을 한 번만 수정을 함

#### 결론

![](https://velog.velcdn.com/images/for24ng/post/865e6ecb-b694-42df-a70c-13287a9acf47/image.png)

서비스의 규모가 커질 수록 점점 힘들어짐
하지만,React에서는 자동으로 됨

### React의 렌더링 프로세스

React는 **2단계**를 거쳐 화면에 UI를 렌더링함
Render Phase와 Commit Phase
![](https://velog.velcdn.com/images/for24ng/post/8fb34476-d478-4b33-8ef3-0db321462b63/image.png)

#### Render Phase

1. 컴포넌트를 호출해 결과값을 계산
   ![](https://velog.velcdn.com/images/for24ng/post/cbea9cf9-8e9e-4275-826a-527dc397489d/image.png)
   객체값이 반환됨

![](https://velog.velcdn.com/images/for24ng/post/7036f780-6818-4fd4-91bc-ee4c1b551e46/image.png)

Render Element: 컴포넌트가 렌더링하고자 하는 정보를 다 포함하고 있는 객체

2. React Element 들을 모아 Virtual DOM을 생성

![](https://velog.velcdn.com/images/for24ng/post/4e8aa00f-1e74-4c36-b0e4-76633db61170/image.png)

#### Virtual DOM

React Element 라고 부르는 객체 값의 모임

- 실제 DOM은 아님(복제라고 보면 됨)
- **값으로 표현된 UI(Value UI)**라고 이해하는 게 더 정확함

3. Render Phase 정리
   : React 컴포넌트가 렌더링해야 하는 UI를 Virtual DOM이라는 객체 값으로 변환하는 과정

![](https://velog.velcdn.com/images/for24ng/post/f4ce502a-dbed-4f9e-8cf8-8f65248027c3/image.png)

#### Commit Phase 시작

Virtual DOM을 Actual DOM에 반영
commit : 확정하다, 결정하다

진짜 브라우저가 렌더링하게 될 DOM에 반영하기

![](https://velog.velcdn.com/images/for24ng/post/593dee85-6227-4586-a26a-7075d63fbba3/image.png)

![](https://velog.velcdn.com/images/for24ng/post/3ac9f1a1-f5f1-4a62-aa8e-3c71f392c632/image.png)

#### 왜 이렇게 복잡하게 할까?

: DOM 수정을 최소화하기 위해서 (대부분의 상황에 충분히 빠른 업데이트를 보장하기 위해서)

![](https://velog.velcdn.com/images/for24ng/post/5a04ed0f-94e4-443e-9675-95ef7bdbcaf8/image.png)
빨간색의 변경사항 반영

![](https://velog.velcdn.com/images/for24ng/post/f50a18f2-db35-4ac4-8ce2-9c3be501032c/image.png)
이전 DOM과 차이점 비교

![](https://velog.velcdn.com/images/for24ng/post/f2e640c6-0591-4586-98a9-f4c798afc946/image.png)

#### Reconciliation(재조정)

![](https://velog.velcdn.com/images/for24ng/post/4546c086-cbc2-4019-83f1-60a7212c9910/image.png)

리액트를 사용한다면 자동으로 가능하다.
두 개의 DOM이 화해하는 것 같아 재조정으로 표현함

하지만 React가 모든 시간에 빠른 속도로 최소의 시간을 사용하는 건 아니다. 계산에 시간이 필요하기 때문

### 총 정리

: 순수한 Js만 이용해 DOM을 조작할 때는 DOM 수정을 최소화해야 함

- Reflow, Repaint를 최소한으로 발생시키기 위함
- 동시에 발생하는 업데이트를 최대한 모아 한 번만 DOM을 수정해야 함
- 서비스 규모가 커질수록 쉽지 않음

: React는 자체적인 렌더링 프로세스를 사용하므로 이런 걱정에서 자유로움

- Render Phase와 Commit Phase로 나뉨
- Render Phase에 Virtual DOM을 생성하여 동시에 발생하는 업데이트를 모음
- Commit Phase에 Virtual DOM에 반영된 모든 업데이트를 Actual DOM에 한 번만 반영함

🐾이상 느낀점
: 리액트를 사용하는 이유는 알고 있었지만 이렇게 자세하게 들으니까 더 이해가 잘 되었다. 하지만 React가 항상 최소 시간이 걸리지는 않는다는 것도 한번 더 들으니 기억이 더 잘되는 것 같다. 순수 Js를 사용할 때는 조심해야 겠다.
