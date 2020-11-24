# 2020.11.24

## 원격저장소(Remote Repository)
- 소스코드 백업
- CO-WORK 협업

### # 원격저장소 / 지역저장소 
- 저장소 기능만 수행가능한 Git 생성 Option
- .git 내부에 File을 생성함.
- 원격저장소 / 순수하게만 작업/수정 불가.(가상)
```
git init --bare
```
### # 원격저장소를 지역저장소로 복제(Github)            
- 원격저장소 제공 서비스 중 하나 Github
- Open Source인 경우 Github 무료제공
- 해당 디렉토리에 원격저장소 repo.를 Clone.
```
git clone [github-url] [directory]
```

- git 로그를 거꾸로 보다.
```
git log --reverse
```

- Commit-Id 당시의 소스로 회귀한다.(checkout)
```
git checkout [Commit-Id]
```

- Remote를 추가한다.
- [Remote-Name] 원격 별칭
- [Remote-Url] 원격 실제 주소
- 여러개 설정가능함.
```
git remote add [Remote-Name] [Remote-url]
```

- Remote 삭제
```
git remote remove [Remote-Name]
```

### # 원격저장소 <-> 지역저장소 작업
- Push A B
- A(원격리모트) <- B(로컬브랜치) 변경사항을 Push한다.
- -u Setting.
```
git push -u A B
```

- B(로컬브랜치) <- A(원격리모트) 변경사항을 가져온다.(Pull)
- 공개저장소를 쓰고있기 때문에 로그인하지 않아도 된다.
- 모든 저장소는 버전/소스코드를 가지고 어디서든 작업가능하다.
- 절대 날아갈 확률이 거의거의 없다.
```
git pull
```