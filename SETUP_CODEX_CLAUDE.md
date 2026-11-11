# Dùng REA với Codex và Claude Code

Đây là bản fork của [morluto/rea](https://github.com/morluto/rea), được chuẩn bị để kết nối **REA (Reverse Engineer Anything)** vào Codex CLI hoặc Claude Code. REA hỗ trợ phân tích/dịch ngược chương trình, ứng dụng và mã đã biên dịch. Nếu bạn chỉ cần **đọc hoặc giải thích source code** thông thường, Codex và Claude Code đã có thể làm việc trực tiếp với source mà không cần REA.

> **Quan trọng:** Chỉ gửi link GitHub `https://github.com/hpb282/REA` trong một cuộc chat **không tự cài hay chạy REA**. Repo lưu mã nguồn và khai báo plugin; công cụ REA chỉ hoạt động sau khi plugin/MCP được cài vào **môi trường thực thi** của Codex hoặc Claude Code.

## Chuẩn bị

- Cài **Codex CLI** hoặc **Claude Code** trên máy/môi trường bạn muốn dùng.
- Có **Node.js** phiên bản được REA hỗ trợ: 22.23.4+ thuộc nhánh 22, 24.22.1+ thuộc nhánh 24, hoặc 26.12.1+ (Node 23/25 không được hỗ trợ).
- Chỉ phân tích ứng dụng/nhị phân mà bạn sở hữu hoặc có quyền kiểm tra. Một số tác vụ native có thể cần thêm Hopper, Ghidra, IDA hoặc trình phân tích khác.

## Cách 1 — Codex CLI

Mở terminal (PowerShell trên Windows cũng được) và chạy **một lần**:

```bash
codex plugin marketplace add hpb282/REA
codex plugin add rea@rea
codex plugin list
```

Kiểm tra danh sách đã có `rea@rea`. Khi làm việc trong bản clone của repo REA, file `.codex/config.toml` đã đặt plugin thành enabled; Codex chỉ đọc cấu hình dự án khi bạn đánh dấu dự án đáng tin cậy. Cài plugin cũng có thể đưa REA vào các dự án khác tùy cấu hình Codex.

Nếu phiên bản Codex không hỗ trợ lệnh `codex plugin`, hãy nâng cấp Codex CLI hoặc dùng phương án MCP thông qua lệnh `npx rea-agents setup` ở phần cuối.

## Cách 2 — Claude Code

Mở terminal và chạy **một lần**:

```bash
claude plugin marketplace add hpb282/REA
claude plugin install rea@rea --scope user
claude plugin list
```

Trong phiên Claude Code tương tác, bạn cũng có thể dùng:

```text
/plugin marketplace add hpb282/REA
/plugin install rea@rea
```

Chọn **Install for you** nếu muốn dùng REA trong nhiều dự án khác nhau. Kiểm tra `/plugin` → **Installed** và `/mcp` để xác nhận MCP server của REA đang chạy. Repo có file `.claude/settings.json` khai báo marketplace và bật REA trong phạm vi dự án; **khai báo này không tự tải plugin** về máy mới. Bạn vẫn cần cài plugin một lần.

## Khi sử dụng

1. Mở dự án cần phân tích trong Codex CLI / Claude Code (hoặc cung cấp đường dẫn tệp cần phân tích trong phiên làm việc).
2. Kiểm tra REA đã được bật và MCP server khả dụng.
3. Ví dụ yêu cầu: **“Hãy sử dụng các công cụ REA để phân tích file này, mô tả cấu trúc, luồng xử lý và ghi rõ chỗ nào chỉ là suy đoán.”**

Bạn **không cần** sao chép mã nguồn của REA vào từng dự án. Plugin được cài ở môi trường chạy công cụ; link repo chủ yếu dùng để tra cứu hoặc cài plugin.

## Các giới hạn quan trọng

- **ChatGPT chat thông thường** hoặc **Claude chat thông thường** chỉ nhận link GitHub sẽ không có MCP server REA chỉ nhờ link đó.
- **Codex Cloud** và **Claude Code phiên cloud/web** có chính sách plugin riêng. Đặc biệt, Claude Code cloud hiện không tải plugin được bật qua `.claude/settings.json`; các lệnh cài ở trên dành cho **terminal/local/IDE** hỗ trợ plugin.
- Dự án REA này dùng gói npm `rea-agents` đã được pin trong manifest của upstream. Chúng ta chưa build hoặc chạy REA trên máy của bạn.
- Không chạy đồng thời plugin REA **và** cấu hình MCP do `npx rea-agents setup` tạo cho cùng một client, vì có thể sinh hai server REA. Chọn một trong hai cách.

## Nếu không sử dụng được plugin

Trong terminal có Node.js phù hợp, chạy:

```bash
npx rea-agents setup
```

Chọn client cần thiết, **đọc kỹ kế hoạch thay đổi**, rồi xác nhận nếu đồng ý. Lệnh này thay đổi cấu hình trên **máy đang chạy lệnh** chứ không thay đổi GitHub repo. Không chạy nếu đã cài plugin REA thành công.

Xem chi tiết trong [tài liệu cài đặt gốc](docs/getting-started/installation.md) và [README](README.md).

---
*Thiết lập bổ sung dành cho fork `hpb282/REA`; các file gốc và workflow của dự án upstream được giữ nguyên.*
