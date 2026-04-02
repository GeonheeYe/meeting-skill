# meeting-skill

AI 에이전트용 회의 처리 스킬. 오디오 파일 하나로 STT → 화자분리 → 요약 → 위키 업로드까지 자동화한다.

## 설치 (Claude Code)

AI 에이전트에게 다음 URL을 주고 "이 스킬 설치하고 세팅해줘"라고 하면 자동 설정된다:

```
https://github.com/GeonheeYe/meeting-skill
```

또는 직접:

```bash
# 초기 설정 (meeting-tools 클론 + 패키지 설치 + .env 생성 + Dooray 연결)
/meeting setup
```

## 사용법

```bash
/meeting ~/meetings/audio.wav                              # 기본 처리
/meeting ~/meetings/audio.wav 회의제목 2명                 # 화자분리 포함
/meeting ~/meetings/audio.wav 제목 2명 키워드 docs.pdf     # 참고 문서 포함
/meeting record                                           # 녹음 시작
```

## 지원 환경

| 환경 | STT 백엔드 |
|---|---|
| Apple Silicon (M1/M2/M3/M4) | mlx-whisper (Metal GPU 가속) |
| NVIDIA GPU ≥8GB VRAM | faster-whisper large-v3 float16 |
| NVIDIA GPU 4-8GB VRAM | faster-whisper large-v3 int8 |
| CPU (Linux / macOS Intel) | faster-whisper large-v3 int8 |

`/meeting setup` 실행 시 자동으로 최적 백엔드를 감지하여 설치한다.

## 요구사항

- Python 3.9+
- ffmpeg
- HF_TOKEN (화자 분리 사용 시 — [huggingface.co/settings/tokens](https://huggingface.co/settings/tokens))
- Dooray 계정 (선택 — 위키 자동 업로드)

## 실행 코드

[GeonheeYe/meeting-tools](https://github.com/GeonheeYe/meeting-tools)
