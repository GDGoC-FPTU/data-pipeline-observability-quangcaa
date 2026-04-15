[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574042&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** 26ai.quangnv2@vinuni.edu.vn
**Student ID:** 2A202600243
**Name:** Nguyễn Việt Quang

---

## Mo ta

Bai lab nay xay dung mot ETL Pipeline tu dong de xu ly du lieu san pham. Pipeline thuc hien 4 buoc chinh: Extract (doc du lieu tu file JSON), Validate (loai bo cac ban ghi khong hop le), Transform (tinh gia giam va chuan hoa du lieu), va Load (luu ket qua ra file CSV). Ngoai ra, bai lab cung bao gom thi nghiem stress test de so sanh hieu suat cua AI Agent khi su dung du lieu sach va du lieu rac.

---

## Cach chay (How to Run)

### Prerequisites
```bash
python -m venv venv
# Windows:
.\venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

pip install pandas pytest
```

### Chay ETL Pipeline
```bash
python solution.py
```
Sau khi chay, file `processed_data.csv` se duoc tao ra voi du lieu da duoc lam sach va transform.

### Chay Agent Simulation (Stress Test)
```bash
# Buoc 1: Tao du lieu rac
python generate_garbage.py

# Buoc 2: Chay agent voi ca 2 bo du lieu (clean va garbage)
python agent_simulation.py
```

### Chay Tests
```bash
pytest tests/test_autograder.py -v
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script (extract, validate, transform, load)
├── raw_data.json            # Du lieu dau vao (5 san pham)
├── processed_data.csv       # Output cua pipeline (3 san pham hop le)
├── agent_simulation.py      # Script mo phong AI Agent
├── generate_garbage.py      # Script tao du lieu rac de stress test
├── experiment_report.md     # Bao cao thi nghiem clean vs garbage data
├── tests/
│   └── test_autograder.py   # Autograding tests (100 diem)
└── README.md                # File nay
```

---

## Ket qua

- **Extract:** Doc duoc 5 records tu `raw_data.json`
- **Validate:** Loai bo 2 records khong hop le (1 co gia am, 1 co category rong), giu lai 3 records
- **Transform:** Tinh discounted_price (giam 10%), chuan hoa category thanh Title Case, them timestamp
- **Load:** Luu thanh cong 3 records vao `processed_data.csv`
- **Stress Test:** Agent tra loi chinh xac voi du lieu sach (Laptop - $1200), nhung tra loi sai voi du lieu rac (Nuclear Reactor - $999999)
