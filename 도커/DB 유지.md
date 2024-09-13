# DB 유지
컨테이너는 파일을 만들고, 업데이트하고, 삭제할 수 있지만 컨테이너를 제거하면 해당 변경 사항이 손실되고 Docker는 해당 컨테이너에 대한 모든 변경 사항을 격리합니다.  
즉, 컨테이너의 수명이 끝나면 그 안의 데이터도 손실됩니다.  

예를 들어, MySQL 컨테이너를 띄워놓고 작업을 한 다음 컨테이너를 삭제하면 데이터가 다 날아가게 됩니다.  

이런 데이터 손실을 방지하기 위한 가장 일반적인 방법이 볼륨(Volumes)입니다.  
MySQL 컨테이너를 실행할 때 데이터 저장소를 외부 볼륨에 연결하면 컨테이너를 삭제해도 데이터는 손실되지 않습니다.  

## 볼륨

![volume](./이미지/volume.png)

볼륨은 도커 컨테이너에서 데이터를 지속적으로 저장하고 공유하는 데 중요한 메커니즘입니다.  
바인드 마운트와는 달리, 볼륨은 도커가 관리하며, 여러 환경에서 호환성이 뛰어나고 다양한 기능을 제공합니다.  

### 볼륨과 바인드 마운트의 차이
* 볼륨: 볼륨은 도커가 자체적으로 관리하는 저장소입니다.  
호스트 머신의 OS와 무관하게 동작하며, 백업과 마이그레이션이 쉽습니다.
* 바인드 마운트: 바인드 마운트는 호스트의 특정 디렉토리를 컨테이너 내부에 연결하는 방식입니다.  
호스트의 디렉토리 구조에 따라 동작하며, 직접 파일 경로를 지정해야 합니다.  
* 바인드 마운트는 호스트 머신의 디렉토리 구조에 따라 동작하기 때문에, 호스트의 운영 체제(OS)에 종속적입니다.  
즉, 바인드 마운트를 사용할 때는 호스트 OS의 파일 시스템 구조와 경로를 고려해야 합니다.  
반면에 볼륨은 도커에서 자체적으로 관리되는 스토리지 메커니즘이기 때문에 운영 체제와 무관하게 동일하게 동작합니다. 
* Docker Desktop의 볼륨은 Mac 및 Windows 호스트의 바인드 마운트보다 훨씬 더 높은 성능을 제공합니다.

## 볼륨 생성 및 관리
* 볼륨 생성
```
docker volumn create my_mysql_data
```

* 볼륨 목록
```
docker volume ls

-------------------------
DRIVER    VOLUME NAME
local     my_mysql_data
-------------------------
```

* 볼륨 검사
```
docker volume inspect my_mysql_data

-------------------------
[
    {
        "CreatedAt": "2024-09-13T05:01:58Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/my_mysql_data/_data",
        "Name": "my_mysql_data",
        "Options": null,
        "Scope": "local"
    }
]
-------------------------
```

* 볼륨 제거
```
docker volume rm my_mysql_data
```

* 볼륨이 있는 컨테이너 시작
```
docker run -d \
    --name mysql-container \
    -e MYSQL_ROOT_PASSWORD=my-secret-pw \
    -v my_mysql_data:/var/lib/mysql \
    mysql:latest

-v my_mysql_data:/var/lib/mysql는 호스트의 my_mysql_data 볼륨을 컨테이너 내의 /var/lib/mysql 경로에 연결하는 것을 의미합니다.
MYSQL_ROOT_PASSWORD는 MySQL의 루트 비밀번호 설정입니다.
```

## Docker Compose로 볼륨 사용
```
version: '3.8'

services:
  db:
    image: mysql:8.0
    container_name: mysql-container
    environment:
      MYSQL_ROOT_PASSWORD: example
      MYSQL_DATABASE: example_db
      MYSQL_USER: user
      MYSQL_PASSWORD: password
    volumes:
      - mysql_data:/var/lib/mysql
    ports:
      - "3306:3306"

  app:
    image: your_spring_app_image
    container_name: spring-app
    depends_on:
      - db
    ports:
      - "8080:8080"
    environment:
      SPRING_DATASOURCE_URL: jdbc:mysql://db:3306/example_db
      SPRING_DATASOURCE_USERNAME: user
      SPRING_DATASOURCE_PASSWORD: password
    volumes:
      - ./your_app:/app
    command: ./mvnw spring-boot:run

volumes:
  mysql_data:
```

## 참조
(DB 유지)[https://docs.docker.com/get-started/workshop/05_persisting_data/]  
(볼륨)[https://docs.docker.com/engine/storage/volumes/]