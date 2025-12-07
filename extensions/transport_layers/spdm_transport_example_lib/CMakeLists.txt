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

# 이 라이브러리를 extensions 목록에 추가
# 주의: 실제 사용 시에는 이 라인을 주석 처리하거나 제거하세요
# set(EXTENSIONS_LIBRARIES ${EXTENSIONS_LIBRARIES} spdm_transport_example_lib PARENT_SCOPE)

message(STATUS "Built extension library: spdm_transport_example_lib")
