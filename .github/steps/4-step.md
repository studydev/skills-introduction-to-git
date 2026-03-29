## 단계 4: 변경 사항 비교하기

"되돌리기" 방법을 이해했으니, 이제 실제로 게임을 변경해 봅시다! 그리고 더 중요한 것은, Git이 저장소 히스토리에 커밋하기 **전에** 무엇이 변경되었는지 보여주는 방법을 배우는 것입니다.

파일 차이를 이해하는 것은 작업을 검토하고 오류를 발견하는 데 매우 중요합니다!

### 📖 이론: Diff 이해하기

Git은 기호와 색상을 사용하여 파일 변경 사항을 보여줍니다:

- `+` 녹색은 추가된 줄을 나타냅니다
- `-` 빨간색은 삭제된 줄을 나타냅니다

예시:

```diff
+ 이것은 추가된 줄입니다
- 이것은 삭제된 줄입니다
```

> [!TIP]
> 아래 명령어로 Git의 기본 비교 색상을 변경할 수 있습니다.
>
> ```bash
> git config --global color.diff.old yellow
> git config --global color.diff.new blue
> ```

### 중요한 Git 명령어는 무엇인가요?

`git diff` 명령어는 개발 상태 간의 차이를 보여줍니다.

- `git diff` - 작업 디렉토리와 스테이징 영역 간의 차이
- `git diff --staged` - 스테이징 영역과 이전 커밋 간의 차이
- `git diff HEAD~1` - 현재 커밋과 이전 커밋 간의 차이

### ⌨️ 활동 1: 차이점 보기 (CLI 사용)

게임을 수정한 다음 CLI를 사용하여 차이점을 확인해 봅시다.

1. `src/index.html`을 엽니다.

1. `20번째 줄`에서 점수 표시 관련 `info-section` 영역을 아래 예시로 교체합니다.

   ```txt
   <div class="info-section">
      <h3>Current Score</h3>
      <div class="score" id="score">0</div>
      <h3>High Score</h3>
      <div class="high-score" id="high-score">0</div>
   </div>
   ```

   이렇게 하면 3가지 종류의 변경 사항이 시연됩니다:

   - `Score` 라벨을 `Current Score`로 수정
   - `High Score` 정보 추가
   - `status` 정보 삭제

1. 작업 디렉토리와 마지막 커밋 사이의 차이를 봅니다.

   ```bash
   git diff src/index.html
   ```

   <img width="500px" src="https://github.com/user-attachments/assets/f41d6917-1651-4549-bb7b-5441a1832e38"/>

1. 변경 사항을 스테이징 영역으로 올립니다.

   ```bash
   git add src/index.html
   ```

1. 같은 비교를 다시 실행합니다. 작업 디렉토리가 이제 스테이징 영역과 일치하기 때문에 변경 사항이 표시되지 않습니다.

   ```bash
   git diff src/index.html
   ```

1. 스테이징 영역과 마지막 커밋 간의 차이를 봅니다.

   ```bash
   git diff --staged src/index.html
   ```

   <img width="500px" src="https://github.com/user-attachments/assets/f6aad38c-56fa-49ed-8209-9fe249c209ff"/>

1. 다음 메시지로 변경 사항을 커밋합니다.

   ```md
   git commit -m "Add element for showing high score"
   ```

   <img width="500px" src="https://github.com/user-attachments/assets/8381b943-ca22-4b22-97b5-4520e174fc4c"/>

### ⌨️ 활동 2: 차이점 보기 (VS Code 사용)

게임을 좀 더 수정한 다음 VS Code를 사용하여 차이점을 확인해 봅시다.

1. `src/patterns.js`를 엽니다.

1. `3번째 줄`에서 `Null Pointer` 영역을 아래 예시로 교체하여 패턴을 변경합니다.

   ```txt
   {
     name: "Null Pointer",
     pattern: [
       [0, 1, 1, 1, 0],
       [0, 1, 0, 1, 0],
       [0, 1, 1, 1, 0],
       [0, 0, 1, 0, 0],
       [0, 0, 1, 0, 0],
     ],
   },
   ```

1. **파일 탐색기**에서 파일명 `patterns.js`의 색상이 변경되고 `M`이 표시되어 수정되었음을 나타냅니다.

   <img width="350px" src="https://github.com/user-attachments/assets/93a8f34c-9b16-4783-bc46-81532cdeffdf"/>

1. **Source Control** 탭을 엽니다. **Changes** 목록에서 `patterns.js` 파일을 더블 클릭하여 Diff(비교) 뷰를 엽니다.

   <img width="350px" src="https://github.com/user-attachments/assets/4dce9e42-caca-4c6e-a6fe-8d83d58cd06d"/><br/>

   <img width="500px" src="https://github.com/user-attachments/assets/4c410689-2a53-462f-9200-79d21bddbf2c"/>

   > 💡 **팁**: 비교 뷰에서 내용을 수정하면 실시간으로 피드백을 받을 수 있습니다!

1. 파일을 **스테이징** 영역으로 올립니다. ⚠️ 아직 커밋하지 마세요!

   현재 파일이 스테이징 영역과 일치하기 때문에 비교 뷰에서 변경 사항이 사라진 것을 확인합니다.

   <img width="500px" src="https://github.com/user-attachments/assets/b1274ece-2b03-42d2-88e8-9f3aaaa8f2c5"/>

1. **Staged Changes** 목록에서 `patterns.js` 파일을 더블 클릭하여 Diff(비교) 뷰를 엽니다.

   스테이징 영역은 커밋을 위해 잠겨 있으므로 이제 변경할 수 없습니다.

   <img width="350px" src="https://github.com/user-attachments/assets/da306727-49f1-4f73-9f38-3a0e5d406cef"/><br/>

   <img width="500px" src="https://github.com/user-attachments/assets/de1448eb-d0dd-4ec5-89a2-74fb4aa1cf5f"/>

1. 다음 메시지로 변경 사항을 커밋합니다.

   ```txt
   Make null pointer pattern easier to complete
   ```

1. 새로운 커밋이 저장소에 추가되면, Mona가 이미 여러분의 작업을 확인하고 있을 것입니다. 잠시 기다리며 댓글을 확인하세요. 진행 상황과 다음 단계가 표시됩니다.

<details>
<summary>문제가 있나요? 🤷</summary><br/>

- 변경 목록이 한 화면보다 길면 `q`를 눌러 스크롤 뷰어를 종료할 수 있습니다.

</details>
