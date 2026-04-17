# 🌲 PINE 2기 7회차 — AI 에이전트 개발 2차

> **유스AI프로젝트:D** | 마포청소년문화의집 × KB데이타시스템 × Microsoft  
> 사용 기술: **Microsoft Agent Framework (MAF) 1.0.0** + Azure OpenAI (API Key)

---

## 📋 오늘 배울 내용 (180분)

| 파트 | 주제 | Builder | 시간 |
|------|------|---------|------|
| Part 1 | Sequential 순차 파이프라인 | `SequentialBuilder` | 10:15~10:40 |
| Part 2 | Concurrent 병렬 에이전트 | `ConcurrentBuilder` | 10:40~11:05 |
| Part 3 | GroupChat 역할 토론 | `GroupChatBuilder` | 11:05~11:40 |
| Part 4 | Session 대화 메모리 | `create_session()` | 11:40~12:05 |
| Part 5 | RAG 외부 지식 검색 | `@tool` | 12:05~12:45 |

---

## ⚡ 빠른 시작 (GitHub Codespace)

1. `< > Code` → `Codespaces` → `Create codespace on main`  
2. 자동으로 Python 3.11 + 패키지 설치 (약 2분)
3. 터미널에서 `.env` 설정 후 노트북 실행!

```bash
cp .env.example .env
# .env 파일에 강사가 제공한 API 키 입력
```

---

## ⚠️ MAF 1.0.0 핵심 API (이전 버전과 다름!)

```python
# ✅ GroupChatBuilder — 생성자 파라미터 방식
workflow = GroupChatBuilder(
    participants=[a, b, c],       # 생성자에 직접!
    selection_func=my_func,
).build()

# ✅ GroupChatState 필드명
state.current_round   # int
state.participants    # OrderedDict
state.conversation    # list[Message]

# ✅ create_session()은 동기 함수!
session = agent.create_session()  # await 없음!

# ✅ run() 결과
response = await agent.run("...", session=session)
print(response.text)              # .text 속성
```

---

## 📓 노트북 실행 순서

```
1️⃣  session7_main.ipynb     ← 메인 강의 (여기서 시작!)
2️⃣  session7_quiz1.ipynb    ← 🔴 번역 파이프라인 (Quiz 1)
3️⃣  session7_quiz2.ipynb    ← 🔴 공부 플래너 (Quiz 2)
4️⃣  session7_quiz3.ipynb    ← 🔴 RAG 진로상담 (Quiz 3)
```

---

## 📁 파일 구조

```
Azure-AI-Agent-MAF-1_0/
├── .devcontainer/devcontainer.json   # Codespace 자동 환경
├── data/rag_source.md                # RAG 한국어 지식베이스
├── session7_main.ipynb               # 메인 강의 (5개 패턴)
├── session7_quiz1~3.ipynb            # 독립 Quiz 노트북
├── .env.example                      # API 키 템플릿
├── requirements.txt                  # agent-framework==1.0.0
└── README.md
```

---

## ❓ FAQ

**`ModuleNotFoundError: agent_framework`**  
→ `pip install agent-framework==1.0.0`

**`GroupChatState` 필드 오류**  
→ `state.current_round` / `state.participants` / `state.conversation` (딕셔너리 키 아님!)

**`create_session()` 오류**  
→ `await` 없이 동기 호출! `session = agent.create_session()`

**`response`에서 텍스트 추출**  
→ `response.text` 사용 (문자열이 아님!)

---

*🌲 Made with ❤️ for PINE 2기 | Microsoft × KB데이타시스템 × 마포청소년문화의집*
