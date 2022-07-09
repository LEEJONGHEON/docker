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

### 도커에서 node 실행
- docker hub에서 image 가져와서 설치하기
- docker run node : 로컬에 node image없어서 docker hub에서 설치받아서 실행
## ![image](https://user-images.githubusercontent.com/54635552/178096453-393994a8-7018-4f10-b28b-a2e84aa53dfa.png)
- docker ps -a : 도커가 생성한 모든 프로세스 확인
## ![image](https://user-images.githubusercontent.com/54635552/178096546-ac3ac063-d951-4edd-92fd-4092eef9fe19.png)
- docker run -it node : Container안에 있는 node 명령어 shell 바깥으로 나오게하기
- 현재 컨테이너 내부에서 node가 실행중이고, 해당 명령어 shell을 바깥으로 나오게하여 상호작용하게함
- node는 local 컴퓨터에서 작동되고있는것이아니라, 컨테이너 내부에서 실행중
- 이미지 는 설정파일, 코드를 저장하고있고, 해당 이미지 기반으로 run을하면 Container가 생성됨 

### Custom Dockerfile 생성
## ![image](https://user-images.githubusercontent.com/54635552/178097565-c313590d-6469-4e5c-a7f2-eabbe97c19b8.png)
- FROM : 특정 이미지 이름 or docker hub 상 이미지 이름 기반에서 이미지 작성하게 ex)FROM node
- WORKDIR : 작업디렉토리 지정, 도커 내부에서 해당 작업디렉토리에서 작업하게 설정
- COPY : COPY [컨테이너 외부 경로] [이미지가 복사되어야 할 위치] ex) COPY . /app : 현재폴더의 모든파일 도커의 /app 경로로 이동
- RUN npm install : node 종속성 설치
- EXPORT : 도커 내부의 포트 열기 ex) EXPORT 80
- CMD ["node","server.js"] : RUN과 CMD 차이는 CMD는 이미지 기반으로 컨테이너가 시작될때만 실행되는코드
#### 출처 : Docker & Kubernetes: 실전 가이드(Udemy)


