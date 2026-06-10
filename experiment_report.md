# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-001
**Name:** Nguyen Van An
**Date:** 2026-06-10

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 9 | Agent tra loi chinh xac, xac dinh dung san pham dien tu gia cao nhat |
| Garbage Data (`garbage_data.csv`) | Agent Error: I'm choking on the data! (could not convert string to float: 'ten dollars') | 1 | Agent bi loi hoan toan do du lieu sai kieu (wrong data type) |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi Agent su dung du lieu "rac" (garbage data), no gap nhieu van de nghiem trong ve chat luong du lieu dan den ket qua sai hoac loi hoan toan:

**Duplicate IDs:** Record co ID=1 xuat hien 2 lan (mot la Laptop gia $1200, mot la Banana gia $2). Dieu nay gay nhap nhem va co the khien Agent chon sai san pham khi tim kiem theo ID.

**Wrong Data Types (Sai kieu du lieu):** Record "Broken Chair" co gia la chuoi "ten dollars" thay vi so. Khi Agent co tinh toan hoac so sanh gia, Python se nem loi `ValueError` vi khong the chuyen chuoi thanh so thuc. Day chinh la nguyen nhan gay ra loi "Agent Error: I'm choking on the data!" trong ket qua thi nghiem.

**Extreme Outliers (Gia tri bat thuong):** Nuclear Reactor voi gia $999,999 la mot ngoai lai cuc lon. Neu Agent tinh gia trung binh cua electronics, gia tri nay se lam lech toan bo ket qua, khien Agent dua ra khuyen nghi vo nghia.

**Null Values (Gia tri trong/rong):** Record "Ghost Item" co ID=None va category=None. Cac gia tri None nay co the gay ra loi khi Agent co loc theo category hoac hien thi thong tin san pham.

Tat ca nhung van de nay chung minh rang du lieu khong sach se pha vo logic cua Agent, du logic do duoc viet tot den dau. Garbage In = Garbage Out.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Dong y hoan toan.

Mot AI Agent du co prompt tot den dau cung se cho ket qua sai neu du lieu dau vao bi o nhiem. Trong thi nghiem nay, Agent voi du lieu sach cho ra cau tra loi chinh xac va co ich (accuracy=9/10), trong khi voi garbage data Agent bi crash hoan toan (accuracy=1/10). Dieu nay chung to rang Data Quality la nen tang quan trong hon ca Prompt Engineering. ETL Pipeline voi buoc Validate la lop bao ve then chot giua du lieu thuc te va he thong AI.
