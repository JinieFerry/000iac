1. 도커 디렉토리 만들기
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c63f4eb7-04d6-40e2-ba54-4681658c0e3d" />
```
mkdir docker
cd docker/
mkdir doc_nginx
ls
```

2.index.html 파일 만들기
```
# Nginx를 베이스 이미지로 사용하여 html 파일을 복사하는 설정
cat <<EOF > Dockerfile
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html
EOF
# 이미 만들어져 있는 거 가져오기
cat /usr/share/nginx/html/index.html  > ./index.html
```

3. 도커 파일 만들기 (vi로 해도 됨) index.html 파일 COPY명령이 실행이 되어야 함
```
vi index.html
```
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/46eda4b5-856f-4825-b051-c7581052e6f2" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5755af4e-bef1-4bb5-aa09-57affafbb98f" />

# 4. 이미지 빌드 (-t는 태그/이름 설정)
```
docker build -t my-web-app:v1 .

```
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/3769da1e-a4c0-4ec1-af06-c301db1b6742" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0176104c-bbf2-48ef-9b55-d3e78a5db6e5" />

5. 도커 이미지 생성 됐는지 확인
```
docker images
```
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/28d8e650-853f-4c8e-99bb-9dd815a2f17f" />

my-web-app:v1 이 생기고,ID는 해시값으로 나옴

6.빌드 : 워드쳐 둔 걸 이미지로 만든다 (컴퓨터가 알아듣는 바이너리) 아직까진 저장된거니까 실행시키기
# -d는 오래 걸릴 때 쓰는 옵션 다른 거 할 수 있게
```
docker run -d -p 8080:80 --name web_con1 my-web-app:v1
```
6-2. 에러 : 8080 포트가 이미 쓰는 중
```
#8080포트 확인
sudo lsof -i :8080

#docker프로세스 내부 따로 확인
docker ps

#nginx 확인 
sudo systemctl status nginx

#포트 다르게 받기
docker run -d -p 8088:80 --name web_con1 my-web-app:v1
```
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/babe4870-542f-42ab-872b-7e703556dd55" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/897f6c16-e810-412e-9c3b-43ac8434790e" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/84573fda-8962-4fe8-b61e-f4528af93e22" />

앞서 만든 my-wbe-app 삭제
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/55dfbd4d-aeb0-4253-b616-3d82b82c292f" />

7. 이름 바꾸기 (Tag 변경)
도커 허브에 올리기 위해서는 사용자ID/이미지명 형식을 갖춰야 합니다. tag 명령어로 이름을 바꿀 수 있습니다.
```
# docker tag [기존이미지:태그] [새이름:태그]
docker tag my-web-app:v1 jinieferry/nginx01:v1

# 바뀐 이름 확인
docker images | grep my-web-app
```

8. 도커 허브 업로드 (Push) 및 다운로드 (Pull)
빌드한 이미지를 원격 저장소에 저장하고 다시 내려받습니다.
```
# 도커 허브 로그인 (발급받은 토큰 사용)
docker login -u ferryjin
#두번째 토큰 사용

#  이미지 업로드
docker push ferryjin/my-web-app:v1

#  로컬 이미지 삭제 (테스트를 위해)
docker tag my-web-app:v1 ferryjin/my-web-app:v1

#  도커 허브에서 이미지 다운로드
docker pull ferryjin/my-web-app:v1
```

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/989a6f05-439f-42cc-b459-847e0bd13e2f" />

9.docker인프라로 들어각기
```
docker exec -it web01 /bin/bash
```
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/96695a5d-a152-4dc9-97e4-c676bfa09666" />


