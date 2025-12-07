# Extensions CMakeLists.txt
# 이 파일은 모든 extensions를 통합 관리합니다

# Transport Layer Extensions
# 새로운 transport layer를 추가하려면 아래 주석을 해제하고 경로를 수정하세요
# add_subdirectory(transport_layers/spdm_transport_<name>_lib)

# Test Case Extensions
# 새로운 테스트 케이스를 추가하려면 아래 주석을 해제하고 경로를 수정하세요
# add_subdirectory(test_cases/<name>)

# 모든 extensions가 빌드된 후 spdm-emu executables에 자동으로 링크
# link_extensions_to_spdm_emu() 함수는 root CMakeLists.txt에서 정의되어 있습니다
# 새로운 extension 라이브러리를 추가한 후, root CMakeLists.txt의 
# link_extensions_to_spdm_emu() 함수 내부의 EXTENSIONS_LIBRARIES에 추가하세요
if(COMMAND link_extensions_to_spdm_emu)
    link_extensions_to_spdm_emu()
endif()

