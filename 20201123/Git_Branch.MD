# 2020.11.23

## Git Branch
- Version Control Manager는 본래 Branch의 기능이 있지만 무겁고 불편함.
- Git은 이를 혁신적으로 해결함.
- Git Branch는 혁신 가볍고 빠르다. 하지만 효용에 대한 대가가 따른다.
> Branch는 언제 필요한가?
> - 고객사에게 제공하는 특별한 기능. Customizing 기능을 추가할때.
> - 필요없을 것 같은 개발 건. 나중에 버리기 쉬움.
> - main-test 분기해야할 때 branch를 사용함.

### # Branch 생성.
- Branch 생성.
- 현재 속해있는 master Branch와 같은 상태로 그대로 복사한다.
```
git branch [branch-name]
```

- Branch Checkout.
- Checkout Branch을 바라보고 작업함.
```
git checkout [branch-name]
```

- Branch 생성 및 Checkout
```
git checkout -b [branch-name]
```

### # Branch 정보확인.             
- graph / 다른 Branch Commit 상태가 각자 다를때.
- oneline / 한 줄로 표현.
- branches / 모든 Branch 지칭.
- decoratde / Branch, Commit 상태 확인.
```
git log --banches --decorate --graph --oneline
```

- A Branch에는 없고 B Branch만 존재하는 것.
```
git log A..B
```

- A Branch에는 없고 B Branch만 존재하는 것. + Code 추가.
```
git log -p A..B
```

### # Git Branch 병합.
- A Branch로 B Branch를 병합(A <-- B)
```
git checkout A
git merge B
```

- Branch 삭제.
```
git branch -d "Branch-name"
```

- Merge 안했을 때 강제로 삭제도 가능.
```
git branch -D "Branch-name"
```

### # Branch 병합 시 충돌해결.
- File이 다를 때 자동으로 Merge.
- File이 같더라도 수정내용이 다르면 자동으로 Merge.
> 문제 발생! 같은 파일 + 수정 위치가 같을 때.
>- 해당 File이 변경되어있음.
>- `<<<<`HEAD 현재 Branch 변경사항.
>- `>>>>`"Branch-name" 변경사항.
>- 잘 보고 판단하여 수정 -> git add -> git commit
>- 해결!!!!!!!!!

### # Git stash / 감추다, 숨기다.
> stash 언제?
> - Branch 활발히 작업 -> 작업이 끝나지 않음.
> - 다른 Branch checkout 해야 할 때.
> - Commit 하지 않으면 checkout 할 수 없다.
> - 새로운 Branch에 영향을 주기 때문에.
> - Branch의 가장최근 Commit.
> - HEAD의 Version으로 이동해서 다른 Branch로 Checkout 가능함.

- Working Directory 내용이 Save.
- 작업중 변경사항이 Save.
- 작업이 끝나지 않더라도 다른 Branch 이동가능함.
```
git stash (save)
```

- 임시 저장이 살아남.
```
git apply
```

- 임시저장 list 확인.
```
git list
```

- 임시저장 없는 상태로 reset.
```
git reset --hard (HEAD)
```

- 최근 stash list 하나 삭제
```
git stash drop
```

- apply + drop
```
git stash pop
```