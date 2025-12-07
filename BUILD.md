# 빌드 가이드

이 프로젝트는 spdm-emu를 submodule로 사용하며, **spdm-emu submodule은 수정하지 않고** root repo에서 확장 기능을 추가합니다.

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

### Root Repo에서 통합 빌드 (권장)

**spdm-emu submodule을 수정하지 않고** root repo에서 모든 것을 빌드합니다:

```bash
# 프로젝트 루트에서
mkdir build
cd build
cmake -DARCH=x64 -DTOOLCHAIN=GCC -DTARGET=Debug -DCRYPTO=mbedtls ..
make copy_sample_key
make
```

이렇게 하면:
- spdm-emu가 자동으로 빌드됩니다
- extensions 라이브러리들이 빌드됩니다
- extensions가 spdm-emu의 executables (`spdm_requester_emu`, `spdm_responder_emu`)에 자동으로 링크됩니다

빌드 결과물은 `build/bin/` 디렉토리에 생성됩니다.

## Extensions 추가하기

### Transport Layer 추가

1. `extensions/transport_layers/spdm_transport_<name>_lib/` 디렉토리 생성
2. `spdm_transport_example_lib/`를 참고하여 구현
3. `extensions/CMakeLists.txt`에 다음 추가:
   ```cmake
   add_subdirectory(transport_layers/spdm_transport_<name>_lib)
   ```
4. `CMakeLists.txt`의 `link_extensions_to_spdm_emu()` 함수에서 `EXTENSIONS_LIBRARIES`에 라이브러리 이름 추가:
   ```cmake
   set(EXTENSIONS_LIBRARIES
       spdm_transport_<name>_lib
   )
   ```
5. 재빌드하면 자동으로 spdm-emu executables에 링크됩니다

### Test Case 추가

1. `extensions/test_cases/` 디렉토리에 새 테스트 추가
2. `extensions/CMakeLists.txt`에 다음 추가:
   ```cmake
   add_subdirectory(test_cases/<name>)
   ```
3. 필요시 `CMakeLists.txt`의 `link_extensions_to_spdm_emu()` 함수에서 링크 설정

## 작동 원리

1. Root `CMakeLists.txt`가 spdm-emu를 `add_subdirectory`로 추가하여 전체 빌드 시스템을 로드합니다
2. Extensions가 `extensions/CMakeLists.txt`에서 빌드됩니다
3. `link_extensions_to_spdm_emu()` 함수가 extensions 라이브러리들을 spdm-emu executables에 자동으로 링크합니다
4. **spdm-emu submodule은 전혀 수정되지 않습니다**

## 주의사항

- spdm-emu submodule의 파일은 수정하지 마세요
- 모든 확장 기능은 `extensions/` 디렉토리에 추가하세요
- 새로운 extension을 추가한 후에는 `CMakeLists.txt`의 `EXTENSIONS_LIBRARIES`를 업데이트해야 합니다

