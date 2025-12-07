cmake_minimum_required(VERSION 3.5)

project("spdm-emu-extensions" C)

# spdm-emu submodule 경로 설정
set(SPDM_EMU_DIR ${CMAKE_CURRENT_SOURCE_DIR}/spdm-emu)
set(LIBSPDM_DIR ${SPDM_EMU_DIR}/libspdm)

# spdm-emu의 CMakeLists.txt를 include하여 기본 설정 로드
# spdm-emu의 CMakeLists.txt는 이미 많은 설정을 포함하고 있으므로,
# 이를 활용하기 위해 spdm-emu를 부모 프로젝트로 설정

# 확장 라이브러리 출력 경로
set(EXTENSIONS_LIBRARY_OUTPUT_PATH ${CMAKE_CURRENT_BINARY_DIR}/lib)
set(EXTENSIONS_EXECUTABLE_OUTPUT_PATH ${CMAKE_CURRENT_BINARY_DIR}/bin)

# Include directories
include_directories(${LIBSPDM_DIR}/include
                    ${SPDM_EMU_DIR}/include
                    ${CMAKE_CURRENT_SOURCE_DIR}/extensions
)

# Transport Layer Extensions
# 새로운 transport layer를 추가하려면 여기에 subdirectory 추가
# add_subdirectory(extensions/transport_layers/spdm_transport_<name>_lib)

# Test Case Extensions
# 새로운 테스트 케이스를 추가하려면 여기에 subdirectory 추가
# add_subdirectory(extensions/test_cases/<name>)

message(STATUS "spdm-emu-extensions CMake configuration loaded")
message(STATUS "SPDM_EMU_DIR: ${SPDM_EMU_DIR}")
message(STATUS "LIBSPDM_DIR: ${LIBSPDM_DIR}")

