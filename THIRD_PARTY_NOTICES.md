# 외부 스킬 출처와 라이선스

## 1. 적용 범위

| 보관 경로 | 원본과 버전 | 반영 방식 | 라이선스 |
| --- | --- | --- | --- |
| `skills/requirements-review/` | Matt Pocock의 `grilling`, `5863806dd4e15c63174bee4e7515a4256792ecfa` | 구현 전 해결 방향·계획 점검과 근거 문서 대조, 사용자 주도 질문 검토에 맞춰 개작 | MIT, Copyright (c) 2026 Matt Pocock |
| `skills/security-audit/` | Cloudflare의 `security-audit-skill`, `c1c8a8c1471069fb0e188eeaff69b8e8db6564a8` | 원본 `skills/security-audit/` 전체를 내용과 상대 경로 그대로 복사하고 저장소 루트의 LICENSE를 함께 보관 | MIT, Copyright (c) 2025-2026 Cloudflare, Inc. |

위 표는 각 스킬 경로에 포함된 외부 저작물과 개작물의 라이선스를 안내한다. 확인일은 2026-11-18이다. 해당 스킬을 복사하거나 배포할 때는 각 폴더의 LICENSE에 있는 원본 저작권 표시와 허가문을 함께 포함한다.

## 2. 구현 전 해결 방향과 계획 검토 스킬

- 원본 진입점은 [grill-me/SKILL.md](https://github.com/mattpocock/skills/blob/5863806dd4e15c63174bee4e7515a4256792ecfa/skills/productivity/grill-me/SKILL.md)다.
- 개작에 참고한 절차는 [grilling/SKILL.md](https://github.com/mattpocock/skills/blob/5863806dd4e15c63174bee4e7515a4256792ecfa/skills/productivity/grilling/SKILL.md)다.
- 개작 내용은 [스킬 본문](skills/requirements-review/SKILL.md)에, 원본 라이선스 전문은 [스킬 LICENSE](skills/requirements-review/LICENSE)에 둔다.

## 3. Cloudflare 보안 스킬

- 원본은 [security-audit-skill](https://github.com/cloudflare/security-audit-skill/tree/c1c8a8c1471069fb0e188eeaff69b8e8db6564a8)이다.
- 복사 범위는 [원본 스킬 폴더](https://github.com/cloudflare/security-audit-skill/tree/c1c8a8c1471069fb0e188eeaff69b8e8db6564a8/skills/security-audit)다.
- 원본 저작권 표시와 MIT 라이선스 전문은 [스킬 LICENSE](skills/security-audit/LICENSE)에 보존한다.
