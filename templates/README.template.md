# {{REPO_TITLE}}

{{ONE_LINE_DESCRIPTION}}

<div align="center">

[![License](https://img.shields.io/badge/License-MIT-2f6f4f?style=for-the-badge&logo=mit)](LICENSE)
[![{{TARGET_BADGE_LABEL}}](https://img.shields.io/badge/{{TARGET_BADGE_LABEL}}-{{TARGET_BADGE_VALUE}}-2f6f4f?style=for-the-badge&logo={{TARGET_BADGE_LOGO}})]({{TARGET_BADGE_URL}})
[![{{TOOL_BADGE_LABEL}}](https://img.shields.io/badge/{{TOOL_BADGE_LABEL}}-{{TOOL_BADGE_VALUE}}-2f6f4f?style=for-the-badge&logo=gnubash)]({{TOOL_BADGE_URL}})
[![Docs](https://img.shields.io/badge/docs-guide-2f6f4f?style=for-the-badge)](docs/recovery-plan.md)
[![Release](https://img.shields.io/badge/release-v1.0.0-2f6f4f?style=for-the-badge)]({{RELEASE_URL}})

</div>

<div align="center">
  <img src="assets/og-image.png" alt="{{REPO_TITLE}}" width="80%" />
</div>

> [!NOTE]
> {{ONE_SENTENCE_OUTCOME}}

## Quick summary

- **Subject**: {{SUBJECT_NAME}}, version {{SUBJECT_VERSION}}
- **Symptom**: {{SYMPTOM_DESCRIPTION}}
- **Root cause**: {{ROOT_CAUSE}}
- **Fix**: {{FIX_DESCRIPTION}}
- **Outcome**: {{OUTCOME_DESCRIPTION}}

## Capability matrix

| Capability | Status | Notes |
| - | - | - |
| {{CAPABILITY_1}} | {{STATUS_1}} | {{NOTES_1}} |
| {{CAPABILITY_2}} | {{STATUS_2}} | {{NOTES_2}} |
| {{CAPABILITY_3}} | {{STATUS_3}} | {{NOTES_3}} |

## The fix

{{FIX_PROCEDURE}}

## Checksums

| File | SHA-256 | SHA-1 |
| - | - | - |
| {{FILE_NAME}} | {{SHA256}} | {{SHA1}} |

## Repo layout

```
{{REPO_NAME}}/
  README.md                  # this file
  LICENSE                    # MIT
  CONTRIBUTING.md            # scope, anti-slop checklist
  SECURITY.md
  CODE_OF_CONDUCT.md
  .gitignore
  assets/
    og-image.png             # 1200x630 social card
  .github/
    social-preview/
      social-preview.png     # 1280x640 GitHub social preview
    workflows/
      verify.yml             # CI: blocks em-dashes, unfinished markers
  docs/
    recovery-plan.md         # canonical provenance
    recovery-completed.md    # exit report
    cross-ai-review.md        # cross-AI review pass
  templates/
    README.template.md       # this template
```

## Documentation

- [`docs/recovery-plan.md`](docs/recovery-plan.md) - the full validated plan
- [`docs/recovery-completed.md`](docs/recovery-completed.md) - evidence records
- [`docs/cross-ai-review.md`](docs/cross-ai-review.md) - independent AI peer review

## Contributing and License

- [Contributing guide](CONTRIBUTING.md)
- [Security policy](SECURITY.md)
- [Code of conduct](CODE_OF_CONDUCT.md)
- [MIT License](LICENSE)

## Changelog

- {{DATE}}: v1.0 - initial record, assets, CI workflow, production README

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos={{GITHUB_OWNER}}/{{REPO_NAME}}&type=Date)](https://star-history.com/#{{GITHUB_OWNER}}/{{REPO_NAME}}&Date)

---

## Template usage notes

Replace every `{{PLACEHOLDER}}` with your actual values. Required placeholders:
- `REPO_TITLE`, `ONE_LINE_DESCRIPTION`, `REPO_NAME`, `GITHUB_OWNER`
- `SUBJECT_NAME`, `SUBJECT_VERSION`
- `SYMPTOM_DESCRIPTION`, `ROOT_CAUSE`, `FIX_DESCRIPTION`, `OUTCOME_DESCRIPTION`
- `FIX_PROCEDURE` (multi-line)
- `FILE_NAME`, `SHA256`, `SHA1` (per file row)
- `TARGET_BADGE_*`, `TOOL_BADGE_*` (for the badge row)
- `RELEASE_URL`, `DATE`

Optional placeholders:
- `CAPABILITY_*`, `STATUS_*`, `NOTES_*` (rows in the capability matrix)

After filling:
1. Run `avoid-ai-writing` detect mode. Require 0 em dashes / 0 curly quotes / 0 AI-isms.
2. Run `design-taste-frontend` for hero image, badge consistency, callout quality.
3. Re-run anti-slop check; ship if 0/0/0.
4. Push, then via Composio set 8-12 topic tags, set homepage to the README URL, create v1.0.0 release with anti-slop checked notes.