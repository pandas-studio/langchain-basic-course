# 🤖 생성형 AI / LLM 입문 with LangChain v1.0

> **인프런 · 유튜브 판다스 스튜디오 무료 강의 자료**
>
> 카드 등록 없이 무료로 시작하는 생성형 AI · LangChain v1.0 입문 트랙 (6강, 약 2~3시간)

[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg)](./LICENSE)
[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![LangChain](https://img.shields.io/badge/LangChain-v1.0%2B-green.svg)](https://python.langchain.com/)

---

## 📚 이 강의는 무엇인가요?

**"카드 등록·결제 부담 없이 LLM 첫 실습을 끝내고 싶다"** 는 분을 위한 입문 트랙입니다.

- 🎯 **대상**: 파이썬 기초 문법은 알지만 LLM·LangChain은 처음인 분
- ⏱ **분량**: 6개 노트북, 약 2~3시간 + 한국어 실습 시나리오
- 🆓 **비용**: **0원** (Google Gemini 2.5 Flash-Lite 무료 한도 또는 로컬 Ollama로 진행)

---

## 📖 커리큘럼 (01~06)

> 📓 **본편 6강 노트북·영상이 모두 공개되었습니다 (2026-04-28).**

| # | 노트북 | 핵심 개념 | 🎬 영상 |
|---|--------|----------|--------|
| 01 | **GenAI 개론** | "다음 토큰 예측" 자판기 비유 · OpenAI SDK 첫 호출 · `temperature` · JSON 출력 | ✅ 이론편 · ✅ 실습편 |
| 02 | **LangChain Core + LCEL** | `init_chat_model` · LCEL 파이프 (`\|`) · Runnable 4종 · Streaming · Batch | ✅ 이론편 · ✅ 실습편 |
| 03 | **Prompt + Structured Output** | Zero/One/Few-shot 도화지 비유 · Pydantic 엑셀 양식 비유 · Example Selector | ✅ 이론편 · ✅ 실습편 |
| 04 | **Tools** | `@tool` 데코레이터 · `bind_tools` · 수동 ReAct 루프 · Tavily 웹검색 + 폴백 | ✅ 이론편 · ✅ 실습편 |
| 05 | **Agents** | `create_agent` 한 줄 · ReAct 다이어그램 · MemorySaver · 구조화 출력 · `@dynamic_prompt` | ✅ 이론편 · ✅ 실습편 |
| 06 | **RAG Data Pipeline** | 임베딩 = 의미 좌표계 · FAISS · 청크 시각화 · LCEL 한 줄 RAG | ✅ 이론편 · ✅ 실습편 |

---

## 🚀 빠른 시작

### 1️⃣ 클론 + 가상환경

```bash
git clone https://github.com/pandas-studio/langchain-basic-course.git
cd langchain-basic-course
uv sync   # 또는: python -m venv .venv && source .venv/bin/activate && pip install -r requirements.txt
```

### 2️⃣ API 키 1개 발급 (무료 옵션 추천)

```bash
cp .env.example .env
# .env 파일을 열어 키 한 개만 채우세요
```

| 옵션 | 비용 | 발급 링크 | 한국어 |
|------|------|----------|--------|
| ✅ Google Gemini 2.5 Flash-Lite | **무료** (카드 X) | <https://aistudio.google.com/apikey> | ⭐⭐⭐⭐⭐ |
| ✅ Groq Qwen3 32B | **무료** | <https://console.groq.com/keys> | ⭐⭐⭐⭐⭐ |
| ✅ Ollama Gemma 4 E4B | **완전 무료** (로컬) | <https://ollama.com> | ⭐⭐⭐⭐ |
| ⚙️ OpenAI gpt-4.1-mini | 유료 | <https://platform.openai.com/api-keys> | ⭐⭐⭐⭐⭐ |

> 자세한 환경 설정은 [`SETUP.md`](./SETUP.md) 를 참고하세요 (10~20분 소요).

### 3️⃣ Jupyter 시작

```bash
uv run jupyter lab
# → 01번 노트북 열기
```

---

## 🛠 기술 스택 (2026-04 기준)

- **Python** 3.10+ (권장 3.12)
- **LangChain v1.0+** — `langchain.chat_models`, `langchain.messages`, `langchain.tools`
- **LangGraph 1.0+** — 05번 노트북부터 `create_agent`
- **무료 LLM**: `gemini-2.5-flash-lite`, `qwen/qwen3-32b`, `gemma4:e4b`
- **임베딩**: `bge-m3` (Ollama 로컬, BAAI 다국어, 1024차원, API 키 불필요)
- **VectorDB**: FAISS
- **웹검색**: Tavily (선택)

---

## 📺 강의 영상 채널

본 저장소의 강의 영상은 **인프런** 과 **유튜브 판다스 스튜디오** 채널에 게시됩니다. 강의 1개당 **이론편(슬라이드) + 실습편(노트북 시연) 2편** 으로 구성되어 있으며 (총 12편 — 본편 6×2), 본 노트북은 **실습편 영상에서 다루는 자료** 입니다.

| 강의 | 이론편 | 실습편 |
|------|--------|--------|
| 01 생성형 AI 개론 | ✅ 공개 | ✅ 공개 |
| 02~06 본편 | ✅ 공개 | ✅ 공개 |

- 🎓 **인프런 강의** : <https://inf.run/avW8v>
- 📺 **유튜브 재생목록** : <https://www.youtube.com/playlist?list=PL5bzmUGXvZNR9EXdqjCuETGfrKs_hdk7K>

> 🆕 **본편 6강 노트북·영상이 모두 공개되었습니다 (2026-04-28).**

---

## 📜 라이선스

본 저장소는 **CC BY-NC-ND 4.0** 라이선스를 따릅니다.

- ✅ **개인 학습**: 자유롭게 clone·실행·수정 가능 (단, 수정본 재배포는 금지)
- ❌ **강의·기업 교육 사용**: 사전 서면 동의 필수
- ❌ **상업 목적 활용**: 금지

자세한 내용은 [`LICENSE`](./LICENSE) 와 한국어 안내 [`NOTICE.md`](./NOTICE.md) 를 반드시 확인해주세요.

> ⚠️ **본 저장소를 clone 하거나 다운로드 하는 행위는 위 라이선스 조건에 동의함을 의미합니다.**

---

## 🐛 이슈 / 질문

- **오타·코드 오류**: [GitHub Issues](https://github.com/pandas-studio/langchain-basic-course/issues) (Label: `bug`)
- **학습 질문**: **인프런 강의 Q&A 게시판[](https://inf.run/avW8v)만 사용해주세요** (GitHub 저장소는 코드 이슈 전용)
- **라이선스 문의**: [GitHub Issues](https://github.com/pandas-studio/langchain-basic-course/issues) (Label: `license-inquiry`)

---

## 🙏 Acknowledgements

- LangChain · LangGraph 팀의 v1.0 단순화에 감사드립니다
- Google AI Studio · Groq · Ollama 의 무료 한도 정책 덕분에 입문자도 카드 없이 시작할 수 있습니다

---

**Made with ❤️ by 판다스 스튜디오 (Pandas Studio)** · 2026
