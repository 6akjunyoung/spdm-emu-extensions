# 빌드 가이드

이 프로젝트는 spdm-emu를 submodule로 사용하며, 확장 기능을 추가합니다.

## 사전 요구사항

1. CMake (버전 3.5 이상)
2. GCC (GCC5 이상) 또는 LLVM (LLVM9 이상)
3. Git (submodule 관리용)

## Submodule 초기화

처음 클론한 경우:

```bash
git submodule update --init --recursive
```

Submodule 업데이트:

```bash
git submodule update --recursive
```

## 빌드 방법

### 방법 1: spdm-emu의 빌드 시스템 사용 (권장)

spdm-emu의 빌드 시스템을 직접 사용하여 빌드합니다:

```bash
cd spdm-emu
mkdir build
cd build
cmake -DARCH=x64 -DTOOLCHAIN=GCC -DTARGET=Debug -DCRYPTO=mbedtls ..
make copy_sample_key
make
```

확장 라이브러리를 추가하려면 `spdm-emu/CMakeLists.txt`에 다음을 추가:

```cmake
# Extensions from spdm-emu-extensions
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../extensions/transport_layers/spdm_transport_example_lib)
```

### 방법 2: 독립적인 확장 라이브러리 빌드

확장 라이브러리만 빌드하려면:

```bash
mkdir build
cd build
cmake -DSPDM_EMU_DIR=../spdm-emu -DLIBSPDM_DIR=../spdm-emu/libspdm ..
make
```

## Transport Layer 추가하기

1. `extensions/transport_layers/spdm_transport_<name>_lib/` 디렉토리 생성
2. `spdm_transport_example_lib/`를 참고하여 구현
3. `CMakeLists.txt`에 라이브러리 추가
4. spdm-emu의 `CMakeLists.txt`에 통합

## Test Case 추가하기

1. `extensions/test_cases/` 디렉토리에 새 테스트 추가
2. spdm-emu의 테스트 프레임워크와 통합
3. `CMakeLists.txt`에 테스트 추가

