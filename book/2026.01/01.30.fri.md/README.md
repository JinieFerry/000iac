# 우분투에서 로그인 네임과 마스터 패스워드 변경: vmmaster1,vm1,vm2
```
# 마스터 Full Name []: ferry로 변경
sudo chfn master
# room number 등등은 enter로 생략

# 마스터 패스워드 변경 : jj968096 -> 1234로 변경 
sudo passwd master

# 변경사항 적용하기 위해 리부팅
sudo reboot
```

확인
```
whoami
→ master

id
→ uid=1000(master)
→ groups= adm, sudo, docker 관련 그룹 포함

```

### 패스워드 : 2026.01.30.금 기준
+ master passwd: 1234
+ BECOME passwd: 1234

### 호스트네임 통일
```
# 1. vmmaster1에서 호스트네임 설정
sudo hostnamectl set-hostname vmmaster1

# 2. vm1에서 호스트네임 설정
sudo hostnamectl set-hostname vm1

# 3. vm2에서 호스트네임 설정
sudo hostnamectl set-hostname vm2

# 확인
hostname
cat /etc/hostname

```
### 호스트네임으로 간단하게 DNS 접속 가능하게 설정
+ 아이피를 바로 hosts에서 찾을 수 있음
+ ssh master@vm1같은 형식으로 간단하게 DNS 접속 가능
+ /etc/host는 자기 이름 짓는 파일<->/etc/hosts DNS 서버 이름 짓는 파일
```


sudo vi /etc/hosts

#vm1에서
127.0.0.1 localhost 
192.168.115.251 vmmaster1
192.168.115.2 vm2

#자기자신이 localhost : vm1에서는 192.168.115.1이 localhost

#확인
cat /etc/hosts
```
목적: 아래와 같은 형식으로 접속 가능하도록     
> ssh master@vm1     
> ssh master@vm2      
> ping vmmaster1      

