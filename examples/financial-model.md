# Example: Creating a Financial Model

This example demonstrates how to build a financial report model from scratch using the Sheet Plus REST API.

## Scenario

Create a "Quarterly Sales Report" containing product sales data, auto-summary formulas, conditional formatting highlights, and style beautification.

## Steps

### 1. Verify API Connection

```bash
curl http://127.0.0.1:3000/
# Returns {"success":true} to proceed
```

### 2. Create a New Sheet

```bash
curl -X POST http://127.0.0.1:3000/create_sheet \
  -H "Content-Type: application/json" \
  -d '{"sheetName":"Quarterly Sales Report"}'
```

### 3. Write Headers and Data

```bash
curl -X POST http://127.0.0.1:3000/set_sheet_data \
  -H "Content-Type: application/json" \
  -d '{
    "sheetName": "Quarterly Sales Report",
    "range": "A1:F7",
    "values": [
      ["Product", "Q1", "Q2", "Q3", "Q4", "Total"],
      ["Product A", 12000, 13500, 14200, 15800, null],
      ["Product B", 8000, 9200, 8800, 9600, null],
      ["Product C", 15000, 16200, 17100, 18500, null],
      ["Product D", 5000, 5500, 5200, 6100, null],
      ["Product E", 9800, 10200, 11000, 11500, null],
      ["Quarterly Total", null, null, null, null, null]
    ]
  }'
```

### 4. Set Summary Formulas

```bash
# Product total column (SUM of columns B-E for each row)
for row in 2 3 4 5 6; do
  curl -X POST http://127.0.0.1:3000/set_formula \
    -H "Content-Type: application/json" \
    -d "{\"sheetName\":\"Quarterly Sales Report\",\"range\":\"F${row}\",\"formula\":\"=SUM(B${row}:E${row})\"}"
done

# Quarterly total row (SUM of each column)
for col in B C D E F; do
  curl -X POST http://127.0.0.1:3000/set_formula \
    -H "Content-Type: application/json" \
    -d "{\"sheetName\":\"Quarterly Sales Report\",\"range\":\"${col}7\",\"formula\":\"=SUM(${col}2:${col}6)\"}"
done
```

### 5. Set Header Styles

```bash
curl -X POST http://127.0.0.1:3000/set_range_style \
  -H "Content-Type: application/json" \
  -d '{
    "sheetName": "Quarterly Sales Report",
    "range": "A1:F1",
    "style": {
      "backgroundColor": "#4472C4",
      "fontColor": "#FFFFFF",
      "fontWeight": "bold",
      "horizontalAlignment": "center"
    }
  }'
```

### 6. Set Data Area Styles

```bash
# Add thousands separator format to number area (by setting styles for the number range)
curl -X POST http://127.0.0.1:3000/set_range_style \
  -H "Content-Type: application/json" \
  -d '{
    "sheetName": "Quarterly Sales Report",
    "range": "B2:F7",
    "style": {
      "horizontalAlignment": "right"
    }
  }'

# Bold the total row
curl -X POST http://127.0.0.1:3000/set_range_style \
  -H "Content-Type: application/json" \
  -d '{
    "sheetName": "Quarterly Sales Report",
    "range": "A7:F7",
    "style": {
      "fontWeight": "bold",
      "backgroundColor": "#D9E2F3"
    }
  }'

# Add borders
curl -X POST http://127.0.0.1:3000/set_range_style \
  -H "Content-Type: application/json" \
  -d '{
    "sheetName": "Quarterly Sales Report",
    "range": "A1:F7",
    "style": {
      "border": {
        "type": "all",
        "style": "THIN",
        "color": "#808080"
      }
    }
  }'
```

### 7. Add Conditional Formatting — Highlight Sales ≥ 15,000

```bash
curl -X POST http://127.0.0.1:3000/add_conditional_formatting \
  -H "Content-Type: application/json" \
  -d '{
    "sheetName": "Quarterly Sales Report",
    "range": "B2:E6",
    "ruleType": "number",
    "condition": {
      "operator": "greaterThanOrEqual",
      "value1": 15000
    },
    "format": {
      "backgroundColor": "#C6EFCE",
      "fontColor": "#006100"
    }
  }'
```

### 8. Verify Results

```bash
curl "http://127.0.0.1:3000/get_sheet_data?sheetName=Quarterly Sales Report&range=A1:F7"
```

## Tools Used

| Order | Tool | Purpose |
|------|------|------|
| 1 | [check-status](../tools/check-status/SKILL.md) | Verify connection |
| 2 | [create-sheet](../tools/create-sheet/SKILL.md) | Create a new sheet |
| 3 | [set-sheet-data](../tools/set-sheet-data/SKILL.md) | Write data |
| 4 | [set-formula](../tools/set-formula/SKILL.md) | Set summary formulas |
| 5 | [set-range-style](../tools/set-range-style/SKILL.md) | Beautify styles |
| 6 | [add-conditional-formatting](../tools/add-conditional-formatting/SKILL.md) | Highlight outliers |
| 7 | [get-sheet-data](../tools/get-sheet-data/SKILL.md) | Verify results |
