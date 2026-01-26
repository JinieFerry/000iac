STEP 1. 새 Windows 데스크탑에서 할 일 (사람이 직접)
1️⃣ 관리자 권한 PowerShell 열기

시작 버튼 → PowerShell

우클릭 → 관리자 권한으로 실행

2️⃣ WinRM 최초 1회 설정
```
#아래 그대로 복붙:

Set-ExecutionPolicy RemoteSigned -Force

$ProgressPreference = 'SilentlyContinue'
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
Invoke-WebRequest https://raw.githubusercontent.com/ansible/ansible-documentation/devel/examples/scripts/ConfigureRemotingForAnsible.ps1 -OutFile ConfigureRemotingForAnsible.ps1
.\ConfigureRemotingForAnsible.ps1 -SkipNetworkProfileCheck
```

 끝나면 창 닫아도 됨
 
<img width="859" height="732" alt="image" src="https://github.com/user-attachments/assets/15a02e94-59b0-4c53-b6da-20b8db4bc00f" />

3️⃣ 새 데스크탑 IP 확인 (중요)
```
ipconfig
```
<img width="859" height="732" alt="image" src="https://github.com/user-attachments/assets/589ee229-ec79-4d39-8b2e-1d4ebcd24991" />

