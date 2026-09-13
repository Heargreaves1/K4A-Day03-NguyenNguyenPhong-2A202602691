# 📊 BÁO CÁO THU HOẠCH NGHIỆM THU BÀI LAB 3 (BƯỚC 3 — SUBMISSION ARTIFACT)

> **Họ và Tên Học viên:** [Nguyễn Nguyên Phong] 
> **Mã Sinh Viên / Mã Học viên:** [2A202602691]  
> **Chủ đề Lựa chọn:** [Điền tên chủ đề đã chọn từ docs/DANH_SACH_DE_TAI.md hoặc Đề tài Mở]  

---

## 1. BẢNG CHẤM ĐIỂM AGENTIC FIT SCORING MATRIX (ĐÁNH GIÁ CHỦ ĐỀ)

| Tiêu chí Đánh giá | Mức độ (1 - 5) | Giải trình chi tiết lý do chọn điểm |
| :--- | :---: | :--- |
| **1. Multi-step Reasoning** | 5/ 5 | Bài toán đòi hỏi chuỗi xử lý liên hoàn: Đầu tiên tra cứu hồ sơ sinh viên → Trích xuất tên cố vấn học tập phụ trách→ Sử dụng tên cố vấn và thông tin lịch hẹn để kích hoạt công cụ đặt lịch. |
| **2. Tool Interaction** | 5/ 5 |LLM không thể tự biết GPA, tình trạng học vụ hay lịch trống nội bộ của nhà trường. Hệ thống bắt buộc phải gọi các Tool (academic_query, schedule_appointment) qua MCP Server để đọc/ghi dữ liệu thực tế.? |
| **3. Dynamic Decision** | 4/ 5 | Quyết định bước tiếp theo phụ thuộc vào kết quả quan sát (Observation): Nếu mã SV hợp lệ → tiếp tục phân tích cố vấn và đặt lịch; nếu trả về NOT_FOUND→ dừng luồng và thông báo lỗi, không tự bịa đặt thông tin. |
| **4. Long Horizon Goal** | 4/ 5 | Agent phải duy trì ngữ cảnh xuyên suốt cuộc hội thoại: từ tiếp nhận nhu cầu ban đầu của sinh viên đến khi hoàn tất gửi mã xác nhận lịch hẹn (booking_id). |
| **TỔNG ĐIỂM AGENTIC FIT** | 18/ 20 | *Nếu tổng điểm > 12/20: Bài toán rất phù hợp triển khai Agentic System.* |

---

## 2. TRÍCH XUẤT KẾT QUẢ WATERFALL TRACE LOG (SAU KHI CHẠY TEST SUITE TRÊN API THẬT)

> ⚠️ **YÊU CẦU NGHIỆM THU:** Mở tệp `.env` điền `GEMINI_API_KEY` (hoặc `OPENAI_API_KEY`) để kết nối LLM thật trước khi thực thi `python src/app.py --all`. Bài nộp chỉ dùng Mock Offline Provider sẽ không đạt điểm nghiệm thực tế.

Dán 1 đoạn trích xuất log tiêu biểu từ file `docs/trace_waterfall.json` sinh ra từ phản hồi LLM API thật:

```json
[
  {
    "step": 1,
    "query": "Tôi là sinh viên SV2026001, hãy đặt giúp tôi một lịch hẹn tư vấn học vụ với thầy PGS.TS Nguyễn Văn A vào lúc 09:00 ngày 20/09/2026.",
    "action_type": "TOOL_EXECUTION",
    "tool_name": "schedule_appointment",
    "arguments": {
      "datetime_str": "09:00 20/09/2026",
      "advisor_name": "PGS.TS Nguyễn Văn A",
      "student_id": "SV2026001"
    },
    "observation": {
      "status": "SUCCESS",
      "booking_id": "BK-SV2026001-99",
      "student_id": "SV2026001",
      "datetime": "09:00 20/09/2026",
      "advisor": "PGS.TS Nguyễn Văn A",
      "message": "Đặt lịch thành công cho sinh viên SV2026001 với PGS.TS Nguyễn Văn A vào lúc 09:00 20/09/2026."
    },
    "latency_ms": 1794.61
  },
  {
    "step": 2,
    "query": "Tôi là sinh viên SV2026001, hãy đặt giúp tôi một lịch hẹn tư vấn học vụ với thầy PGS.TS Nguyễn Văn A vào lúc 09:00 ngày 20/09/2026.",
    "action_type": "FINAL_ANSWER",
    "thought": "Tổng hợp kết quả từ MCP Server thành công.",
    "output": "Đặt lịch thành công cho sinh viên SV2026001 với PGS.TS Nguyễn Văn A vào lúc 09:00 20/09/2026.",
    "latency_ms": 10.0
  }
]
```

---

## 3. TỔNG KẾT KẾT QUẢ NGHIỆM THU & NỘP BÀI

- [x] Đã điền API Key thật trong `.env` và xác nhận Agent chạy mượt mà trên LLM API thật (Gemini `gemini-3.5-flash-lite`).
- **Tổng số Test Cases đã chạy thành công:** 5 / 5 test cases.
- **Số lượt gọi Tool qua MCP Server chính xác:** 4 lượt (TC02: `academic_query`, TC03: `schedule_appointment`, TC04: `academic_query`, TC05: `academic_query` nhận diện edge case `NOT_FOUND`).
- **Kết quả đẩy Repo nộp bài:** [x] Đã Commit và Push mã nguồn thành công lên GitHub cá nhân.

---

> ✅ **HOÀN TẤT NỘP BÀI:** Sao chép đường link GitHub Repository cá nhân của bạn và dán vào ô nộp bài trên hệ thống LMS VLearn để hoàn tất Bài Lab 3!
