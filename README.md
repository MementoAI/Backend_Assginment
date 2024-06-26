## 과제: URL 단축 서비스 구현

### 개요
URL 단축 서비스는 긴 URL을 짧게 단축하여 사용하고, 단축된 URL을 통해 원본 URL로 리디렉션하는 기능을 제공합니다.

### 요구사항
**1. 필수 기능**
- **단축 URL 생성**
  - `POST /shorten`: 입력받은 긴 URL을 고유한 단축 키로 변환하고 데이터베이스에 저장.
  - 요청 본문: `{"url": "<original_url>"}`
  - 응답 본문: `{"short_url": "<shortened_url>"}`
  - **알고리즘 요구사항**:
    - 단축 키는 고유해야 하며, 중복되지 않는 키 생성.
    - 키 생성 알고리즘은 자유롭게 구현할 수 있으나 보안성과 효율성을 고려해야 함.
  
- **원본 URL 리디렉션**
  - `GET /<short_key>`: 단축된 키를 통해 원본 URL로 리디렉션.
  - 응답:
    - 키가 존재하면 301 상태 코드로 원본 URL로 리디렉션.
    - 키가 존재하지 않으면 404 상태 코드로 오류 메시지 반환.

**2. 추가 요구사항**
- **데이터베이스**: 원본 URL과 단축 키 매핑을 저장하기 위한 데이터베이스 사용. (여러 개의 데이터베이스를 혼합적으로 사용해도 됨)
  - SQLite, PostgreSQL, MongoDB, Redis 등 자유롭게 선택 가능.
  - 단, 확장성과 애플리케이션의 특성, 관리의 용이성을 종합적으로 고려해서 가장 적절한 데이터베이스(들)를 선택하여야 하고, 그 사유를 간략히 과제 제출 시 기재. 유저의 수가 많아질 수 있음을 반드시 고려해서 DB 스택을 설계해야함.
- **문서화**: 작성한 API에 대한 Swagger 문서 생성.

### 보너스 기능 (각 기능 구현 시 가산점)
**1. URL 키 만료 기능**
- 키 생성 시 만료 기간을 지정할 수 있으며, 만료된 키는 삭제 처리.
- `POST /shorten`: 요청 본문에 만료 기간을 선택적으로 추가할 수 있어야 함.

**2. 통계 기능**
- 각 단축 키의 조회 수를 추적하고 이를 반환하는 통계 엔드포인트 추가.
- `GET /stats/<short_key>`: 해당 키의 조회 수 반환.

**3. 테스트 코드**
- 단위 테스트 및 통합 테스트 코드 포함.

### 개발 및 제출 가이드라인
**1. 기술 스택**
- FastAPI를 활용해 백엔드 서버 구현
- 데이터베이스는 SQLite, PostgreSQL, MongoDB 등, 자유로이 선택 (단, 선택 이유를 README.md에 기술해야함)
- 구현에 필요한 라이브러리는 자유로이 선택 후 사용 가능
  

**2. 제출 형태**
- 깃허브 리포지토리를 생성 후 업로드하여 URL 제출
- README.md에 프로젝트에 대한 설명 및 설치, 실행 방법 작성

**3. 제출 기한**
- 과제 부여 후 5일 후 자정까지
- 예) 5/10 과제가 부여된 경우, 5/15 자정까지 제출


