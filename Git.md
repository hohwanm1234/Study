# Git

- git init : 폴더 감지 명령어
- git add 파일명 : 폴더 선택
- git commit -m '메모' :  commit + 메모
- git add . : 모든 파일 스테이징
- git status : 스테이터스 확인
- git log --all --oneline : 로그 확인
- git diff : 최근 커밋과 현재코드 비교
- git difftool commitid : 현재파일 / 특정 커밋 id랑 비교 가능
                        : 2개 입력시 둘이 서로 비교
- git switch - 브랜치 변경

# Git 전략 방식
- 3-way merge : 일반적인 merge 방식
![3-way merge](https://github.com/hohwanm1234/Study/assets/46438755/b6b900df-35de-4e35-bdfc-911d485fced8)

- fast-forward merge : 새로운 브랜치에 그대로 merge
![fast-forward merge](https://github.com/hohwanm1234/Study/assets/46438755/2bb0c76a-fc36-4626-8c82-8c210531e711)

- git branch -d/D 브랜치명 : 삭제
- rebase : history 등에서 깔끔하게 보이기 위해 사용 (merge 할 main 브랜치 변경)
![rebase](https://github.com/hohwanm1234/Study/assets/46438755/8f164b39-3295-4f32-b50e-ccaf62b97aaf)

- squash : 다른 브랜치에서 하던 commit을 한번에 merge 후 메인 브랜치에 이어서 merge (깔끔하게 보이기 위함)
![squash merge](https://github.com/hohwanm1234/Study/assets/46438755/ed0415fa-59d7-4cb4-b34a-8d1c851db0b4)

- git restore 파일명 : 파일 복구
                    --sourece 커밋 아이디 : 커밋아이디 시점으로 변경
                    --staged : 스테이징 취소
- git revert 커밋아이디 : 커밋 취소
- git reset --hard 커밋아이디 : 아이디 시절로 하드 리셋

- git flow :  깃플로우 전략
![깃 플로우](https://github.com/hohwanm1234/Study/assets/46438755/b9e80b0b-cbe2-4293-a2bf-fb1835d72c8c)

- Trunk-based : Trunk-based 전략
![Trunk-based](https://github.com/hohwanm1234/Study/assets/46438755/b704ad26-0c24-4064-8828-632e1fd10884)
