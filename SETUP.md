# 환경 설정 가이드

> **이 문서를 끝까지 따라 하면, 카드 등록 없이도 모든 강의를 진행할 수 있습니다.**
>
> 설치에 막히면 [자주 발생하는 오류](#7-자주-발생하는-오류) 섹션을 먼저 보세요.

---

## 0. 한눈에 보는 전체 흐름

```
1. Python 3.10+ 확인
   ↓
2. UV (또는 pip) 설치
   ↓
3. 프로젝트 가상환경 생성 + 패키지 설치
   ↓
4. API 키 1개 이상 발급 (Gemini 권장 — 무료, 카드 X)
   ↓
5. .env 파일 작성
   ↓
6. Jupyter 실행 → 첫 노트북 열기
```

소요 시간: 약 **10~20분** (Ollama 로컬 모델까지 받으면 +10분)

---

## 1. Python 설치 확인

터미널에서:

```bash
python3 --version
# → Python 3.10.x 이상이어야 함 (권장: 3.12)
```

설치되어 있지 않다면:

- **Mac**: `brew install python@3.12`
- **Windows**: <https://www.python.org/downloads/> 에서 3.12 설치 (설치 시 "Add to PATH" 체크)
- **Linux (Ubuntu)**: `sudo apt install python3.12 python3.12-venv`

---

## 2. UV 설치 (권장) — 또는 pip 사용

UV는 Python 패키지 매니저 중 가장 빠른 도구입니다 (pip 대비 10~100배 빠름).

```bash
# Mac / Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

설치 확인:

```bash
uv --version
```

> **UV 없이 pip로만 진행하고 싶다면?** 3번 단계에서 `pip install -r requirements.txt` 를 사용하세요.

---

## 3. 프로젝트 가상환경 + 패키지 설치

### 3-A. UV 사용 (권장)

프로젝트 폴더로 이동 후:

```bash
cd langchain-basic-course
uv sync
```

`uv sync` 한 번이면 가상환경 생성 + `pyproject.toml` 의 모든 패키지 설치가 끝납니다.

### 3-B. pip 사용

```bash
cd langchain-basic-course
python3 -m venv .venv
source .venv/bin/activate     # Mac / Linux
# .venv\Scripts\activate      # Windows
pip install -r requirements.txt
```

### Jupyter 커널 등록 (UV / pip 공통)

```bash
# UV
uv run python -m ipykernel install --user --name=langchain-basic-2026

# pip (가상환경 활성화 상태)
python -m ipykernel install --user --name=langchain-basic-2026
```

VS Code · Jupyter Lab 에서 노트북 우상단 커널 선택 시 `langchain-basic-2026` 을 고르세요.

---

## 4. API 키 발급 — 3개 옵션 중 1개만 있으면 됩니다

### ✅ Option 1: Google Gemini (가장 추천)

**왜 추천?** 카드 등록 불필요, 무료 한도 큼, 한국어 우수.

1. <https://aistudio.google.com/apikey> 접속 (Google 계정 로그인)
2. **"Create API key"** 클릭 → 프로젝트 선택 (없으면 자동 생성)
3. 생성된 키를 복사

**무료 한도 (2026-04 기준)**

| 모델 | 분당 요청 (RPM) | 일일 요청 (RPD) | 분당 토큰 (TPM) |
|------|--------------|--------------|---------------|
| `gemini-2.5-flash-lite` | 15 | 1,000 | 250,000 |
| `gemini-2.5-flash` | 10 | 250 | 250,000 |

> 강의 실습용으로는 **`gemini-2.5-flash-lite`** 가 가장 여유롭습니다.

### ✅ Option 2: Groq (매우 빠름, 한국어 강함)

1. <https://console.groq.com/keys> 접속 → GitHub/Google 로그인
2. **"Create API Key"** 클릭 → 키 복사

**제공 모델 (무료 한도 내)**

- `qwen/qwen3-32b` — 한국어 매우 우수 (Alibaba Qwen3, 128K 컨텍스트)
- `llama-3.3-70b-versatile` — 범용성 좋음
- `gemma2-9b-it` — 가벼운 모델

### ✅ Option 3: Ollama (완전 무료, 로컬)

API 키조차 필요 없는 로컬 실행 옵션입니다. 첫 다운로드만 시간이 걸립니다.

1. <https://ollama.com> 에서 OS별 설치 파일 다운로드 → 실행
2. 터미널에서 모델 다운로드:

```bash
# LLM (선택 — Option 3 으로 LLM도 로컬 실행할 때만)
ollama pull gemma4:e4b   # 약 4GB, 입문용
# ollama pull gemma4:e2b # 약 2GB, 더 가벼움

# 임베딩 (필수 — 03/06 노트북에서 사용)
ollama pull bge-m3       # 약 1.2GB, BAAI 다국어 임베딩 (1024차원)
```

3. 백그라운드에서 자동 실행됨 (`localhost:11434`)

> **임베딩(`bge-m3`) 은 LLM 옵션과 무관하게 모든 시청자에게 권장됩니다.** 03번(`SemanticSimilarityExampleSelector`) 과 06번(RAG) 노트북이 임베딩을 사용하며, 본 강의는 API 키 부담을 줄이기 위해 로컬 Ollama 임베딩으로 통일했습니다.

> **사양 권장**: RAM 16GB 이상이면 `gemma4:e4b` + `bge-m3` 동시 운용이 부드럽게 동작. 8GB 환경이라면 LLM 은 클라우드(Gemini/Groq) 로, 임베딩만 로컬 `bge-m3` 로 사용하는 조합이 안전합니다.

### ⚙️ Option 4 (선택): OpenAI — 유료

> 입문자에게는 카드 등록이 부담일 수 있어 선택 옵션입니다. 위 3개로 강의는 모두 끝까지 진행됩니다.

1. <https://platform.openai.com/api-keys> → "Create new secret key"
2. 결제 카드 등록 필요 ([Billing 설정](https://platform.openai.com/account/billing))

### 🔎 (04 Tools 노트북 전용) Tavily

웹 검색 도구 노트북에서 사용. 무료 1,000회/월.

1. <https://app.tavily.com> 회원가입 → API 키 자동 생성

---

## 5. `.env` 파일 작성

프로젝트 루트의 `.env.example` 을 복사:

```bash
cp .env.example .env
```

`.env` 를 열어 사용하려는 옵션의 키만 채우세요. **3개 중 1개만 있어도 됩니다.**

```env
# 가장 추천하는 입문 세팅 (예시)
GOOGLE_API_KEY=AIzaSy...
TAVILY_API_KEY=tvly-...
```

> 노트북은 `python-dotenv` 패키지로 `.env` 의 값을 환경 변수에 로드합니다. `uv sync` 또는 `pip install -r requirements.txt` 시 자동 설치되므로 별도 설치는 필요 없습니다. 만약 `ModuleNotFoundError: No module named 'dotenv'` 가 나면 7번 트러블슈팅을 참고하세요.

> ⚠️ `.env` 는 **절대 GitHub에 커밋하지 마세요.** `.gitignore` 에 이미 등록돼 있습니다.

---

## 6. Jupyter 실행

```bash
# UV
uv run jupyter lab

# pip (가상환경 활성화 상태)
jupyter lab
```

브라우저가 자동으로 열립니다. `[LLM]_01_GenAI_Intro[Lecture].ipynb` 부터 시작하세요.

---

## 7. 자주 발생하는 오류

### Q1. `OPENAI_API_KEY가 설정되지 않았습니다` 에러

01번 노트북은 OpenAI SDK를 사용합니다. **OpenAI 키가 없다면 02번부터 시작**하셔도 됩니다 (02번부터는 3-option 블록으로 무료 모델 사용 가능). 또는 01번에서 OpenAI 키 대신 Gemini 무료 키로 진행하는 변형 코드는 노트북 내 "트러블슈팅" 셀에 안내되어 있습니다.

### Q2. `langchain_google_genai not found`

```bash
uv add langchain-google-genai
# 또는
pip install langchain-google-genai
```

### Q2-1. `ModuleNotFoundError: No module named 'dotenv'`

`.env` 로딩에 사용하는 `python-dotenv` 가 설치되지 않은 상태입니다. 보통 `uv sync` 또는 `pip install -r requirements.txt` 를 한 번도 실행하지 않았거나, 활성화된 가상환경이 다른 경우입니다.

```bash
# UV
uv sync                # 또는 개별 설치: uv add python-dotenv

# pip (가상환경 활성화 상태)
pip install python-dotenv
```

설치 후에도 같은 오류가 나면, Jupyter 커널이 강의용 가상환경(`langchain-basic-2026`)을 사용 중인지 노트북 우상단에서 확인하세요.

### Q3. Ollama에서 `model not found: gemma4:e4b` 또는 `bge-m3`

```bash
ollama list                  # 설치된 모델 확인
ollama pull gemma4:e4b       # LLM (Option 3 사용 시)
ollama pull bge-m3           # 임베딩 (03/06 노트북 필수)
```

Ollama 앱이 실행 중이어야 합니다 (메뉴바 아이콘 확인). 로컬 서비스 주소는 기본적으로 `http://localhost:11434` 입니다.

### Q3-1. 03/06 노트북에서 임베딩 호출 시 `Connection refused` 또는 `model not found: bge-m3`

03번(예시 선택자) 과 06번(RAG) 노트북은 Ollama 임베딩 모델 `bge-m3` 를 사용합니다. 다음을 확인하세요.

1. Ollama 앱이 실행 중인가? (메뉴바 / 트레이 아이콘)
2. `ollama list` 결과에 `bge-m3` 가 있는가? 없다면 `ollama pull bge-m3`.
3. 첫 호출 시에는 모델 로딩에 수십 초가 걸릴 수 있습니다 (이후 빨라집니다).

### Q4. Apple Silicon Mac에서 `faiss-cpu` 설치 오류

Python 3.12에서 발생 가능. 다음 중 하나를 시도:

```bash
# 방법 1: conda 사용
conda install -c conda-forge faiss-cpu

# 방법 2: Python 3.11 사용
uv venv --python=3.11
uv sync
```

### Q5. Groq `429 Rate limit exceeded`

Groq 무료 한도(분당 요청 수)를 초과한 상태입니다. 1분 정도 기다리거나 Gemini 옵션으로 전환하세요.

### Q6. Jupyter 커널이 `langchain-basic-2026` 으로 안 보임

3번 단계의 **커널 등록** 명령을 다시 실행 후 Jupyter Lab을 재시작하세요.

---

## 8. 다음 단계

설치가 끝났다면:

1. `[LLM]_01_GenAI_Intro[Lecture].ipynb` 부터 순서대로 진행
2. 막히면 노트북 상단의 **"트러블슈팅"** 셀 또는 본 문서 7번을 참고
3. 입문 트랙(01~06)을 끝낸 뒤에는 심화 학습용으로 [`advanced/`](./advanced/) 폴더의 자료를 참고하세요
