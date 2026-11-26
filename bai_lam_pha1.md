# BÀI LÀM PHA 1 – HACKATHON 02

- **Mã đề:** 08
- **Họ tên:**Trần Đình Lộc
- **Lớp:**HCM-K26-CNTT2
- **Link repository Pha1:**

> Pha 1 (70 phút đầu, KHÔNG dùng AI). Viết xong, kéo thả file này vào repository Pha1 trước mốc giờ giám thị công bố.

## 4.1. Bảo vệ dữ liệu và chống ảo giác

### a) Ghi chú đã ẩn danh hoá

**GHI CHU DA AN DANH**

```text
Khách hàng [Ten_khach], số điện thoại [So_dien_dien_thoai], số CCCD [SO_CCCD], email [dia_chi_email], đặt lịch cạo vôi răng (mã CAOVOI) ngày 23/12/2026 cho 2 người lớn và 1 trẻ em 10 tuổi. Khách đã chuyển khoản đặt cọc 200.000 đồng. Khách yêu cầu khám buổi chiều.
```


### b) Hai câu lệnh chống ảo giác

**CAU LENH**

```text
Câu1:Chỉ trả lời dựa trên nội dung có trong file chính sách hủy lịch hẹn cuả công ty đính kèm,tuyệt đối không suy đoán,không bịa đặt hay lấy thông tin bên ngoài.Nếu file không đề cập đến trường hợp khách hủy hẹn trước giờ khám 3 tiếng thì có bị mất cọc không thì phải ghi rõ là "File không có thông tin về trường hợp này".

Câu2:Với mỗi ý trả lời,bắt buộc ghi rõ thông tin đó lấy từ mục,khoản hoặc điều khoản nào trong file đính kèm.
```

## 4.2. Trích xuất tin nhắn đặt lịch khám ra JSON

**PROMPT**

```text
C-CONTEXT:Bạn là nhân viên hỗ trợ đặt lịch làm răng của Nha Khoa Nụ Cười,cần trích thông tin đặt lịch khám răng từ tin nhắn của khách hàng để chuyển sang định dạng JSON chuẩn.
R-REQUEST:Chuyển đổi 3 tin nhắn TN1,TN2,TN3 thành một mảng JSON gồm đúng 3 đối tượng theo đúng thứ tự TN1,TN2,TN3,mỗi đối tượng có đúng 6 trường:("ma_dich_vu": "CAOVOI", "ngay_hen": "2026-11-12", "nguoi_lon": 1, "tre_em": 2, "khung_gio": "sang", "ghi_chu": "1 bé rất sợ khoan") như kết quả mẫu
E-EXPLANATION:Tin nhắn đặt lịch của khách hàng viết tự do nên cần chuẩn hóa thống nhất theo bằng mã gói và quy tắc để đảm bảo dữ liệu chính xác và đồng bộ.
A-ACTION:Đọc kĩ bảng mã gói,5 quy tắc chuẩn hóa và 2 ví dụ Few-shot,sau đó trích xuất lần lượt TN1,TN2,TN3 trong cặp thẻ <tin_nhan>...</tin_nhan> thành mảng JSON.
T-TONE:Chính xác,khách quan,tuyệt đối tuân thủ quy tắc và định dạng đầu ra.
E-EXTRAS:
BẢNG MÃ DỊCH VỤ
CAOVOI – Khám và cạo vôi răng
TRAM – Trám răng thẩm mỹ (1 răng)
TAYTRANG – Tẩy trắng răng
5 quy tắc chuẩn hóa:
1. ma_dich_vu lấy theo bảng mã dịch vụ.
2. ngay_hen dạng YYYY-MM-DD; tin nhắn không ghi năm thì lấy năm 2026; không có ngày cụ thể thì null.
3. Khách không nhắc trẻ em thì tre_em là 0 và mọi khách là người lớn.
4. khung_gio chỉ nhận "sang", "chieu" hoặc null.
5. ghi_chu chỉ ghi yêu cầu đặc biệt về sức khoẻ, bệnh nền, dị ứng, tâm lý; không có thì null.
Ví dụ 1:
Đặt lịch cạo vôi răng ngày 12/11/2026 cho 1 người lớn và 2 bé, buổi sáng nha. Một bé rất sợ khoan.
Kết quả đúng:
{"ma_dich_vu": "CAOVOI", "ngay_hen": "2026-11-12", "nguoi_lon": 1, "tre_em": 2, "khung_gio": "sang", "ghi_chu": "1 bé rất sợ khoan"}
Ví dụ 2:
Tẩy trắng còn lịch buổi chiều không ạ, em đi 1 mình, hôm nào cũng được.
Kết quả đúng:
{"ma_dich_vu": "TAYTRANG", "ngay_hen": null, "nguoi_lon": 1, "tre_em": 0, "khung_gio": "chieu", "ghi_chu": null}
<tin_nhan>
TN1: Cho mình hẹn trám răng ngày 17/12 nhé, 2 người lớn với 1 bé 9 tuổi, buổi chiều.

TN2: Đặt lịch cạo vôi cho 3 người ngày 06/01/2027 ạ. Một người bị tiểu đường.

TN3: Tẩy trắng răng cuối năm còn lịch không ạ? Nhà em 4 người lớn, một người dị ứng thuốc tê, đi buổi sáng.
</tin_nhan>
Chỉ trả về duy nhất mảng JSON hợp lệ,không chào hỏi,không giải thích.
```

## 4.3. Báo giá bằng Chain-of-Thought

### a) Prompt

**PROMPT**
Hãy tính tổng tiền cho yêu cầu báo giá dưới đây theo đúng bảng giá và quy tắc tính giá.
<du_lieu_bao_gia>
BẢNG GIÁ DỊCH VỤ (đồng/người lớn)
CAOVOI – Khám và cạo vôi răng: 350.000
TRAM – Trám răng thẩm mỹ (1 răng): 500.000
TAYTRANG – Tẩy trắng răng: 2.500.000
QUY TẮC TÍNH GIÁ:
1. Trẻ em từ 6 đến 12 tuổi tính 80% giá người lớn. Trẻ dưới 6 tuổi được khám miễn phí.
2. Nhóm từ 5 người lớn trở lên được giảm 10% trên tiền dịch vụ (tiền người lớn + tiền trẻ em).
3. Phí chụp X-quang: 150.000 đồng/phim. Phí này không được giảm giá.
4. Tổng tiền = tiền dịch vụ sau giảm + phí chụp X-quang.

YÊU CẦU BÁO GIÁ
Nhóm nhân viên công ty làm dịch vụ CAOVOI gồm 6 người lớn, 2 trẻ em (7 tuổi và 11 tuổi) và 1 bé 4 tuổi. Có 3 người cần chụp X-quang (mỗi người 1 phim).
</du_lieu_bao_gia>
Hãy suy luận từng bước theo đúng thứ tự sau và ghi rõ phép tính ở từng bước:
1 tiền người lớn:<phep_tinh>=<ket qua>
2 tiền trẻ em:<phep_tinh>=<ket qua>
3 tiền khám:<phep_tinh>=<ket qua>
4 giảm giá nhóm:<phep_tinh>=<ket qua>
5 phụ thu:<phep_tinh>=<ket qua>
6 tổng tiền:<phep_tinh>=<ket qua>
Dòng cuối cùng của câu trả lời bắt buộc phải có đúng dạng
[RESULT : <tổng tiền> đồng]

```text

```

## 4.4. Dây chuyền xử lý khiếu nại (Prompt Chaining)

### a) Prompt Trạm 1

**PROMPT**

```text
Bạn là bộ phận tiếp nhận khiếu nại khách hàng của Nha Khoa Nụ Cười.Hãy đọc email khiếu nại trong thẻ <email_khieu_nai> và trích xuất thông tin thành đúng một đối tượng JSON gồm 4 trường.
Quy định bắt buộc:
-Chi trả về đúng một đối tượng JSON hợp lệ,không chào hỏi không giải thích.
-Đúng 4 trường và đúng kiểu dữ liệu:
{"loai_su_co": một trong "tre_hen" | "thiet_bi" | "bac_si" | "khac", "so_khach": số nguyên, "so_lan_hen_bi_tre": số nguyên hoặc null, "tom_tat": "không quá 20 từ"}
<email_khieu_nai>
Gia đình tôi 3 người đã đặt lịch cạo vôi răng. Cả 2 lần hẹn ngày 05/11/2026 và 12/11/2026 chúng tôi đều phải chờ hơn 1 tiếng so với giờ hẹn. Bác sĩ Nam khám rất kỹ, tôi không có gì phàn nàn về bác sĩ. Tôi đề nghị phòng khám giải quyết thỏa đáng.
</email_khieu_nai>
```

### b) Hai điều cần kiểm tra ở JSON đầu ra của Trạm 1

1.

2.

### c) Câu lệnh viết tiếp

**CAU LENH**

```text

```

## 4.5. Prompt chấm bài theo Rubric

**PROMPT**

```text
(Viết prompt vào đây – xoá dòng này)
```

## 4.6. Hoàn thiện System Prompt

> Phần Vai trò và Chuẩn đầu ra đã cho sẵn. Viết tiếp phần Quy tắc ràng buộc và Xử lý ngoại lệ.

```text
[Vai trò]
Bạn là "Trợ lý Nụ Cười", nhân viên tư vấn trên website của Nha khoa Nụ Cười, giúp khách chọn và đặt lịch một trong 3 dịch vụ: CAOVOI (Khám và cạo vôi răng), TRAM (Trám răng thẩm mỹ), TAYTRANG (Tẩy trắng răng).

[Quy tắc ràng buộc]
1.
2.
3.

[Chuẩn đầu ra]
Trả lời bằng tiếng Việt, lịch sự, tối đa 120 từ. Giá dịch vụ trình bày dạng gạch đầu dòng. Kết thúc bằng một câu hỏi về nhu cầu tiếp theo của khách.

[Xử lý ngoại lệ]
- Khách hỏi ngoài phạm vi:
- Khách cung cấp thiếu thông tin:
```
