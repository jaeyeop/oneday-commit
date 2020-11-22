# 2020.11.22

## Git Version Control Management.

### # 저장소 만들기
- Create an empty Git Repository 
- Reinitialize
- 여기서 Git 작업할게.
- 해당 폴더 .git File이 생성되고 이는 Version 정보가 들어간다.
```
git init
```

### # Git이 관리할 대상으로 파일 등록             
- f1.txt File Create/Modify.
```
vi f1.txt
```
- Git의 현재 상태확인.
- Untracked Files
- Git에게 Version 관리 시작하라고 할 때까지 무시함.
```
git status
```
- Change to be commited
- 관리 시작 요청. Stage Area 입성.
- Commit 대기 Stage Area로.
```
git add f1.txt
```

### # Git이 관리할 대상으로 파일 등록   
- Version ? 어떤 작업이 완결된 상태를 버전이라고 칭함.
- Config 설정.
- Git 관리에 대한 대상자 설정.
```
git config --global user.name "jyjeong"
git config --global user.email "jyjeong@_____.com"
```

- Git commit.
```
git commit
```

- Git Log 확인.
- Git Version 확인.
```
git log 
```

### # 변경사항 확인하기
- 소스 단위 log 확인가능.
```
git log -p
```

- 해당 Commit-Id를 가진 Version 하위만 Show
```
git log [Commit-Id]
```

- 두 Commit-Id를 가진 Version의 소스를 비교함.
```
git diff [Commit-Id]..[Commit-Id]
```

- Commit 하기 전 diff로 확인이 가능함.
- 작업 전/후 Code 차이점을 파악할 수 있는 마지막 기회를 제공함.
- git add 후 볼 수 없음. <- Stage Area 가기 전.
```
git diff
```

### # 과거의 버전으로 돌아가기
- 실제로 Version 관리에는 남아있으며 나에게만 보이지 않음.
- Github 원격 저장소에 올렸을 때는 절대로 Reset 금지.
- 안쓴다고 생각하면 됨.
```
git reset [Commit-Id] --hard
```