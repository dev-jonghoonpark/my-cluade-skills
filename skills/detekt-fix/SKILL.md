---
name: detekt-fix
description: Kotlin 정적 분석 도구 detekt를 실행하고 발견된 이슈를 분석하여 자동으로 수정합니다.
---

# Detekt 분석 및 자동 수정

Kotlin 프로젝트에서 detekt 정적 분석을 실행하고, 발견된 이슈를 분석하여 수정합니다.

## 실행 단계

### 1. Detekt 실행
```bash
./gradlew detekt 2>&1 || true
```

만약 특정 모듈만 분석하려면:
```bash
./gradlew :svc-membership:detekt 2>&1 || true
```

### 2. 결과 분석
detekt 출력에서 다음 정보를 추출합니다:
- **파일 경로**: 이슈가 발생한 파일
- **라인 번호**: 이슈 위치
- **룰 이름**: 위반한 detekt 규칙 (예: `MaxLineLength`, `LongMethod`, `MagicNumber`)
- **메시지**: 상세 설명

### 3. 이슈 분류 및 수정 전략

#### 자동 수정 가능한 이슈
| 룰 | 수정 방법 |
|-----|----------|
| `MaxLineLength` | 긴 줄을 적절히 분리 |
| `MagicNumber` | 상수로 추출 (companion object) |
| `WildcardImport` | 명시적 import로 변경 |
| `UnusedImports` | 미사용 import 제거 |
| `NewLineAtEndOfFile` | 파일 끝에 개행 추가 |
| `NoBlankLineBeforeRbrace` | 불필요한 빈 줄 제거 |
| `TrailingWhitespace` | 후행 공백 제거 |
| `UnnecessaryAbstractClass` | abstract 제거 또는 구조 변경 |
| `ReturnCount` | 조기 반환 패턴 또는 when 식으로 리팩토링 |
| `LongParameterList` | 파라미터 객체 패턴 적용 또는 @Suppress 추가 |
| `ComplexCondition` | 조건을 의미있는 변수로 추출 |
| `TooManyFunctions` | 클래스 분리 또는 @Suppress 추가 |

#### Suppress 어노테이션이 필요한 경우
- `LongMethod`: 로직상 분리가 어려운 경우
- `ComplexMethod`: 복잡도가 높지만 정당한 경우
- `ThrowsCount`: 다양한 예외 처리가 필요한 경우

### 4. 수정 원칙
1. **안전한 수정 우선**: 동작 변경 없이 코드 스타일만 수정
2. **컨텍스트 이해**: 해당 파일을 읽고 전체 맥락 파악 후 수정
3. **최소 변경**: 필요한 부분만 수정, 과도한 리팩토링 금지
4. **Suppress는 최후 수단**: 먼저 코드 수정 시도, 불가능할 때만 @Suppress 사용

### 5. 출력 포맷
수정 완료 후 다음 정보를 제공합니다:
- 발견된 총 이슈 수
- 자동 수정된 이슈 목록
- @Suppress가 추가된 이슈 목록
- 수동 검토가 필요한 이슈 목록
- 수정 후 detekt 재실행 결과

## 사용 예시

```
/detekt-fix                    # 전체 프로젝트 분석 및 수정
/detekt-fix svc-membership     # 특정 모듈만 분석 및 수정
/detekt-fix --check-only       # 분석만 수행 (수정 없음)
```

$ARGUMENTS
