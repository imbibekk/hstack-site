# tech-meeting_2.0 — hstack 소개 사이트 (Redesigned)

ccunpacked.dev 스타일 인터랙티브 구조. 단일 페이지, 제로 빌드.

## 구성

```
tech-meeting_2.0/
├── index.html              — 사이트 본체 (~1,600 lines)
├── README.md               — 이 파일
├── .nojekyll               — GitHub Pages Jekyll 우회
└── assets/
    └── favicon.svg
```

## 변경점 (vs. tech-meeting/)

- **섹션 순서 재배치**: Origin → SKILL.md Anatomy → Input → Rules → Concepts → Stage Trace → Start
  (정적 foundation 먼저, 동적 flow 나중)
- **신규 § II · SKILL.md Anatomy** — 파일 트리, 트리거 phrase, 3-tab 프리뷰 (Frontmatter / Workflow / Rules Index)
- **§ VI · Stage Trace 전면 재설계**:
  - 터미널 + 한국어 프롬프트 타이핑 애니메이션 (ccunpacked 패턴)
  - 번호 pill 탭 (progress line 위)
  - 내레이션 paragraph + 컴팩트 메타 스트립
  - `세부 보기` 접이식 토글 — 원본 rich data 보존
  - 0.5× / 1× / 2× speed가 타이핑 속도까지 제어
- **라이브 데모 섹션 삭제** — Stage Trace가 그 역할을 흡수 (asciinema 의존성 제거)

## 인터랙티브 컴포넌트

| 컴포넌트 | 위치 | 동작 |
|---|---|---|
| **SKILL.md 탭 프리뷰** | § II | 3개 탭 클릭 → Frontmatter / Workflow / Rules Index 전환 |
| **Stage Trace** | § VI | 12-tab, 타이핑 애니메이션, ▶ 자동재생, ← → 수동, 0.5×/1×/2× 속도 |
| **Rule 필터** | § IV | 단계별 필터 (All / Baseline / Stage 1. 문서수집 / ...) |
| **Rule 상세 토글** | § IV | 각 rule 클릭 시 "ACTIVE AT" 라인 확장 |

## 로컬 미리보기

```sh
cd tech-meeting_2.0
python3 -m http.server 8000
# → http://localhost:8000
```

Tailwind/Fonts는 CDN. 인터넷 필요.

## 배포

GitHub Pages workflow는 `tech-meeting/`을 배포하도록 설정되어 있음. 2.0을 배포하려면
`.github/workflows/pages.yml`의 `path`를 `tech-meeting_2.0`으로 변경하거나, 2.0이 승인되면
`tech-meeting/`에 덮어쓴다.

## 콘텐츠 수정

- **Stage 프롬프트**: `index.html` 하단 `stages` 배열의 `prompt`, `narration`, `sourceRef` 필드
- **Rule 내용**: `rules` 배열
- **SKILL.md 프리뷰**: `mdContent` 객체의 `frontmatter`/`workflow`/`rules` 키

## 미리보기 체크리스트 (미팅 전)

- [ ] 전체 7개 섹션 시각 확인
- [ ] Stage Trace — ▶ 누르고 12단계 자동 재생 확인
- [ ] Stage Trace — 0.5×/2× 속도 확인 (타이핑 속도가 변하는지)
- [ ] Rule 필터 — Stage 6 선택 시 관련 rule만 남는지
- [ ] SKILL.md 탭 — 3개 탭 전환 확인
- [ ] 모바일 뷰 간단 점검
- [ ] Hero의 "GitHub" 링크 없음 — repo URL 확정 후 navbar에 추가
- [ ] Stage Trace의 source reference badge (`SKILL.md · §N`) 는 현재 비활성 링크 — 필요 시 실제 repo URL 연결
