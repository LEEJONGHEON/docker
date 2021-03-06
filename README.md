# docker
## ![image](https://user-images.githubusercontent.com/54635552/178084635-59112f1a-47e3-484e-a833-9687e0cbcbbb.png)

# 도커사용이유
- local에서 잘실행되는 코드 다른 환경에서 Version 이슈로 실행되지않을 가능성이 존재함 -> 도커를 통해 라이브러리 각 종속성문제해결
- Container에 해당 코드가 실행되게하는 종속성을 지니고 있어 회사내부에서 서로다른 팀간 서로다른 환경에서도 실행가능
- 동시에 여러작업을 진행할경우 각 작업의 버전이 충돌되지않게 방지

# Virtual Machine 장단점
## ![image](https://user-images.githubusercontent.com/54635552/178085094-80e1a7fc-dc8b-450a-a6dd-3e666ffd504c.png) 

# 도커 구조
## ![image](https://user-images.githubusercontent.com/54635552/178085210-66219e33-a421-481a-973b-652ab849fa76.png)

# 도커 Vs Virtual Machine
## ![image](https://user-images.githubusercontent.com/54635552/178085337-270f8954-e597-40ed-bd8b-740d00064970.png)

# 로컬에서 도커 실행하기
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

# 도커에서 node 실행
- docker hub에서 image 가져와서 설치하기
- docker run node : 로컬에 node image없어서 docker hub에서 설치받아서 실행
## ![image](https://user-images.githubusercontent.com/54635552/178096453-393994a8-7018-4f10-b28b-a2e84aa53dfa.png)
- docker ps -a : 도커가 생성한 모든 프로세스 확인
## ![image](https://user-images.githubusercontent.com/54635552/178096546-ac3ac063-d951-4edd-92fd-4092eef9fe19.png)
- docker run -it node : Container안에 있는 node 명령어 shell 바깥으로 나오게하기
- 현재 컨테이너 내부에서 node가 실행중이고, 해당 명령어 shell을 바깥으로 나오게하여 상호작용하게함
- node는 local 컴퓨터에서 작동되고있는것이아니라, 컨테이너 내부에서 실행중
- 이미지 는 설정파일, 코드를 저장하고있고, 해당 이미지 기반으로 run을하면 Container가 생성됨 

# Custom Dockerfile 생성
## ![image](https://user-images.githubusercontent.com/54635552/178097565-c313590d-6469-4e5c-a7f2-eabbe97c19b8.png)
- FROM : 특정 이미지 이름 or docker hub 상 이미지 이름 기반에서 이미지 작성하게 ex)FROM node
- WORKDIR : 작업디렉토리 지정, 도커 내부에서 해당 작업디렉토리에서 작업하게 설정
- COPY : COPY [컨테이너 외부 경로] [이미지가 복사되어야 할 위치] ex) COPY . /app : 현재폴더의 모든파일 도커의 /app 경로로 이동
- RUN npm install : node 종속성 설치
- EXPORT : 도커 내부의 포트 열기 ex) EXPORT 80
- CMD ["node","server.js"] : RUN과 CMD 차이는 CMD는 이미지 기반으로 컨테이너가 시작될때만 실행되는코드
- docker build [dockerfile 경로] : dockerfile을 기본으로 새 커스텀 이미지를 빌드해라
- docker run -p : -p [액세스 하려는 로컬 포트]:[내부 도커 컨테이너 포트]
## ![image](https://user-images.githubusercontent.com/54635552/178098029-6f89137f-32d5-4352-a2ce-3f584296913e.png)
- docker ps : 현재 실행중인 docker process 표시

# 도커의 이미지와 컨테이너 개념
- Image는 읽기전용으로 과거시점에 docker build . 을 했을경우 그 시점기준 코드로 Image build됨
- 실시간 local환경의 code 변경이 image에 갱신되지않음
- 이미지를 새롭게 build 해야지 해당 내용이 갱신됨
- Docker에는 캐쉬개념이있어서 변경사항없이 동일 내용으로 build을 할시에 cache를 이용하여 빠르게 build됨
- 이러한것은 레이어 기반 아키텍처를 사용하고있음
- 코드를 변경하여 다시 build하면 캐시의 일부 결과만을 사용하므로 속도가 비교적느려짐
- docker는 레이어 구조이므로 dockerfile의 순서를 바꾸어서 최적화를 시킬수 있음, 파일만 바꾸고 패키지 종속성이 변경되지않을 경우
- dockerfile의 RUN npm install 순서를 바꾸어서 더 빠르게 build 하는 최적화를 가능하게함

# docker run과 start
- docker --help : 도커 명령어 나옴
- docker run : 이미지 기반으로 새로운 컨테이너 만들고 실행하기, 이미지가 변경되지않을경우 새 컨테이너를 안만들고 기존 컨테이너를 실행시키면됨
- docker start [도커 이름 or 컨테이너 ID] : 해당 컨테이너 실행(새롭게 컨테이너 만들지않고 컨테이너 실행)

# attached와 deattached 모드
- docker start : deattached모드 백그라운드 실행 
- docker run : attached모드 포그라운드 실행, 컨테이너의 출력결과를 출력함
- docker run -d : deattached모드로 실행
- docker container attach [콘테이너 이름] : 다시 attached 모드로 변경
- docker logs [컨테이너 이름] : 출력된 과거의 로그 확인 가능
- docker logs -f [컨테이너 이름] : 로그 수신창으로 접속
- docker run -it : Stdin 표준입력을 할수있는 터미널 생성 
- docker start -a : 수신 전용 모드로 실행
- docker -a -i : 수신, 입력 둘다하는 모드로 실행

# docker 컨테이너와 이미지 삭제
- docker rm [컨테이너 이름] : 해당 컨테이너 삭제(실행중인 컨테이너를 삭제불가능)
- docker images : 현재 로컬의 도커 이미지 리스트를 출력
- docker rmi [이미지 ID] : 도커 image 삭제, 해당 image로 존재하는 container가 없어야만 삭제가능
- docker run --rm : 해당 컨테이너가 종료될때 자동으로 컨테이너 삭제되게하기
#### 출처 : Docker & Kubernetes: 실전 가이드(Udemy)


