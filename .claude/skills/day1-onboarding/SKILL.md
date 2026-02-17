# Day 1 Onboarding: 디자이너, 리서처, PM을 위한 Claude Code

## Skill Metadata
- **Trigger**: `/day1-onboarding`
- **Description**: 디자이너/리서처/PM 특화 Claude Code 1일 온보딩 프로그램 (7블록, ~110분, 사전 준비 포함)

---

## STOP PROTOCOL

이 스킬은 **STOP PROTOCOL**을 따른다. 모든 블록은 두 Phase로 나뉜다.

### Phase A: EXPLAIN → EXECUTE → STOP

1. 블록의 `EXPLAIN` 섹션을 읽고 사용자에게 **설명**한다.
2. 블록의 `EXECUTE` 섹션을 읽고 사용자에게 **실행 지시**를 전달한다.
3. "직접 실행해보세요!" 메시지를 출력한 뒤 **즉시 멈춘다 (STOP)**.

### Phase B: QUIZ → NEXT

1. 사용자가 "완료", "done", "다음", "next" 등을 입력하면 Phase B 시작.
2. 블록의 `QUIZ` 섹션을 읽고 퀴즈를 출력한다 (AskUserQuestion 사용).
3. 퀴즈 완료 후 다음 블록의 Phase A로 진행한다.

### 절대 금지 사항

- Phase A에서 퀴즈를 내거나 AskUserQuestion을 호출하지 않는다.
- Phase A에서 "해봤나요?", "실행해봤나요?" 같은 확인 질문을 하지 않는다.
- EXECUTE를 설명만 하고 넘어가지 않는다. 반드시 사용자가 직접 실행하도록 멈춘다.
- 블록을 건너뛰지 않는다. 반드시 순서대로 진행한다.
- QUIZ가 없는 블록(Block 0, 7)은 Phase A만 진행하고 바로 다음으로 넘어간다.

---

## 진행 흐름

### 1단계: 사전 준비 확인

프로그램 시작 시, AskUserQuestion으로 사전 준비 완료 여부를 확인한다:

```
질문: "사전 준비 가이드를 완료하셨나요? (Claude Code 설치 + 로그인)"
옵션:
  - 네, 완료했어요
  - 아직이요
```

- **"네, 완료했어요"** → 2단계(역할 선택)로 진행
- **"아직이요"** → `references/pre-setup-guide.md`를 Read로 읽고 내용을 안내한 뒤 STOP. "준비가 되면 다시 `/day1-onboarding`을 실행해주세요!" 메시지 출력.

### 2단계: 역할 선택

AskUserQuestion으로 역할을 선택받는다:

```
질문: "어떤 역할에 더 가까운가요?"
옵션:
  - 디자이너 (Product Designer, UX/UI Designer)
  - 리서처 (UX Researcher, 서비스 기획자)
  - PM (Product Manager, 서비스 기획)
```

선택된 역할을 `{ROLE}`로 저장하고, 이후 모든 블록에서 해당 역할의 트랙만 사용한다.

### 3단계: 블록 순차 진행

```
Block 0: Setup (10분) ─── Phase A only (퀴즈 없음)
  ↓
Block 1: Experience (15분) ─── Phase A → STOP → Phase B
  ↓
Block 2: Why CLI? (10분) ─── Phase A → STOP → Phase B
  ↓
Block 3: CLAUDE.md + Skill (15분) ─── Phase A → STOP → Phase B
  ↓
☕ Break (5분) ─── "5분 쉬고 오세요!"
  ↓
Block 4: MCP (20분) ─── Phase A → STOP → Phase B
  ↓
Block 5: Subagent (10분) ─── Phase A → STOP → Phase B
  ↓
Block 6: Build (15분) ─── Phase A → STOP → Phase B
  ↓
Block 7: Graduation (5분) ─── Phase A only (퀴즈 없음)
```

### 4단계: 블록 실행 방법

각 블록 실행 시:

1. `references/block{N}-{name}.md` 파일을 Read로 읽는다.
2. `{ROLE}` 값에 따라 해당 트랙의 섹션만 사용한다:
   - `{ROLE}` = "디자이너" → `### 디자이너 트랙` 섹션 사용
   - `{ROLE}` = "리서처" → `### 리서처 트랙` 섹션 사용
   - `{ROLE}` = "PM" → `### PM 트랙` 섹션 사용
3. STOP PROTOCOL에 따라 Phase A → STOP → Phase B 순서로 진행한다.

---

## 블록 맵

| 블록 | 파일 | 핵심 내용 |
|------|------|----------|
| Pre | `pre-setup-guide.md` | 구독, 터미널, 설치, 로그인 (사전 완료) |
| 0 | `block0-setup.md` | 설치 확인, 첫 대화, MCP 연결 확인 |
| 1 | `block1-experience.md` | 역할별 Before/After 데모 3개 |
| 2 | `block2-why.md` | GUI vs CLI, 왜 터미널인가 |
| 3 | `block3-foundations.md` | CLAUDE.md = 영구 기억, Skill = 업무 레시피 |
| 4 | `block4-mcp.md` | Figma/Notion/Slack MCP 실습 |
| 5 | `block5-subagent.md` | Task 도구로 위임과 병렬 처리 |
| 6 | `block6-build.md` | 졸업 과제: 나만의 워크플로우 |
| 7 | `block7-graduation.md` | 전체 맵 + 다음 학습 경로 |

---

## 역할별 비유 사전

블록 설명 시 아래 비유를 일관되게 사용한다:

| 개념 | 디자이너 비유 | 리서처 비유 | PM 비유 |
|------|-------------|------------|---------|
| CLAUDE.md | 브랜드 가이드라인 | 리서치 프로토콜 | 제품 스펙 문서 |
| Skill | 디자인 템플릿/컴포넌트 라이브러리 | 분석 프레임워크/코드북 | PRD 양식/기능 템플릿 |
| MCP | Figma 플러그인 | 데이터 커넥터 | PM 도구 연동 (Notion+Slack) |
| Subagent | 주니어 디자이너에게 위임 | 리서치 어시스턴트에게 위임 | 팀원에게 업무 위임 |
| Hook | Auto Layout 제약 조건 | 자동 데이터 검증 | 자동 상태 리포트 |
| Context Window | 캔버스 크기 | 작업 기억 용량 | 스프린트 범위 |
| System Prompt | 마스터 컴포넌트 | 인터뷰 가이드 | 제품 원칙 문서 |

---

## 톤 & 스타일

- 존댓말 사용 (~ 해보세요, ~ 입니다)
- 전문 용어는 첫 등장 시 비유로 설명
- 코드 블록은 복붙 가능하게 완전한 형태로 제공
- 실행 결과를 미리 보여주지 않음 (사용자가 직접 확인하도록)
- "틀렸습니다" 대신 "거의 다 왔어요! 힌트를 드리면..."

---

## 시작

아래 순서로 시작한다:

1. 환영 메시지 출력:
   ```
   🎓 디자이너, 리서처, PM을 위한 Claude Code Day 1 온보딩에 오신 걸 환영합니다!

   총 7개 블록, 약 110분 과정입니다 (사전 준비 ~10분 포함).
   중간에 쉬는 시간도 있으니 편하게 따라와주세요.
   ```

2. AskUserQuestion으로 사전 준비 완료 확인 (1단계)

3. AskUserQuestion으로 역할 선택 (2단계)

4. Block 0부터 순차 진행
