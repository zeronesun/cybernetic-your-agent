[English](../en/README.md) | [简体中文](../../README.md) | [繁體中文](../zh_TW/README.md) | [日本語](../ja/README.md) | 한국语 | [Русский](../ru/README.md) | [Deutsch](../de/README.md)

# 첸쉐썬의 공학 사이버네틱스로 AI 에이전트 훈련하기

> AI에 새로운 지식을 가르치지 마세요. **피드포워드, 적분 제어, 계층 분리, 자가 모니터링**이라는 네 가지 개념을 사용하여 에이전트의 기억과 기술 아키텍처를 재구성하고, '수동적인 도구'에서 '스스로 수정하고 진화하는 협업 엔진'으로 전환하세요.

---

## 이 프로젝트 소개

완전하고 재현 가능한 실습 튜토리얼입니다.

첸쉐썬의 『공학 사이버네틱스』의 핵심 아이디어를 현대 AI 에이전트 플랫폼(Hermes, Claude with MCP, 커스텀 GPT 등)에 적용합니다. 프롬프트 항목을 추가하거나 새로운 모델을 도입하지 않고 **아키텍처 재구성**을 통해 에이전트가 다음을 수행하도록 합니다:

- 🎯 **피드포워드로 함정 회피** — 작업 시작 전에 사용자의 선호도와 과거 교훈을 능동적으로 로드
- 🔧 **적분 제어로 진동 방지** — 일회성 불만은 임시 수정에 그치고, 동일한 피드백이 두 번 쌓이면 체계적으로 변경
- 🧹 **계층 분리** — 기억에는 '이유'만 저장하고, 스킬에는 '방법'만 저장하며, 절대 혼합하지 않음
- 🚦 **자가 모니터링 전달 게이트** — 출력 전에 5단계 품질 검사를 실행하고, 통과하지 못하면 전달하지 않음
- 🔄 **폐쇄 루프 진화** — 일주일에 한 번 "이륙"이라고 말하면 에이전트가 자동으로 검토하고 스스로 최적화

---

## 빠른 시작

에이전트에게 이 명령을 보내면 자동으로 전체 훈련을 완료합니다(약 40분):

```
github.com/zeronesun/cybernetic-your-agent의 scripts/deployment-commands.md를 참조해서 나를 훈련시켜줘. 매 단계마다 확인해주고, 완료 후에 폐쇄 루프 테스트를 실행해줘.
```

**전제 조건**: 에이전트가 GitHub에 접근하고, 메모리에 쓰고, 스킬을 생성할 수 있어야 합니다. 충족되지 않으면 아래 수동 단계를 따르세요.

1. 에이전트 플랫폼에 **영구 기억** + **스킬/절차적 모듈**이 있는지 확인하세요
2. 튜토리얼을 읽으세요(순서대로 읽는 것이 좋으며, 적어도 1장을 읽고 접근 방식을 이해하세요)
3. [5장](chapters/05-deployment.md)으로 가서 명령어를 복사하여 단계별로 배포하세요(약 1시간)
4. [6장](chapters/06-daily-usage.md)은 일상적인 사용법과 작동 확인 방법을 알려줍니다

---

## 튜토리얼 구조

| 장      | 파일                                                         | 한 줄 요약                                            |
| :------ | :----------------------------------------------------------- | :---------------------------------------------------- |
| 서문    | [`PREFACE.md`](PREFACE.md)                                   | AI가 모든 지식을 배워도 왜 여전히 '당신을 이해하지' 못하는가 |
| 1장     | [`chapters/01-background.md`](chapters/01-background.md)     | 배경과 핵심 철학                                      |
| 2장     | [`chapters/02-prerequisites.md`](chapters/02-prerequisites.md) | 적용 조건과 준비                                      |
| 3장     | [`chapters/03-core-theory.md`](chapters/03-core-theory.md)   | 네 가지 사이버네틱스 개념 상세 (피드포워드/적분/분리/자가 모니터링) |
| 4장     | [`chapters/04-architecture.md`](chapters/04-architecture.md) | 시스템 아키텍처 상세 (3계층 기억 + 스킬 계층 + 데이터 흐름) |
| 5장     | [`chapters/05-deployment.md`](chapters/05-deployment.md)     | 실습 가이드 (단계별 배포 명령어, 바로 복사 가능)     |
| 6장     | [`chapters/06-daily-usage.md`](chapters/06-daily-usage.md)   | 일상 사용과 검증                                      |
| 7장     | [`chapters/07-faq-extensions.md`](chapters/07-faq-extensions.md) | 문제 해결 + 다중 에이전트/새로운 이론 확장            |
| 에필로그 | [`EPILOGUE.md`](EPILOGUE.md)                                 | 배포 이후: 아키텍처의 의미와 향후 방향                |

### 파일 이름 참고 사항

루트 디렉토리와 장 파일 이름은 크로스 플랫폼 및 도구 체인 호환성을 위해 영어를 사용합니다. 중국어 원본 파일 이름과 GitHub 이름 매핑:

| 로컬 파일 이름 (중국어)             | GitHub 파일 이름              |
| :---------------------------------- | :---------------------------- |
| 서문: 왜 AI…md                      | `PREFACE.md`                  |
| 1장: 배경과 핵심 이념.md            | `chapters/01-background.md`   |
| 2장: 적용 조건과 준비 작업.md       | `chapters/02-prerequisites.md`|
| 3장: 핵심 이론 상세.md              | `chapters/03-core-theory.md`  |
| 4장: 시스템 아키텍처 상세.md        | `chapters/04-architecture.md` |
| 5장: 실천 가이드.md                 | `chapters/05-deployment.md`   |
| 6장: 일상 사용과 검증.md            | `chapters/06-daily-usage.md`  |
| 7장: 자주 묻는 질문과 확장.md       | `chapters/07-faq-extensions.md`|
| 에필로그: 아키텍처 이후.md          | `EPILOGUE.md`                 |

파일 내부 제목과 본문은 중국어로 유지됩니다. `translations/` 디렉토리는 다른 언어 번역(예: `en/`, `ja/`)을 위해 예약되어 있습니다.

### 보충 파일

| 파일                                                         | 설명                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [`scripts/deployment-commands.md`](scripts/deployment-commands.md) | 5장의 모든 명령어를 순수 추출 (설명 없이 빠른 실행용)       |
| [`examples/`](examples/)                                     | L2/L3 예시, 적분 제어 테이블 예시, 심층 검토 출력 예시      |
| [`CONTRIBUTING.md`](CONTRIBUTING.md)                         | 기여 가이드라인                                              |
| [`LICENSE`](LICENSE)                                         | 오픈소스 라이선스                                            |

---

## 지원 플랫폼

- ✅ **Hermes 3** (완전한 네이티브 지원, 모든 명령어가 원활하게 작동)
- ✅ **Claude (with MCP)** (도구 호출 구문에 약간의 수정 필요, 핵심 아키텍처는 완전히 적용 가능)
- ✅ **커스텀 GPTs** (Knowledge 파일로 기억을, Actions로 스킬을 시뮬레이션)
- 🔸 **영구 기억 + 스킬/절차적 모듈**을 갖춘 기타 에이전트 플랫폼
- 🔸 스킬 기능이 없는 플랫폼 (하향 조정하여 실행 가능, [7장 7.1절](chapters/07-faq-extensions.md) 참조)

---

## 한눈에 보기: 전과 후

| 차원           | 전                                           | 후                                               |
| :------------- | :------------------------------------------- | :----------------------------------------------- |
| 작업 시작      | 사용자가 요구사항을 말하고 에이전트가 바로 시작 | 에이전트가 함정 회피 체크리스트와 위험 평가를 먼저 출력하고 확인 |
| 반복되는 실수  | 매번 수정해도 같은 실수 반복                 | 두 번째 발생 시 자동으로 규칙으로 하향 적용, 세 번째에는 발생하지 않음 |
| 기억 신호 대 잡음비 | 원칙, 단계, 사례가 모두 혼재                 | 3계층 분리, 원칙과 단계가 각자 제자리를 가짐       |
| 출력 품질      | 사용자가 검사하고, 상투어구/서식 문제 발견 후 수정 요청 | 에이전트가 5단계 품질 게이트를 스스로 실행, 통과해야 전달 |
| 시스템 진화    | 직감에 의존해 가끔 조정                       | 매주 "이륙"이라고 말하면 자동 검토 및 자동 최적화 |

---

## 핵심 철학

> **당신이 하는 것은 프롬프트 엔지니어링이 아니라 아키텍처 엔지니어링입니다.**
>
> 에이전트에게 새로운 지식을 가르치는 것이 아니라, 시스템 엔지니어링적 사고로 안정적으로 실행되고 지속적으로 진화하는 내부 아키텍처를 설계하는 것입니다.

더 많은 배경과 설명은 [서문](PREFACE.md)과 [1장](chapters/01-background.md)을 참조하세요.

---

## 프로젝트 이름

**Cybernetic Your Agent** — 에이전트에 사이버네틱스 유전자를 주입합니다.

우리는 AI에 새로운 지식을 가르치지 않습니다. 첸쉐썬의 공학 사이버네틱스의 네 가지 개념인 피드포워드, 적분 제어, 계층 분리, 자가 모니터링을 사용하여 에이전트의 기억 및 스킬 아키텍처를 재구성합니다. 에이전트가 명령을 이해하는 것에서 당신의 판단 논리를 이해하는 것으로 진화하여 진정으로 *당신의* 에이전트가 되도록 합니다.

---

## 라이선스

이 프로젝트는 [MIT License](LICENSE)에 따라 라이선스가 부여됩니다.

---

## 감사의 말

- 첸쉐썬의 『공학 사이버네틱스』 — 이 튜토리얼의 이론적 기반
- 최초로 "사이버네틱스로 에이전트 기억 체계를 조직"하는 아이디어를 제안한 노트 작성자와 댓글에서 테스트하고 피드백을 준 모든 분들
- 초기 버전에서 아키텍처를 테스트하고 개선하는 데 도움을 준 모든 분

## Star History

<a href="https://www.star-history.com/?repos=zeronesun%2Fcybernetic-your-agent&type=date&legend=bottom-right">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?repos=zeronesun/cybernetic-your-agent&type=date&theme=dark&legend=bottom-right" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?repos=zeronesun/cybernetic-your-agent&type=date&legend=bottom-right" />
   <img alt="Star History Chart" src="https://api.star-history.com/chart?repos=zeronesun/cybernetic-your-agent&type=date&legend=bottom-right" />
 </picture>
</a>
