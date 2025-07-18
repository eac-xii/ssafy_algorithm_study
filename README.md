
# Guidance for local-remote repository

---

## Setting

1. C드라이브에 algorithm_study 폴더 생성

![setting](/images/guidance_git/image_setting_01.png)

2. Visual Studio Code 우측 상단 File -> Open Folder -> algorithm_study 폴더 선택

![setting](/images/guidance_git/image_setting_02.png)

3. ctrl + ` -> TERMINAL -> Git Bash

![setting](/images/guidance_git/image_setting_03.png)

4. git clone https://github.com/eac-xii/ssafy_algorithm_study.git .

![setting](/images/guidance_git/image_setting_04.png)

5. git config --global user.email "*(자신의 깃헙이메일)*"

	ex) git config --global user.email "*eacxii1870@naver.com*"

![setting](/images/guidance_git/image_setting_05.png)

6. git config --global user.name "**(자신의 이름)**"

	ex) git config --global user.name "eacxii1870"

![setting](/images/guidance_git/image_setting_06.png)

7. touch .gitignore

![setting](/images/guidance_git/image_setting_07.png)

8. .gitignore 파일에 .gitignore 기입

	`ps - (중요) 원격 레포지토리에 푸시하지 않을 파일은 미리 .gitignore 파일에 확장자명을 포함하여 기입해주세요!!`

![setting](/images/guidance_git/image_setting_08.png)