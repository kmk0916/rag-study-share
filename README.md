# RAG 학습 및 공유용 자료
이 자료는 RAG(Retrieval-Augmented Generation) 개념을 직접 학습하고,  
동료 개발자나 스터디원에게 공유하기 위해 개인이 정리한 실습 예제입니다.

LangChain 프레임워크와 Upstage LLM, Pinecone Vector Database를 활용하여 문서 기반 AI 질문/답변 체인을 구현합니다.

---

## 📁 파일 구성

- **.env**  
  - API 키를 저장하는 환경 변수 파일  
  - Upstage API 및 Pinecone API 키 설정 필요  

- **1. LangChain 프레임워크를 통해 upstage라는 AI모델(LLM)을 호출하여 질문하기.ipynb**  
  - LangChain에서 Upstage LLM 모델을 호출하고 단순히 질문/답변을 테스트하는 예제

- **2. Vector Database 구성하여 AI모델(LLM)을 호출하여 질문하기.ipynb**  
  - 문서를 Chunking 후 Upstage Embeddings를 활용하여 벡터화  
  - Pinecone Vector Database에 업로드  
  - Retrieval 기반으로 LLM 질문/답변 구현 예제

- **3. keyword 사전 활용.ipynb**  
  - 사용자 질문을 Knowledge Base 용어에 맞게 자동 변환  
  - LangChain Expression Language(LCEL)와 Chain을 활용한 질문 전처리 예제

- **tax_with_markdown.docx**  
  - Vector Database를 구성할 대상 문서 예시

---

## 🔹 학습 목표

1. LangChain 기반 LLM 호출 방법 이해  
2. 문서 Vectorization 및 Pinecone 활용법 습득  
3. Retrieval-Augmented Generation(RAG) 체인 구성 이해  
4. 사용자 질문 전처리와 Prompt 활용 방법 학습  
5. 실제 질문을 AI가 참조 문서 기반으로 답변하도록 구현  

---

## 🔹 실행 순서 (권장)

1. `.env` 파일에 Upstage API Key, Pinecone API Key 입력  
2. **1번 노트북**으로 LLM 기본 호출 연습  
3. **2번 노트북**으로 문서 벡터화 및 Retrieval QA 체인 구성  
4. **3번 노트북**으로 질문 전처리 체인 실습  
5. Pinecone과 LLM 연계로 최종 질문 → 답변까지 확인  

---

## 🔹 참고

- Upstage API 문서: [https://console.upstage.ai/docs/getting-started](https://console.upstage.ai/docs/getting-started)  
- Pinecone 가입 및 API 발급: [https://app.pinecone.io](https://app.pinecone.io)  
- LangChain 공식 문서: [https://python.langchain.com](https://python.langchain.com)

---

## ⚡ Tip

- Vector Database에 업로드할 때는 batch 단위로 업로드하는 것이 안정적  
- 질문 전처리 및 Prompt 설계를 통해 AI 답변 정확도를 높일 수 있음
- RAG 체인은 “질문 → Retrieval → Prompt → 답변” 순으로 구성됨

<br/>

# 🧩 실습 환경 설정 가이드 (Windows)

Windows 환경에서 Python 가상환경을 설정하는 방법을 안내 
LangChain, Upstage, Pinecone 등을 실습하기 전에 **안정적인 Python 개발 환경**을 먼저 구성.

---

## 🧱 1️⃣ 환경 구성 정보

| 항목 | 버전 / 도구 |
|------|--------------|
| OS | Windows 11 |
| Python 버전 | 3.11.2 |
| 가상환경 관리도구 | pyenv-win |
| 가상환경 생성 방식 | venv |

---

## 🪄 2️⃣ pyenv-win 설치

### 🔗 설치 경로
- 공식 GitHub: [https://github.com/pyenv-win/pyenv-win/blob/master/docs/installation.md#powershell](https://github.com/pyenv-win/pyenv-win/blob/master/docs/installation.md#powershell)


### 📦 설치 방법 요약
1. Windows PowerShell을 **관리자 권한**으로 실행  
2. 아래 명령어 입력:
   ```bash
   Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"; &"./install-pyenv-win.ps1"
   ```
3. PowerShell을 새로 열고 설치 확인
   ```bash
   pyenv --version
   ```

## 🧩 3️⃣ Python 버전 설치 및 지정

- 프로젝트 폴더를 생성하고, 해당 프로젝트 폴더에서 원하는 Python 버전을 설치하고 사용할 버전을 지정.
  ```bash
  # Python 3.11.2 설치
  pyenv install 3.11.2

  # 현재 프로젝트에서 Python 3.11.2 사용 지정
  pyenv local 3.11.2
  ```

- ✅ 명령어 실행 후, 폴더 안에 .python-version 파일이 생성되면 정상.
해당 폴더에서 실행되는 모든 Python 명령은 이 버전을 따름.


## 🧰 4️⃣ 가상환경 생성
- 설치한 Python 버전을 기반으로 가상환경을 생성.
 - llm-application 은 가상환경 폴더 이름 예시.
    ```
    python -m venv llm-application
    ```
 - 생성이 완료되면 아래 구조가 생깁니다:
    ```plaintext
    rag-study-share/
    ├── llm-application/
    │   ├── Scripts/
    │   ├── Lib/
    │   └── pyvenv.cfg
    ```

## ⚡ 5️⃣ 가상환경 활성화

- 가상환경을 실행(활성화)하려면 아래 명령어를 입력.

  ```
  .\llm-application\Scripts\activate
  ```
- 성공 시, 프롬프트 앞에 (llm-application) 이 표시:
  ```
  (llm-application) C:\Users\username\rag-study-share>
  ```
- 비활성화는 다음 명령어로 가능:
  ```
  deactivate
  ```