# Test Case Extensions

이 디렉토리는 spdm-emu의 테스트 케이스를 확장하는 코드를 포함합니다.

## 구조

- `requester/` - Requester 테스트 케이스 확장
- `responder/` - Responder 테스트 케이스 확장
- `common/` - 공통 테스트 유틸리티

## 사용 방법

새로운 테스트 케이스를 추가하려면:

1. 적절한 디렉토리에 새 테스트 파일 생성
2. `CMakeLists.txt`에 테스트 케이스 추가
3. spdm-emu의 테스트 프레임워크와 통합

