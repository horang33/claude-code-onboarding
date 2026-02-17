# 사전 준비 가이드

> 온보딩 시작 **전**에 완료해주세요. 총 ~10분 소요됩니다.
> 이 가이드는 Claude Code 설치 전에 읽는 문서이므로, 온보딩 Skill과는 별도로 진행합니다.

---

## 1단계: 구독 확인 (~2분)

1. [claude.ai](https://claude.ai) 접속 → 로그인
2. 좌측 하단 또는 설정에서 구독 상태 확인
3. **Claude Pro ($20/월)** 또는 **Max** 구독이 활성화되어 있어야 합니다

> 구독이 없으면 Claude Code를 사용할 수 없습니다. 먼저 결제를 완료해주세요.

---

## 2단계: 터미널 열기 (~1분)

터미널은 컴퓨터에게 텍스트로 명령을 내리는 프로그램입니다.
아래에서 본인의 운영체제에 맞는 방법을 따라해주세요.

### Mac

**방법 1** (추천): `Cmd + Space` → "터미널" 입력 → 실행

**방법 2**: Finder → 응용 프로그램 → 유틸리티 → 터미널

### Windows

시작 메뉴 → "PowerShell" 검색 → **"Windows PowerShell"** 실행

> "명령 프롬프트(cmd)"가 아니라 **"PowerShell"**이어야 합니다.

---

## 3단계: Claude Code 설치 (~3분)

터미널/PowerShell에 아래 명령어를 **복사해서 붙여넣기**하세요.

### Mac / Linux

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

### Windows (PowerShell)

```powershell
irm https://claude.ai/install.ps1 | iex
```

> Node.js, npm 같은 별도 프로그램 설치가 필요 없습니다. 위 한 줄이면 끝입니다.

---

## 4단계: 설치 확인 (~1분)

터미널에 아래를 입력하세요:

```bash
claude --version
```

버전 번호가 출력되면 설치 성공입니다.

---

## 5단계: 첫 실행 + 로그인 (~2분)

```bash
claude
```

1. 로그인 화면이 나타납니다
2. 브라우저가 열리면 Anthropic 계정으로 인증합니다
3. 터미널에 대화창이 표시되면 완료입니다

> 대화창이 뜨면 `exit`를 입력해서 종료해주세요. 온보딩 당일에 다시 실행합니다.

---

## 트러블슈팅

| 증상 | 해결 방법 |
|------|----------|
| `command not found` | 터미널을 완전히 닫고 다시 열어주세요 |
| Windows에서 설치 스크립트 실행 안 됨 | PowerShell을 **관리자 권한**으로 실행해보세요 |
| 로그인 화면이 안 나옴 | [claude.ai](https://claude.ai)에서 구독 상태를 다시 확인해주세요 |
| 브라우저 인증 후 터미널이 반응 없음 | 터미널 창을 클릭한 뒤 잠시 기다려주세요 |

---

## 6단계: MCP 사전 연결 (~3분, 선택)

MCP(Model Context Protocol)는 Claude Code에서 Figma, Notion, Slack 등 외부 도구를 직접 사용할 수 있게 해주는 기능입니다. 온보딩 Block 4에서 실습하므로, 미리 연결해두면 훨씬 수월합니다.

### 연결 방법

1. 브라우저에서 [claude.ai/settings](https://claude.ai/settings) 접속
2. 좌측 메뉴에서 **"Integrations"** 클릭
3. 본인 역할에 맞는 서비스를 연결하세요:

| 역할 | 필수 연결 | 권장 연결 |
|------|----------|----------|
| 디자이너 | Figma | Notion, Slack |
| 리서처 | Notion | Slack |
| PM | Notion, Slack | — |

4. 각 서비스 옆 **"Connect"** 클릭 → OAuth 인증 진행
5. 연결 후 터미널에서 Claude Code 재시작 (`exit` → `claude`)
6. `/mcp` 입력으로 연결 확인

> MCP를 지금 연결하지 않아도 온보딩 진행은 가능합니다 (시뮬레이션 모드 제공).
> 하지만 **실제 연결 후 실습하는 것이 학습 효과가 훨씬 큽니다.**

---

## 체크리스트

아래 항목을 확인하면 온보딩 준비 완료입니다.

**필수 (4개)**
- [ ] Claude Pro/Max 구독 활성화
- [ ] 터미널/PowerShell 열 수 있음
- [ ] `claude --version`에서 버전 번호 출력됨
- [ ] `claude` 실행 후 대화창 표시됨

**선택 (MCP 연결)**
- [ ] `/mcp`에서 Figma/Notion/Slack 중 1개 이상 connected 표시됨

> 필수 4개가 체크되셨으면, 온보딩 당일 `/day1`으로 바로 시작할 수 있습니다!
