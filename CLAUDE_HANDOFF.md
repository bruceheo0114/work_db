# Claude 작업 인계서

## 목적

피알원 업무 허브에서 지출결의서, KOL 단가·계약서, 업무보고, 소셜 지표 수집기를 한 화면에 연결한다.

## 기준 저장소

- 통합 포털: `bruceheo0114/work_db`
- 지출결의서: `bruceheo0114/Expense-Report`
- KOL 단가 DB: `bruceheo0114/campaign_cost`
- KOL 계약서: `bruceheo0114/Contract_Generator`
- 업무보고: `bruceheo0114/work_report2`
- 소셜 지표: `bruceheo0114/social-metrics-team`

## 현재 구현

- 한 페이지 안에서 기존 GitHub Pages 도구를 iframe으로 전환한다.
- 도구 검색, 업무 분류, 즐겨찾기와 새 창 열기를 제공한다.
- 소셜 지표 수집기는 팀용 ZIP 다운로드와 설치된 확장 프로그램 실행 연결을 제공한다.
- KOL 단가 DB에는 비밀번호 확인 화면과 실패 횟수 제한을 추가한다.
- AI 일일 사용량을 수동 표시하고 90%부터 Claude 인계문 복사를 안내한다.

## 보안 원칙

- API 키나 공유 비밀번호 평문을 GitHub에 커밋하지 않는다.
- KOL 단가 DB의 브라우저 비밀번호 화면은 캐주얼 접근 차단용이다. 실제 기밀 데이터는 서버 인증 또는 비공개 데이터 소스로 이전해야 한다.
- 소셜 지표 팀용 ZIP에 포함된 YouTube 키는 YouTube Data API v3에만 제한한다.

## 이어서 작업할 때

1. 저장소의 최신 파일을 먼저 읽는다.
2. 기존 도구의 GitHub Pages 실행 주소가 HTTP 200인지 확인한다.
3. 변경 후 데스크톱·모바일 레이아웃과 키보드 사용을 확인한다.
4. 완료 내용과 남은 작업을 이 파일에 갱신한다.

## 2026-08-28 Claude 이어받은 작업

### 완료

- 포털에 **바이탈뷰티 데일리 모니터링 Word 생성기 v9** 카드를 추가했다. 웹 도구가 아니라 데스크톱 프로그램이라 소셜 수집기와 같은 ZIP 다운로드 방식으로 붙였다.
- 다운로드 패널을 도구별 데이터로 그리도록 일반화했다. `TOOLS[id].download` 가 `{ title, body, file, label, note, extension }` 을 갖는다.
- 소셜 지표 수집기 다운로드 링크를 고쳤다. 기존 링크가 가리키던 `social-metrics-team` 릴리스 `v2.2.0-team` 은 존재하지 않아 404였다.
- 두 ZIP을 `assets/` 에 함께 두고 상대 경로로 연결했다. 릴리스 없이도 즉시 내려받힌다.
- 빠른 실행 목록과 Claude 인계문에도 데일리 모니터링을 반영했다.
- KOL 단가 DB 비밀번호 게이트는 `campaign_cost` 에 이미 반영·배포된 것을 확인했다. PBKDF2 210,000회, 실패 시 30초 잠금, 세션 단위 유지.

### 확인한 상태

- 실행 주소 HTTP 200: Expense-Report, campaign_cost, Contract_Generator, work_report2
- `work_db` Pages 는 404. 저장소가 비어 있어 포털이 아직 배포되지 않았다.

### 남은 작업

1. 이 폴더를 `bruceheo0114/work_db` 에 올리고 Pages 를 켠다. 아직 사용자 확인 전이라 푸시하지 않았다.
2. 배포 후 iframe 안에서 도구 4종이 실제로 뜨는지, 모바일 레이아웃과 키보드 이동을 확인한다.
3. `assets/` 의 ZIP 두 개를 저장소에 함께 둘지, GitHub 릴리스로 옮기고 링크만 바꿀지 정한다.
4. v9 ZIP 에는 네이버 API 키가 없다. 팀 배포 시 키 입력 안내를 어디에 둘지 정한다.
