[[10분 테코톡] 헤나의 HTTPS](https://www.youtube.com/watch?v=KpyzbEFYE_E)

### 1. HTTP 전송

![](https://velog.velcdn.com/images/for24ng/post/3e9de33d-5411-4c7a-bb5a-3e9773d093ac/image.png)

빠르게 정보를 읽을 수 있어 좋지만 비정상적인 사용자가 읽게 된다면 데이터가 유출될 수 있음 -> HTTPS 개념이 나오게 됨, 암호화하여 보냄으로써 데이터를 가로챈다 해도 읽을 수 없음

### 2. SSL/TLS (Secure Socket Layer/Transport Layer Security)

SSL은 구버전, TLS는 신버전이라 생각하면 됨, 지금은 TLS 사용
: 데이터를 암호화하는 통신 프로토콜

- 데이터를 암호화하여 제3자가 데이터를 볼 수 없게 보호함
- 데이터 변조 여부를 검증함
- 상호 인증을 지원함

상대가 신뢰할 수 있는 상대인지 확인하고 어떻게 암호화할지 결정

![](https://velog.velcdn.com/images/for24ng/post/2c83fcbc-6039-463e-8783-1bee38ca99a7/image.png)

### 3. HTTPS 사용 이유 세 가지

시간이 지연되어도 사용하는 이유?

- 데이터 기밀성 : 데이터를 어떻게 암호화할 것인가?
- 데이터 무결성 : 데이터가 조작되지 않았음을 어떻게 알 수 있는가?
- 통신 상대 인증 : 통신 상대를 신뢰할 수 있는가?

#### a. 데이터 기밀성

대칭키 암호화
![](https://velog.velcdn.com/images/for24ng/post/0e184358-0565-4cd4-863a-2effd780480c/image.png)

비대칭키 암호화(공개키 암호화) 개인키를 통해 복호화해서 메세지를 받을 수 있음
![](https://velog.velcdn.com/images/for24ng/post/943dea52-73a7-4d1f-99a8-39c2ce85d0c5/image.png)

#### b. 데이터 무결성

암호화 해시 함수: 동일하게 해시하지만 같지 않으면 데이터가 같지 않다. = 변조되지 않았음
![](https://velog.velcdn.com/images/for24ng/post/ff125416-d237-4ed4-af04-e0e618ec9180/image.png)

#### c. 통신 상대 인증

인증 기관 개념 도입(Certification Authority)
인증기관은 서버인증서를 서버에 보내고 서버는 클라이언트에게 보냄

하지만 가짜 인증기관을 만든다면?
인증서 체인을 사용하기 때문에 괜찮음, 인증서는 중간인증서, root인증서와 체인되어있음

### 4.HTTPS 통신 흐름

![](https://velog.velcdn.com/images/for24ng/post/b9bf3e03-0c65-4ce7-9749-abf5ee705ba7/image.png)
맞다고 생각하면 클라이언트 대칭키를 만들어 정상적 서버에게 보내어 복호화함.

🧂 개발자 이상의 느낌 점:
사실 개발을 공부하기 전에는 http와 https의 차이점도 잘 몰랐고 위험성도 몰랐는데 이렇게 설명을 들으니 잘 이해가 가고 다른 사람들에게도 알려줄 수 있게 되었다. 정처기 공부하기 전에 들었으면 암기가 필요하지 않았을 정도 ㅋㅋ
