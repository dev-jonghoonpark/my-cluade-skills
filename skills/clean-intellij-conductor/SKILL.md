---
name: clean-intellij-conductor
description: IntelliJ IDEA의 최근 프로젝트 목록에서 conductor로 생성된 모든 프로젝트를 제거합니다.
---

# Clean IntelliJ Conductor Projects

IntelliJ IDEA의 `recentProjects.xml` 파일에서 conductor workspace로 생성된 프로젝트 항목들을 모두 제거합니다.

## 작업 절차

1. **IntelliJ 실행 상태 확인**
   - 다음 명령어로 IntelliJ가 실행 중인지 확인합니다:
     ```bash
     pgrep -f "IntelliJIdea"
     ```
   - **IntelliJ가 실행 중이면:**
     - 사용자에게 IntelliJ가 실행 중임을 알리고 종료해야 함을 명확히 안내합니다.
     - 5초마다 반복해서 체크하는 루프를 시작합니다.
     - 종료가 확인될 때까지 기다립니다.
     - 예시 메시지: "⚠️  IntelliJ IDEA가 실행 중입니다. 작업을 진행하려면 IntelliJ를 완전히 종료해주세요. (5초마다 확인 중...)"
   - IntelliJ가 종료되면 다음 단계로 진행합니다.

2. **최신 IntelliJ 버전 찾기**
   - 다음 명령어로 설치된 IntelliJ 버전들을 확인합니다:
     ```bash
     ls -d ~/Library/Application\ Support/JetBrains/IntelliJIdea* 2>/dev/null | sort -V | tail -1
     ```
   - 버전 번호가 가장 높은 디렉토리를 사용합니다.
   - 파일 경로: `{찾은_디렉토리}/options/recentProjects.xml`

3. **Conductor 프로젝트 식별**
   - `$USER_HOME$/conductor/workspaces/` 경로를 포함하는 `<entry>` 요소들을 찾습니다.
   - 제거 대상 프로젝트 목록을 사용자에게 보여줍니다.

4. **사용자 확인**
   - 제거할 프로젝트 목록을 보여주고 진행 여부를 확인합니다.

5. **프로젝트 제거**
   - 해당 `<entry>` 요소들을 XML에서 제거합니다.
   - `lastOpenedProject`, `lastProjectLocation` 값도 conductor 경로인 경우 초기화합니다.

6. **결과 보고**
   - 제거된 프로젝트 개수를 보고합니다.
   - IntelliJ를 재시작하라는 안내를 제공합니다.

## 주의사항
- IntelliJ IDEA가 실행 중이면 변경사항이 덮어씌워질 수 있습니다.
- 스킬이 자동으로 IntelliJ 실행 상태를 확인하고, 실행 중이면 종료를 기다립니다.
- 작업 전 원본 파일을 백업합니다.

$ARGUMENTS
