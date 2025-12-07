cmake_minimum_required(VERSION 3.5)

project("spdm-emu-extensions" C)

# spdm-emu submodule 경로 설정
set(SPDM_EMU_DIR ${CMAKE_CURRENT_SOURCE_DIR}/spdm-emu)
set(LIBSPDM_DIR ${SPDM_EMU_DIR}/libspdm)

# spdm-emu의 빌드 설정을 그대로 사용하기 위해 변수들을 먼저 설정
# 사용자가 cmake 실행 시 전달하는 변수들을 spdm-emu에 전달
# 예: cmake -DARCH=x64 -DTOOLCHAIN=GCC -DTARGET=Debug -DCRYPTO=mbedtls ..

# spdm-emu를 add_subdirectory로 추가하여 전체 빌드 시스템 로드
# 이렇게 하면 spdm-emu의 모든 설정과 라이브러리들이 로드됨
add_subdirectory(${SPDM_EMU_DIR} ${CMAKE_CURRENT_BINARY_DIR}/spdm-emu-build)

# Include directories for extensions
include_directories(${LIBSPDM_DIR}/include
                    ${SPDM_EMU_DIR}/include
                    ${CMAKE_CURRENT_SOURCE_DIR}/extensions
)

# ============================================
# Extensions 라이브러리 빌드
# ============================================

# Extensions 빌드
# extensions/CMakeLists.txt에서 모든 extensions를 관리
add_subdirectory(extensions)

# ============================================
# Extensions를 spdm-emu executables에 링크
# ============================================

# spdm-emu의 executables에 extensions 라이브러리를 링크
# 이 함수는 extensions 라이브러리들을 spdm-emu의 타겟에 추가로 링크합니다
function(link_extensions_to_spdm_emu)
    # extensions 라이브러리 목록 (여기에 추가된 라이브러리들이 자동으로 링크됨)
    set(EXTENSIONS_LIBRARIES
        # 예: spdm_transport_example_lib
        # 여기에 추가한 extensions 라이브러리들을 나열
    )
    
    # spdm_requester_emu에 extensions 링크
    if(TARGET spdm_requester_emu)
        foreach(ext_lib ${EXTENSIONS_LIBRARIES})
            if(TARGET ${ext_lib})
                target_link_libraries(spdm_requester_emu PRIVATE ${ext_lib})
                message(STATUS "Linked extension library ${ext_lib} to spdm_requester_emu")
            endif()
        endforeach()
    endif()
    
    # spdm_responder_emu에 extensions 링크
    if(TARGET spdm_responder_emu)
        foreach(ext_lib ${EXTENSIONS_LIBRARIES})
            if(TARGET ${ext_lib})
                target_link_libraries(spdm_responder_emu PRIVATE ${ext_lib})
                message(STATUS "Linked extension library ${ext_lib} to spdm_responder_emu")
            endif()
        endforeach()
    endif()
endfunction()

# extensions 라이브러리들이 모두 빌드된 후에 링크
# link_extensions_to_spdm_emu()는 extensions/CMakeLists.txt에서 호출됩니다

message(STATUS "spdm-emu-extensions CMake configuration loaded")
message(STATUS "SPDM_EMU_DIR: ${SPDM_EMU_DIR}")
message(STATUS "LIBSPDM_DIR: ${LIBSPDM_DIR}")
message(STATUS "Extensions will be linked to spdm-emu executables after build")

