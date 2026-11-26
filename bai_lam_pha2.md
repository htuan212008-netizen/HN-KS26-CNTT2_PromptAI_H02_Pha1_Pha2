# BÀI LÀM PHA 2 – HACKATHON 02

- **Mã đề:** 06
- **Họ tên:** Hồ Anh Tuấn
- **Lớp:** CNTT2
- **Link repository Pha2:** https://github.com/htuan212008-netizen/HN-KS26-CNTT2_PromptAI_H02_Pha1_Pha2/blob/main/bai_lam_pha2.md
- **Công cụ AI đã dùng (ChatGPT/Claude/Gemini):** Gemini

> Pha 2 (20 phút cuối). Mỗi mục: mở cuộc trò chuyện mới, gửi nguyên văn prompt đã viết trong bai_lam_pha1.md, dán câu trả lời và link chia sẻ vào đây. Xong, kéo thả file này vào repository Pha2.

## 4.2. Trích xuất tin nhắn đặt bàn ra JSON

**KET QUA AI**

```text
[
  {
    "ma_buffet": "NUONG",
    "ngay_dat": "2026-12-19",
    "nguoi_lon": 2,
    "tre_em": 1,
    "khu_vuc": "trong_nha",
    "ghi_chu": null
  },
  {
    "ma_buffet": "HAISAN",
    "ngay_dat": "2027-01-03",
    "nguoi_lon": 3,
    "tre_em": 0,
    "khu_vuc": null,
    "ghi_chu": "Một người dị ứng sữa"
  },
  {
    "ma_buffet": "LAU",
    "ngay_dat": "2026-12-24",
    "nguoi_lon": 4,
    "tre_em": 0,
    "khu_vuc": "san_vuon",
    "ghi_chu": "ông ngoại đi xe lăn"
  }
]
```

**Link trò chuyện:** https://share.gemini.google/lmTMaYXSoTht

## 4.3. Báo giá bằng Chain-of-Thought

**KET QUA AI**

```text
```python
adult_price = 399000
adults = 10
adult_total = adults * adult_price

# Children: 1.1m, 1.2m, 1.35m -> 3 children between 1m and 1.4m (50%), 1 child 0.8m (<1m, free)
child_price = adult_price * 0.5
children_50 = 3
child_total = children_50 * child_price

buffet_total = adult_total + child_total
discount = buffet_total * 0.05 if adults >= 10 else 0
buffet_after_discount = buffet_total - discount
surcharge = 500000
grand_total = buffet_after_discount + surcharge

print(f"{adult_total=}, {child_total=}, {buffet_total=}, {discount=}, {buffet_after_discount=}, {surcharge=}, {grand_total=}")


```

```text
adult_total=3990000, child_total=598500.0, buffet_total=4588500.0, discount=229425.0, buffet_after_discount=4359075.0, surcharge=500000, grand_total=4859075.0


```

Bước 1: Tiền người lớn
Đoàn gồm 10 người lớn sử dụng gói buffet nướng (NUONG) đơn giá 399.000 đồng/người:
10 × 399.000 = 3.990.000 đồng

Bước 2: Tiền trẻ em

* 3 trẻ em cao 1,1 m, 1,2 m và 1,35 m (nằm trong khoảng từ 1 m đến 1,4 m) được tính 50% giá người lớn: 399.000 × 50% = 199.500 đồng/trẻ em.
* 1 bé cao 0,8 m (dưới 1 m) được miễn phí: 0 đồng.
Tổng tiền trẻ em: 3 × 199.500 + 1 × 0 = 598.500 đồng

Bước 3: Tiền buffet
3.990.000 + 598.500 = 4.588.500 đồng

Bước 4: Giảm giá đoàn
Do đoàn có 10 người lớn (đạt mức từ 10 người lớn trở lên) nên được giảm 5% trên tổng tiền buffet:
4.588.500 × 5% = 229.425 đồng

Bước 5: Phụ thu
Đoàn thuê 1 phòng riêng:
1 × 500.000 = 500.000 đồng

Bước 6: Tổng tiền
Tiền buffet sau giảm: 4.588.500 - 229.425 = 4.359.075 đồng
Tổng tiền thanh toán: 4.359.075 + 500.000 = 4.859.075 đồng

[RESULT: 4.859.075 đồng]
```

**Link trò chuyện:** https://share.gemini.google/DF9HFKQPCqIe

### b) Kiểm tra kết quả AI

Đúng

## 4.4. Dây chuyền xử lý khiếu nại – kết quả Trạm 1

**KET QUA AI**

```text
{
  "loai_su_co": "khac",
  "so_khach": 5,
  "so_hiep_bi_anh_huong": 2,
  "tom_tat": "Khách phàn nàn buffet hải sản hết tôm hùm và cua, chờ bổ sung không có."
}
```

**Link trò chuyện:** https://share.gemini.google/dXWo62FGw4Qe

## 4.5. Prompt chấm bài theo Rubric

**KET QUA AI**

```text
| Tiêu chí | Điểm | Minh chứng | Đề xuất sửa |
| --- | --- | --- | --- |
| Đúng thông tin (50%) | 1,0/5,0 | "Buffet lẩu bên em 279k/người lớn thôi" và "Chị trễ 40 phút em vẫn giữ bàn cho chị nha." sai giá 299.000đ và sai quy định trễ trên 30 phút phải huỷ bàn. | Buffet lẩu bên em có giá 299.000 đồng/người lớn, và nếu trễ trên 30 phút thì nhà hàng sẽ huỷ bàn theo quy định. |
| Đầy đủ (30%) | 1,0/3,0 | Chỉ nêu giá và trường hợp trễ 40 phút mà không nhắc mốc trễ dưới 15 phút hay 15-30 phút, cũng không mời khách cung cấp ngày, giờ đến, số khách. | Trễ dưới 15 phút giữ nguyên bàn, trễ 15-30 phút giữ bàn nếu còn chỗ; chị cho em xin ngày, giờ đến và số lượng khách để đặt bàn nhé. |
| Giọng điệu (20%) | 1,0/2,0 | "Dạ chào chị nha!", "ngon bá cháy luôn", "nha" và "nhé" dùng từ ngữ chưa đủ trang trọng, chuyên nghiệp. | Dạ em chào chị, buffet lẩu bên em rất hấp dẫn; chị cho em xin thông tin đặt bàn để bên em phục vụ chu đáo ạ. |
| Tổng điểm | 3,0/10 | Nhân viên báo sai giá, sai quy định giữ bàn, thiếu thông tin đặt bàn và dùng từ ngữ suồng sã. | Cần nắm vững thông tin chuẩn, hỏi đủ thông tin đặt bàn và giữ giọng điệu lịch sự, chuyên nghiệp hơn. |
```

**Link trò chuyện:** https://share.gemini.google/PwLg6jVZJf2P
