# Block 4: MCP - 외부 도구 연결 (~20분)

> 킬러 블록. Figma/Notion/Slack을 Claude Code에서 직접 쓰는 체험.
> 디자이너: Figma MCP 중심 / 리서처: Notion MCP 중심 / PM: Notion+Slack 중심

---

## EXPLAIN

### MCP란?

MCP(Model Context Protocol)는 Claude Code가 **외부 도구와 대화하는 통로**입니다.

#### 디자이너 트랙

MCP는 **Figma 플러그인**과 같습니다.
- Figma 플러그인: Figma 안에서 추가 기능을 쓸 수 있게 해주는 확장
- MCP: Claude Code 안에서 Figma/Notion/Slack을 직접 쓸 수 있게 해주는 확장

차이점이 하나 있다면 — Figma 플러그인은 Figma 안에서만 동작하지만,
MCP는 **여러 도구를 하나로 연결**합니다.
Figma에서 읽은 내용을 Notion에 쓰고, Slack으로 공유하는 것이 한 대화에서 가능합니다.

#### 리서처 트랙

MCP는 **데이터 커넥터**와 같습니다.
- 스프레드시트에서 외부 DB를 연결하듯, Claude Code에서 Notion/Slack 등을 직접 연결
- 수동 복붙 없이 데이터를 가져오고, 분석하고, 다시 저장할 수 있습니다

#### PM 트랙

MCP는 **PM 도구 연동**과 같습니다.
- Jira/Notion/Slack 등 PM이 매일 쓰는 도구를 Claude Code 안에서 직접 조작
- 이슈 만들기, 문서 검색, 메시지 전송을 대화 한 번으로 처리

핵심 차이: 각 도구를 따로 열지 않고, **하나의 대화에서 여러 도구를 연결**합니다.
스프린트 회고 → Notion 정리 → Slack 공유가 한 대화에서 가능합니다.

### MCP 서버 구조

```
Claude Code ←→ MCP 서버 ←→ 외부 도구
                  │
                  ├── Figma MCP ←→ Figma API
                  ├── Notion MCP ←→ Notion API
                  └── Slack MCP ←→ Slack API
```

### 사용 가능한 주요 MCP 도구

**Figma MCP** (디자이너 필수):
- `get_metadata` — 파일 정보 확인
- `get_screenshot` — 스크린샷 가져오기
- `get_design_context` — 디자인 컨텍스트 분석
- `get_code_connect_suggestions` — 코드 연결 제안

**Notion MCP** (리서처 필수):
- `notion-search` — 페이지/DB 검색
- `notion-fetch` — 페이지 내용 가져오기
- `notion-create-pages` — 새 페이지 생성
- `notion-update-page` — 페이지 수정

**Slack MCP** (공통):
- `slack_search_channels` — 채널 검색
- `slack_read_channel` — 채널 메시지 읽기
- `slack_search_public` — 메시지 검색
- `slack_send_message_draft` — 메시지 초안 작성

---

## EXECUTE

### 공통: MCP 연결 확인

먼저 현재 연결된 MCP를 확인합니다:

```
/mcp
```

목록에 Figma, Notion, Slack이 보이는지 확인하세요.

---

### MCP 연결 가이드 (연결이 안 되어 있다면)

Figma, Notion, Slack MCP는 **터미널에서 `claude mcp add` 명령어**로 연결합니다.

#### 연결 방법

Claude Code를 종료(`exit`)한 뒤, 일반 터미널에서 아래 명령어를 실행합니다:

```bash
# Figma 연결 (디자이너 필수)
claude mcp add --transport http figma https://mcp.figma.com/mcp -s user

# Notion 연결 (리서처/PM 필수)
claude mcp add --transport http notion https://mcp.notion.com/mcp -s user

# Slack 연결 (공통 권장)
claude mcp add --transport http slack https://mcp.slack.com/mcp -s user
```

> `-s user` 옵션을 붙이면 모든 프로젝트에서 사용할 수 있습니다.

> API 키를 따로 발급받거나 별도 설정을 할 필요가 없습니다. 아래 명령어만 실행하면 됩니다.

각 명령어 실행 시 브라우저가 열리며 OAuth 인증을 진행합니다. OAuth 인증이란 브라우저에서 "허용" 버튼을 눌러 연결을 승인하는 방식입니다.
인증 완료 후 Claude Code를 다시 실행(`claude`)합니다.

> **OAuth 연결이 안 된다면?** 회사 보안 정책으로 OAuth가 차단된 경우일 수 있습니다. IT팀에 문의하거나, 연결 없이 진행해도 괜찮습니다 — 각 실습에 MCP 없이도 체험할 수 있는 대체 프롬프트가 준비되어 있습니다.

#### 연결 확인

Claude Code 대화창에서 `/mcp`을 입력하세요. 연결된 서비스가 목록에 보이면 성공입니다.

> 모든 서비스를 연결할 필요는 없습니다. 본인 역할에 필요한 것만 연결하면 됩니다.
> - 디자이너: Figma 필수, Notion/Slack 권장
> - 리서처: Notion 필수, Slack 권장
> - PM: Notion + Slack 필수

#### 연결이 안 될 때 (트러블슈팅)

| 증상 | 해결 방법 |
|------|----------|
| `Error: could not connect` | 인터넷 연결 확인 후 재시도 |
| 브라우저가 열리지 않음 | URL을 직접 복사해서 브라우저에 붙여넣기 |
| OAuth 인증 후 터미널이 반응 없음 | 터미널 창을 클릭한 뒤 10초 기다리기 |
| `/mcp`에서 목록이 비어 있음 | Claude Code 종료(`exit`) 후 재시작(`claude`) |
| `Error: server not found` | 명령어의 URL을 다시 확인 (오타 주의) |

---

### 디자이너 트랙

#### 실습 1: Figma 메타데이터 확인

```
Figma 파일의 메타데이터를 확인해줘.
파일 URL: [여기에 본인의 Figma 파일 URL 붙여넣기]
```

> Figma MCP가 없다면 시뮬레이션:
> "Figma MCP가 연결되어 있다고 가정하고, get_metadata 도구가 반환할 일반적인 정보 구조를 보여줘"

#### 실습 2: 컴포넌트 목록 정리

```
이 Figma 파일에서 사용된 컴포넌트 목록을 카테고리별로 정리해줘.
Foundation / Component / Pattern 으로 분류해줘.
```

#### 실습 3: 스크린샷 가져오기

```
이 Figma 파일의 첫 번째 페이지 스크린샷을 가져와줘.
```

#### 보너스: Figma → Notion 연결

```
Figma에서 가져온 컴포넌트 목록을 Notion 페이지에 정리해줘.
```

> 이것이 MCP의 진짜 힘입니다 — **도구 간 연결**.

---

### 리서처 트랙

#### 실습 1: Notion 페이지 검색

```
Notion에서 "리서치" 또는 "인사이트"가 포함된 페이지를 검색해줘.
```

> Notion MCP가 없다면 시뮬레이션:
> "Notion MCP가 연결되어 있다고 가정하고, notion-search 도구로 '리서치'를 검색하면 어떤 결과가 나올지 예시를 보여줘"

#### 실습 2: 페이지 내용 읽기

```
검색된 페이지 중 하나를 선택해서 내용을 요약해줘.
```

#### 실습 3: Slack 대화 검색

```
Slack에서 "유저 리서치" 관련 최근 대화를 검색해줘.
```

> Slack MCP가 없다면 시뮬레이션:
> "Slack MCP가 연결되어 있다고 가정하고, slack_search_public 도구로 '유저 리서치'를 검색하면 어떤 결과가 나올지 예시를 보여줘"

#### 보너스: Slack → Notion 연결

```
Slack에서 찾은 리서치 관련 논의를 정리해서 Notion 페이지에 기록해줘.
```

> 이것이 MCP의 진짜 힘입니다 — **도구 간 연결**.

---

### PM 트랙

#### 실습 1: Notion에서 제품 문서 검색

```
Notion에서 "PRD" 또는 "스펙" 또는 "기획"이 포함된 페이지를 검색해줘.
```

> Notion MCP가 없다면 시뮬레이션:
> "Notion MCP가 연결되어 있다고 가정하고, notion-search 도구로 'PRD'를 검색하면 어떤 결과가 나올지 예시를 보여줘"

#### 실습 2: Slack 채널에서 피드백 수집

```
Slack에서 "버그" 또는 "개선" 관련 최근 대화를 검색하고,
주요 이슈를 카테고리별로 정리해줘.
```

> Slack MCP가 없다면 시뮬레이션:
> "Slack MCP가 연결되어 있다고 가정하고, slack_search_public 도구로 '버그 리포트'를 검색하면 어떤 결과가 나올지 예시를 보여줘"

#### 실습 3: Notion 페이지 내용 요약

```
검색된 페이지 중 하나를 선택해서 핵심 내용을 3줄로 요약해줘.
```

#### 보너스: Slack → Notion 연결

```
Slack에서 수집한 버그/개선 피드백을 정리해서 Notion에 이슈 목록으로 만들어줘.
```

> 이것이 MCP의 진짜 힘입니다 — **도구 간 연결**.

---

> 직접 실행해보세요! 3가지 실습(+보너스)을 마치면 "완료"라고 입력해주세요.

---

## QUIZ

### 퀴즈 1

```
질문: MCP의 가장 큰 장점은?
옵션:
  A) AI가 더 똑똑해진다
  B) 여러 외부 도구를 하나의 대화에서 연결해서 쓸 수 있다
  C) 인터넷 속도가 빨라진다
정답: B
해설: MCP의 핵심은 "도구 간 연결"입니다.
      Figma에서 읽고 → Notion에 쓰고 → Slack으로 공유하는 것이
      하나의 대화에서 가능합니다. 각 도구를 따로 열 필요가 없습니다.
```

### 퀴즈 2

```
질문: Figma MCP와 Notion MCP를 동시에 사용하면 가능한 것은?
옵션:
  A) Figma 파일을 Notion 스타일로 변환
  B) Figma 디자인 분석 결과를 Notion에 자동으로 정리
  C) Notion 문서를 Figma 디자인으로 변환
정답: B
해설: MCP를 조합하면 한 도구에서 읽은 데이터를 다른 도구에 쓸 수 있습니다.
      디자인 분석 → 문서화 같은 워크플로우를 자동화할 수 있는 것이 핵심입니다.
```
