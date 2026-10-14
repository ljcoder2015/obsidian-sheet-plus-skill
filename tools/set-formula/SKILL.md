---
name: obsidian-sheet-plus-set-formula
description: Use when adding Excel-style formulas (SUM, AVERAGE, IF, VLOOKUP, etc.) to cells — for calculations, aggregations, or dynamic cell values
---

# set-formula
Set a cell formula. Supports Excel-compatible formulas such as SUM, AVERAGE, IF, VLOOKUP, etc. Formulas are automatically calculated and updated.

> **Range fill semantics**: when `range` covers more than one cell, the formula is filled the same way Excel fills down/right — **relative references are shifted** by each cell's offset from the top-left of the range. `range: "E1:E3"` with `formula: "=B1*2"` therefore writes `=B1*2` / `=B2*2` / `=B3*2`. `$`-locked parts (`$A$1`, `$A1`, `A$1`) are never shifted. Pass `fillMode: "same"` to write the identical formula text into every cell instead.

## Prerequisites
- Obsidian is running, Sheet Plus plugin is enabled
- Verified API availability via `GET /`

## REST API
| Field | Value |
|------|-----|
| Method | POST |
| Path | `/set_formula` |
| Auth | None by default. Requires `X-API-KEY` header when enabled |
| Content-Type | `application/json` |

## Parameters
| Parameter | Type | Required | Default | Description |
|------|------|------|--------|------|
| sheetName | string | No | Current active worksheet | Target worksheet name |
| range | string | Yes | - | Cell or range, e.g. `A1` or `A1:B10` |
| formula | string | Yes | - | Formula, must start with `=`, e.g. `=SUM(B1:B10)` |
| fillMode | string | No | `relative` | Only meaningful for a multi-cell range. `relative` = shift relative references per cell (Excel fill behaviour); `same` = write the identical formula text into every cell |

## Response
```json
{
  "success": true,
  "data": {
    "range": "A1",
    "formula": "=SUM(B1:B10)",
    "fillMode": "single-cell"
  }
}
```

## Example
```bash
curl -X POST http://127.0.0.1:3000/set_formula \
  -H "Content-Type: application/json" \
  -d '{
    "sheetName": "Sheet1",
    "range": "A1",
    "formula": "=SUM(B1:B10)"
  }'
```

## Common Errors
| Error | Cause | Solution |
|------|------|------|
| `Formula must start with =` | Formula does not start with `=` | Ensure formula starts with `=` |
| `Unsupported fillMode` | `fillMode` is neither `relative` nor `same` | Use `relative` (default) or `same` |
| `#REF!` | Formula references a non-existent cell | Check that the referenced range is correct; a fill offset that pushes a relative reference off the grid is rewritten to `#REF!` |
| `#NAME?` | Function name is misspelled or not supported | Confirm function name spelling and whether it is supported |
| `Sheet not found` | Worksheet name does not exist | Call get-sheet-list first to confirm the sheet name |
