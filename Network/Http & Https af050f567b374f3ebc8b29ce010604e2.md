# Http & Https

## Http

Http(HyperText Transfer Protocol)은 서버와 클라이언트 사이에 데이터를 주고받기 위한 프로토콜이다. Http는 80번 포트를 이용하여 서버와 클라이언트는 각각 80번 포트로 요청, 응답을 하게된다.

Http는 상태를 가지고 있지 않은 프로토콜이며, 애플리케이션 계층으로 TCP/IP위에서 동작한다. 아래 사진은 Http헤더의 일부로 요청방식, http버전, 메시지 헤더등이 있다. 추가로 HTML혹은 다른 형태의 데이터가 메시지 본문으로 들어가 전송된다. 


<img src= "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbkdJ4Q%2FbtqK6AXLEtC%2FjBZzMuJBWzdLYmqILo5Ri1%2Fimg.png"/>
하지만 Http는 서버와 클라이언트가 주고 받는 데이터를 감청하기 매우 쉬워 보안문제에 취약 하다는 단점이 있는데 이를 해결해주는 프로토콜이 Https이다.

## Https

Http를 암호화하여 전송하는 것을 Https라고 볼 수 있다. 주고 받는 데이터는 같지만 443번 포트를 이용한다는 점과 데이터를 암호화하기 때문에 중간에 감청할 수 없다는 점이 특징이다. 또한 Https의 장점으로 SEO(검색엔진 최적화)에도 큰 혜택을 볼 수 있다고한다. 

Https의 암호화 방식으로는 대칭키, 비대칭키가 있는데 자세한 내용은 [여기](https://github.com/tommysgit/TIL/blob/6aad2584bc3718ca7b149f175a27bc6b44927941/Network/%EB%8C%80%EC%B9%AD%ED%82%A4%20&%20%EB%B9%84%EB%8C%80%EC%B9%AD%ED%82%A4%20d567c8466dc14588b1ae1fa26bc0cc1f.md)를 확인해보면 된다.

## Https 발급과정

1. A 사이트는 Https 적용을 위해 공개키, 개인키를 발급받는다.
2. A 사이트는 무료 혹은 유료로 CA기업에게 인증서 발급을 요청한다.
3. CA기업은 서비스의 정보(인증서 발급한 CA정보, 도메인 등등), A사이트의 공개키 정보등을 CA기업의 개인키로 암호화한 인증서를 A 사이트에게 발급한다.

**CA** : 인증서의 역할은 클라이언트가 방문한 사이트에 대해 신뢰성을 검증해주는 것인데 이것을 인증해주는 민간기 업들을 CA라고한다. 이미 브라우저에는 검증된 CA들의 공개키를 가지고 있다.

**사설 인증기관**

일부 사이트에 접속하면 하단의 사진과 같은 경우를 볼 수 있는데 이는 CA의 역할을 자신이 하여 인증서를 발급할 수 있다. 하지만 인증된 CA가 아니라면 브라우저는 아래와 같은 주소창을 띄우고 경고창을 띄운다.


<img src= "https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/228/1536.gif"/>

## Https 동작과정

1. A클라이언트가 B사이트에 접속한다.
2. B사이트에 처음 접속하는 것이라면 Https가 아닌 Http요청을 보낼 것이며 B사이트는 Https요청이 아닌 경우 인증서를 A클라이언트에 보낸다.
3. 인증서는 CA기업의 개인키로 암호화 되어있으나 브라우저는 이미 CA기업들의 공개키를 가지고 있어 인증서를 복호화 할 수 있다.
4. 복호화한 인증서에서 B사이트의 공개키를 획득한다.
5. A클라이언트는 B의 공개키를 이용하여 자신의 대칭키를 암호화하여 B서버에게 전송한다.
6. B서버는 자신의 개인키로 복호화를 한다. B의 공개키로 암호화된 대칭키는 개인키를 가지고 있는 B만 복호화할 수 있어 보안에 문제가 없다.
7. A의 대칭키를 가지고 있는 A클라이언트와 B서버는 대칭키를 이용하여 데이터를 암호화, 복호화하여 통신한다.
<img src= "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcCodLU%2FbtrqRZnoOFq%2Fe6kFHjADoVby70466Jkq51%2Fimg.png"/>
