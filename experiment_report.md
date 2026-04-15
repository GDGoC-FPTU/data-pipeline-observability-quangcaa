# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600243
**Name:** Nguyễn Việt Quang
**Date:** 2026-04-15

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 9 | Ket qua chinh xac, Laptop la san pham electronics dat nhat trong du lieu sach |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 2 | Ket qua sai lech nghiem trong, Agent goi y mot san pham khong thuc te voi gia cuc ky cao |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi su dung Garbage Data, Agent da tra loi hoan toan sai lech vi nhieu ly do lien quan den chat luong du lieu dau vao. Du lieu rac chua nhieu van de nghiem trong nhu sau:

**Duplicate IDs:** Trong garbage_data.csv, id = 1 xuat hien hai lan (Laptop va Banana). Dieu nay lam cho he thong khong phan biet duoc dau la ban ghi chinh xac, gay ra su nham lan khi truy van va tong hop du lieu. Neu Agent dua vao id de dinh danh san pham, no se bi conflict.

**Wrong Data Types:** Ban ghi "Broken Chair" co gia tri price la "ten dollars" thay vi mot so. Khi Agent co gang so sanh gia, gia tri nay se gay ra loi hoac bi xu ly sai vi khong the chuyen doi sang kieu so de tinh toan.

**Extreme Outliers:** "Nuclear Reactor" co gia 999999 USD, day la mot gia tri cuc ky bat thuong (outlier) so voi cac san pham binh thuong. Agent chi don gian tim san pham co gia cao nhat, nen no da chon Nuclear Reactor — mot san pham khong thuc te va khong nen xuat hien trong catalog ban le.

**Null Values:** Ban ghi "Ghost Item" co id = None, price = 0 va category = None. Nhung gia tri null nay co the gay ra loi khi Agent co gang loc hoac so sanh du lieu, lam giam do tin cay cua ket qua tra ve.

Tat ca nhung van de tren cho thay rang neu khong co buoc validation va lam sach du lieu truoc khi dua vao Agent, ket qua dau ra se hoan toan khong dang tin cay. Du Agent co logic tot den may, du lieu dau vao xau se dan den ket qua xau — day chinh la nguyen tac "Garbage In, Garbage Out".

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Dong y. Du lieu chat luong quan trong hon viec toi uu hoa prompt. Trong thi nghiem nay, cung mot cau hoi (prompt) nhung voi du lieu sach, Agent tra loi chinh xac (Laptop - $1200), con voi du lieu rac, Agent tra loi sai (Nuclear Reactor - $999999). Dieu nay chung minh rang du prompt co tot den dau, neu du lieu dau vao khong duoc lam sach va kiem tra ky luong, ket qua cua Agent se khong dang tin cay. Do do, xay dung pipeline ETL voi buoc validation la buoc bat buoc truoc khi su dung du lieu cho bat ky ung dung AI nao.
