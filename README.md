# NextJS_Tutoreal
NextJS 학습 공간

특징
1. 라우팅 - 레이아웃. 중첩 라우팅, 로딩 상태, 오류 처리 등 지원
2. 표현 - 클라이언트 사이드 렌더링, 서버 사이드 렌더링 둘 다 지원(동적, 정적 렌더링 최적화)
3. 데이터 페칭 - async/await을 사용한 데이터 가져오기와 fetch 요청에 대한 메모 생성, 데이터 캐싱 및 재검증을 위한 확장된 api 제공
4. 스타일링 - 선호하는 스타일링 방식 지원
5. 최적화 - 이미지, 글꼴, 스크립트 등 최적화
6. 타입스크립트 

# Next.js  설정 파일들
---
Next.config.js - Next.js에 대한 구성 파일
package.json - 프로젝트 종속성 및 스크립트
middleware.ts - Next.js 요청 미들웨어
.env - 환경 변수
.eslintrc.json - ESLint에 대한 구성 파일
.gitignore - 무시할 Git 파일 및 폴더
Next-env.d.ts - Next.js에 대한 Typescript 선언 파일
tsconfig.json - Typescript에 대한 구성 파일

# 라우팅 파일
layout.tsx - 중첩 디자인
page.tsx - 페이지 라우팅
loading.tsx - UI 로딩 중일때 라우팅
not-found.tsx - 존재하지 않는 페이지일 때 라우팅
error.tsx - 오류일 때 라우팅
global-error.tsx - 전체 오류일 때 라우팅
route.ts - api 엔드포인트
template.tsx - 재렌더링
default.tsx - 병렬 경로 대체 페이지
중첩된 경로는 폴더로 만들 수 있음.

# 동적 경로
[folder] - 동적 경로 구간
[...folder] - 포괄적인 경로 구간
[[...folder]] - 선택 가능한 포괄적인 경로 구간

# 경로 그룹 및 개인 폴더
(folder) - 라우팅에 영향을 주지 않고 경로 그룹화
_folder - 라우팅에서 속한 폴더 및 파일 제외

# 경로 끼어들기
(.)folder - 같은 레벨 가로채기
(..)folder - 한 단계 위 가로채기 (...)루트에서 가로채기

# SEO 최적화
sitemap.xml - 사이트맵 파일

/* 중간 점검 */
api폴더에는 route.ts가 아닌 db.ts같은 파일은 라우팅 되지않음.
마찬가지로 폴더 안에는 page.tsx가 아닌 nav.tsx같은 파일은 라우팅 되지않음. 
경로 그룹은 사이트를 섹션으로 나눌 때 또는 중첩 레이아웃을 사용할 때 유용. 어드민 경로 그룹과 유저 경로 그룹 같은 경우
components와 lib같은 애플리케이션 코드들은 app폴더 안에 폴더를 만들 수도 있지만, 그건 전역적으로 공유되는 코드들로 하고 폴더 내에 components랑 lib 폴더를 만들어 보다 세부적인 코드를 저장할 수 있음

# 이미지
로컬 이미지는 import를 하여 사용 width와 height 필수x 자동으로 결정해줌
원격 이미지는 url 사용 width와 height 필수 / next.config.ts에서 원격 이미지 허용 제한 가능

# 폰트
public폴더에 next/font/gogle이나 next/font/local 과 같이 만들면 자동 셀프 호스팅을 해줌.

# tailwind
tailwind.config.ts 에서 content: [경로를 넣어줌('./src/**/*.{tsx}')]
글로벌 스타일시트 초기화 후 테일윈드 지침을 추가 그리고 루트 레이아웃에서 호출하면 사용 가능

# 데이터 가져오기
서버 구성요소는 Api = fetch와 Orm 또는 DB
api를 호출하려면 export default async function Page() { const data = await fetch('url') const posts = await data.json() } 처럼 사용해야됨. async/await 필수 fetch 한 뒤 사용할 함수에 .json() 
또는 db나 orm이 있는 경우 async/await은 필수고 const allPosts = await db.select().from(posts) 와 같이 쿼리문 사용

# 클라이언트에서 데이터 사용
방법은 2가지
1. useHook 2. React 쿼리
   1번 방법은 사용할 페이지에서 데이터를 사용해서 만들어진 클라이언트 렌더링(Posts)을 불러오고 함수에 연결(const posts = getPosts) 후 리턴문에서 서스펜스로 불러올 때까지 막은 다음에(<Suspense fallback={<div>Loading...<div>}><Posts posts={posts} /></Suspense> 사용 posts 함수를 만든 이유는 컴포넌트에서 프롭스를 원하기 때문.
   posts라는 클라이언트 렌더링 컴포넌트에는 use 라는 훅을 사용하고 프롭스를 지정(export default function Posts({posts})) 후 함수 선언(const posts = use(posts) 그리고 리턴문에 사용하면 됨.

# 스트리밍
서버 사이드 렌더링 시 동적 렌더링을 선택하는 과정을 async/await이 해줌. 느린 데이터 요청일 시 렌더링을 차단해버림. 그래서 스켈레톤UI가 필요한거고 loading.tsx가 있는 것 점진적 페이지 로딩
보통 loading.tsx를 사용하면 전체 페이지를 로딩하는데 세부적으로 로딩을 하고 싶을 땐 Suspense 를 사용해서 값에 loading.tsx를 넣으면 됨. 그러면 그 부분만 데이터를 받아올 동안 로딩이 됨.



