## 단계 1: Git 버전 관리 소개

프로젝트를 진행하면서 백업을 정리하기가 점점 어려워졌습니다. 게다가 모두가 업데이트를 다른 방식으로 공유하기 때문에 협업도 매우 혼란스럽습니다.

빠르게 검색한 결과 [Git](https://git-scm.com/)에 대해 알게 되었습니다. Git을 사용하면 변경 사항을 추적하고 다른 사람들과 쉽게 협업할 수 있다고 합니다. 파일 이름 규칙, 공유 드라이브, 이메일로 파일 복사본을 주고받는 등 기존의 혼란스러운 방식을 없애줍니다.

> [!IMPORTANT]
> 이 실습은 Git이 이미 설치된 환경에서 Git 사용법을 가르칩니다.
> 자신의 컴퓨터에 설치하려면 다양한 컴퓨터 환경에 맞는 설치 가이드가 있는 공식 [Git 사이트](https://git-scm.com)를 권장합니다.

### 📖 이론: 버전 관리란 무엇인가?

버전 관리 시스템은 개발자가 시간이 지남에 따라 코드 변경을 관리할 때 겪는 일반적인 문제를 해결합니다. 예를 들면:

- 백업 및 복구
- 격리된 실험 환경
- 병렬 개발
- 잠긴 파일
- 파일 중복
- 충돌하는 변경 사항
- 팀 협업

아래 상황을 경험해 본 적이 있다면, Git 버전 관리가 마음에 들 것입니다! 😎

- `my-project-final-v2-really3.zip`
- "언제 작동이 멈춘 거지? 나는 아무것도 안 바꿨는데!" (하지만 바꿨다는 걸 알고 있습니다)
- "파일이 잠겨 있어요. 월요일에 돌아올 때까지 복사본으로 작업할게요."
- "v2가 어떤 이메일에 있었지? 지난 수요일 것인 것 같은데."

### "Git" 버전 관리란 무엇인가?

Git은 [분산 버전 관리 시스템](https://en.wikipedia.org/wiki/Distributed_version_control)으로, 각 개발자가 프로젝트 히스토리의 완전한 복사본을 가지고 있습니다. 이는 공유 위치에 하나의 복사본만 있는 중앙 집중식 시스템과 다릅니다.

이러한 방식은 다음과 같은 장점을 제공합니다:

- 오프라인 작업 - 대부분의 작업이 로컬에서 처리됩니다.
- 향상된 안정성 - 분산된 복사본이 백업 역할을 합니다.
- 유연한 워크플로우 - 개발자가 자신만의 프로세스와 도구를 사용할 수 있습니다.

### Git은 어떻게 사용하나요?

Git은 개발자를 위해 개발자가 만든 [오픈 소스](https://en.wikipedia.org/wiki/Open_source) 도구입니다. 이에 따라 커뮤니티가 대부분의 필요를 충족하는 기능을 지속적으로 개발해 왔습니다.

예를 들어, 커뮤니티는 거의 모든 개발 워크플로우에 Git을 통합했습니다. 몇 가지 예시입니다:

- **커맨드 라인 인터페이스(CLI)** - 모든 기능의 원천이자 가장 강력한 도구입니다.
- **코드 에디터** - 즐겨 사용하는 코딩 에디터/도구와 함께 사용. 예시:
  - Visual Studio Code
  - JetBrains IDEs
  - Xcode
  - Emacs/VIM
- **호스팅 서비스** - 중앙 집중식 Git 호스트, 웹 브라우저를 통한 온라인 편집 지원. 예시:
  - GitHub
  - GitLab
  - Gitea
  - Azure DevOps
  - AWS CodeCommit
  - BitBucket
- **데스크톱 애플리케이션** - 친숙한 그래픽 인터페이스. 예시:
  - GitHub Desktop
  - Sourcetree
  - TortoiseGit
  - GitKraken
  - Git Butler
  - 더 많은 도구: https://git-scm.com/tools/guis

### ⌨️ 활동: 샘플 프로젝트 열기

Git 연습을 시작하기 위해, 먼저 사전 설정된 개발 환경을 열고 샘플 프로젝트를 살펴봅시다.

1. 아래 버튼을 마우스 오른쪽 클릭하여 새 탭에서 **Codespace 만들기** 페이지를 엽니다. 기본 설정을 사용하세요.

   [![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/{{full_repo_name}}?quickstart=1)

   > 🪧 **참고**: 일반적으로 [GitHub Codespace](https://github.com/features/codespaces)는 저장소 코드와 모든 필수 설정을 자동으로 포함합니다. 이 실습은 처음부터 연습할 수 있도록 수정된 환경입니다.

1. **Repository** 필드가 원본이 아닌 본인의 실습 복사본인지 확인한 후 녹색 **Create Codespace** 버튼을 클릭합니다.

   - ✅ 본인 것: `/{{full_repo_name}}`
   - ❌ 원본: `/skills-kr/introduction-to-git`

1. 브라우저에서 Visual Studio Code가 로드될 때까지 잠시 기다립니다.

1. 왼쪽 탐색 탭에서 **파일 탐색기(File Explorer)**를 선택하여 파일을 표시합니다. `src/index.html`을 마우스 오른쪽 클릭하고 **Show Preview**를 선택하여 샘플 게임을 확인합니다.

   > ❗️ **주의**: 아무것도 변경하지 마세요!
   > 아직 버전 관리를 추가하지 않았습니다! 😱

   <img width="350px" src="https://github.com/user-attachments/assets/c5f60f24-27fb-4670-ab0a-c00aa723672c"/><br/>

   <img width="500px" src="https://github.com/user-attachments/assets/a20529f3-8e42-464b-8d84-b0880dd14383"/>

> [!TIP]
> 변경 사항을 적용하면서 게임을 열어 두고 계속 플레이해 보세요! 🧑‍🚀

### ⌨️ 활동 2: CLI에서 Git 사용하기

커맨드 라인 인터페이스(CLI)에서 Git을 사용해 봅시다. CLI는 모든 Git 기능의 원천이자 가장 강력한 옵션입니다.

1. 통합 터미널이 아직 열려 있지 않다면 `Ctrl+Shift+P`를 누르고 `View: Toggle Terminal`을 검색하여 선택합니다.

   <img width="500px" src="https://github.com/user-attachments/assets/4bbf918a-f87c-4875-b7fd-61d8b16a70e1"/>

1. 현재 설치된 Git 버전을 확인하여 Git이 설치되어 있는지 검증합니다.

   ```bash
   git --version
   ```

   <img width="500px" src="https://github.com/user-attachments/assets/0e09991b-829f-4028-b951-87bc5fa47bfc"/>

1. Git 도움말 문서를 확인합니다.

   ```bash
   git --help
   ```

   <img width="500px" src="https://github.com/user-attachments/assets/c447adf3-9cc1-4106-9a49-f2bf705d396c"/>

### ⌨️ 활동 3: Git 사용자 정보 설정

게임의 버전 관리를 시작하기 전에, Git에 사용자 정보를 제공하여 변경 사항의 작성자로 연결할 수 있도록 합시다.

> [!WARNING]
> Git은 작성자의 이름과 이메일을 히스토리에 저장하며, 저장소에 접근 권한이 있는 누구나 볼 수 있습니다. GitHub는 계정 [이메일 설정](https://github.com/settings/emails)에서 활성화할 수 있는 선택적 [noreply 이메일 주소](https://docs.github.com/en/account-and-profile/reference/email-addresses-reference#your-noreply-email-address)를 제공합니다.

1. 표시 이름을 설정합니다.

   ⚠️ `First`와 `Last`를 본인의 이름으로 바꾸는 것을 잊지 마세요!

   ```bash
   git config --global user.name "First Last"
   ```

1. 이메일 주소를 설정합니다. 추가적인 개인정보 보호를 위해, 계정 [이메일 설정](https://github.com/settings/emails)에서 noreply 주소를 활성화하는 것을 고려하세요.

   ⚠️ `me@example.com`을 본인의 이메일로 바꾸는 것을 잊지 마세요!

   ```bash
   git config --global user.email "me@example.com"
   ```

1. 설정을 확인합니다.

   ```bash
   git config --global --list
   ```

   <img width="500px" src="https://github.com/user-attachments/assets/62688039-3601-4a23-8f61-408210faff0a"/>

1. 사용자 정보가 설정되면, Mona가 이미 여러분의 작업을 확인하고 있을 것입니다. 잠시 기다리며 댓글을 확인하세요. 진행 상황과 다음 단계가 표시됩니다.

> [!TIP]
> 여러 계정을 사용하는 경우, 프로젝트별로 사용자 이름과 이메일을 변경할 수도 있습니다. **기존** 프로젝트 저장소에서는 `--global` 대신 `--local`을 사용하세요.

<details>
<summary>문제가 있나요? 🤷</summary><br/>

- "First Last"와 "me@example.com"을 실제 본인의 정보로 교체했는지 확인하세요.

</details>
