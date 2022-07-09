# docker
## ![image](https://user-images.githubusercontent.com/54635552/178084635-59112f1a-47e3-484e-a833-9687e0cbcbbb.png)

### 도커사용이유
- local에서 잘실행되는 코드 다른 환경에서 Version 이슈로 실행되지않을 가능성이 존재함 -> 도커를 통해 라이브러리 각 종속성문제해결
- Container에 해당 코드가 실행되게하는 종속성을 지니고 있어 회사내부에서 서로다른 팀간 서로다른 환경에서도 실행가능
- 동시에 여러작업을 진행할경우 각 작업의 버전이 충돌되지않게 방지

### Virtual Machine 장단점
## ![image](https://user-images.githubusercontent.com/54635552/178085094-80e1a7fc-dc8b-450a-a6dd-3e666ffd504c.png) 

### 도커 구조
## ![image](https://user-images.githubusercontent.com/54635552/178085210-66219e33-a421-481a-973b-652ab849fa76.png)

### 도커 Vs Virtual Machine
## ![image](https://user-images.githubusercontent.com/54635552/178085337-270f8954-e597-40ed-bd8b-740d00064970.png)

### 로컬에서 도커 실행하기
-도커는 이미지 기반에서 실행, 이미지 라는것을 먼저 생성해야함
- 1.Dockerfile : 도커파일 설정작성
- 2.docker build . : 도커 이미지 빌드
## ![image](https://user-images.githubusercontent.com/54635552/178095727-e5a58596-5621-4427-802f-a7da7d6d473f.png)
- 해당 숫자부분이 이미지 ID
- 3.docker run [ID] : 해당 도커 이미지 실행
- 4.docker ps : 현재 실행중인 Docker 출력
## ![image](https://user-images.githubusercontent.com/54635552/178095771-8e73cbd6-3997-4097-b465-c33930e76f01.png)
- 해당 adoring_blackwell 부분이 이름
- 5.docker stop [이름] : 실행중인 도커 종료



#### 출처 : Docker & Kubernetes: 실전 가이드(Udemy)


