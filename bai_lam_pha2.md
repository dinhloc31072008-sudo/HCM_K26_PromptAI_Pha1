# BÀI LÀM PHA 2 – HACKATHON 02

- **Mã đề:** 08
- **Họ tên:**
- **Lớp:**
- **Link repository Pha2:**
- **Công cụ AI đã dùng (ChatGPT/Claude/Gemini):**

> Pha 2 (20 phút cuối). Mỗi mục: mở cuộc trò chuyện mới, gửi nguyên văn prompt đã viết trong bai_lam_pha1.md, dán câu trả lời và link chia sẻ vào đây. Xong, kéo thả file này vào repository Pha2.

## 4.2. Trích xuất tin nhắn đặt lịch khám ra JSON

**KET QUA AI**

```text
[
  {"ma_dich_vu": "TRAM", "ngay_hen": "2026-12-17", "nguoi_lon": 2, "tre_em": 1, "khung_gio": "chieu", "ghi_chu": null},
  {"ma_dich_vu": "CAOVOI", "ngay_hen": "2027-01-06", "nguoi_lon": 3, "tre_em": 0, "khung_gio": null, "ghi_chu": "1 người bị tiểu đường"},
  {"ma_dich_vu": "TAYTRANG", "ngay_hen": null, "nguoi_lon": 4, "tre_em": 0, "khung_gio": "sang", "ghi_chu": "1 người dị ứng thuốc tê"}
]
```

**Link trò chuyện:**
https://claude.ai/share/20bb87b8-7e9c-44cc-b258-81169706cf34

## 4.3. Báo giá bằng Chain-of-Thought

**KET QUA AI**

```text
Tính theo đúng thứ tự yêu cầu:

1 tiền người lớn: 6 × 350.000 = 2.100.000 đồng

2 tiền trẻ em: 2 trẻ (7 và 11 tuổi) × 350.000 × 80% = 2 × 280.000 = 560.000 đồng. Bé 4 tuổi (dưới 6 tuổi) được khám miễn phí nên tính 0 đồng.

3 tiền khám (tiền dịch vụ trước giảm): 2.100.000 + 560.000 = 2.660.000 đồng

4 giảm giá nhóm: Nhóm có 6 người lớn (từ 5 người lớn trở lên) nên được giảm 10%: 2.660.000 × 10% = 266.000 đồng. Tiền dịch vụ sau giảm: 2.660.000 − 266.000 = 2.394.000 đồng

5 phụ thu (X-quang, không được giảm giá): 3 × 150.000 = 450.000 đồng

6 tổng tiền: 2.394.000 + 450.000 = 2.844.000 đồng

[RESULT : 2.844.000 đồng]
```

**Link trò chuyện:**
https://claude.ai/share/ea3a80f1-3c8c-485f-a937-8ee8cd9ec1f9

### b) Kiểm tra kết quả AI

kết quả đúng:
1 Tiền người lớn: 6 × 350.000 = 2.100.000
2 Tiền khám (tiền dịch vụ trước giảm): 2.100.000 + 560.000 = 2.660.000
3 Giảm giá nhóm: nhóm có 6 người lớn (≥ 5) nên được giảm 10% trên tiền dịch vụ: 2.660.000 × 10% = 266.000. Tiền dịch vụ sau giảm: 2.660.000 − 266.000 = 2.394.000
4 Phụ thu (X-quang, không được giảm giá): 3 × 150.000 = 450.000
5 Tổng tiền: 2.394.000 + 450.000 = 2.844.000
Kết quả sai:
Tiền trẻ em: 2 trẻ (7 và 11 tuổi) tính 80% giá người lớn: 2 × (350.000 × 0,8) = 2 × 280.000 = 560.000. Bé 4 tuổi dưới 6 tuổi được miễn phí: 1 × 0 = 0. Tổng tiền trẻ em = 560.000 + 0 = 560.000(Sai)

## 4.4. Dây chuyền xử lý khiếu nại – kết quả Trạm 1

**KET QUA AI**

```text
{"loai_su_co":"tre_hen","so_khach":3,"so_lan_hen_bi_tre":2,"tom_tat":"Gia đình 3 người phải chờ hơn 1 tiếng trong cả hai lần hẹn cạo vôi răng, đề nghị phòng khám giải quyết."}
```

**Link trò chuyện:**
https://claude.ai/share/d0d1dc56-a8fe-433f-a0da-ad2b1c15a23b
## 4.5. Prompt chấm bài theo Rubric

**KET QUA AI**

```text
(Dán câu trả lời của AI vào đây (bấm nút Copy dưới câu trả lời) – xoá dòng này)
```

**Link trò chuyện:**
