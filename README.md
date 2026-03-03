# CSKH Game System (AI-Powered Support Agent)

Hệ thống AI Agent tự động hỗ trợ chăm sóc khách hàng chuyên biệt cho lĩnh vực Game. Hệ thống tích hợp xử lý hình ảnh (OCR), xác minh danh tính người dùng qua hóa đơn giao dịch và tra cứu thông tin sự kiện thời gian thực (RAG).

## 🚀 Tính năng chính

- **Phân loại yêu cầu tự động (Router):** Nhận diện và chuyển hướng yêu cầu vào các nhánh ACCOUNT, TRANSACTION hoặc QA GAME.
- **Xác minh chính chủ qua hóa đơn:** Quy trình kiểm tra 5-10 hóa đơn nạp tiền để xác minh quyền sở hữu tài khoản.
- **Hệ thống "Trạm gác" (Guards):** Kiểm tra trạng thái bảo trì và xác thực User ID trước khi can thiệp nghiệp vụ.
- **Hỗ trợ hỏi đáp thông minh (RAG):** Tra cứu thông tin sự kiện (Event) và hướng dẫn tân thủ từ cơ sở dữ liệu tri thức.

## 🛠 Tech Stack

- **Framework:** Python, LangChain/CrewAI.
- **Database:** - **MongoDB:** Lưu trữ Chat History và Ticket (Dự án cá nhân chạy Local hoặc Cloud Atlas).
  - **MySQL (Game DB):** Đối soát thông tin nạp và tài khoản qua API.
  - **Redis:** Quản lý Session và trạng thái hội thoại.
- **AI Tools:** Vision OCR (Triton/OpenAI), RAG Engine.

## 📊 Sơ đồ hệ thống

![Flowchart](assets/images/flowchart.png)
*(Xem chi tiết logic nghiệp vụ tại [Logic Documentation](docs/README_logic.md))*

## 📂 Cấu trúc dự án (Project Tree)

```text
ai-cskh-game/
├── assets/                 # Tài nguyên tĩnh phục vụ hiển thị
│   └── images/             # Chứa ảnh flowchart.png cho README
├── config/                 # Cấu hình hệ thống (API Keys, Database, Maintenance Level)
├── data/                   # Chứa tài liệu RAG (Event, Hướng dẫn tân thủ, VPN)
├── docs/                   # Tài liệu thiết kế và đặc tả logic
│   ├── diagrams/           # Chứa file HD_CSKH_GAME.drawio gốc
│   └── README_logic.md     # Giải thích chi tiết quy tắc nghiệp vụ AI
├── src/
│   ├── agents/             # Định nghĩa các Agent (Router, Account, Transaction, QA)
│   ├── tools/              # Hiện thực hóa các công cụ xử lý (9 Tools)
│   │   ├── vision.py       # Tool 1: vision_ocr
│   │   ├── system.py       # Tool 2: check_maintenance_status
│   │   ├── user.py         # Tool 3, 4: verify_user_id, send_otp
│   │   ├── invoice.py      # Tool 5, 7: verify_invoices_batch, check_transaction
│   │   ├── rag.py          # Tool 8, 9: game_knowledge, check_event_eligibility
│   │   └── ticket.py       # Tool 6: create_support_ticket
│   ├── workflows/          # Chứa logic rẽ nhánh (Flowchart logic)
│   │   ├── main_router.py  # Phân loại vào 3 nhánh lớn
│   │   ├── account_flow.py # Logic login, bảo trì, xác minh
│   │   └── qa_flow.py      # Logic hỏi đáp event
│   └── utils/              # Xử lý format JSON, log chat, quản lý session
├── tests/                  # Test case cho từng tool và workflow
├── main.py                 # File chạy chính của chatbot
└── requirements.txt        # Danh sách thư viện (LangChain, OpenAI, Pydantic, v.v.)
```