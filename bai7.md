
 

```text
[C - Context (Bối cảnh & Vai trò)]
Bạn là một Chuyên viên Tuyển dụng Kỹ thuật (IT Recruiter) có kinh nghiệm đánh giá hồ sơ lập trình viên Backend. Bộ phận nhân sự đang cần sàng lọc sơ bộ danh sách CV ứng tuyển vị trí Junior Backend Developer dựa trên Mô tả công việc (JD) chuẩn của công ty.

[R - Request (Yêu cầu cốt lõi)]
Hãy đọc dữ liệu CV của từng ứng viên, đối chiếu trực tiếp với các tiêu chí trong JD để chấm điểm chi tiết, tính tổng điểm trên thang 100, phân loại mức độ phù hợp và liệt kê rõ điểm mạnh cũng như thông tin còn thiếu của từng người.

[E - Explanation (Giải thích, Quy tắc chấm điểm & Ràng buộc)]
1. Tiêu chuẩn JD & Thang điểm chi tiết (Tổng 100 điểm):
   - Kỹ năng chuyên môn (Tối đa 70 điểm):
     + Java cơ bản: 20 điểm
     + Lập trình hướng đối tượng (OOP): 15 điểm
     + SQL: 10 điểm
     + PostgreSQL: 10 điểm
     + Sử dụng Git: 15 điểm
   - Kinh nghiệm / Dự án (Tối đa 30 điểm):
     + Có kinh nghiệm làm việc thực tế từ 1 năm trở lên: 30 điểm
     + Có kinh nghiệm thực tập thực tế (khoảng 6 tháng): 25 điểm
     + Chỉ có dự án cá nhân (từ 1-2 dự án): 15 điểm
     + Chưa có dự án hoặc kinh nghiệm: 0 điểm
   - Kỹ năng làm việc nhóm (teamwork): Mặc định chấm 0 điểm do JD và dữ liệu đầu vào không cung cấp thông tin tiêu chí này.

2. Ngưỡng phân loại (classification):
   - Từ 80 điểm trở lên: "PHÙ HỢP CAO"
   - Từ 60 đến dưới 80 điểm: "CẦN XEM XÉT"
   - Dưới 60 điểm: "CHƯA PHÙ HỢP"

3. Ràng buộc chống suy diễn (Bắt buộc tuân thủ):
   - Tuyệt đối KHÔNG tự suy diễn kỹ năng hoặc kinh nghiệm không được ghi rõ trong CV (ví dụ: CV chỉ ghi "PostgreSQL" thì không tự suy diễn là có kỹ năng "SQL" tổng quát nếu không liệt kê; CV chỉ ghi "Java" thì không tự mặc định là biết "OOP").
   - Không tự ý bổ sung dữ liệu còn thiếu. Nếu trường thông tin nào không có trong dữ liệu CV, phải ghi nhận là "Chưa có thông tin".
   - Không sử dụng lại điểm số trong các ví dụ mẫu để gán cho ứng viên thật.
   - Kết quả chỉ phục vụ mục đích sàng lọc sơ bộ, không thay thế quyết định tuyển dụng cuối cùng.

[A - Action (Các bước thực hiện)]
Thực hiện tuần tự 4 bước cho từng ứng viên:
- Bước 1: Trích xuất chính xác danh sách kỹ năng và kinh nghiệm hiện có trong CV.
- Bước 2: Đối chiếu từng từ khóa với thang điểm JD ở phần Explanation để tính điểm `technical`, `experience`, `teamwork` và `totalScore`.
- Bước 3: Xác định nhãn `classification` dựa trên `totalScore`.
- Bước 4: Tổng hợp mảng `strengths` (các điểm khớp với JD) và mảng `missingInformation` (các yêu cầu JD còn thiếu hoặc thông tin chưa được đề cập trong CV).

[T - Tone (Giọng điệu & Văn phong)]
Khách quan, chính xác, trung thực với dữ liệu gốc, ngắn gọn và chuyên nghiệp theo chuẩn nghiệp vụ nhân sự.

[E - Extras (Ví dụ mẫu Few-shot, Dữ liệu đầu vào & Định dạng đầu ra)]
*** Ví dụ mẫu (Few-shot Examples) ***

Ví dụ 1:
- Đầu vào: Hoàng X | Kỹ năng: Java, OOP, SQL, PostgreSQL, Git | Kinh nghiệm: 1 năm làm Backend Developer
- Kết quả JSON chuẩn:
{
  "name": "Hoàng X",
  "scores": {
    "technical": 70,
    "experience": 30,
    "teamwork": 0
  },
  "totalScore": 100,
  "classification": "PHÙ HỢP CAO",
  "strengths": [
    "Đáp ứng đầy đủ 100% kỹ năng chuyên môn trong JD (Java, OOP, SQL, PostgreSQL, Git)",
    "Có 1 năm kinh nghiệm làm việc thực tế đúng chuyên ngành"
  ],
  "missingInformation": [
    "Kỹ năng làm việc nhóm (Chưa có thông tin)"
  ]
}

Ví dụ 2:
- Đầu vào: Vũ Y | Kỹ năng: C++, MySQL | Kinh nghiệm: 1 dự án cá nhân
- Kết quả JSON chuẩn:
{
  "name": "Vũ Y",
  "scores": {
    "technical": 0,
    "experience": 15,
    "teamwork": 0
  },
  "totalScore": 15,
  "classification": "CHƯA PHÙ HỢP",
  "strengths": [
    "Đã từng thực hiện 1 dự án cá nhân"
  ],
  "missingInformation": [
    "Thiếu toàn bộ kỹ năng chuyên môn yêu cầu: Java, OOP, SQL, PostgreSQL, Git",
    "Chưa có kinh nghiệm dự án thực tế tại doanh nghiệp",
    "Kỹ năng làm việc nhóm (Chưa có thông tin)"
  ]
}

*** Dữ liệu CV cần đánh giá thực tế ***
1. Nguyễn A | Kỹ năng: Java, OOP, SQL, Git | Kinh nghiệm: 2 dự án cá nhân
2. Trần B | Kỹ năng: Python, HTML, CSS | Kinh nghiệm: Chưa có dự án
3. Lê C | Kỹ năng: Java, OOP, PostgreSQL, Git | Kinh nghiệm: 6 tháng thực tập
4. Phạm D | Kỹ năng: Java, SQL | Kinh nghiệm: 1 năm làm việc

*** Yêu cầu định dạng đầu ra ***
Chỉ xuất duy nhất dữ liệu JSON hợp lệ theo cấu trúc dưới đây, không kèm văn bản giải thích bên ngoài:
{
  "candidates": [
    {
      "name": "Tên ứng viên",
      "scores": {
        "technical": 0,
        "experience": 0,
        "teamwork": 0
      },
      "totalScore": 0,
      "classification": "NHÃN PHÂN LOẠI",
      "strengths": [],
      "missingInformation": []
    }
  ]
}
```

---

## III. Kết quả JSON đầu ra khi thực thi Prompt

```json
{
  "candidates": [
    {
      "name": "Nguyễn A",
      "scores": {
        "technical": 60,
        "experience": 15,
        "teamwork": 0
      },
      "totalScore": 75,
      "classification": "CẦN XEM XÉT",
      "strengths": [
        "Có nền tảng kỹ năng chuyên môn tốt: Java, OOP, SQL, Git",
        "Đã có kinh nghiệm thực hành qua 2 dự án cá nhân"
      ],
      "missingInformation": [
        "Kiến thức về PostgreSQL (Chưa có thông tin)",
        "Kinh nghiệm dự án/làm việc thực tế tại doanh nghiệp (Chưa có thông tin)",
        "Kỹ năng làm việc nhóm (Chưa có thông tin)"
      ]
    },
    {
      "name": "Trần B",
      "scores": {
        "technical": 0,
        "experience": 0,
        "teamwork": 0
      },
      "totalScore": 0,
      "classification": "CHƯA PHÙ HỢP",
      "strengths": [],
      "missingInformation": [
        "Thiếu toàn bộ kỹ năng chuyên môn yêu cầu: Java, OOP, SQL, PostgreSQL, Git",
        "Chưa có dự án cá nhân hoặc kinh nghiệm làm việc thực tế",
        "Kỹ năng làm việc nhóm (Chưa có thông tin)"
      ]
    },
    {
      "name": "Lê C",
      "scores": {
        "technical": 60,
        "experience": 25,
        "teamwork": 0
      },
      "totalScore": 85,
      "classification": "PHÙ HỢP CAO",
      "strengths": [
        "Đáp ứng tốt các kỹ năng cốt lõi: Java, OOP, PostgreSQL, Git",
        "Có 6 tháng kinh nghiệm thực tập thực tế"
      ],
      "missingInformation": [
        "Từ khóa kỹ năng SQL tổng quát (Chưa có thông tin - không tự suy diễn từ PostgreSQL)",
        "Kỹ năng làm việc nhóm (Chưa có thông tin)"
      ]
    },
    {
      "name": "Phạm D",
      "scores": {
        "technical": 30,
        "experience": 30,
        "teamwork": 0
      },
      "totalScore": 60,
      "classification": "CẦN XEM XÉT",
      "strengths": [
        "Có kiến thức về Java và SQL",
        "Có 1 năm kinh nghiệm làm việc thực tế"
      ],
      "missingInformation": [
        "Lập trình hướng đối tượng OOP (Chưa có thông tin - không tự suy diễn từ Java)",
        "Kiến thức về PostgreSQL (Chưa có thông tin)",
        "Kỹ năng sử dụng Git (Chưa có thông tin)",
        "Kỹ năng làm việc nhóm (Chưa có thông tin)"
      ]
    }
  ]
}
```

---



* **Nguyễn A (75 điểm - CẦN XEM XÉT):** Đạt 4/5 kỹ năng chuyên môn (`Java` 20đ + `OOP` 15đ + `SQL` 10đ + `Git` 15đ = 60đ) và 15đ cho `2 dự án cá nhân`. Thiếu `PostgreSQL` và kinh nghiệm thực tế tại doanh nghiệp.
* **Trần B (0 điểm - CHƯA PHÙ HỢP):** Các kỹ năng (`Python, HTML, CSS`) không nằm trong danh sách yêu cầu của JD Backend Java và chưa có dự án nào.
* **Lê C (85 điểm - PHÙ HỢP CAO):** Đạt `Java` (20đ) + `OOP` (15đ) + `PostgreSQL` (10đ) + `Git` (15đ) = 60đ kỹ năng (tuân thủ nghiêm ngặt quy tắc không tự suy diễn từ khóa `SQL` dù biết `PostgreSQL`), cộng với 25đ từ `6 tháng thực tập`.
* **Phạm D (60 điểm - CẦN XEM XÉT):** Đạt `Java` (20đ) + `SQL` (10đ) = 30đ kỹ năng (không tự suy diễn biết `OOP` từ `Java`) và điểm tối đa 30đ cho `1 năm làm việc` thực tế.