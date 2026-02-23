# Kumu Leverage Point Analysis

## 1. Project Background

This project was developed as part of an internship initiative to analyze **why participation rates in career institution events remain persistently low**. The underlying system was mapped using **Kumu**, a system thinking and causal loop diagram tool, which captures the relationships between variables that drive or suppress student engagement.

Understanding *which* variables matter most is non-trivial in a complex system — pulling on the wrong lever wastes effort, while the right leverage point can create outsized, lasting change. This script applies **network degree analysis** to the Kumu map export, ranking each variable by how connected it is within the causal system. Variables with high outgoing connections drive the most downstream effects, making them strong candidates for intervention.

---

## 2. Input, Output & Impact

### Input
- A **Kumu JSON export** (`.json`) of a causal loop diagram
- The JSON must contain `elements` (variables/nodes) and `connections` (causal links between them)

### Output
- A **CSV file** (`kumu_degree.csv`) with the following columns:

| Column | Description |
|---|---|
| 節點名稱 | Variable name (as labeled in Kumu) |
| 連出 (Out-degree) | Number of variables this node influences |
| 連入 (In-degree) | Number of variables that influence this node |
| 總連結數 (Total degree) | Sum of in + out connections |

The CSV is sorted by **total degree** (descending), so the most systemically connected variables appear at the top.

### Impact
This output directly supports **leverage point identification** — a core concept in systems thinking (Meadows, 1999). By ranking variables numerically, teams can:
- **Prioritize interventions** based on structural influence rather than intuition
- **Communicate findings** to stakeholders with clear, quantitative evidence
- **Avoid high-effort, low-impact actions** by deprioritizing variables with few connections

---

## 3. How to Use From Scratch

### Prerequisites
- Python 3.7 or above installed on your machine
- No external libraries required (uses only built-in `json` and `csv` modules)

### Step-by-step

**Step 1 — Export your Kumu map as JSON**

In Kumu, go to your project → `Settings` → `Export` → choose **JSON**. Save the file to your Desktop.

**Step 2 — Download the script**

Save `kumu_degree.py` to your Desktop (or the same folder as your JSON file).

**Step 3 — Update the file paths in the script**

Open `kumu_degree.py` in any text editor and update these two lines:

```python
# Line 6 — path to your Kumu JSON export
with open(r"C:\Users\YourName\Desktop\your-kumu-export.json", encoding="utf-8") as f:

# Line 35 — path where the CSV will be saved
output_path = r"C:\Users\YourName\Desktop\kumu_degree.csv"
```

**Step 4 — Run the script**

Open Terminal (Mac) or Command Prompt (Windows), then run:

```bash
python "C:\Users\YourName\Desktop\kumu_degree.py"
```

**Step 5 — Open the output**

Find `kumu_degree.csv` on your Desktop. Open it with Excel or Google Sheets. The variables are sorted from most to least connected — the top rows are your strongest leverage point candidates.
