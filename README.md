
# Guidance for local-remote repository

---

## Setting

1. C드라이브에 `algorithm_study` 폴더 생성

![setting](/images/guidance_git/image_setting_01.png)

2. Visual Studio Code 우측 상단 `File` -> `Open Folder` -> `algorithm_study` 폴더 선택

![setting](/images/guidance_git/image_setting_02.png)

3. ctrl + \` -> `TERMINAL` -> `Git Bash`

![setting](/images/guidance_git/image_setting_03.png)

4. `git clone https://github.com/eac-xii/ssafy_algorithm_study.git .`

![setting](/images/guidance_git/image_setting_04.png)

5. `git config --global user.email "\_(자신의 깃헙이메일)\_"`

	ex) git config --global user.email "_eacxii1870@naver.com_"

![setting](/images/guidance_git/image_setting_05.png)

6. `git config --global user.name "\*\*(자신의 이름)\*\*"`

	ex) git config --global user.name "**eacxii1870**"

![setting](/images/guidance_git/image_setting_06.png)

7. `touch .gitignore`

![setting](/images/guidance_git/image_setting_07.png)

8. `.gitignore` 파일에 `.gitignore` 기입

	```ps - (중요) 원격 레포지토리에 푸시하지 않을 파일은 미리 .gitignore 파일에 확장자명을 포함하여 기입해주세요!! [폴더는 확장자명 없이 기입]```

![setting](/images/guidance_git/image_setting_08.png)

---

## Push

1. bash를 켜시고 현재 최종경로가 아래 사진인 상태에서 `git switch [자기 팀 ex)team3]`

	ex) git switch team3

![push](/images/guidance_git/image_push_guidance_01.png)

2. 현재경로 우측의 브랜치가 (자신의 팀) 사진의 빨간 박스와 같이 바뀔경우 파란 박스처럼 (자신의 팀)의 브랜치에 있는 파일들이 자동이로 로컬 레포지토리로 들어옵니다. 항상 모든 작업은 _자신의 팀 브랜치_에서만 부탁드립니다. **main인 상태에서 절대 사용금지!**

![push](/images/guidance_git/image_push_guidance_02.png)

3. 작업의 변경사항이 생기면 `Untracked` -> 약식 `U` 라고 표시됩니다.

![push](/images/guidance_git/image_push_guidance_03.png)

4. `git add 파일명.확장자 혹은 .`을 이용하여 스테이징공간에 추가하면 `Added` -> 약식 `A` 라고 표시됩니다.

![push](/images/guidance_git/image_push_guidance_04.png)

5. 모든 진행 전후에는 `git status`로 진행사항 확인해주세요!

![push](/images/guidance_git/image_push_guidance_05.png)

6. 또한 커밋 전 `git log --oneline`으로 마지막 커밋 메세지 버전을 확인해주시고 사진과 같이 메세지 형식 준수해서 작성해주세요!

![push](/images/guidance_git/image_push_guidance_06.png)

7. 마지막으로 푸시할 때 명령어 구문 마지막은 **(자신의 팀)**으로 작성해주시면 됩니다!

![push](/images/guidance_git/image_push_guidance_07.png)