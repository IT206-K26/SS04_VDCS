## BÁO CÁO BÀI TẬP: THIẾT KẾ GIẢI PHÁP PROMPTING TỰ ĐỘNG HÓA CHĂM SÓC KHÁCH HÀNG

### 1. Bối cảnh & Vấn đề thực tế
Cửa hàng bán lẻ thiết bị điện tử cần tự động hóa quy trình xử lý khiếu nại của khách hàng gửi về hệ thống. Chúng ta sẽ sử dụng kỹ thuật **Chain-of-Thought**, **Prompt Chaining** và cài cắm **bẫy dữ liệu** để AI tự động phát hiện nếu khách hàng cung cấp thiếu thông tin.

### 2. Bước 1: Thiết kế giải pháp (I/O)
*   **Input (Đầu vào):** 
    *   `[TIN_NHẮN]`: Nội dung khiếu nại/feedback của khách hàng.
    *   `[MÃ_ĐƠN_HÀNG]`: Mã số đơn hàng trên hệ thống (có thể trống nếu khách quên nhập).
*   **Output (Đầu ra mong muốn):** 
    *   **Phần 1 - Tư duy (Chain-of-Thought):** AI phải tự phân tích vấn đề.
    *   **Phần 2 - Kết quả:** Một email phản hồi khách hàng phù hợp.

### 3. Bước 2: Viết prompt (Áp dụng Chain-of-Thought & Bẫy lỗi)
**Prompt Thực thi:**
> **Đóng vai:** Bạn là Chuyên viên Xử lý Khiếu nại cấp cao của hệ thống điện máy.
> **Nhiệm vụ:** Phân tích thông tin từ khách hàng và đưa ra hướng giải quyết cũng như viết email phản hồi tự động.
> 
> **THÔNG TIN ĐẦU VÀO (INPUT):**
> - Tin nhắn khách hàng: [TIN_NHẮN]
> - Mã đơn hàng: [MÃ_ĐƠN_HÀNG]
> 
> **QUÁ TRÌNH TƯ DUY (CHAIN-OF-THOUGHT) - Hãy suy nghĩ từng bước:**
> *   Bước 1 (Nhận diện): Cảm xúc của khách hàng đang như thế nào? Vấn đề cốt lõi họ gặp phải là gì?
> *   Bước 2 (Kiểm tra dữ liệu): Khách hàng đã cung cấp đủ [MÃ_ĐƠN_HÀNG] chưa? Tin nhắn có đề cập tên sản phẩm không? *(Lưu ý: Nếu một trong hai dữ liệu này trống hoặc không rõ ràng, đánh dấu trạng thái là "THIẾU_THÔNG_TIN").*
> *   Bước 3 (Quyết định): Nếu "THIẾU_THÔNG_TIN", hướng giải quyết là xin lỗi và yêu cầu bổ sung. Nếu đủ thông tin, hướng giải quyết là xử lý bảo hành/đổi trả.
> 
> **ĐỊNH DẠNG ĐẦU RA (OUTPUT):**
> Trả về kết quả theo đúng cấu trúc sau, không thêm lời chào:
> **1. Bảng Phân Tích Logic:**
> **2. Trạng Thái Dữ Liệu:** Hợp lệ / Thiếu thông tin.
> **3. Email Phản Hồi:** 

### 4. Kết quả chạy thử (Test Case để nộp)
*   **Dữ liệu truyền vào:**
    *   `[TIN_NHẮN]`: *"Tôi mới mua cái máy sấy tóc hôm qua mà về cắm điện không lên. Cửa hàng làm ăn chán thế, giải quyết ngay cho tôi không tôi bóc phốt!"*
    *   `[MÃ_ĐƠN_HÀNG]`: *(Để trống)*

*   **Kết quả AI phản hồi:**
> **1. Bảng Phân Tích Logic:**
> - Bước 1: Khách hàng đang có cảm xúc bức xúc, tức giận. Vấn đề cốt lõi: Sản phẩm máy sấy tóc bị lỗi nguồn (cắm không lên điện) ngay sau khi mua.
> - Bước 2: Kiểm tra dữ liệu: Đã có tên sản phẩm (máy sấy tóc), nhưng trường dữ liệu [MÃ_ĐƠN_HÀNG] đang bị bỏ trống.
> - Bước 3: Quyết định: Vì thiếu mã đơn hàng nên hệ thống không thể xác minh giao dịch và tiến hành bảo hành đổi mới. Cần gửi email xoa dịu và khéo léo xin khách cung cấp mã đơn hoặc số điện thoại.
> 
> **2. Trạng Thái Dữ Liệu:** Thiếu thông tin
> 
> **3. Email Phản Hồi:**
> Chào Quý khách,
> Cửa hàng điện máy rất xin lỗi vì trải nghiệm không mong muốn mà Quý khách đang gặp phải với sản phẩm máy sấy tóc.
> Để chúng tôi có thể tra cứu hệ thống và lập tức tiến hành thủ tục bảo hành/đổi mới, Quý khách vui lòng cung cấp giúp chúng tôi **Mã đơn hàng** hoặc **Số điện thoại** đã dùng để mua hàng. 
> Ngay khi nhận được thông tin, bộ phận kỹ thuật sẽ liên hệ và xử lý cho Quý khách trong thời gian sớm nhất.
> Mong nhận được phản hồi từ Quý khách và một lần nữa thành thật xin lỗi vì sự cố này!
> Trân trọng.
