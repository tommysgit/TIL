# ORM

## ORM이란?

애플리케이션에서 작성한 엔티티의 맵핑정보를 통하여 데이터베이스의 테이블과 애플리케이션의 객체를 자동으로 맵핑, 영속화 해주는 기술이다. 하이버네이트나 JPA는 이러한 맵핑정보를 이용하여 ORM이 필요한 SQL을 생성하여 깔끔하게 객체에 영속화 해준다.

## 장점

1. 생산성
    
    → 쉽고빠르게 CRUD가능
    
2. 유지보수
    
    → 간결한 코드 → 직관적인 비즈니스 로직
    
3. 성능
    
    → 단건의 SQL을 비교하자면 ORM이 느릴 수 있으나 캐시를 이용하여 불필요한 쿼리를 날리지 않는다.
    ex) 하나의 트랜잭션안에 객체를 여러번 Update할 경우 최종적으로 바뀐 상태로 한번만 Update 쿼리를 날린다.
    → ORM이 객체의 변화를 감지하고 최종적으로 중복되는 부분을 최소화하여 최적화된 쿼리를 날린다.
    → 또한 필요에 따라 JPQL과 같은 쿼리를 직접 작성하여 이용할 수 있다.
    
4. 밴더 독립성
→ 각 데이터베이스에 맞게 쿼리문을 작성해야하는 sql문과 달리 ORM이 데이터베이스 밴더에 맞게 쿼리를 생성해준다.

- 기존 JDBC 대신 ORM 사용하는 이유
    - 객체 맵핑을 통한 OOP 장점을 살릴 수 있다.
    - 디자인 패턴 적용 용이
    - 코드 재사용
    - 간결한 코드 → 직관적인 비즈니스 로직, 테스트 용이 → 유지, 보수에 유리하다.

## ORM 패러다임 불일치

애플리케이션의 객체와 데이터베이스의 엔티티가 일치하지 않아 발생하는 문제들

- 밀도 문제
    - 애플리케이션 : 다양한 크기의 객체와 커스텀한 타입을 정하여 사용할 수 있다.
    - 데이터베이스 : 정해져있는 기본 타입만 사용가능하다.
- 서브타입 문제
    - 애플리케이션 : 상속을 많이 사용하고 구조를 만들기 쉽다.
    - 데이터베이스 : OOP라는 개념이 적용되지 않고 상속 이라는 것이 존재하지 않는다. 즉, 다형성을 구현할 수 없다.
- 식별성 문제
    - 애플리케이션 : 동일성, 동등성 등으로 객체 식별
    - 데이터베이스 : 주요 키(Primary Key)를 이용하여 식별
- 관계 문제
    - 애플리케이션 : 레퍼런스로 관계를 표현하고 방향, 다대다 관계 등이 존재한다.
    - 데이터베이스 : 다대다 관계를 표현하려면 하나의 테이블이 1:N, N:1 관계를 지어야한다.
                           Join을 이용하여 원하는 컬럼끼리 묶어 조회할 수 있다.
                           테이블 간의 관계는 외래키를 이용하여 표현한다.
- 데이터 네비게이션 문제 : 경우에 따라 성능의 차이가 발생하고 어려운 문제이기에 가장 주의해야할 문제
    - 애플리케이션 : 객체의 레퍼런스를 통하여 다른 객체로 이동이 가능하고 스트림, 컬렉션을 이용하여 객체 순환 가능
    - 데이터베이스 : 데이터의 참조를 통한 이동 혹은 순환이 어렵다. Join을 이용하여 다른 데이터와 연결하여 조회가 가능하지만 유연하지 못하고 필요에 따라 테이블별로 쿼리를 날리고 받은 데이터로 또 쿼리를 날려야하는 일이 발생한다. 이는 성능저하를 발생시킬 수 있다.

## Reference

[스프링 데이터 JPA - 인프런 | 강의](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EB%8D%B0%EC%9D%B4%ED%84%B0-jpa/dashboard)