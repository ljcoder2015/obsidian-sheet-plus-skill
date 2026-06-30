# Example: Creating a Project Management Tracker

This example demonstrates how to build a project progress tracking sheet with data validation and conditional formatting using the Sheet Plus REST API.

## Scenario

Create a "Project Tracker" containing task names, assignees, due dates, statuses, and progress, using dropdown lists, date constraints, and conditional formatting highlights.

## Steps

### 1. Verify API Connection

```bash
curl http://127.0.0.1:3000/
```

### 2. Create a Sheet

```bash
curl -X POST http://127.0.0.1:3000/create_sheet \
  -H "Content-Type: application/json" \
  -d '{"sheetName":"Project Tracker"}'
```

### 3. Write Headers and Initial Data

```bash
curl -X POST http://127.0.0.1:3000/set_sheet_data \
  -H "Content-Type: application/json" \
  -d '{
    "sheetName": "Project Tracker",
    "range": "A1:F6",
    "values": [
      ["Task", "Assignee", "Start Date", "Due Date", "Status", "Progress%"],
      ["Requirements Analysis", "Zhang San", "2024-01-08", "2024-01-15", "Completed", 100],
      ["Prototype Design", "Li Si", "2024-01-15", "2024-01-22", "In Progress", 60],
      ["Frontend Development", "Wang Wu", "2024-01-22", "2024-02-15", "In Progress", 30],
      ["Backend Development", "Zhao Liu", "2024-01-22", "2024-02-15", "Not Started", 0]
    ]
  }'
```

### 4. Set Header Styles

```bash
curl -X POST http://127.0.0.1:3000/set_range_style \
  -H "Content-Type: application/json" \
  -d '{
    "sheetName": "Project Tracker",
    "range": "A1:F1",
    "style": {
      "backgroundColor": "#2F5496",
      "fontColor": "#FFFFFF",
      "fontWeight": "bold",
      "horizontalAlignment": "center"
    }
  }'
```

### 5. Set Data Validation — Status Dropdown List

```bash
curl -X POST http://127.0.0.1:3000/set_data_validation \
  -H "Content-Type: application/json" \
  -d '{
    "sheetName": "Project Tracker",
    "range": "E2:E100",
    "type": "list",
    "formula1": "Not Started,In Progress,Completed,Delayed,Cancelled"
  }'
```

### 6. Set Progress Percentage Validation (0-100 Integer)

```bash
curl -X POST http://127.0.0.1:3000/set_data_validation \
  -H "Content-Type: application/json" \
  -d '{
    "sheetName": "Project Tracker",
    "range": "F2:F100",
    "type": "whole",
    "formula1": "0",
    "formula2": "100",
    "operator": "between"
  }'
```

### 7. Set Date Validation (due date must be after start date — noted via custom rule)

```bash
# Add basic styling to date columns
curl -X POST http://127.0.0.1:3000/set_range_style \
  -H "Content-Type: application/json" \
  -d '{
    "sheetName": "Project Tracker",
    "range": "C2:D100",
    "style": {
      "horizontalAlignment": "center"
    }
  }'
```

### 8. Add Conditional Formatting — Status Colors

```bash
# In Progress → Blue highlight
curl -X POST http://127.0.0.1:3000/add_conditional_formatting \
  -H "Content-Type: application/json" \
  -d '{
    "sheetName": "Project Tracker",
    "range": "E2:E100",
    "ruleType": "text",
    "condition": {
      "textOperator": "equals",
      "text": "In Progress"
    },
    "format": {
      "backgroundColor": "#BDD7EE",
      "fontColor": "#1F4E79"
    }
  }'

# Completed → Green highlight
curl -X POST http://127.0.0.1:3000/add_conditional_formatting \
  -H "Content-Type: application/json" \
  -d '{
    "sheetName": "Project Tracker",
    "range": "E2:E100",
    "ruleType": "text",
    "condition": {
      "textOperator": "equals",
      "text": "Completed"
    },
    "format": {
      "backgroundColor": "#C6EFCE",
      "fontColor": "#006100"
    }
  }'

# Delayed → Red highlight
curl -X POST http://127.0.0.1:3000/add_conditional_formatting \
  -H "Content-Type: application/json" \
  -d '{
    "sheetName": "Project Tracker",
    "range": "E2:E100",
    "ruleType": "text",
    "condition": {
      "textOperator": "equals",
      "text": "Delayed"
    },
    "format": {
      "backgroundColor": "#FFC7CE",
      "fontColor": "#9C0006"
    }
  }'
```

### 9. Add a Filter

```bash
curl -X POST http://127.0.0.1:3000/add_filter \
  -H "Content-Type: application/json" \
  -d '{
    "sheetName": "Project Tracker",
    "range": "A1:F100"
  }'
```

### 10. Verify Results

```bash
curl "http://127.0.0.1:3000/get_sheet_data?sheetName=Project Tracker"
```

## Tools Used

| Order | Tool | Purpose |
|------|------|------|
| 1 | [check-status](../tools/check-status/SKILL.md) | Verify connection |
| 2 | [create-sheet](../tools/create-sheet/SKILL.md) | Create a new sheet |
| 3 | [set-sheet-data](../tools/set-sheet-data/SKILL.md) | Write headers and data |
| 4 | [set-range-style](../tools/set-range-style/SKILL.md) | Set header styles |
| 5 | [set-data-validation](../tools/set-data-validation/SKILL.md) | Status dropdown + progress constraints |
| 6 | [add-conditional-formatting](../tools/add-conditional-formatting/SKILL.md) | Status color highlights |
| 7 | [add-filter](../tools/add-filter/SKILL.md) | Add a filter |
| 8 | [get-sheet-data](../tools/get-sheet-data/SKILL.md) | Verify results |
