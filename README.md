# 온음(ONUM) 홈페이지

틴휘슬 음악지도사 자격증 브랜드 **온음(ONUM)**의 공식 홈페이지입니다.
연주를 넘어 가르치는 사람으로 — 늘봄·방과후 음악수업을 위한 틴휘슬 지도사 양성 과정을 안내합니다.

## 페이지

| 파일 | 내용 |
|---|---|
| `index.html` | 메인 홈 (감성 에디토리얼) — 캐노니컬 |
| `B-certification-research.html` | 자격증 안내 페이지 |
| `A-home-research.html` | 홈 대안 (리서치형 레이아웃) |

## 디자인 시스템 (단일 소스 토큰)

색·타이포·간격을 바꿀 땐 **이 3개 파일만** 수정합니다 (HTML에 인라인 config 추가 금지).

| 파일 | 역할 |
|---|---|
| `onum-design.md` | 명세·근거·변경 이력 |
| `onum-tokens.js` | Tailwind config (1벌) |
| `onum-base.css` | CSS 변수(라이트/다크) + 공통 유틸 |

**방향**: 웜 에디토리얼 — 딥그린 `#004639` + 크림 `#fbf9f3`, Playfair Display(헤드라인) + Noto Sans KR(본문). `<html class="dark">` 토글로 라이트/다크 전환.

## 기술

CDN Tailwind 프로토타입(빌드 과정 없음). GitHub Pages로 정적 호스팅.

## 남은 작업

- [ ] 히어로 이미지를 실제 온음 클래스룸 사진으로 교체 (현재 placeholder)
- [ ] 트러스트 섹션 실사진 추가
- [ ] 내비게이션의 Certification 링크를 자격증 페이지로 연결
