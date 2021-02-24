---
id: 0
title: "🛫 Starchaser의 Blog 이륙합니다"
subtitle: "Handmade-Blog를 이용해 Github Pages 세팅하기"
date: "2021.02.24"
tags: "블로그"
---

개발자를 희망하는, 컴퓨터공학과 학생으로서 쌓여가는 지식과 스쳐가는 아이디어를 기록하기 위해 블로그를 만들었습니다. 노션 블로그 https://starchaser.cf 는 개인적인 메모 창고와 서재의 기능을 하고, github pages에는 개발 경험과 아이디어를 끄적일 예정입니다.

## 개발자스럽게, 블로그 이륙하기

평소에 개발자들의 블로그, 특히 평범함을 벗어나 자신만의 길을 닦아가는 사람들의 기록을 염탐하는 것을 좋아합니다. 특히 [박성범 님의 블로그](https://parksb.github.io)를 자주 정찰하는데, 특유의 깔끔함과 톡톡 튀는 글 내용이 마음에 들었습니다.

최근 군대를 제대하고, 복학해서 들을 [시스템 프로그래밍](http://csapp.cs.cmu.edu/3e/home.html) 수업을 준비하면서 컴퓨터에 대한 기본 이해를 요구받기 시작했습니다. 더불어 전산학부 학부생으로 살아가기 위해 기본적인 도구를 갖추고자 [MIT의 Missing Semester](https://missing.csail.mit.edu/)를 공부하면서, 익히고 연습한 기억을 기록해야 할 필요성을 느꼈습니다.

고로 저만의 공간을 하나 마련하기로 했습니다. 깃과 텍스트 에디터 사용을 연습할 겸 Github Pages를 열기로 했고, 마침 박성범님이 [Handmade Blog](https://github.com/parksb/handmade-blog)를 공개해 주셨기에 이 템플릿을 사용하기로 했습니다.

### 이륙 과정

저도 개발자의 세계를 이제 막 엿보기 시작했기에, npm과 git을 이용한 블로그 생성에는 애를 먹었습니다. 혹시 되돌아볼 일이 있을지도 모르기에, 이륙 과정을 기록해 놓기로 했습니다.
모든 내용은 https://github.com/parksb/handmade-blog 를 참고하여 작성했습니다.

먼저 https://github.com 에 본인의 계정으로 로그인합니다.
[handmade-blog repository](https://github.com/parksb/handmade-blog)로 가서, repository를 fork합니다. 이 과정에서, 모든 구성물을 가져오기 위해 `include all branches`를 체크합니다.

Fork를 완료했으면, 본인 repository의 settings 탭에 들어가 GitHub Pages의 source branch를 `gh-pages`로 설정합니다. 이를 완료하면 `https://{YOUR_ID}.github.io`를 통해 자신의 블로그로 접속할 수 있게 됩니다.

이후 repository를 clone하고, node packages를 깔아 생성된 주소에 내용을 입력합니다.

```css
$ git clone https://github.com/{YOUR_ID}/{REPOSITORY_NAME}.git # git clone https://github.com/alexhonggi/alexhonggi.github.io.git
$ cd {REPOSTORY_NAME} # cd alexhonggi.github.io
$ npm install
```

main page의 내용은 `services` 디렉토리의 `config.json` 파일을 수정하여 바꿀 수 있습니다.

```css
{
  "blogTitle": "Starchaser",
  "blogSubtitle": "Honggi Lee"
  "article": {
    "tableOfContents": true
  }
}
```
파일을 수정한 뒤에는, `npm start` 스크립트를 실행해 로컬 서버를 열어 수정된 사항을 확인합니다. 로컬 서버는 `http://localhost:1234/`에 오픈됩니다.

```css
$ npm start
```
로컬 서버를 열고 반영하고 싶은 요소들이 모두 반영됨을 확인했다면, 모든 변경사항을 원격 저장소에 커밋하고 푸시합니다.

```css
$ git add ./services/config.json
$ git commit -m "Set the blog title and subtitle"
$ git push origin master
```

깃과 깃헙을 통해 원격 저장소에 로컬 저장소의 변경점을 동기화했다면, `deploy` 스크립트를 사용해 웹사이트를 호스트할 준비가 되었습니다. `npm run deploy`를 통해 로컬 파일에 `dist` 디렉토리를 만들고, `gh-pages` 브랜치에 이를 푸시해줍니다. GitHub Pages는 `gh-pages`를 자동적으로 참고해 당신의 웹사이트를 `https://{YOUR_ID}.github.io`에 호스트 해줄 것입니다.

```css
$ npm run deploy
```

### 블로그 가꾸기

위의 과정을 통해 무사히 당신의 GitHub Pages를 이륙시키는 것에 성공했다면, 이제는 글을 작성해 내부를 가꿀 수 있습니다. 글을 작성하고 게시하는 법은 `config.json`을 수정해 블로그를 이륙시키는 과정과 비슷합니다.

1. `_articles` 또는 `_works` 디렉토리에 글을 작성합니다.
2. `npm run publish article` 또는 `npm run publish work`을 통해 마크다운으로 작성된 컨텐츠를 HTML로 변환합니다.
3. `npm start` 스크립트를 통해 변경된 사항이 반영되었는지 확인합니다.
4. 반영하고 싶은 변경점을 커밋하고 푸시한 뒤, `npm run deploy`를 통해 적용합니다.

글을 블로그에 반영하는 데에는 위의 과정이면 충분하지만, [마크다운 활용](https://whatismarkdown.com/)이 익숙하지 않은 사람들에게는 텍스트 에디터를 사용해 블로그 글을 작성한다는 것은 고역일 것입니다. 그동안 WYSIWYG에만 익숙해 왔던 제게도 마크다운 글 작성법에 대해 익숙해져야 할 필요성이 있었습니다. 고심 끝에 일상에서 빠르게 컨텐츠를 수집하고 기억에 남기 쉽게 기록해야 하는 일은 [노션 블로그](https://starchaser.cf)에 작성하기로 했고, 개발 관련 공부의 성과와 아이디어 기록에는 [GitHub Pages](https://alexhonggi.github.io)를 사용하기로 했습니다.

먼저 프로젝트의 구조를 이해할 필요가 있습니다.
본인의 로컬 저장소 (저의 경우에는 `/Users/starchaser/alexhonggi.github.io`)에서 아래의 내용을 확인할 수 있습니다.

- `_articles`: 블로그 포스트 파일 모음
- `_works`: 포트폴리오 모음
- `app`
  - `assets`: 이미지, 글꼴 등과 같이 HTML 파일로 가져올 파일입니다.
  - `public`: `publish` 스크립트에서 생성된 HTML 파일입니다. `server`와 `dist` 디렉토리는 이 디렉토리를 기반으로 합니다. 이 디렉토리 아래의 파일들은 직접 변경할 일이 없습니다.
    - `article`: `_articles` 디렉토리에서 전환된 HTML 파일입니다.
    - `work`: `_works` 디렉토리에서 전환된 HTML 파일입니다.
  - `src`: HTML 파일에서 가져올 소스 코드입니다.
    - `css`: `build` 스크립트에서 생성된 css 파일입니다.
    - `scss`
    - `ts`
  - `staic`: `robot.txt`, `sitemap.xml`등과 같이 `build` 스크립트로 컴파일되지 않은 정적 파일입니다. `build` 스크립트는 이 디렉토리 아래의 모든 파일을 `dist` 디렉토리에 복사합니다.
  - `templates`: EJS 템플릿 파일입니다. `publish` 스크립트는 이 디렉토리 아래의 템플릿을 HTML 파일로 변환합니다.
- `dist`: `build` 스크립트로 컴파일된 파일입니다. `deploy` 스크립트는 이 디렉토리를 기반으로 GitHub Pages에 웹 사이트를 배포합니다. 이 디렉토리 아래의 파일은 변경할 일이 없습니다.
- `server`: `build` 스크립트로 컴파일된 파일입니다. `start` 스크립트는 로컬 서버를 엽니다. 디렉토리 아래의 파일은 변경할 일이 없습니다.
- `services`: `publish` 스크립트를 구현하는 소스 코드입니다.
  - `classes`
  - `models`
- `tools`: 다양한 npm 스크립트를 구현하는 소스 코드입니다.

다음은 직접 작성시 참고할 마크다운 문법입니다.

`구절 강조`: backtick 두개로 강조할 구절을 감쌉니다.
[하이퍼링크](https://ko.wikipedia.org/wiki/%ED%95%98%EC%9D%B4%ED%8D%BC%EB%A7%81%ED%81%AC): 하이퍼링크를 삽입하고 싶은 부분을 대괄호로 감싸고, 뒤이어 괄호로 감싼 링크를 입력합니다.
인용[^1]: 인용하고 싶은 구절 뒤에 대괄호로 감싼, 캐럿과 이어진 숫자로 표시한다.
강조 표시: 강조하고 싶은 부분은 css를 적용하여 표시한다. backtick 세 개를 이용해 css를 감싼다.
제목, 부제목: # 을 삽입하여 글씨의 크기를 조정한다.
이미지 삽입: 하이퍼링크와 동일하나 앞에 느낌표를 붙인다. 대괄호 안에는 캡션을 넣는다.

여기까지가 기본적인 글 작성 방법입니다. 이제 블로그를 채워나갈 일만 남았습니다. 어떤 글들로 채워 나갈지 고민해보아야겠습니다.

[^1]: 인용 연습
