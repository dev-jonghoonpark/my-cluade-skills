---
name: generate-test-code
description: 커밋되지 않은 변경사항(git diff)을 분석하여 단위/통합 테스트 코드를 작성합니다. 테스트 커버리지를 극대화하고 SOTA급 테스트 패턴을 적용합니다.
agent: Plan
---

# Generate SOTA Test Code

현재 작업 디렉토리의 커밋되지 않은 변경사항(`git diff`)을 분석하여 다음 기준에 따라 테스트 코드를 생성하세요.

## 1. 분석 단계
- `git diff`를 실행하여 변경된 로직과 새로 추가된 함수/클래스를 식별합니다.
- 기존 테스트 파일이 있다면 해당 파일의 스타일과 프레임워크(Jest, Pytest, Go test 등)를 파악합니다.

## 2. 테스트 작성 원칙 (SOTA Standard)
- **Triple-A 패턴**: Arrange(준비), Act(실행), Assert(검증) 구조를 엄격히 준수합니다.
- **포괄적 커버리지**:
    - Happy Path (정상 케이스)
    - Edge Cases (null, empty, max/min values 등)
    - Error Handling (예외 발생 및 처리 검증)
- **단위 테스트**: 외부 의존성(DB, API)은 Mock/Stub 처리하여 격리된 로직을 검증합니다.
- **통합 테스트**: 컴포넌트 간의 상호작용 및 실제 흐름을 검증하는 케이스를 최소 1개 이상 포함합니다.

## 3. 출력 포맷
- 변경 사항이 반영된 **전체 테스트 코드**를 제공합니다.
- 테스트가 커버하는 구체적인 시나리오를 리스트로 요약합니다.
- 기존 테스트 파일에 추가해야 할지, 새 파일을 만들어야 할지 가이드를 제공합니다.

$ARGUMENTS
