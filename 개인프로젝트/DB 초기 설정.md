1. MySQL을 사용할 것이기 때문에, mysql 최신버전의 이미지를 다운받는다.  
```
docker pull mysql:latest
```

2. 환경변수를 적어서 컨테이너를 실행
```
docker run --name mysql-container \
  -e MYSQL_ROOT_PASSWORD=rootpassword \
  -e MYSQL_DATABASE=project_db_name \
  -e MYSQL_USER=username \
  -e MYSQL_PASSWORD=password \
  -p 3307:3306 \
  -d mysql:latest
```
```
실행 옵션에 대한 설명
1. --name mysql-container
컨테이너 이름을 tochookpi-mysql로 지정합니다.

1. -e MYSQL_ROOT_PASSWORD=rootpassword
MySQL root 사용자의 비밀번호를 rootpassword로 설정합니다.

1. -e MYSQL_DATABASE=project_db_name
생성할 기본 데이터베이스 이름을 project_db_name으로 설정합니다.

1. -e MYSQL_USER=username
생성할 일반 사용자 이름을 username으로 설정합니다.

1. -e MYSQL_PASSWORD=password
tochookpi_user 사용자의 비밀번호를 password으로 설정합니다.

1. -p 3307:3306
호스트의 3307 포트를 컨테이너의 3306 포트와 매핑합니다.
로컬 DB가 3306포트를 사용중이라 3307로 설정.
```

3. 실행중인 컨테이너 확인
```
docker ps
```

4. 컨테이너에 접속
```
docker exec -it mysql-container mysql -u username -p
```

5. DB 생성 확인
```
SHOW DATABASES;
``` 

6. Entity 생성
```java
@Entity
@Table(name = "users")
@NoArgsConstructor
@AllArgsConstructor
@Setter
@Getter
public class User {
    @Id
    @GeneratedValue(strategy =  GenerationType.IDENTITY)
    private Long id;

    private String username;
    private String email;
    private String password;
}
```

```java
@Entity
@Table(name = "meetings")
@NoArgsConstructor
@AllArgsConstructor
@Setter
@Getter
public class Meeting {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String meetingName;
    private String location;

    @ManyToOne
    @JoinColumn(name = "organizer_id")
    private User organizer; // 모임 주최자
}
```

7. application.properties 설정
```
spring.application.name=project-name

spring.datasource.url=jdbc:mysql://localhost:3307/project_db_name
spring.datasource.username=username
spring.datasource.password=password

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect
```

8. 실행 후 테이블 및 컬럼 생성 확인
```
SHOW DATABASES;
USE project_db_name;
SHOW TABLES;
SHOW columns FROM user;
SHOW columns FROM meetings;
```