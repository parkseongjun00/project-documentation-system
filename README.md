# Project Documentation System

프로젝트의 문제와 목표, 설계 기준, 기능 범위, 작업 순서, 결정 이력, 현재 작업 상태를 관리하는 문서 템플릿입니다. [문서 체계](docs/DocSystem.md)에서 문서별 역할, 편집 방식, 이관 조건을 확인할 수 있습니다.

## 1. 사용 방법

1. 필요한 문서를 프로젝트 문서 폴더에 복사합니다. 여러 문서를 함께 복사할 때는 상대 링크가 유지되도록 폴더 구조를 유지합니다.
2. 일러두기와 목차를 읽고, 해당 프로젝트의 내용으로 본문을 채웁니다.
3. 기존 문서나 이슈 트래커가 같은 역할을 맡고 있다면 해당 위치를 문서 지도에 연결합니다.

| 작업 | 사용할 문서 |
|---|---|
| 문제와 목표, 해결 방향, 동작 규칙과 제약을 정한다 | [ProjectSpec.md](docs/ProjectSpec.md) |
| 구현 범위를 정리한다 | [Systems.md](docs/Systems.md) |
| 작업 묶음별 구현·확장 순서를 정한다 | [DevPlan.md](docs/DevPlan.md) |
| 결정과 그 사유를 보존한다 | [개발 노트](docs/DevNotes/README.md) · [양식](docs/DevNotes/Template.md) |
| 다시 다룰 과제를 보존한다 | [Backlog.md](docs/Backlog.md) |
| 다음 세션에 현재 작업을 넘긴다 | [HANDOFF.md](docs/HANDOFF.md) |
| 세션별 논의·검토 내용을 적는다 | [논의 초안](docs/DiscussionDrafts/README.md) · [양식](docs/DiscussionDrafts/Template.md) |
| 문제의 조사 경로와 시행착오를 보존한다 | [트러블슈팅](docs/Troubleshooting/README.md) · [양식](docs/Troubleshooting/Template.md) |

## 2. 작성 규칙

- 문서를 편집할 때는 [WritingGuide.md](docs/WritingGuide.md)와 대상 문서의 일러두기를 확인합니다.
- 병행 세션은 각자 [논의 초안 양식](docs/DiscussionDrafts/Template.md)을 복사해 자기 파일을 갱신합니다.
- [SKILL.md](SKILL.md)는 Codex가 사용자 설명과 기존 자료를 바탕으로 실제 프로젝트 문서를 작성할 때 사용하는 절차입니다. [AGENTS.md](AGENTS.md)는 이 저장소에서 적용하는 작업 지침입니다.

## 3. Codex에서 프로젝트별 설치

대상 프로젝트의 루트에서 아래 블록을 Bash에 붙여넣습니다. Git과 GitHub 접근이 필요합니다.

```bash
src=$(mktemp -d) &&
git clone --depth 1 https://github.com/parkseongjun00/project-documentation-system.git "$src" &&
mkdir -p .agents/skills &&
mkdir .agents/skills/project-documentation-system &&
cp -R "$src/SKILL.md" "$src/docs" .agents/skills/project-documentation-system/
```

같은 프로젝트에서 새 Codex 세션을 열고 `$project-documentation-system 현재 프로젝트에 문서 체계를 도입해줘.`라고 요청합니다.
