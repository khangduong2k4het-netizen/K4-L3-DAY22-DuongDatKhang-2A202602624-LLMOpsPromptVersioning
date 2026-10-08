# Nhận xét RAGAS — V1 và V2

Đánh giá dùng 50 cặp hỏi–đáp cho mỗi phiên bản, cùng reference, cùng 3 đoạn context và hai prompt giống hệt nhiệm vụ 2. Mỗi metric có đủ 50 điểm hữu hạn; một lượt context_precision của V2 bị timeout đã được chấm lại bằng mẫu gốc lấy từ LangSmith.

| Metric | V1 | V2 |
| --- | ---: | ---: |
| faithfulness | 0.9683 | 0.8111 |
| answer_relevancy | 0.9090 | 0.8155 |
| context_recall | 1.0000 | 1.0000 |
| context_precision | 0.9450 | 0.9450 |

Cả hai phiên bản đạt faithfulness ≥ 0.8. Trong lượt đánh giá này, V1 cao hơn V2 khoảng 0.1571 về faithfulness và 0.0934 về answer_relevancy. V1 yêu cầu trả lời ngắn, trực tiếp; V2 yêu cầu thêm phần định nghĩa, cơ chế và ý nghĩa, nên câu trả lời có xu hướng chứa nhiều nhận định hơn. Đây là một cách giải thích phù hợp với các mẫu đã kiểm tra, chưa phải kết luận nhân quả được chứng minh qua nhiều lượt chạy.

Ví dụ, với câu hỏi về LangSmith datasets, faithfulness của V1 là 1.0000, còn V2 là 0.5455. V2 thêm nhận định rằng batch evaluation bảo đảm thay đổi sẽ cải thiện hiệu năng, trong khi context chỉ nói evaluation cho phép so sánh các phiên bản. Việc đánh giá không tự bảo đảm kết quả tốt hơn. V1 giữ câu trả lời gần với các thông tin trực tiếp trong context.

Context recall và context precision bằng nhau ở 4 chữ số thập phân vì hai phiên bản dùng đúng cùng các đoạn truy xuất. Chênh lệch context precision ở các chữ số rất nhỏ chỉ ở mức số học, không thể coi là ưu thế của prompt. Kết quả này nghiêng về chọn V1 cho bộ câu hỏi hiện tại; nếu cải tiến V2, nên yêu cầu phần cơ chế và ý nghĩa chỉ xuất hiện khi context có bằng chứng rõ ràng, rồi đánh giá lại cả hai phiên bản với prompt đã version mới.

Nguồn: data/ragas_report.json, data/ragas_v1_details.json, data/ragas_v2_details.json và evidence/03_ragas_evaluation_log.txt. Ảnh evidence/03_ragas_scores.png là ảnh Playwright chụp bảng HTML từ JSON thật; không phải ảnh terminal.
