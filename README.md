# Nearmix

**Your sound. Your control.**

기존 디지털 믹서와 DAW의 오디오를 연주자별 스마트폰으로 전달하고, 각자 개인 모니터 믹스를 조절하는 로컬 실시간 오디오·컨트롤 플랫폼입니다.

운영자가 Host와 Audio Tap을 설정하면, 연주자는 QR로 접속해 유선 이어폰으로 듣고 자신의 믹스를 조절하는 경험을 목표로 합니다. iPhone은 앱 설치 없는 Safari 사용을 핵심 가설로 검증합니다.

> 현재는 개발 계획 단계입니다. 실행 가능한 Host·플러그인·웹 믹서와 검증된 성능 수치는 아직 없습니다. Nearmix는 작업명이며 도메인과 상표는 별도 확인이 필요합니다.

## 첫 제품의 범위

- 단일 Host·단일 합주실에서 VST3 Audio Tap으로 Ableton 소스를 캡처합니다.
- Host에서 연주자별 독립 스테레오 믹스를 만들고 Gain·Mute·master를 제공합니다.
- iPhone Safari와 Android 브라우저 수신, QR 접속, 안전한 재생 시작과 연결 진단을 목표로 합니다.
- 초기 실험은 생성 신호 2~4개로 시작하고, 실제 장비에서 최대 16개 소스를 단계적으로 검증합니다.

MIDI 컨트롤, 인증 공유기 Nearmix Link, Android 네이티브 수신기는 모니터링 검증 이후의 확장 영역입니다. Bluetooth 이어폰의 낮은 지연과 모든 기기·무선 환경의 무중단 동작은 보장하지 않습니다.

## 개발 순서

1. 실제 장비 라우팅과 물리 루프백 측정 환경을 기록합니다.
2. 생성 PCM을 Safari로 보내 WebTransport와 WebRTC를 실측 비교합니다.
3. 화면 잠금·악보 앱 전환·로컬 HTTPS를 검증하고 제품 가능성을 판정합니다.
4. 안전한 개인 믹스와 Listener별 송출 격리, 장기 클록 보정을 구현합니다.
5. VST3 Audio Tap과 Ableton을 연결한 뒤 모바일 믹서와 운영자 UI를 만듭니다.
6. 반복 합주와 외부 파일럿을 통과한 조건으로 베타를 제공합니다.

유선 출력의 P95 종단 간 지연 40ms 이하, 2시간 안정성, 첫 접속 1분 이내는 탐색 목표입니다. 성능 판단은 네트워크 RTT나 JS 타이밍 대신 실제 이어폰 출력의 물리 측정과 드롭아웃 기록을 기준으로 합니다.

## PR 단위 기술 명세

[`.tech-specs` 폴더](.tech-specs/)에 구현·설계·검증 작업 40개를 정리했습니다. 각 번호 Markdown 파일이 PR 하나의 범위이며, 선행 PR·산출물·검증 방법·완료 기준을 포함합니다. 번호 순서보다 선행 관계를 따릅니다.

처음에는 [개발 기반](.tech-specs/001.md), [장비 라우팅 조사](.tech-specs/002.md), [물리 측정 도구](.tech-specs/003.md), [사용자 흐름](.tech-specs/004.md)부터 진행합니다. [Safari 판정 ADR](.tech-specs/012.md)을 통과하거나 제품 전제를 수정한 뒤 후속 구현에 착수합니다.

## 저장소와 실행

```sh
git clone git@github.com:tonyfromundefined/nearmix.git
cd nearmix
```

현재 저장소에는 README와 기술 명세만 있습니다. 빌드·실행·테스트 명령은 첫 구현 PR에서 추가합니다. 예정 구조는 다음과 같습니다.

```text
apps/host/               # Host 설정·진단
apps/web/                # Safari 실험 수신기, 이후 게스트 믹서
plugins/audio-tap-vst3/   # DAW 패스스루 캡처
packages/protocol/       # 패킷·제어 스키마
benchmarks/              # 지연·손실·부하 측정
docs/                   # 라우팅·시험 계획·ADR
```

Host 엔진 언어와 라이브러리, 지원 OS, 인증서 전략은 선행 실험으로 결정합니다. 핵심 엔진과 프로토콜 공개를 지향하며, 라이선스는 의존성 검토 후 확정합니다.
