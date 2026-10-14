---
name: obsidian-sheet-plus-remove-conditional-formatting
description: Use when removing conditional formatting rules from a specific range — to clean up or reset formatting rules
---

# remove-conditional-formatting
Removes conditional formatting rules from a specified range only. Other ranges are unaffected.

Matching is by **intersection**: every rule whose applied range overlaps the given range is removed in a single call. A rule does not have to sit exactly on the given range — passing a superset (e.g. `A1:C5` for rules on `A1:A5`, `B1:B5` and `C1:C5`) removes all of them. Rules are removed as a whole, so a rule that only partially overlaps the range is removed entirely.

## Prerequisites
- Obsidian is running, Sheet Plus plugin is enabled
- Verified API availability via `GET /`

## REST API
| Field | Value |
|------|-----|
| Method | POST |
| Path | `/remove_conditional_formatting` |
| Auth | None by default. When enabled, requires `X-API-KEY` header |
| Content-Type | `application/json` |

## Parameters
| Parameter | Type | Required | Default | Description |
|------|------|------|--------|------|
| sheetName | string | No | Current active sheet | Target sheet name |
| range | string | Yes | - | Cell range, e.g. `B1:B10` |

## Response
```json
{
  "success": true,
  "data": {
    "range": "B1:B10",
    "rulesRemoved": 1
  }
}
```
`rulesRemoved` is the number of rules that were actually deleted; `0` means nothing in that range had a rule.

## Example
```bash
curl -X POST http://127.0.0.1:3000/remove_conditional_formatting \
  -H "Content-Type: application/json" \
  -d '{
    "sheetName": "Sheet1",
    "range": "B1:B10"
  }'
```

## Common Errors
| Error | Cause | Solution |
|------|------|------|
| `Range is invalid` | Invalid range format | Use A1 notation (e.g. `A1:C10`) |
| `Sheet not found` | Sheet name does not exist | Call get-sheet-list first to confirm the sheet name |

## Related Tools
- **add-conditional-formatting**: Add conditional formatting rules
- **clear-all-conditional-formatting**: Clear all conditional formatting from the sheet
