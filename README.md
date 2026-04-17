# 🌲 PINE 2기 7회차 — AI 에이전트 개발 2차

> **유스AI프로젝트:D** | 마포청소년문화의집 × KB데이타시스템 × Microsoft  
> **사용 기술**: Microsoft Agent Framework (MAF) 1.0.0 + Azure OpenAI (API Key)

---

## 📋 오늘 배울 내용

| 파트 | 주제 | 시간 |
|------|------|------|
| Part 1 | 멀티 에이전트 & GroupChat | 10:15~10:55 |
| Part 2 | 메모리 & 세션 관리 | 10:55~11:35 |
| Part 3 | RAG 에이전트 개발 | 11:35~12:30 |
| 마무리 | 팀 발표 & Q&A | 12:30~13:00 |

---

## ⚡ 빠른 시작 (GitHub Codespace — 권장)

1. 이 페이지 상단 **`< > Code`** → **`Codespaces`** → **`Create codespace on main`**
2. VS Code가 브라우저에서 열리고 Python 환경이 자동 설치됩니다 (약 2분)
3. 터미널에서 `.env` 파일을 만들고 API 키를 입력하면 바로 시작!

---

## 🔑 환경 변수 설정 (필수!)

```bash
# 1) .env.example 복사
cp .env.example .env

# 2) .env 파일 열어서 강사에게 받은 값 입력
```

`.env` 파일 내용 예시:
```
AZURE_OPENAI_ENDPOINT=https://your-resource.openai.azure.com/
AZURE_OPENAI_API_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
AZURE_OPENAI_MODEL=gpt-4o-mini
AZURE_OPENAI_API_VERSION=2024-08-01-preview
```

> ⚠️ `.env` 파일은 절대 GitHub에 올리지 마세요! (`.gitignore`에 이미 포함)

---

## 📦 사용 패키지

| 패키지 | 버전 | 역할 |
|--------|------|------|
| `agent-framework` | 1.0.0 | Microsoft Agent Framework (MAF) |
| `python-dotenv` | ≥1.0.0 | .env 파일 로드 |
| `scikit-learn` | ≥1.4.0 | TF-IDF RAG 검색 |
| `numpy` | ≥1.26.0 | 벡터 연산 |

```bash
# 수동 설치가 필요한 경우
pip install -r requirements.txt
```

---

## 📓 노트북 실행 순서

```
1️⃣  session7_main.ipynb     ← 메인 강의 (여기서 시작!)
2️⃣  session7_quiz1.ipynb    ← 🔴 Quiz 1: 멀티 에이전트 GroupChat 설계
3️⃣  session7_quiz2.ipynb    ← 🔴 Quiz 2: 세션 기반 공부 플래너
4️⃣  session7_quiz3.ipynb    ← 🔴 Quiz 3: RAG 진로 상담 에이전트 완성
```

---

## 🏗 기술 아키텍처

```
Azure OpenAI (API Key 방식)
        │
        ▼
Microsoft Agent Framework 1.0.0  ← 순수 Local 실행
        ├── Agent + OpenAIChatClient   (단일 에이전트)
        ├── GroupChatBuilder           (멀티 에이전트 협업)
        ├── Session (create_session)   (메모리/대화 이력)
        └── @tool 데코레이터            (도구 등록)
                    │
                    └── TF-IDF 검색 → RAG 에이전트
```

> **참고**: AI Foundry Agent Service (Managed Agent)는 사용하지 않습니다.  
> 모든 에이전트는 로컬에서 실행되며 Azure OpenAI LLM만 API Key로 호출합니다.

---

## 📁 파일 구조

```
session7/
├── .devcontainer/
│   └── devcontainer.json     # Codespace 자동 환경 설정
├── data/
│   └── rag_source.md         # RAG 실습용 한국어 지식베이스
├── answers/
│   ├── quiz1_answer.py       # Quiz 1 정답 (강사 참고용)
│   ├── quiz2_answer.py       # Quiz 2 정답 (강사 참고용)
│   └── quiz3_answer.py       # Quiz 3 정답 (강사 참고용)
├── session7_main.ipynb       # 메인 강의 노트북
├── session7_quiz1.ipynb      # Quiz 1: 멀티 에이전트
├── session7_quiz2.ipynb      # Quiz 2: 세션 메모리
├── session7_quiz3.ipynb      # Quiz 3: RAG 에이전트
├── .env.example              # 환경 변수 템플릿
├── .gitignore                # .env 보호
├── requirements.txt          # Python 패키지
└── README.md                 # 이 파일
```

---

## ❓ 자주 묻는 문제 (FAQ)

### `AuthenticationError` — API 키 오류
- `.env` 파일이 프로젝트 루트에 있는지 확인
- API 키에 공백이나 따옴표가 없는지 확인
- `AZURE_OPENAI_MODEL`에 실제 배포 이름이 입력되어 있는지 확인

### `ModuleNotFoundError: No module named 'agent_framework'`
```bash
pip install agent-framework==1.0.0
```

### Jupyter에서 `await`가 작동하지 않을 때
Jupyter Notebook/Lab은 기본적으로 `await`를 셀에서 직접 지원합니다.  
만약 오류가 나면 노트북 첫 셀에서 먼저 실행:
```python
import nest_asyncio
nest_asyncio.apply()
```

### `ServiceResponseException: Resource not found` 오류
`AZURE_OPENAI_MODEL`이 배포 이름(deployment name)과 정확히 일치하는지 확인하세요.

---

## 🔗 참고 링크

- [MAF 1.0.0 공식 발표](https://devblogs.microsoft.com/agent-framework/microsoft-agent-framework-version-1-0/)
- [MAF Python 문서](https://learn.microsoft.com/en-us/agent-framework/)
- [agent-framework PyPI](https://pypi.org/project/agent-framework/)
- [GitHub Codespaces 가이드](https://docs.github.com/ko/codespaces)

---

*Made with ❤️ for PINE 2기 고등학생 여러분 | Microsoft × KB데이타시스템 × 마포청소년문화의집*
