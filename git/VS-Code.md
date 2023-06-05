# VS Code

## VS Code에서 git clone
- F1 -> git clone -> 토큰 연동 -> 레파지토리 선택 -> localPc 저장위치 선택 -> clone완료

<br>

## VS Code에서 git commit & push
### 터미널 명령어
- git add . : 변경사항이 있는 파일 전부를 대상으로 저장
- git commit -m "커밋 메세지"
- git push 원격저장소명 브랜치명
- git remote : 저장소명 확인
- git push -u 원격저장소명 브랜치명 : 다음 push부터 git push로 가능하게 함
- git config --global push.default current : 현재 브랜치를 기준으로 원격저장소에 푸쉬
- git reset HEAD^ : 커밋 취소
- git push origin master : 강제 푸쉬

