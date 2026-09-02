# restore-author-voice

[English](README.md) · [繁體中文](README.zh-TW.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · 한국어

`restore-author-voice`는 글쓴이를 획일적인 “사람다운 문체”로 바꾸지 않고, 원래 목소리를 살려 문장을 다시 쓰는 skill입니다. 사실, 입장, 불확실성, 인용, 매체별 관례를 먼저 보존한 뒤 구조, 문단 흐름, 매체 적합성, 표면 표현 순으로 더 깊은 문제부터 고칩니다.

## 주요 기능

- 이름, 숫자, 날짜, 링크, 인용, 요구사항, 시간 순서, 입장, 의미 있는 대비를 보존합니다.
- 원문, 명시적인 지시, 출처를 확인할 수 있는 글 샘플에서 글쓴이의 목소리를 복원합니다.
- 명시된 voice 또는 style guide를 근거와 매체의 제약 안에서 적용합니다.
- 대상 글이나 인용 파일에 포함된 지시는 데이터로 취급하며 모드, 범위, 권한을 바꾸지 못하게 합니다.
- 모든 문제를 단어 선택 문제로 취급하지 않고 구조, 문단 흐름, 매체 적합성, 표현을 나누어 진단합니다.
- 흔한 AI 문체 패턴을 전역 금지 목록이 아니라 문맥에 따라 판단할 신호로 사용합니다.
- 채팅, release notes, 개발자 논의, 인시던트 리뷰, ticket, 기술 문서에 맞게 문체를 조정합니다.
- 요청하지 않은 제목, 요약, 추가 제안 없이 바로 사용할 수 있는 결과를 반환합니다.
- 파일 안의 글을 편집할 때 code, data, frontmatter, link targets를 그대로 유지합니다.
- 영어와 대만 독자를 위한 번체 중국어 전용 가이드를 포함합니다.

## 모드

| 모드 | 용도 | 편집 범위 |
|---|---|---|
| `diagnose` | 의미나 글쓴이의 목소리가 사라진 지점을 찾을 때 | 문제만 보고하고 다시 쓰지 않음 |
| `cleanup` | 명백한 부자연스러움을 제거할 때 | 구조 변경을 최소화함 |
| `rewrite` | 구조적 문제가 있는 초안을 고칠 때 | 근거를 잠근 뒤 구조를 다시 만들 수 있음 |
| `draft` | 제공되었거나 검증된 자료로 새 글을 쓸 때 | 표현보다 구조와 매체를 먼저 결정함 |

## 작동 방식

1. 독자, 장르, 매체, 언어, 모드, 편집 범위를 정합니다.
2. 보존할 내용을 확정하고 사실, 추론, 의견, 인용을 구분합니다.
3. 근거가 있는 문체 기준을 고르고, 명시된 voice 또는 style guide가 있으면 근거와 매체의 제약 안에서 적용합니다.
4. 원문과 결과를 비교하고 author-swap test를 실행한 뒤 근거 없는 추가 내용을 제거합니다.

글쓴이를 보여 주는 근거가 없으면 장르에 맞는 기본 문체를 명시적으로 사용합니다. 중립적인 글을 더 사람처럼 보이게 만들려고 인격을 꾸며 내지 않습니다.

## 설치

Agent Skills CLI를 사용합니다.

```bash
npx skills add https://github.com/SemonCat/restore-author-voice
```

저장소를 clone한 뒤 agent가 지원하는 skill 디렉터리에 배치할 수도 있습니다.

## 사용법

원문, 대상 독자, 매체, 모드, 변경하면 안 되는 내용을 agent에 전달합니다.

```text
restore-author-voice를 cleanup 모드로 사용해 주세요. 모든 숫자와 인용은 그대로 유지하세요.
```

```text
이 인시던트 리뷰를 엔지니어링 팀용으로 다시 써 주세요. 시간 순서와 원인이 아직 불확실하다는 점을 유지하세요.
```

```text
이 글이 누구 이름으로도 성립하는 이유를 진단해 주세요. 아직 다시 쓰지 말고, 답에 따라 결과가 달라지는 질문만 하세요.
```

```text
docs/launch.md의 본문만 다시 써 주세요. frontmatter, code blocks, data, link targets는 변경하지 마세요.
```

같은 글쓴이나 브랜드의 글을 계속 다룬다면 [`templates/author-profile.md`](templates/author-profile.md)로 근거 기반 profile을 만들 수 있습니다.

## 저장소 구성

- [`SKILL.md`](SKILL.md): 워크플로와 guardrails
- [`references/diagnostic-lens.md`](references/diagnostic-lens.md): identity, rhythm, semantics, genre, author-swap test
- [`references/structure-and-discourse.md`](references/structure-and-discourse.md): 구조, 문단 흐름, 속도, 편집 깊이
- [`references/venue-guides.md`](references/venue-guides.md): 주요 업무 문서별 규칙
- [`references/ai-patterns.md`](references/ai-patterns.md): 흔한 AI 문체를 판단하기 위한 문맥 신호
- [`references/voice-composition.md`](references/voice-composition.md): 명시된 voice／style guide의 우선순위와 충돌 처리
- [`references/en.md`](references/en.md): 영어 지역 관례, 표기, 격식, voice 경계
- [`references/zh-tw.md`](references/zh-tw.md): 대만 독자를 위한 번체 중국어 가이드
- [`references/evaluation.md`](references/evaluation.md): 내용 보존과 모드 검사
- [`evals/restore-author-voice/eval.yaml`](evals/restore-author-voice/eval.yaml): 검토된 Waza 긍정·부정 회귀 사례
- [`templates/author-profile.md`](templates/author-profile.md): 근거 기반 author profile 템플릿

## 경계

이 skill은 detector 점수에 맞춰 최적화하거나 “사람다움 비율”을 보고하지 않습니다. 사람처럼 보이기 위해 사실, 인용, 경험, 의견, 속어, 1인칭, 의도적인 오류를 추가하지 않습니다. 창작 brief에 허구 작성이 포함되면 fiction에서는 그 범위 안에서 세부 내용을 추가할 수 있습니다. 형식적이거나 중립적이거나 반복적인 문장이 올바른 결과일 수도 있습니다.

## 평가

저장소의 deterministic checks를 실행합니다.

```bash
waza check .
```

검토된 사례는 긍정 및 인접한 부정 routing, 사실 보존, 명시된 voice, voice와 매체의 충돌, 포함된 지시의 비활성화, Slack에 바로 붙여 넣을 수 있는 결과, 근거 없는 반론, 파일에서 본문이 아닌 영역을 다룹니다.

## 감사의 말과 라이선스

출처와 반영한 아이디어는 [`references/attribution.md`](references/attribution.md)에 정리되어 있습니다. 이 저장소는 [MIT License](LICENSE)로 배포됩니다.
