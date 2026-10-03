# 클라우드 체크아웃 안내

이 저장소는 ChatGPT의 클라우드 작업 공간에서 바로 살펴보고 개발할 수 있는
정적 블로그 생성기 프로젝트입니다.

## 프로젝트 구성

- `_articles`: 블로그 글의 Markdown 원본
- `_works`: 포트폴리오 작업의 Markdown 원본
- `app/templates`: EJS 페이지 템플릿
- `app/src`: TypeScript와 SCSS 소스
- `services`: 글과 작업을 발행하는 TypeScript 코드
- `tools`: 로컬 실행, 빌드, 발행, 배포 스크립트

## 클라우드 환경 준비

이 프로젝트는 Node.js 프로젝트이며 `package-lock.json`을 포함합니다. 재현 가능한
설치를 위해 다음 명령을 설치 스크립트로 사용할 수 있습니다.

```sh
npm ci
```

설치 후에는 다음 명령으로 상태를 확인합니다.

```sh
npm test
npm run build
```

로컬 미리보기 서버는 `npm start`로 실행되며 기본 주소는
`http://localhost:1234/`입니다.

## 소스 관리

클라우드 작업 공간의 파일 상태는 Git 원격 저장소를 대신하지 않습니다. 중요한
변경 사항은 브랜치에 커밋한 뒤 원격 저장소에 푸시하고 Pull Request로 검토하세요.
새 클라우드 작업을 시작할 때는 게시된 환경을 기반으로 별도의 격리 작업 공간이
만들어지므로, 작업 사이에 전달할 변경 사항은 반드시 Git에 저장하는 것이 좋습니다.
