
# 💡 Giải pháp chăm sóc khách hàng bằng LLM cho doanh nghiệp dịch vụ nhỏ

> **Nền tảng nhắn tin CSKH sử dụng kiến trúc RAG & Multi-Agent**

---

## 🚀 Tính năng nổi bật

- **Dịch vụ nhắn tin chuyên biệt cho CSKH**
- **Agent phản hồi nghiệp vụ:** hỏi đáp, lên đơn
- **Agent chuyển tiếp:** các yêu cầu vượt quá khả năng & khiếu nại
- **Tự động trích xuất thông tin khách hàng**
- **Tự động lên đơn khi phát hiện nhu cầu**

---

## 🖥️ Giao diện hệ thống

### Khách hàng
![Màn nhắn tin 1](public/demo/khungchatkhach.png)
![Màn nhắn tin 2](public/demo/nhantinkhach.png)

### Nhân viên
![Màn nhắn tin nhân viên 1](public/demo/khungchatnhanvien.png)

**Chế độ vận hành:**

| Chế độ   | Mô tả |
|----------|-------|
| **Auto** | Agent tương tác trực tiếp với khách hàng |
| **Manual** | Agent hỗ trợ quyết định cho nhân viên |

![Màn nhắn tin nhân viên 2](public/demo/khungchatnhanvien2.png)
![Màn nhắn tin nhân viên 3](public/demo/khungchatnhanvien3.png)

> 💬 **Tin nhắn không trả lời được (RAG không ra kết quả) sẽ lưu lại để nhân viên xử lý.**

![Màn nhắn tin nhân viên 4](public/demo/khungchatnhanvien4.png)

**Thông tin khách hàng trích xuất hiển thị trong khung chat:**
![Màn quản lý](public/demo/manquanly.png)


---

## 📑 Mục lục

- [1. Phân tích thiết kế](#1-phan-tich-thiet-ke)
- [2. Xây dựng sản phẩm](#2-xay-dung-san-pham)

---

## 1. 🧩 Phân tích thiết kế

### Tổng quan Usecase
![Usecase tổng quan](public/usecase/TongQuan.png)

**Ba tác nhân chính:**

- Nhân viên
- Quản lý doanh nghiệp
- Khách hàng

### Usecase nhắn tin
![Usecase nhắn tin](public/usecase/QLHT.png)

**Logic:**
- Đảm bảo tại một thời điểm, một khách chỉ nhắn với một nhân viên
- Agent phản hồi dựa trên chế độ hội thoại

### Usecase quản lý đơn
![Usecase quản lý đơn](public/usecase/QLDH.png)

**Logic:**
- Agent trích xuất thông tin từ hội thoại
- Nhận biết ý định lên đơn và tạo đơn

---

## 2. 🏗️ Xây dựng sản phẩm

### Cấu trúc thư mục
![folder](public/etc/folderStructure.png)

### Tổng quan dự án
![Tổng quan](public/container/overview.png)

### Cấu trúc backend server
![backend](public/container/backend.png)

#### Chat Server
![chatserver](public/etc/chatserver.png)

---

### 🗄️ Tổ chức dữ liệu

#### Redis
**Cấu trúc:**
![redisStructure](public/etc/redisStructure.png)

**Chi tiết schema:**
![redisschema](public/etc/redisschema.png)

> **message_queue**: chứa tin nhắn của khách hàng chưa được nhận

#### MongoDB
**Cấu trúc:**
![mongoschema](public/etc/mogoschema.png)

---

### 🔄 Workflow sinh phản hồi

#### Kiến trúc langGraph
![langGraph](public/etc/langGraph.png)

**Node reAct agent:** phối hợp 2 agent & 1 RAG pipeline

**Node decompose:**
![decompose](public/etc/decompose.png)
> Nhận truy vấn đa ý định, trả về mảng ý định. VD: "tôi muốn A, tôi muốn B" → `["muốn A", "muốn B"]`

#### Kiến trúc ReAct agent
![agent](public/etc/agent.png)

#### Agent Conversation
![Conversationagent](public/etc/conversationAgent.png)

#### Agent Reservation
![ReservationAgent](public/etc/reservationAgent.png)

#### RAG pipeline
![pipeline](public/etc/ragpipeline.png)

**Logic tìm kiếm:**
1. Lần 1: hệ số alpha 0.7 (gần tìm kiếm vector) → tìm kiếm rộng
2. Lần 2: hệ số alpha 0.3 (gần tìm kiếm text)

![retrieval](public/etc/retrieval.png)

---

### 🗃️ Hệ quản trị nội dung
**Các chức năng của hệ quản trị nội bộ:**
![internal](public/etc/internal.png)



