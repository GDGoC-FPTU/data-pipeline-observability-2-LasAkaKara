# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600694
**Name:** Hoàng Lê Bách
**Date:** 10/06/2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Testing with CLEAN data:
Agent: Based on my data, the best choice is Laptop at $1200. | 10/10 | chắc thế, do câu hỏi là best nên không biết chọn giữa monitor hay laptop. Nhưng câu trả lời dựa trên data đúng|
| Garbage Data (`garbage_data.csv`) | Testing with GARBAGE data:
Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 0/10 | Data không nên có row này nên agent trả lời không thể realistic được |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Agent trả lời sai khi dùng Garbage Data vì dữ liệu đầu vào chứa nhiều nhiễu và lỗi, dẫn đến việc Agent đưa ra quyết định dựa trên thông tin sai lệch. Cụ thể:
- Các giá trị bất thường (outliers) như "Nuclear Reactor" với mức giá khổng lồ ($999999) làm lệch lạc hoàn toàn bức tranh dữ liệu tổng thể. Khi Agent đánh giá hoặc sắp xếp dữ liệu, nó sẽ dễ dàng chọn những dòng dữ liệu vô lý này thay vì các sản phẩm thực tế như Laptop hay Monitor.
- Dữ liệu bị khuyết (null values) hoặc sai kiểu dữ liệu (wrong data types) khiến cho việc tính toán, so sánh, hoặc trích xuất thông tin bị gián đoạn, thậm chí gây ra lỗi phần mềm trong quá trình xử lý.
- Việc trùng lặp (Duplicate IDs) làm hỏng tính định danh duy nhất của sản phẩm, có thể khiến Agent bối rối khi tổng hợp hoặc truy xuất thông tin của một đối tượng cụ thể.

Tóm lại, sự thiếu toàn vẹn của dữ liệu (Data Integrity) sẽ khiến mô hình của Agent hiểu sai bối cảnh (context), từ đó đưa ra những suy luận phi logic và cung cấp cho người dùng những câu trả lời hoàn toàn vô nghĩa (Garbage In, Garbage Out).

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Đồng ý.

Chất lượng dữ liệu mang tính nền tảng và quyết định kết quả. Dù một prompt có được thiết kế hoàn hảo, chi tiết và sắc bén đến đâu, nếu nó được áp dụng lên một bộ dữ liệu đầy rác và sai lệch, kết quả trả về chắc chắn vẫn sẽ sai (nguyên lý "Garbage in, Garbage out"). Ngược lại, với một bộ dữ liệu sạch và chuẩn xác, ngay cả những prompt cơ bản cũng có thể giúp Agent suy luận và trích xuất được những thông tin đúng đắn, hữu ích.
