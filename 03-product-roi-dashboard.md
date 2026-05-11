**Part A**

| Trường                        | Ví dụ điền                                                                                                                     |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Product                       | AI customer support assistant                                                                                                  |
| Người dùng chính              | Diến giả, host cuộc hội thảo                                                                                                   |
| 2-4 workflow chính            | Record cuộc hội thảo, auto detect câu hỏi và đáp án, gom nhóm và ranking bộ câu hỏi                                            |
| AI làm gì?                    | Nhận diện câu hỏi và câu trả lời, gom nhóm câu hỏi và ranking                                                                  |
| Con người kiểm tra ở đâu?     | Câu hỏi và câu trả lời khi được ai tự động nhận diện, gom nhóm câu hỏi, ranking cá câu hỏi khó                                 |
| Khi AI sai thì xử lý thế nào? | Lưu record vocie, lưu câu hỏi, câu trả lời. Update thuật toán cho bộ dữ liệu đặc trưng                                         |
| Rào cản ADKAR chính           | Awareness + Desire: cần thay đổi hành vi của người dùng để học cách làm việc mới                                               |
| 3 tactic                      | Human-in-loop checklist; QA sample hằng tuần; dashboard cảnh báo khi dislike tăng, người dùng tắt tính năng voice của ứng dụng |

**Part B**

| Layer                   | Metric                                      |                     Baseline |                                                    Target | Data source          | Owner            | Red-team risk                                             | Fix                                                            |
| ----------------------- | ------------------------------------------- | ---------------------------: | --------------------------------------------------------: | -------------------- | ---------------- | --------------------------------------------------------- | -------------------------------------------------------------- |
| Product / Activation    | % Hội thảo sử dụng tính năng AI Q&A         |                 0% (Lọc tay) |                              > 70% hội thảo có > 50 người | Event log            | Product Manager  | Host bật nhưng không dùng kết quả AI vì không tin         | Theo dõi tỷ lệ "Interaction rate" (click vào câu hỏi AI gợi ý) |
| Workflow / Productivity | Thời gian gom nhóm & Ranking                | 5-10 phút (sau khi kết thúc) |                                     < 30 giây (Real-time) | Backend latency log  | AI Engineer      | AI gom nhóm quá chậm, host phải tự đọc chat để cứu vãn    | Tối ưu hóa pipeline xử lý stream voice/text                    |
| Workflow / Quality      | Tỷ lệ câu hỏi AI nhận diện sai (Noise rate) |                          N/A |                                                     < 10% | Human correction log | QA               | KAI nhận diện các câu cảm thán hoặc "troll" thành câu hỏi | Thêm layer lọc Intent (Phân loại ý định) trước khi ranking     |
| Value                   | Chỉ số hài lòng của khán giả về phần Q&A    |                      3/5 sao | > 4/5 sao(sử dụng AI và hội thảo vẫn giư được chất lượng) | Post-event survey    | Customer Success | Q&A nhanh nhưng hời hợt do AI gợi ý đáp án sai            | Ghép Human-in-loop: Host duyệt đáp án trước khi show           |

**Part C**

```text
[Product Coverage]        [Resolution Time]
70% workshops active           < 30s Latency (Real-time grouping)

[Quality]                 [Trust]
Noise rate < 10%               60% AI-ranked questions

[Value]                   [Decision]
+20% Q&A engagement            Continue with Human-in-loop;
```

**Part D**

Khuyến nghị: **continue with guardrails**. Trong môi trường hội thảo trực tiếp, rủi ro về danh tiếng của diễn giả là rất lớn. Do đó, không nên để AI tự động xuất bản (publish) câu hỏi hay câu trả lời mà chưa qua sự xác nhận của Host hoặc trợ lý (Mod).
