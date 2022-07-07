# 수주 관리 웹 프로젝트

부모님의 회사에 사용될 수주 관리 프로그램 

현재 엑셀로 관리 중이지만 대충 만들었기에 부족한 점도 많고 고쳐야 할 점도 많아서 Spring강의 참고로 조금씩 만들어 완성할 예정

---

## 필요 사항

+ 회사명
+ 품목
+ 품목 코드(특정 회사에만 적용)
+ 단가
+ 수량
+ 총액
+ 발주일
+ 납기일

위 필요 사항을 토대로 만든 테이블 생성 코드

``` mysql
CREATE TABLE IF NOT EXISTS management (
id bigint(5) NOT NULL AUTO_INCREMENT,
company_name varchar(255) NOT NULL,
product_name varchar(255) NOT NULL,
product_code varchar(255) ,
price int(10) NOT NULL,
quantity int(10) NOT NULL,
sum int(10) NOT NULL,
order_date date,
due_date date,
PRIMARY KEY (id)
);
```



## 오류

### 07/06

테스트용으로 H2 DB를 생성하고 위 코드를 입력해도 Syntax error가 발생

어디가 틀렸는지도 나오지 않아 헤매던 중 지인이 아주 간단한 해결책을 알려줌

src > main > resources > application.properties에 H2 웹콘솔을 생성했다

```spring.h2.console.enabled=true```

 ```spring.datasource.url=jdbc:h2:mem:testdb ```

여기에

``` spring.datasource.url=jdbc:h2:mem:testdb;MODE=MYSQL```

추가로 간단히 해결

spring boot 2.1.10 이후에는 직접적으로 jdbc-url을 선언하여 h2주소 뒤에 MODE=MYSQL를 붙어야 mysql 테이블 쿼리가 정상 작동된다고 한다



출처: https://msyu1207.tistory.com/entry/spring-boot-JdbcSQLSyntaxErrorException-Syntax-error-in-SQL-statement-expected-identifier-해결-방안#toc- [로띠 로그:티스토리]
