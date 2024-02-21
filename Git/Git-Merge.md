# Git Merge

Git branch를 다른 branch와 합치는 과정을 Git Merge라고 한다.

## Fast Forward Merge

Fast Forward Merge는 가장 기본적인 Merge이다.

Fast Forward Merge는 현재 브랜치의 HEAD가 병합 대상 브랜치의 HEAD까지 옮기는
Merge이다.

![image](https://github.com/pmsu2007/TIL/assets/75938496/a5537b92-4917-4336-aa43-a6968fd2b15b)

### Fast Forward Merge의 한계점

Fast Forward Merge는 중간에 다른 커밋이 껴있고, 해당 커밋이 같은 부분을 수정했다면 Merge Conflict이 발생하여 Merge가 제대로 동작하지 않는다.

## Merge Commit

fourth commit과 fifth commit이 같은 부분을 수정했다면 Merge Conflict가 발생한다.

Merge시 Conflict가 발생한 파일은 git status가 both modified로 바뀐다.

### Conflict

![image](https://github.com/pmsu2007/TIL/assets/75938496/f4bfc85d-4b9a-44db-8cd1-ab38cdab3be6)

```
<<<<<<<<<<< HEAD
[ 현재 브랜치의 변경사항 ]
===========
[ 머지 대상 브랜치의 변경사항 ]
>>>>>>>>>>> [대상 브랜치]
```

Conflict는 `<`, `=`, `>` 를 모두 제거한 후 최종으로 남길 코드만 반영하여 `git add` → `git commit` 해주면 된다.
