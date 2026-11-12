# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

- Mã học viên theo lớp: 2A202603253
- Ngày / CVAT local: 11/11/2026
- Công cụ đã dùng: Polygon, Intelligent Scissors

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | chưa có | 0 / 3 | 32 |
| hard_panoptic | chưa có | 0 / 2 | 30 |
| cp1_holes | chưa có | 0 / 1 | 3 |
| cp2_slice | chưa có | 0 / 1 | 3 |
| cp5_occlusion | chưa có | 0 / 1 | 3 |
| cp3_thin | chưa có | 0 / 1 | 3 |
| cp4_curb | chưa có | 0 / 1 | 3 |
| cp6_coverage | chưa có | 0 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh `000000181542.jpg`, người phụ nữ mặc áo dài trắng ở vị trí trung tâm ảnh đang đi bộ qua đường.
- Class và quy tắc tôi dùng để chọn biên: Class `person`. Quy tắc biên: Sử dụng công cụ Polygon phóng to để bám sát viền cơ thể và tà áo dài nhìn thấy được; loại bỏ bóng đổ dưới chân và phần vạch kẻ đường bên dưới; đường biên bám sát mép vải áo dài bay, không ăn lấn sang nền đường nhựa phía sau.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: Khi thử Intelligent Scissors trên người đi xe máy bên cạnh, đường biên tự động có xu hướng bị hút lấn vào bóng đổ của xe máy trên mặt đường nhựa do độ tương phản màu sắc gắt; tôi đã tự tay dùng Polygon điều chỉnh lại các điểm neo để cắt bỏ phần bóng đen, chỉ giữ lại phần bánh xe và thân xe nhìn thấy thật sự.
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình: Đã nêu chi tiết ở trên.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Task easy_semantic, ảnh 817bca71-00000000.jpg, khu vực lề đường và vỉa hè phía bên phải (đoạn có gờ bó vỉa sơn đỏ/hồng).
- Lỗi thuộc loại: sai lớp / ranh giới biên (road vs sidewalk).
- Bằng chứng tôi nhìn thấy: Khi vẽ nhanh ban đầu, do màu nhựa đường và bê tông của lối vào nhà (driveway) khá tương đồng, tôi đã gộp luôn phần lối vào và vỉa hè vào class road, khiến diện tích sidewalk bị thiếu hụt nghiêm trọng.
- Quy tắc và hành động sửa: Áp dụng quy tắc phân chia theo chức năng và gờ bó vỉa (curb): phần lòng đường xe chạy là `road`, còn mép gờ bó vỉa và dải đường đi bộ/sân trước là sidewalk. Đã dùng Polygon phóng to vẽ lại ranh giới men đúng theo gờ bó vỉa, phân tách rõ `road` và sidewalk.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): Đã chạy script `python scripts/inspect_submissions.py --dir submissions` và kết quả báo `[OK] easy_semantic: easy_semantic.zip`; chưa có điểm vì chưa phát reference. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1. easy_semantic - 817bca71-00000000.jpg: Lối dốc xe vào nhà (driveway) bên phải | (1) Gán road vì ô tô chạy vào được; (2) Gán sidewalk vì nằm sau gờ bó vỉa, thuộc vỉa hè/khuôn viên nhà. | Quy tắc curb: Ranh giới road xác định theo lòng đường lưu thông chính đến chân bó vỉa. Driveway nằm ngoài lòng đường xe chạy. | Quyết định gán là sidewalk/nền khuôn viên nhà, đường road dừng ngay chân gờ bó vỉa. |
| 2. easy_semantic - 81ae7cbb-6bc63a4a.jpg: Dải phân cách cỏ có tuyết giữa lòng đường và vỉa hè | (1) Gán sidewalk vì nằm cùng dải dành cho người đi bộ; (2) Gán vegetation vì bản chất là đất cỏ dù tuyết phủ. | Phân loại ngữ nghĩa ưu tiên bản chất bề mặt tự nhiên (cây cối/thảm thực vật là vegetation). | Quyết định gán phần dải cỏ là vegetation, chỉ gán sidewalk cho dải đường bê tông đi bộ thực sự. |
| 3. medium_instance - 000000181542.jpg: Xe bán tải bị người đi xe máy che cắt đôi thân xe | (1) Tách thành 2 instance truck rời rạc; (2) Giữ là 1 instance `truck` duy nhất vì thuộc cùng một chiếc xe. | Quy tắc occlusion (che khuất): Một vật thể bị vật khác che cắt đôi vẫn là 1 instance (1 ID), chỉ vẽ các phần nhìn thấy. | Quyết định gán cả hai phần nhìn thấy của xe bán tải vào cùng 1 instance ID của class `truck`. |
