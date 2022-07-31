# Web Server와 WAS

## Web Server

> 웹 브라우저 클라이언트로부터 HTTP 요청을 받아들이고 HTML 문서와 같은 웹 페이지를 반환하는 컴퓨터 프로그램
> 

클라이언트가 서버에 요청한 페이지에 해당하는 HTML, CSS, 이미지와 같은 정적 파일들을 넘겨주는 역할을 한다. 웹 서비스가 정적인 페이지만 응답하는 것이라면 웹 서버 만으로 서비스를 구축할 수 있겠지만 개개인에 따라 다른 요청과 응답을 주고받기 위해서는 WAS가 필요하다. 또한 WAS의 앞 단에 프록시의 역할로 로드밸런싱을 통한 부하분산이 가능하다.

### 대표적인 Web Server

- Apache
    - 스레드 / 프로세스 기반구조
    - MPM ( Multi Process Module )
    - 안정정, 호환성, 확장성 우세
- Nginx
    - Event-Driven 처리 기반구조
    - 많은 접속자들 수용가능
    - 성능 우세

## WAS ( Web Application Server )

> 인터넷 상에서 HTTP 프로토콜을 통해 사용자 컴퓨터나 장치에 애플리케이션을 수행해주는 미들웨어로서, 주로 동적 서버 컨텐츠를 수행하는 것으로 웹 서버와 구별이 되며, 주로 데이터베이스 서버와 같이 수행
> 

WAS는 Web Server와 Web Container가 합쳐진 형태로 데이터베이스에 각종 요청을 하거나 로직을 수행하여 사용자에 따른 동적인 요청을 수행할 수 있다. WAS에서도 웹 서버로서의 역할로 정적 파일을 넘겨줄 수 있지만 주로 웹 컨테이너로서의 역할이 크다.

### Web Container

자바 진영에서 서블릿이라고 불리우는 웹 컨테이너는 웹 서버의 컴포넌트 혹은 미들웨어와 같은 역할로 서버로 들어오는 요청이나 응답을 처리한다.

- 동작 순서
    - Servlet Request / Servlet Response 객체 생성
    - 설정 파일을 참고하여 매핑할 Servlet확인
    - 해당 Servlet 인스턴스가 없으면 생성
    - Servlet Container에 스레드를 생성하고, 파라미터 값으로 req, res를 받아 Service실행
    - 실행이 완료된 후 Request Response 객체 제거
        - Servlet 인스턴스는 싱글톤으로 관리되어 제거되지 않고 재사용된다.
        - Servlet Container는 Servlet을 적재적소에 생성하고 제거함으로 생명주기를 관리한다.

### 대표적인 WAS

- Tomcat