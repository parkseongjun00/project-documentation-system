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

대상 프로젝트의 루트 폴더를 터미널에서 열고 아래 블록 전체를 붙여넣습니다. Git과 GitHub 접근이 필요합니다. Linux의 Bash 또는 Windows의 Git Bash에서 실행합니다.

```bash
(
  set -eu
  skill_dir=.agents/skills/project-documentation-system

  if [ -e "$skill_dir" ] || [ -L "$skill_dir" ]; then
    printf '%s\n' "Already exists: $skill_dir" >&2
    exit 1
  fi

  mkdir -p .agents/skills
  work_dir=$(mktemp -d "$PWD/.agents/.project-documentation-system.XXXXXX")
  case "$work_dir" in
    "$PWD"/.agents/.project-documentation-system.*) ;;
    *) exit 1 ;;
  esac
  trap 'rm -rf -- "$work_dir"' EXIT

  git clone --depth 1 https://github.com/parkseongjun00/project-documentation-system.git "$work_dir/source"
  mkdir "$work_dir/skill"
  cp "$work_dir/source/SKILL.md" "$work_dir/skill/"
  cp -R "$work_dir/source/docs" "$work_dir/skill/"
  mv -nT -- "$work_dir/skill" "$skill_dir"
  if [ -d "$work_dir/skill" ]; then
    printf '%s\n' "Already exists: $skill_dir" >&2
    exit 1
  fi

  printf '%s\n' "Installed: $skill_dir"
)
```

설치 후 같은 프로젝트 폴더에서 Codex를 시작합니다. 터미널에서 시작하려면 `codex`를 실행합니다. Codex가 이미 열려 있다면 같은 프로젝트에서 새 세션을 열고 다음과 같이 요청합니다.

```text
$project-documentation-system 현재 프로젝트의 기존 문서를 확인하고 문서 체계를 도입해줘.
```

설치 블록은 스킬과 참조용 문서를 `.agents/skills/project-documentation-system/`에 넣습니다. 같은 이름의 폴더가 있으면 기존 설치를 보존합니다. 실제 프로젝트 문서의 이식은 스킬을 호출할 때 진행합니다.
