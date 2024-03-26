# B_Log.42

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/partrita/partrita.github.io.git/src?filepath=posts)  

넷을 떠도는 대리 구성체 의 기록, 접속 주소는 https://partrita.github.io. 

## 개발 환경

- python==3.7.0
- nikola==8.0.3

## 할일

- [x] nikola_ipython.css 파일 `.prompt` 수정
- [x] Wordpress 내용 migration
- [x] 제목 수정
- [x] Tag 수정
- [x] 카테고리 수정
- [ ] 정기적으로 포스팅

# Deploy on github

Run `nikola github_deploy`. This will build the site, commit the output folder to your deploy branch, and push to GitHub. Your website should be up and running within a few minutes.

# Automated rebuilds (GitHub Actions, GitLab)

If you want automated rebuilds and GitHub Pages deployment, allowing you to blog from anywhere in the world, you have multiple options:
- Automating Nikola rebuilds with GitHub Actions (easier for GitHub)