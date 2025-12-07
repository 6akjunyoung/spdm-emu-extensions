cmake_minimum_required(VERSION 3.5)

# 이 파일은 새로운 transport layer를 위한 템플릿입니다.
# 실제 사용 시 파일명과 내용을 수정하세요.

include_directories(${LIBSPDM_DIR}/include
                    ${SPDM_EMU_DIR}/include
                    ${CMAKE_CURRENT_SOURCE_DIR}/../../..
)

set(src_spdm_transport_example_lib
    common.c
    example.c
)

add_library(spdm_transport_example_lib STATIC ${src_spdm_transport_example_lib})

# spdm-emu의 다른 라이브러리와 링크
target_link_libraries(spdm_transport_example_lib
    spdm_common_lib
    spdm_secured_message_lib
)

