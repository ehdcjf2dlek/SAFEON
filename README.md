# 세이프온 안전기술 홈페이지 (safeonenc.com)

`site/` 폴더가 홈페이지 전체입니다. 빌드 과정 없는 정적 사이트입니다.

```
site/
├─ index.html                 메인 (원페이지)
├─ privacy.html               개인정보처리방침
├─ 404.html                   없는 주소 안내
├─ library/                   안전실무 자료실 글
├─ assets/                    로고·OG 이미지·파비콘·하위페이지 CSS
├─ _headers                   Cloudflare Pages 보안·캐시 헤더
├─ robots.txt, sitemap.xml
└─ favicon.ico
```

## Cloudflare Pages 연결 (최초 1회)

1. Cloudflare 대시보드 → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**
2. GitHub 계정 연결 후 이 저장소 선택
3. 설정
   - Production branch: 홈페이지를 배포할 브랜치
   - Framework preset: **None**
   - Build command: (비워둠)
   - Build output directory: **`site`**
4. 배포 후 **Custom domains** 에서 `safeonenc.com`, `www.safeonenc.com` 추가

이후에는 저장소에 반영(push)되는 즉시 자동 배포됩니다.

## 자료실 글 추가 방법

1. `site/library/` 의 기존 글 하나를 복사해 새 파일명으로 저장 (영문 소문자·하이픈)
2. 제목, description, canonical, og:url, JSON-LD 의 주소·날짜 수정
3. `site/index.html` 자료실 목록의 해당 줄을 `<a class="row rv" href="/library/파일명">` 형태로 바꾸고 `준비중` → `읽기`
4. `site/sitemap.xml` 에 주소 추가

내부 링크와 canonical 은 확장자 없이 씁니다(`/privacy`, `/library/...`). Cloudflare Pages 가 `.html` 주소를 확장자 없는 주소로 자동 전환하기 때문입니다.

## 검색엔진 등록 시

- **구글 서치콘솔**: 도메인 속성으로 등록 → Cloudflare DNS 에 TXT 레코드 추가 (HTML 수정 불필요)
- **네이버 서치어드바이저**: `site/index.html` 상단의 `naver-site-verification` 주석을 풀고 값 입력
- 둘 다 사이트맵 `https://safeonenc.com/sitemap.xml` 제출
