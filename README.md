# Project Documentation System

프로젝트의 문제와 목표, 설계 기준, 기능 범위, 작업 순서, 결정 이력, 현재 작업 상태를 관리하는 문서 템플릿입니다. [문서 체계](docs/DocumentationSystem.md)에서 문서별 역할, 편집 방식, 이관 조건을 확인할 수 있습니다.

## 1. 스킬 없이 사용하는 방법

문서를 직접 복사해 사용하려면 아래 순서를 따릅니다. Codex로 문서 체계를 구축하려면 [3장](#3-codex에서-프로젝트별-설치)을 참고합니다.

1. 필요한 문서를 프로젝트 문서 폴더에 복사합니다. 여러 문서를 함께 복사할 때는 상대 링크가 유지되도록 폴더 구조를 유지합니다. 같은 경로에 있는 기존 파일은 건너뛰고, 같은 이름의 폴더는 재사용합니다. 파일·폴더 유형이 충돌하면 해당 경로를 기록하고 나머지 항목을 복사합니다.
2. 일러두기와 목차를 읽고, 해당 프로젝트의 내용으로 본문을 채웁니다.
3. 기존 문서나 이슈 트래커가 같은 역할을 맡고 있다면 해당 위치를 문서 지도에 연결합니다.
4. AI와 작업한다면 대상 프로젝트에 적용되는 `AGENTS.md` 등에 실제 문서 지도와 작성 가이드의 확인 조건·경로를 연결합니다. 연결할 내용은 [문서 체계 4.2절](docs/DocumentationSystem.md#42-작업-지침과-참조-경로-구성)을 참고합니다.

| 작업 | 사용할 문서 |
| --- | --- |
| 문제와 목표, 해결 방향, 요구사항·제약·제출 조건을 정한다 | [ProjectSpec.md](docs/ProjectSpec.md) |
| 기능 범위와 입력·출력을 정리한다 | [Systems.md](docs/Systems.md) |
| 필수 작업의 순서와 선행 작업·착수 조건을 정한다 | [DevPlan.md](docs/DevPlan.md) |
| 결정과 그 사유를 보존한다 | [개발 노트](docs/DevNotes/README.md) · [양식](docs/DevNotes/Template.md) |
| 다시 다룰 과제를 보존한다 | [Backlog.md](docs/Backlog.md) |
| 다음 세션에 현재 작업을 넘긴다 | [HANDOFF.md](docs/HANDOFF.md) |
| 세션별 논의·검토와 작업별 검증 계획·결과를 적는다 | [논의·검토 초안](docs/DiscussionDraft.md) |
| 문제의 조사 경로와 시행착오를 보존한다 | [트러블슈팅](docs/Troubleshooting/README.md) · [양식](docs/Troubleshooting/Template.md) |

## 2. 작성 규칙

- 문서를 편집할 때는 [WritingGuide.md](docs/WritingGuide.md)와 대상 문서의 일러두기를 확인합니다.
- 문서별 역할과 갱신 흐름은 [DocumentationSystem.md](docs/DocumentationSystem.md), 고유 운영 규칙은 각 문서의 일러두기나 기록 폴더의 README에서 확인합니다.
- [SKILL.md](SKILL.md)는 Codex가 대상 프로젝트에 전체 문서 양식을 복사하는 절차입니다. [AGENTS.md](AGENTS.md)는 이 저장소에서 적용하는 작업 지침입니다. 대상 프로젝트에서는 그 프로젝트에 적용되는 지침에 문서 안내를 연결합니다.

## 3. Codex에서 프로젝트별 설치

### 3.1 스킬 설치

기본 설치는 문서 체계 구축 스킬과 아래 두 추가 스킬을 함께 설치합니다. 추가 스킬의 사용은 필요한 작업에서 선택합니다.

| 설치 이름 | 용도 | 함께 복사할 파일 |
| --- | --- | --- |
| `project-documentation-system` | 전체 문서 양식 복사 | 루트 `SKILL.md`, `docs/` 전체 |
| `requirements-review` | 구현 전 해결 방향·계획을 근거 문서와 대조하고 질문으로 점검하는 초안 | `skills/requirements-review/` 전체와 그 안의 `LICENSE` |
| `security-audit` | Cloudflare의 소스 기반 보안 검토 | `skills/security-audit/` 전체와 그 안의 `LICENSE`, 보조 문서·검증 파일 |

**최초 설치**는 대상 프로젝트의 루트에서 아래 명령을 Bash로 실행합니다. Windows에서는 Git Bash를 사용합니다. 기본 경로는 Git과 GitHub 접근이 필요합니다.

로컬 수정본을 설치하려면 `source_dir=""`를 로컬 저장소의 절대 경로로 바꿉니다. Git Bash에서는 `/c/Users/digif/OneDrive/Desktop/크래프톤/project-documentation-system` 형식을 사용하며, 경로는 큰따옴표로 감쌉니다. 로컬 원본을 지정하면 GitHub에서 내려받지 않습니다.

```bash
(
set -eu
source_dir=""
selected_skills=(project-documentation-system requirements-review security-audit)

if [ -z "$source_dir" ]; then
  source_dir="$(mktemp -d)"
  git clone --depth 1 https://github.com/parkseongjun00/project-documentation-system.git "$source_dir"
fi

for skill in "${selected_skills[@]}"; do
  case "$skill" in
    project-documentation-system)
      test -f "$source_dir/SKILL.md"
      test -d "$source_dir/docs"
      ;;
    requirements-review|security-audit)
      test -f "$source_dir/skills/$skill/SKILL.md"
      test -f "$source_dir/skills/$skill/LICENSE"
      ;;
    *) printf '알 수 없는 스킬: %s\n' "$skill" >&2; exit 1 ;;
  esac
done

mkdir -p .agents/skills
for skill in "${selected_skills[@]}"; do
  target=".agents/skills/$skill"
  if [ -e "$target" ] || [ -L "$target" ]; then
    printf '기존 경로 보존, 설치 건너뜀: %s\n' "$target"
    continue
  fi
  mkdir "$target"
  if [ "$skill" = project-documentation-system ]; then
    cp -R "$source_dir/SKILL.md" "$source_dir/docs" "$target/"
  else
    cp -R "$source_dir/skills/$skill/." "$target/"
  fi
  printf '설치 완료: %s\n' "$target"
done
)
```

원본에 선택한 스킬의 필수 파일이 없으면 대상에 복사하기 전에 중단합니다. GitHub에서 내려받는 경로는 원격 저장소에 반영된 파일을 사용합니다. 커밋·푸시 전의 수정본과 새 파일은 로컬 원본으로 설치합니다.

같은 이름의 파일·폴더·심볼릭 링크가 있으면 **해당 스킬 전체를 건너뛰고** 다른 선택 스킬의 설치를 계속합니다. 기존 폴더에 새 파일을 섞거나 덮어쓰지 않습니다. `.agents/` 또는 `.agents/skills/`가 파일이어서 경로를 만들 수 없으면 중단합니다.

**갱신하거나 복사 실패 후 다시 설치할 때**는 해당 스킬 폴더를 `.agents/skills/` 밖으로 옮겨 보관한 뒤 같은 명령을 다시 실행합니다. 충돌 경로가 파일이나 링크라면 그 항목을 먼저 보관합니다. 기존 프로젝트 문서는 자동 갱신하지 않으며, 새 양식과 비교해 필요한 변경만 반영합니다.

---

### 3.2 문서 체계 구축

같은 프로젝트에서 새 Codex 세션을 열고 `$project-documentation-system 이 프로젝트에 문서 체계를 구축해줘.`라고 요청합니다. 스킬은 설치 경로의 `docs/` 전체를 대상 프로젝트의 `docs/`에 복사합니다. 같은 경로에 있는 기존 파일은 보존하고, 파일·폴더 유형 충돌은 경로와 이유를 보고합니다. 스킬 설치와 프로젝트 문서 복사는 별도 절차입니다. 구축 후에는 필요한 문서를 지정해 작성이나 갱신을 요청합니다.

구축 과정에서는 대상 프로젝트의 실제 문서 지도·WritingGuide 위치와 작업 지침의 연결도 확인합니다. 안내가 없으면 기존 지침을 보존하는 최소 추가안을 보고합니다. 문서 복사와 지속적인 AI 작업 지침 연결은 별도이며, 기본 설치 명령은 공통 `AGENTS.md`를 스킬 폴더에 복사하지 않습니다.

문서 참조 안내만 프로젝트 지침에 연결하는 방법과 공통 전역 지침 전체를 적용하는 방법은 구분합니다. 실제 지침 파일이나 설정 변경은 별도 요청에 따라 진행합니다. 추가 스킬만 설치했다면 문서 체계 구축 절차는 생략합니다.

## 4. 문서 체계 또는 추가 스킬만 선택 설치

3.1절의 명령에서 `selected_skills=(...)` 한 줄만 원하는 구성으로 바꿉니다. 설치 원본 지정, 기존 경로 보존과 갱신 방법은 동일합니다. 추가 스킬은 문서 체계 설치 여부와 관계없이 설치할 수 있습니다.

| 설치할 항목 | 바꿀 한 줄 |
| --- | --- |
| 문서 체계만 | `selected_skills=(project-documentation-system)` |
| 질문 검토만 | `selected_skills=(requirements-review)` |
| 보안 검토만 | `selected_skills=(security-audit)` |
| 추가 두 스킬만 | `selected_skills=(requirements-review security-audit)` |

설치 후 각 스킬은 대상 프로젝트의 `.agents/skills/<설치 이름>/`에 있습니다. 추가 스킬은 해당 폴더 전체를 복사하므로 원본의 상대 경로와 `LICENSE`가 함께 유지됩니다. 출처·원본 버전·개작 여부는 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)를, 원본 저작권 표시와 허가문은 [질문 검토 LICENSE](skills/requirements-review/LICENSE)와 [보안 검토 LICENSE](skills/security-audit/LICENSE)를 확인합니다.
