# SQL Injection

### SQL Injection

* SQL Injections이란?

    악의적인 사용자에 의해 조작된 SQL 쿼리문이 데이터베이스에 그대로 전달되어 비정상적 명령을 실행시키는 공격 기법

### 공격 방법

* Error based SQL Injection

    논리적 에러를 이용함

    에러가 발생되는 사이트에서는 에러 정보를 이용해 DB 및 쿼리 구조 등의 정보 추측 가능

* UNION based SQL Injection

    UNION : 두 개의 쿼리문에 대한 결과를 통합해 하나으 ㅣ테이블로 보여주게 하는 키워드

    정상적인 쿼리문에 하나의 쿠가 쿼리를 삽입해 원하는 정보 획득

    UNION하는 두 테이블의 컬럼 수와 데이터 형이 같은 경우에만 UNION Injection 수행 가능

* Blind SQL Injection(1)

    특정한 값이나 데이터를 전달받는 것이 아닌, 쿼리를 통해 나온 참과 거짓의 정보만을 통해 정보를 취득함\
    (Boolean based SQL)

    서버가 응답하는 성공과 실패 여부를 이용해 DB 테이블 정보 등을 추출해냄

    에러가 발생하지 않는 사이트에서는 논리적 에러나 UNION을 사용할 수 없기 때문에 Blind를 사용함

* Blind SQL Injection(2)

    쿼리 결과를 특정 시간만큼 지연시키는 것\
    (Time based SQL)

    Blind와 동일하게 에러가 발생되지 않는 조건에서 사용하며, True/False의 결과값이 나오지 않아 시간을 잼

    궁극적 목표는 DB 구조를 파악하는 것임

### 방어 방법

* input 값을 받을 때, 특수문자 여부 검사

    로그인과 같은 과정 이전에 검증 로직을 추가해 미리 설정한 특수문자들이 올어온 경우요청을 막아냄

* SQL 서버 오류 발생 시, 해당하는 에러 메세지 감추기

    view를 활용해 원본 DB 테이블의 접근 권한을 높이고 일반 사용자는 view로만 접근하여 에러를 볼 수 없도록 함

* PrepareStatement 사용

    PrepareStatement를 사용하면 특수문자를 자동으로 escaping해줌

         이를 통해 서버 측에서 필터링 과정을 진행하여 공격을 방어함

    