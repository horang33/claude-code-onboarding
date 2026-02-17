# 디자이너, 리서처, PM을 위한 Claude Code Day 1 온보딩

비개발자(Product Designer, UX Researcher, Product Manager)를 위한 Claude Code 1일 온보딩 프로그램입니다.

## 특징

- **7블록, ~110분** 커리큘럼 (사전 준비 ~10분 포함)
- **STOP PROTOCOL** 기반 interactive 교육 (설명 → 실습 → 퀴즈)
- **역할별 트랙**: 디자이너/리서처/PM 선택 시 예제와 실습이 분기
- **MCP 중심**: Figma, Notion, Slack 연결 실습 (Block 4가 킬러 블록)

## 커리큘럼

| 블록 | 제목 | 시간 | 내용 |
|------|------|------|------|
| Pre | 사전 준비 | ~10분 | 구독 확인, 터미널, 네이티브 설치, 로그인 |
| 0 | Setup | 10분 | 설치 확인, 첫 대화, MCP 연결 확인 |
| 1 | Experience | 15분 | 역할별 "와" 데모 3개씩 |
| 2 | Why CLI? | 10분 | GUI vs CLI, 왜 터미널인가 |
| 3 | CLAUDE.md + Skill | 15분 | 영구 기억 + 업무 레시피 |
| - | Break | 5분 | 쉬는 시간 |
| 4 | MCP | 20분 | Figma/Notion/Slack 실습 |
| 5 | Subagent | 10분 | 위임과 병렬 처리 |
| 6 | Build | 15분 | 졸업 과제: 나만의 워크플로우 |
| 7 | Graduation | 5분 | 전체 맵 + 다음 학습 경로 |

## 실행 방법

### 1. 사전 준비 (온보딩 전 완료)

[사전 준비 가이드](.claude/skills/day1-onboarding/references/pre-setup-guide.md)를 따라 Claude Code 설치 + 로그인을 완료해주세요.

### 2. 터미널에서 폴더 열기

**Mac**: 터미널을 열고 아래를 입력하세요.
```bash
cd ~/Downloads/claude-code-onboarding
```

**Windows**: PowerShell을 열고 아래를 입력하세요.
```powershell
cd $HOME\Downloads\claude-code-onboarding
```

> 다른 위치에 풀었다면 경로를 맞춰주세요.

### 3. Claude Code 실행

```bash
claude
```

### 4. 온보딩 시작

Claude Code 대화창이 뜨면 아래를 입력하세요:
```
/day1-onboarding
```

역할 선택(디자이너/리서처/PM) 후 Block 0부터 자동 진행됩니다.

## 역할별 비유

| 개념 | 디자이너 비유 | 리서처 비유 | PM 비유 |
|------|-------------|------------|---------|
| CLAUDE.md | 브랜드 가이드라인 | 리서치 프로토콜 | 제품 스펙 문서 |
| Skill | 컴포넌트 라이브러리 | 분석 프레임워크 | PRD 양식/기능 템플릿 |
| MCP | Figma 플러그인 | 데이터 커넥터 | PM 도구 연동 (Notion+Slack) |
| Subagent | 주니어 디자이너 | 리서치 어시스턴트 | 팀원에게 업무 위임 |

## 파일 구조

```
claude-code-onboarding/
├── .claude/skills/day1-onboarding/
│   ├── SKILL.md                    # 메인 오케스트레이터
│   └── references/
│       ├── pre-setup-guide.md      # 사전 준비 (설치 전 독립 가이드)
│       ├── block0-setup.md         # 설치 확인 + MCP 연결 확인
│       ├── block1-experience.md    # Before/After 데모
│       ├── block2-why.md           # 왜 CLI인가?
│       ├── block3-foundations.md   # CLAUDE.md + Skill
│       ├── block4-mcp.md          # MCP 실습
│       ├── block5-subagent.md     # 서브에이전트
│       ├── block6-build.md        # 나만의 워크플로우
│       └── block7-graduation.md   # 전체 맵 + 다음 단계
└── README.md
```

## 참고

- [ai-native-camp/camp-1](https://github.com/giseongeom/ai-native-camp) — STOP PROTOCOL 기반 교육
- [crystal0224/my-day1](https://github.com/crystal0224/my-day1) — 비개발자 확장
