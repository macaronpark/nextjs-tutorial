# nextjs-tutorial <!-- omit from toc -->

Next.js 공식 튜토리얼 [learn/dashboard-app](https://nextjs.org/learn/dashboard-app)을 따라가며 학습하고 기록합니다.

- 학습 목적
  - Next.js의 기본 개념 및 구조 이해
  - 이후 개인 프로젝트나 포트폴리오에 활용할 기초 다지기
- 시작하기

  ```shell
  corepack enable

  pnpm install
  pnpm dev
  ```

<br>

## 학습 기록 <!-- omit from toc -->

- [Ch 1. Getting Started](#ch-1-getting-started)
- [Ch 2. CSS Styling](#ch-2-css-styling)
- [Ch 3. Optimizing Fonts and Images](#ch-3-optimizing-fonts-and-images)
- [Ch 4. Creating Layouts and Pages](#ch-4-creating-layouts-and-pages)

<br>

### Ch 1. Getting Started

- 개념: 프로젝트 생성과 개발 서버 실행
- 커밋: [learn: Chapter 1, 2](https://github.com/macaronpark/nextjs-tutorial/commit/41cb02cc4ad1d31f21a961aa98497eb3cf671f84)
- 사용법
  - [create-next-app](https://nextjs.org/docs/app/api-reference/cli/create-next-app)으로 빠른 설정
    - 옵션으로 패키지 매니저 지정 가능: `--use-pnpm`
    - pnpm 사용 권장
  - 개발 서버 실행
    ```bash
    pnpm install # or pnpm i
    pnpm dev
    ```
- 학습/이해 포인트
  - 단일 환경에서 개발하는 나의 경우 pnpm을 사용하면 중복 설치가 없어 속도가 빠르고 디스크 공간도 절약됨
  - pnpm i가 pnpm install의 alias라는 걸 알게 됨

<br>

### Ch 2. CSS Styling

- 개념: 스타일 적용
- 커밋: [learn: Chapter 1, 2](https://github.com/macaronpark/nextjs-tutorial/commit/41cb02cc4ad1d31f21a961aa98497eb3cf671f84)
- 사용법
  - 글로벌 스타일
    - top-level 컴포넌트인 [root layout](https://nextjs.org/docs/app/api-reference/file-conventions/layout#root-layout)에 글로벌 스타일 적용
  - tailwindCSS
    - 유틸리티 퍼스트 CSS 프레임워크
    - 빠른 개발, 스타일 충돌 방지, 트리셰이킹
  - clsx
    - 조건부 `className`을 편리하게 구성할 수 있는 유틸리티
    - 빈 문자열/undefined/null 자동 처리
- 학습/이해 포인트
  - 전역 스타일은 최소화하고, tailwind로 스타일링 -> 유지보수 편리
  - clsx를 사용하면 조건부 스타일링 시 삼항 연산자 남발 안 해도 돼서 훨씬 깔끔

<br>

### Ch 3. Optimizing Fonts and Images

- 개념: 폰트와 이미지를 자동으로 최적화하는 방법
- 커밋: [learn: Chapter 3, 4](https://github.com/macaronpark/nextjs-tutorial/commit/231eef757052791efeddd50f056b5892cebf7020)
- 사용법
  - [`next/font`](https://nextjs.org/docs/app/api-reference/components/font)
    - 자동으로 폰트 최적화
      - 빌드 타임에 폰트를 다운로드한 후, static assets으로 호스트하는 방식
    - 외부 네트워크 요청 제거로 보안, 성능 향상
      - 사이트 접속 시 폰트를 추가로 다운받지 않으므로 [Cumulative Layout Shift](https://web.dev/articles/cls)가 발생하지 않음
    - `next/font/google`로 모든 [구글 폰트](https://fonts.google.com/) 사용 가능
  - [`next/image`](https://nextjs.org/docs/app/api-reference/components/image)
    - 자동으로 이미지 최적화
      - 로딩 시 layout shifting 방지
      - 작은 뷰포트에서 이미지 리사이징
      - lazy loading을 default로
      - 브라우저가 지원하는 경우 WebP, AVIF와 같은 최신 포맷으로 이미지 지원
- 학습/이해 포인트
  - 직접 최적화를 위한 관련 처리를 따로 해줄 필요가 없어서 폰트와 이미지 관련 고민이 정말 많이 줄어듦
  - CLS 방지 덕분에 초기 로딩이 깔끔해짐

<br>

### Ch 4. Creating Layouts and Pages

- 개념: file-system 기반 라우팅
- 커밋: [learn: Chapter 3, 4](https://github.com/macaronpark/nextjs-tutorial/commit/231eef757052791efeddd50f056b5892cebf7020)
- 사용법
  - 폴더와 파일 구조로 라우트 구성
  - 공개적으로 접근 가능한 파일
    - `page.tsx` - 특정 라우트에서 렌더할 UI
    - `layout.tsx` - 여러 페이지에서 공유할 UI
      - 네비게이션 시 레이아웃은 상태 보존 O, 리렌더링 X
- 학습/이해 포인트
  - `layout.tsx`은 단순 공통 UI가 아니라 상태를 유지한 채로 라우팅 전환이 가능하다는 게 큰 장점
  - React Router의 Outlet과 유사한 개념인데 next.js는 파일 시스템 기반이라 훨씬 직관적
