시니어 소프트웨어 개발자 관점에서 커밋을 진행해줘.
아래 **Prefix Rule**과 **Template** 규칙을 준수하여 **Steps**을 진행해줘.

**[Steps]**

1. `git diff --cached`를 실행하여, 현재 스테이징에 올라간 파일을 기준으로 분석.
2. 분석한 내용을 기준으로 **Message**를 생성
3. `gie commit -m "{message}"`를 실행하여 커밋
4. 커밋이 완료되면, 메시지만 Markdown으로 감싸서 출력

**[Prefix Rule]**

- new: 새로운 프로젝트 생성 및 개념 추가
- feat: 새로운 기능 개발 및 추가
- fix: 버그 픽스 관련 작업
- refactor: 기능 개선 및 파일 정리

**[Templage]**

```markdown
[{prefix}]: {commit 제목}

{Commit Message Body}
```

** 메시지 생성시 주의할 점 **

- 전문적인 용어의 경우 영문을 작성하여도 되지만, 전체적인 문법과 문맥의 경우 한글로 작성할 것.
- 제목의 경우 간결하게 작성할 것.
- Body의 경우 목록으로 작성하며, 목록 아이템은 한문장으로 종결할 것.
- Body 목록의 경우 제한이 없지만, 가독성을 고려하여 최소한으로 작성할 것.
