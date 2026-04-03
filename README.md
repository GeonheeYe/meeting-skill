# meeting-skill

AI 에이전트용 회의 처리 스킬. 오디오 파일 하나로 STT → 화자분리 → 요약 → 위키 업로드까지 자동화한다.

## 시작하기

AI 에이전트에게 다음 URL을 주고 **"이 스킬 설치하고 세팅해줘"** 라고 하면 된다:

```
https://github.com/GeonheeYe/meeting-skill
```

### 설정 과정 (`/meeting setup`)

AI가 자동으로 아래 과정을 진행한다:

1. **meeting-tools 클론** — `~/meeting_tools`에 실행 코드 설치
2. **하드웨어 감지 + 패키지 설치** — 내 환경에 맞는 STT 백엔드만 설치
   ```
   ✅ 환경 감지 완료
      하드웨어: Apple Silicon (Metal, 16GB RAM)
      사용 모델: mlx-whisper large-v3
   ```
3. **`.env` 생성** — HF_TOKEN 입력 안내
4. **프로젝트 설정** (선택) — 주요 프로젝트 이름을 등록하면 회의마다 고유명사·교정 패턴을 누적 저장해 STT 정확도가 높아짐. 없으면 공통 환경으로 처리.
5. **Dooray 연결** (선택) — dooray-mcp 설치 + 위키 설정. 회의 후 위키 자동 업로드.

---

## 사용법

```bash
/meeting setup                                              # 초기 설정 (처음 한 번)
/meeting record                                             # 녹음 시작
/meeting ~/meetings/audio.wav                               # 기본 처리
/meeting ~/meetings/audio.wav 회의제목 2명                  # 화자분리 포함
/meeting ~/meetings/audio.wav 회의제목 4명 project:내프로젝트  # 프로젝트 용어 활용
/meeting ~/meetings/audio.wav 제목 2명 키워드 docs.pdf      # 참고 문서 포함
```

### 프로젝트 용어 누적

`project:이름` 또는 `@이름`을 붙이면 `~/meeting_tools/projects/{name}/terms.md`에 매 회의마다 고유명사와 STT 교정 패턴이 쌓인다.

```
회의 1회: LRG → LIG 교정 → terms.md에 저장
회의 2회: 자동으로 LIG로 인식
```

---

## 지원 환경

| 환경 | STT 백엔드 |
|---|---|
| Apple Silicon (M1/M2/M3/M4) | mlx-whisper large-v3 (Metal GPU 가속) |
| NVIDIA GPU ≥8GB VRAM | faster-whisper large-v3 float16 |
| NVIDIA GPU 4-8GB VRAM | faster-whisper large-v3 int8 |
| CPU (Linux / macOS Intel) | faster-whisper large-v3 int8 |

`/meeting setup` 실행 시 자동으로 감지하여 최적 패키지만 설치한다.

---

## 요구사항

- Python 3.9+
- ffmpeg (`setup`에서 자동 설치 시도)
- HF_TOKEN (화자 분리 사용 시 — [huggingface.co/settings/tokens](https://huggingface.co/settings/tokens))
- Dooray 계정 (선택 — 위키 자동 업로드)

## 실행 코드

[GeonheeYe/meeting-tools](https://github.com/GeonheeYe/meeting-tools)
