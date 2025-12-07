# Transport Layer Extensions

이 디렉토리는 새로운 transport layer 구현을 추가하는 코드를 포함합니다.

## 구조

각 transport layer는 자체 디렉토리를 가집니다:
- `spdm_transport_<name>_lib/` - 새로운 transport layer 구현

## Transport Layer 구현 가이드

새로운 transport layer를 추가하려면:

1. `spdm_transport_<name>_lib/` 디렉토리 생성
2. 다음 함수들을 구현해야 합니다:
   - `spdm_<name>_get_sequence_number()` - 시퀀스 번호 처리
   - `spdm_<name>_get_max_random_number_count()` - 최대 랜덤 번호 카운트
   - `spdm_<name>_get_secured_spdm_version()` - 보안 메시지 버전
   - `spdm_<name>_encode_message()` - 메시지 인코딩
   - `spdm_<name>_decode_message()` - 메시지 디코딩

3. `CMakeLists.txt`에 라이브러리 추가
4. spdm-emu의 CMakeLists.txt에 통합

## 참고

기존 transport layer 구현 예제:
- `spdm-emu/library/spdm_transport_none_lib/`
- `spdm-emu/library/spdm_transport_mctp_lib/` (libspdm 내부)
- `spdm-emu/library/spdm_transport_pcidoe_lib/` (libspdm 내부)
- `spdm-emu/library/spdm_transport_tcp_lib/` (libspdm 내부)

