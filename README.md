[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=24112801&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** student@vinuni.edu.vn
**Name:** Nguyen Van An
**Student ID:** AI20K-001

---

## Mo ta

Bai lab nay xay dung mot ETL Pipeline tu dong hoan chinh de xu ly du lieu san pham tu file JSON. Pipeline gom 4 buoc chinh: Extract (doc du lieu), Validate (kiem tra chat luong), Transform (chuan hoa & tinh toan), va Load (luu ket qua). Ngoai ra, bai lab thuc hien thi nghiem so sanh hieu qua cua AI Agent khi su dung Clean Data vs Garbage Data de chung minh tam quan trong cua Data Quality.

---

## Cach chay (How to Run)

### Prerequisites

```bash
pip install pandas pytest
```

### Chay ETL Pipeline

```bash
python solution.py
```

Sau khi chay, file `processed_data.csv` se duoc tao ra voi cac records hop le da duoc xu ly.

### Chay Agent Simulation (Stress Test)

```bash
# Buoc 1: Chay ETL pipeline de tao clean data
python solution.py

# Buoc 2: Tao garbage data
python generate_garbage.py

# Buoc 3: Chay thi nghiem so sanh
python agent_simulation.py
```

### Chay Tests (Kiem tra tu dong)

```bash
pytest tests/ -v
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script (chinh)
├── agent_simulation.py      # Stress test: so sanh Clean vs Garbage data
├── generate_garbage.py      # Tao file garbage_data.csv de thi nghiem
├── raw_data.json            # Du lieu dau vao goc
├── processed_data.csv       # Output cua pipeline (sau khi chay solution.py)
├── experiment_report.md     # Bao cao thi nghiem: phan tich Data Quality
├── tests/
│   └── test_autograder.py   # Bo test cham diem tu dong
└── README.md                # File nay
```

---

## Ket qua

- **Tong so records doc vao:** 5 records
- **Records hop le (kept):** 3 records (Laptop, Chair, Monitor)
- **Records bi loai (dropped):** 2 records
  - ID=3: Mystery Box — gia am (-10), khong hop le
  - ID=4: Phone — category rong, khong hop le
- **File output:** `processed_data.csv` voi cac cot: id, product, price, category, discounted_price, processed_at
- **Discounted price:** Giam 10% so voi gia goc (price * 0.9)
- **Category:** Da chuan hoa ve Title Case (vd: "electronics" → "Electronics")

---

## Ket luan Thi nghiem

Thi nghiem chung minh rang **Data Quality > Prompt Quality**. AI Agent voi du lieu sach cho ket qua chinh xac (accuracy 9/10), trong khi voi garbage data, Agent bi crash hoan toan do du lieu sai kieu. ETL Pipeline voi buoc Validate la lop bao ve quan trong nhat.
