# Transport Layer Example Template

이 디렉토리는 새로운 transport layer를 구현하기 위한 템플릿입니다.

## 구현해야 할 함수들

1. `spdm_example_get_sequence_number()` - 시퀀스 번호 처리
2. `spdm_example_get_max_random_number_count()` - 최대 랜덤 번호 카운트
3. `spdm_example_get_secured_spdm_version()` - 보안 메시지 버전
4. `spdm_transport_example_encode_message()` - 메시지 인코딩
5. `spdm_transport_example_decode_message()` - 메시지 디코딩

## 사용 방법

1. 이 디렉토리를 복사하여 새로운 transport layer 이름으로 변경
2. 모든 파일에서 "example"을 실제 transport layer 이름으로 교체
3. 함수들을 실제 transport layer 프로토콜에 맞게 구현
4. `CMakeLists.txt`에 새 라이브러리 추가

