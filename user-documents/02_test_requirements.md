# 테스트 시나리오/케이스 작성 가이드라인

본 문서는 `tests.json` 파일을 일관성 있고 체계적으로 작성하기 위한 가이드입니다.

## 1. 목적
- 개발된(또는 개발 예정인) 모든 기능에 대해 사용자 관점의 테스트 시나리오와 테스트 케이스를 명확히 정의한다.
- 요구사항과 테스트의 추적성을 확보하고, 실제 검증 가능한 결과를 명시하여 품질을 보장한다.

## 2. 파일 위치 및 명명
- 위치: `user-documents\test_specification\`
- 파일명: `tests.json`
   > 파일을 직접 수정하는 것 보다, *Cursor AI* 등을 활용하여 변경/추가된 기능에 대한 TS/TC를 자동 생성하는 것을 권장

## 3. 작성 원칙
- **기능 추가/변경 시 반드시 테스트 시나리오/케이스를 선행 작성**
- **각 케이스는 요구사항 ID와 연동**
- **입력, 사전조건, 기대결과는 실제 검증 가능하게 작성**
- **불필요한 중복/모호한 표현 지양**

## 4. 스키마 구조
```json
{
  "scenarios": [
    {
      "scenario_id": "TS_0001",
      "scenario_title": "시나리오명",
      "scenario_description": "시나리오 설명",
      "scenario_tags": ["tag1", "tag2"],
      "scenario_precondition": "시나리오 수준의 (모든 테스트케이스가 공유하는) 사전조건",
      "test_cases": [
        {
          "case_id": "TC_0001_01",
          "case_title": "테스트 케이스명",
          "case_requirementId": "BCK_FR_0001_01_01",
          "case_preconditions": ["사전조건1", "사전조건2"],
          "case_inputs": [
            { "input_type": "사용자 이벤트|데이터|자동", "input_desc": "입력 설명", "input_value": "값" }
          ],
          "expected_output": {
            "status_code": 201,
            "results": "검증가능한 형태의 예상 결과"
          }
        }
      ],
      "scenario_creationDateTime": "시나리오 생성 일시",
      "scenario_lastUpdateDateTime": "시나리오 최종 업데이트 일시"
    }
  ]
}
```

## 5. 각 필드 작성법
- **scenario_id**: 시나리오 고유 식별자 (예: TS_0001)
- **scenario_title**: 시나리오의 목적이 한눈에 드러나도록 간결하게 작성
- **scenario_description**: 시나리오의 전체 맥락/목적을 명확히 기술
- **scenario_tags**: 시나리오를 분류할 수 있는 태그 배열 (예: ["로그인", "에러처리"])
- **scenario_precondition**: 시나리오에 포함된 모든 테스트케이스가 공통적으로 만족해야 하는 사전조건. 반복되는 케이스별 사전조건은 이곳에 작성하고, 개별 케이스에 특이사항이 있으면 case_preconditions에 별도 작성
- **scenario_creationDateTime**: 시나리오 최초 작성 일시 (ISO 8601 형식 권장)
- **scenario_lastUpdateDateTime**: 시나리오 최종 수정 일시 (ISO 8601 형식 권장)
- **test_cases**: 해당 시나리오에 포함된 테스트 케이스 배열
  - **case_id**: 테스트 케이스 고유 식별자 (예: TC_0001_01)
  - **case_title**: 테스트 케이스의 목적을 간결하게 작성
  - **case_requirementId**: 요구사항 명세서의 ID와 정확히 매칭
  - **case_preconditions**: 테스트 전 반드시 만족해야 하는 조건을 구체적으로 나열 (배열, 시나리오 공통 사전조건 외 개별 케이스 특이사항)
  - **case_inputs**: 실제 입력/이벤트/데이터를 구체적으로 작성 (배열)
    - **input_type**: 입력 유형 (예: 사용자 이벤트, 데이터, 자동)
    - **input_desc**: 입력에 대한 설명
    - **input_value**: 실제 입력 값
  - **expected_output**: 실제로 검증 가능한 결과를 명확히 작성 (객체)
    - **status_code**: HTTP 응답 코드 등 상태값 (필요시)
    - **results**: 검증 가능한 형태의 예상 결과 (UI 변화, 데이터 상태 등)

## 6. 예시
```json
{
  "scenarios": [
    {
      "scenario_id": "TS_0001",
      "scenario_title": "정적 파일 서빙 시나리오",
      "scenario_description": "사용자가 브라우저에서 서비스에 접속하여 index.html 및 정적 리소스를 정상적으로 받아볼 수 있다.",
      "scenario_tags": ["정적파일", "서빙", "접근성"],
      "scenario_precondition": "서버가 실행 중이어야 하며, public/index.html 파일이 존재해야 한다.",
      "test_cases": [
        {
          "case_id": "TC_0001_01",
          "case_title": "index.html 정상 로드",
          "case_requirementId": "BCK_FR_0001_01_01",
          "case_preconditions": [],
          "case_inputs": [
            { "input_type": "사용자 이벤트", "input_desc": "브라우저에서 서비스 메인 URL 접속", "input_value": "http://localhost:3000/" }
          ],
          "expected_output": {
            "status_code": 200,
            "results": "브라우저에 index.html의 내용이 정상적으로 렌더링된다. (주요 UI 요소 확인)"
          }
        }
      ],
      "scenario_creationDateTime": "2024-06-01T10:00:00+09:00",
      "scenario_lastUpdateDateTime": "2024-06-01T10:00:00+09:00"
    }
  ]
}
```

## 7. 주의사항 및 권장사항
- **테스트 케이스는 실제로 검증 가능한 결과만 작성** (ex. "정상 동작한다" → X, "HTTP 200, UI 요소 확인" → O)
- **입력값/사전조건/기대결과는 구체적으로 작성**
- **요구사항 변경 시 테스트 시나리오도 반드시 갱신**
- **자동화 테스트를 염두에 두고 작성하면 더욱 좋음**

---
이 가이드에 따라 test_scenarios.json을 관리하면, 개발-테스트-품질보증의 선순환이 가능합니다. 