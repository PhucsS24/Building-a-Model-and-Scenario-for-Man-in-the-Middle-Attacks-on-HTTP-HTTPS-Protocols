# Building a Model and Scenario for Man-in-the-Middle Attacks on HTTP-HTTPS Protocols

**Sinh viên thực hiện:**
- Nguyễn Hoàng Phúc - 20520277
- Đoàn Đỗ Lâm Trường - 20520338
- Phạm Văn Ngọ - 20520254
- Trương Văn Hiệp - 20521313

## I. Giới thiệu

### 1. Mục tiêu đồ án
- **Xây dựng mô hình Active Directory**: Tạo một mô hình đơn giản để mô phỏng môi trường thực tế.
- **Lên kịch bản tấn công Man-in-the-Middle (MITM)**: Mô phỏng các cuộc tấn công MITM vào máy client trong Active Directory.
- **Sử dụng kỹ thuật MITM**:
  - ARP Spoofing: Đánh lừa máy client để chuyển hướng lưu lượng mạng.
  - DNS Spoofing: Thay đổi thông tin DNS để điều hướng các yêu cầu tới máy chủ giả mạo.
  - LLMNR Poisoning: Khai thác các yêu cầu không thành công để đánh lừa máy client gửi thông tin đăng nhập tới attacker.
  - Kerberos Golden Ticket: Tạo vé vàng Kerberos để chiếm quyền truy cập cao nhất vào hệ thống.
- **Theo dõi và thu thập thông tin**: Sniffing dữ liệu, thu thập thông tin nhạy cảm như tài khoản mạng xã hội (LinkedIn, Facebook), email, và tài khoản của client trong Active Directory.
- **Chiếm quyền kiểm soát hệ thống**: Truy cập trái phép để khai thác dữ liệu quan trọng trong Active Directory.
- **Tấn công Social Engineering**: Sử dụng các phương pháp như Mail Phishing để khai thác và thu thập thông tin từ các nạn nhân trong Active Directory.

### 2. Kỹ thuật tấn công
- **ARP Spoofing**: Thay đổi thông tin ARP để đánh lừa các thiết bị trong mạng, giúp attacker kiểm soát luồng dữ liệu.
- **DNS Spoofing**: Thay đổi địa chỉ IP của máy chủ DNS để hướng người dùng đến các trang web giả mạo.
- **Social Engineering (Mail Phishing)**: Gửi email giả mạo để lừa nạn nhân cung cấp thông tin hoặc tải về malware.
- **LLMNR Poisoning**: Khai thác giao thức LLMNR để thu thập thông tin đăng nhập của người dùng.
- **Kerberos Golden Ticket**: Tạo một vé Kerberos với quyền cao nhất để truy cập vào hệ thống mà không bị phát hiện.

### 3. Tools
- **Zenmap**: Dùng để quét và thu thập thông tin về các thiết bị và dịch vụ trong mạng.
- **Bettercap, Mitmproxy**: Thực hiện tấn công MITM và kiểm soát lưu lượng dữ liệu qua mạng.
- **SET (Social-Engineer Toolkit), Responder**: Thực hiện các cuộc tấn công Social Engineering và LLMNR Poisoning.
- **Hashcat**: Giải mã các hash mật khẩu để lấy thông tin đăng nhập.
- **Psexec.py, Mimikatz**: Truy cập từ xa vào hệ thống với quyền cao nhất và khai thác thông tin nhạy cảm.

### 4. Mô hình
![Model Diagram](link_to_your_image)

### 5. Tổng quan kịch bản
1. **Footprinting**:
   - Sử dụng Zenmap để quét mạng, thu thập thông tin về các máy trong mạng và phát hiện các dịch vụ trong Active Directory.
   
2. **Tấn công ARP Spoofing, DNS Spoofing, Mail Phishing**:
   - Tấn công máy client2 (IP: 192.168.244.139) bằng cách đánh lừa máy này tải về PDF chứa malware và chứng chỉ Mitmproxy. Mục tiêu là chiếm quyền kiểm soát máy client2 và thu thập thông tin tài khoản mạng xã hội, email, và các file quan trọng.

3. **Chiếm quyền kiểm soát mail client2**:
   - Sử dụng thông tin đăng nhập của client2 để gửi email giả mạo đến Administrator, lừa Administrator nhập sai địa chỉ IP trong phần File Sharing. Sau đó, thực hiện tấn công LLMNR Poisoning để lấy được hash NTLMv2 và giải mã bằng Hashcat để có được mật khẩu của Administrator.

4. **Truy cập máy Administrator**:
   - Dùng mật khẩu đã lấy được, sử dụng PsExec để truy cập CMD của máy Administrator với quyền cao nhất. Sau đó, sử dụng Mimikatz để khai thác thông tin trong Active Directory như username, password của tất cả user, thông tin group, và dữ liệu lưu trữ local.

## II. Demo
- **Video Demo:** [Watch on YouTube](link_to_your_video)
- **Report:** [Download PDF](link_to_your_report)
