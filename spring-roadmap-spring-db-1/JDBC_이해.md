# JDBC 이해

<br>
<br>

## 1. JDBC 등장 이유

<br>

애플리케이션을 개발할 때 중요한 데이터는 대부분 데이터베이스에 보관

<br>

<b>클라이언트, 애플리케이션 서버, DB </b>

![img1](./img/JDBC%EC%9D%B4%ED%95%B4_img1.PNG)

<br>

클라이언트 애플리케이션 서버를 통해 데이터를 저장하거나 조회하면, 애플리케이션 서버는 다음 과정을 통해서 데이터베이스를 사용한다.

<br>

<b>애플리케이션 서버와 DB - 일반적 사용법</b>


![img2](./img/JDBC%EC%9D%B4%ED%95%B4_img2.PNG)

<br>

- 커넥션 연결: 주로 TCP/IP를 사용해서 커넥션을 연결
- SQL 전달: 애플리케이션 서버는 DB가 이해할 수 있는 SQL을 연결된 커넥션을 통해 DB에 전달
- 결과 응답: DB는 전달된 SQL을 수행하고 그 결과를 응답한다. 애플리케이션 서버는 응답 결과를 활용한다.

<br>

<b>애플리케이션 서버와 DB - DB 변경 </b>

![img3](./img/JDBC%EC%9D%B4%ED%95%B4_img3.PNG)

<br>

각각의 데이터베이스마다 커넥션을 연결하는 방법, SQL을 전달하는 방법, 결과를 응답 받는 방법이 모두 다르다.(관계형 데이터베이스는 수십개가 있다.)

<br>

<b>2가지 문제점</b>
- 데이터베이스를 다른 종류의 데이터베이스로 변경하면 애플리케이션 서버에 개발된 데이터베이스 사용 코드도 함께 변경해야 한다.
- 개발자가 각각의 데이터베이스마다 커넥션 연결, SQL 전달, 그리고 그 결과를 응답 받는 방법을 새로 학습해야 한다.

<br>

<i>이런 문제를 해결하기 위해 JDBC라는 자바 표준이 등장</i>

<br>
<br>

## 2. JDBC 표준 인터페이스

<br>

> JDBC(Java Database Connectivity)는 자바에서 데이터베이스에 접속할 수 있도록 하는 자바 API. JDBC는 데이터베이스에서 자료를 쿼리하거나 업데이트하는 방법을 제공한다.

<br>

![img4](./img/JDBC%EC%9D%B4%ED%95%B4_img4.PNG)

<br>

대표적으로 다음 3가지 기능을 표준 인터페이스로 정의해서 제공한다.
- java.sql.Connection - 연결
- java.sql.Statement - SQL을 담은 내용
- java.sql.ResultSet - SQL 요청 응답

<br>

자바는 위와 같이 표준 인터페이스를 정의해두고 개발자는 이 표준 인터페이스만 사용해서 개발하면 된다.

<br>

이 JDBC 인터페이스를 각각의 DB 벤더(회사)에서 자신의 DB에 맞도록 구현해서 라이브러리를 제공한다. 이것을 JDBC 드라이버라 한다. 

<br>

![img5](./img/JDBC%EC%9D%B4%ED%95%B4_img5.PNG)

<br>

<b> 정리 </b>

JDBC의 등장으로 2가지 문제가 해결
- 데이터베이스를 다른 종류의 데이터베이스로 변경하면 애플리케이션 서버의 데이터베이스 사용 코드도 함께 변경해야 하는 문제
  - 애플리케이션 로직은 이제 JDBC 표준 인터페이스에만 의존한다.
  - 다른 종류의 데이터베이스로 변경하고 싶다면 JDBC 구현 라이브러리만 변경하면 된다.
- 개발자가 각각의 데이터베이스마다 커넥션 연결, SQL 전달, 결과를 응답 받는 방법을 새로 학습해야하는 문제
  - JDBC 표준 인터페이스 사용법만 학습하면 된다. 수샙개의 데이터베이스에 모두 동일하게 적용가능

<br>

<b> 참고 - 표준화의 한계 </b>

> ANSI SQL이라는 표준이 있기는 하지만 일반적인 부분만 공통화했기 때문에 한계 존재 <br>
> 대표적으로 실무에서 기본으로 사용하는 페이징 SQL은 각각의 데이터베이스마다 사용법이 다르다. <br>
> 데이터베이스를 변경하면 JDBC 코드는 변경하지 않아도 되지만 SQL은 해당 데이터베이스에 맞도록 변경해야 한다. <br>
> JPA(Java persistence API)를 사용하면 이렇게 각각의 데이터베이스마다 다른 SQL을 정의해야하는 문제도 많은 부분 해결할 수 있다.

<br>
<br>

## 3. JDBC와 최신 데이터 접근 기술

<br>

- JDBC는 1997년도에 출시된 오래된 기술이며 사용하는 방법도 복잡
- 최근에는 JDBC를 직접 사용하기 보다는 JDBC를 편리하게 사용하는 다양한 기술이 존재한다.
- 대표적으로 SQL Mapper와 ORM 기술이 있다.

<br>

![img6](./img/JDBC%EC%9D%B4%ED%95%B4_img6.PNG)


- SQL Mapper
  - 장점: JDBC를 편리하게 사용하도록 도와준다.
    - SQL 응답 결과를 객체로 편리하게 변환해준다.
    - JDBC의 반복 코드를 제거해준다.
  - 단점: 개발자가 SQL을 직접 작성해야 한다.
  - 대표 기술: 스프링 Jdbctemplate, MyBatis


<br>


![img7](./img/JDBC%EC%9D%B4%ED%95%B4_img7.PNG)

- ORM 기술
  - ORM은 객체를 관계형 데이터베이스 테이블과 매핑해주는 기술. 
  - 각각의 데이터베이스마다 다른 SQL을 사용하는 문제도 중간에서 해결해 준다.
  - 대표 기술: JPA, 하이버네이트, 이클립스링크
  - JPA는 자바 진영의 ORM 표준 인터페이스, 이것을 구현한 것으로 하이버네이트와 이클립스 링크 등의 구현 기술이 있다.

<br>

<b> SQL Mapper vs ORM 기술 </b>
SQL Mapper와 ORM 기술 둘다 각각 장단점이 있다.
- SQL Mapper는 SQL만 직접 작성하면 나머지 번거로운 일은 SQL Mapper가 대신 해결해준다.
- SQL Mapper는 SQL만 작성할 줄 알면 금방 배워서 사용할 수 있다.

<br>

- ORM기술은 SQL 자체를 작성하지 않아도 되어 개발 생산성이 높아진다. 
- 편리한 반면에 쉬운 기술은 아니므로 실무에서 사용하려면 깊이있게 학습해야 한다.

<br>

> <b>중요</b> <br>
> 위 기술들도 내부에서는 모두 JDBC를 사용한다.
> <br>
> JDBC를 직접 사용하지 않더라도 어떻게 동작하는지 기본 원리를 알아두어야 한다.
> <br>
> JDBC는 자바 개발자라면 꼭 알아두어야 하는 필수 기본 기술이다.



<br>
<br>

## 4. 데이터베이스 연결

<br>

<b> JDBC DriverManager 연결 이해 </b>

<br>

![img8](./img/JDBC%EC%9D%B4%ED%95%B4_img8.PNG)

- JDBC는 java.sql.Connection 표준 커넥션 인터페이스를 정의한다.
- H2 데이터베이스 드라이버는 JDBC Connection 인터페이스를 구현한 org.h2.jdbc.jdbcConnection 구현체를 제공한다.

<br>
<br>

<b> DriverManger 커넥션 흐름 요청 </b>

<br>

![img9](./img/JDBC%EC%9D%B4%ED%95%B4_img9.PNG)

<br>

JDBC가 제공하는 DriverManger는 라이브러리에 등록된 DB 드라이버들을 관리하고, 커넥션을 획득하는 기능을 제공한다.

<br>

- 애플리케이션 로직에서 커넥션이 필요하면 DriverManager.getConnection()을 호출
- DriverManager는 라이브러리에 등록된 드라이버 목록을 자동으로 인식. 이 드라이버들에게 순서대로 다음 정보를 넘겨서 커넥션을 획득할 수 있는지 확인.
  - URL: 예) jdbc:h2:tcp://localhost/~/test
  - 이름, 비밀번호 등 접속에 필요한 추가 정보
  - 각각의 드라이버는 URL 정보를 체크해서 본인이 처리할 수 있는 요청인지 확인
- 이렇게 찾은 커넥션 구현체가 클라이언트에 반환

<br>

<b> H2 데이터베이스 드라이버 라이브러리 </b>

```java
runtimeOnly 'com.h2database:h2' //h2-x.x.xxx.jar
```

<br>
<br>

## 5. JDBC 개발 등록

<br>

- JDBC를 사용해서 회원 데이터를 데이터베이스에 관리하는 기능을 개발
- 소스코드는 아래 링크에 작성
  - https://github.com/Hambak-note/spring-roadmap-spring-db-1


<br>

> <b> 참고 </b> 
> <br>
> 코드 상에서 PreparedStatement는 Statement의 자식 타입인데, ?를 통한 파라미터 바인딩을 가능하게 해준다.
> <br>
> SQL Ingection 공격을 예방하려면 PreparedStatement를 통한 파라미터 바인딩 형식을 사용해야 한다.


<br>

<b> ResultSet </b>
- 보통 select 쿼리의 결과가 순서대로 들어간다.
- 내부에 있는 커서(cursor)를 이동해서 다음 데이터를 조회가능
- rs.next()
  - 호출 시 커서가 다음으로 이동
  - 최초의 커서는 데이터를 가리키고 있지 않기 때문에 최초 한번은 호출해야 데이터 조회 가능

<br>

![img10](./img/JDBC%EC%9D%B4%ED%95%B4_img10.PNG)

<br>




