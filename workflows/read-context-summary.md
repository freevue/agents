---
description: 'create-context-summary' Workflow를 이용하여 만든 'HISTORY.md'를 읽어 다음 작업을 이어갈 수 있게 해줍니다.
---

# Read Context Summary

당신의 역할은 `Global Rule`에 명시해두었습니다. 해당 역할을 사용하여 다음을 수행하세요.

입력받은 파일을 읽어 다음의 작업을 이어갑니다.

## Stpes

1. `list_dir` 기능을 사용하여 해당 프로젝트 `root`경로에서 `HISTORY.md`파일을 찾습니다.
2. 만약 파일이 없다면, `현재 진행된 작업내용이 없습니다.`를 출력합니다.
3. 파일을 찾았다면, `view_file`을 이용해 해당 내용을 불러옵니다.
4. 불러온 내용을 이해하고, 사용자의 다음 요청을 이어갑니다.
