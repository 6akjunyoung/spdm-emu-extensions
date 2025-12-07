# spdm-emu-extensions

이 프로젝트는 [DMTF/spdm-emu](https://github.com/DMTF/spdm-emu)를 submodule로 사용하여 SPDM 에뮬레이터를 확장하는 프로젝트입니다.

## 개요

spdm-emu-extensions는 다음과 같은 확장 기능을 제공합니다:

- **테스트 케이스 확장**: 기존 spdm-emu의 테스트 케이스를 확장하거나 새로운 테스트 케이스 추가
- **Transport Layer 추가**: 새로운 transport layer 프로토콜 구현 및 추가
- **기타 확장 기능**: spdm-emu의 기능을 확장하는 다양한 컴포넌트

## 프로젝트 구조

```
spdm-emu-extensions/
├── spdm-emu/                    # spdm-emu submodule
├── extensions/
│   ├── test_cases/              # 테스트 케이스 확장
│   │   ├── requester/          # Requester 테스트 케이스
│   │   ├── responder/          # Responder 테스트 케이스
│   │   └── common/             # 공통 테스트 유틸리티
│   └── transport_layers/       # Transport Layer 확장
│       └── spdm_transport_example_lib/  # 예제 템플릿
├── CMakeLists.txt              # 메인 CMake 설정
├── BUILD.md                    # 빌드 가이드
└── README.md                   # 이 파일
```

## 시작하기

### 1. 저장소 클론 및 Submodule 초기화

```bash
git clone <repository-url>
cd spdm-emu-extensions
git submodule update --init --recursive
```

### 2. 빌드

자세한 빌드 방법은 [BUILD.md](BUILD.md)를 참조하세요.

기본 빌드:

```bash
cd spdm-emu
mkdir build
cd build
cmake -DARCH=x64 -DTOOLCHAIN=GCC -DTARGET=Debug -DCRYPTO=mbedtls ..
make copy_sample_key
make
```

### 3. 확장 기능 추가

#### Transport Layer 추가

1. `extensions/transport_layers/spdm_transport_<name>_lib/` 디렉토리 생성
2. `spdm_transport_example_lib/`를 참고하여 구현
3. 필요한 함수들 구현:
   - `spdm_<name>_get_sequence_number()`
   - `spdm_<name>_get_max_random_number_count()`
   - `spdm_<name>_get_secured_spdm_version()`
   - `spdm_transport_<name>_encode_message()`
   - `spdm_transport_<name>_decode_message()`
4. `spdm-emu/CMakeLists.txt`에 라이브러리 추가

#### 테스트 케이스 추가

1. `extensions/test_cases/` 디렉토리에 새 테스트 추가
2. spdm-emu의 테스트 프레임워크와 통합
3. `CMakeLists.txt`에 테스트 추가

## 참고 자료

- [spdm-emu 공식 저장소](https://github.com/DMTF/spdm-emu)
- [SPDM Specification](https://www.dmtf.org/standards/spdm)
- [libspdm](https://github.com/DMTF/libspdm)

## 라이선스

이 프로젝트는 spdm-emu와 동일한 BSD-3-Clause 라이선스를 따릅니다.

## 기여

이슈 및 풀 리퀘스트를 환영합니다. 기여하기 전에 프로젝트의 코딩 스타일과 가이드라인을 확인해주세요.