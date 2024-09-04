# Building a Model and Scenario for Man-in-the-Middle Attacks on HTTP-HTTPS Protocols

**Sinh viên thực hiện:**
- Nguyễn Hoàng Phúc - 20520277
- Đoàn Đỗ Lâm Trường - 20520338
- Phạm Văn Ngọ - 20520254
- Trương Văn Hiệp - 20521313

## I. Giới thiệu

### 1. Mục tiêu đồ án
- Xây dựng mô hình Active Directory đơn giản và lên kịch bản tấn công Man-in-the-Middle vào máy client trong Active Directory.
- Sử dụng các kỹ thuật tấn công Man-in-the-Middle như ARP Spoofing, DNS Spoofing, LLMNR Poisoning, Kerberos Golden Ticket để theo dõi, sniffing các dữ liệu, thông tin quan trọng truyền trong mạng từ đó có được thông tin các tài khoản quan trọng như tài khoản mạng xã hội LinkedIn, Facebook, email, và các tài khoản của client trong Active Directory.
- Chiếm quyền kiểm soát, truy cập trái phép vào hệ thống để khai thác các dữ liệu quan trọng trong Active Directory.
- Sử dụng các kỹ thuật tấn công Social Engineering, Mail Phishing để khai thác và thu thập thông tin của các Victim trong Active Directory.

### 2. Kỹ thuật tấn công
- ARP Spoofing
- DNS Spoofing
- Social Engineering (Mail Phishing)
- LLMNR Poisoning
- Kerberos Golden Ticket

### 3. Tools
- Zenmap
- Bettercap, Mitmproxy
- SET, Responder
- Hashcat
- Psexec.py, Mimikatz

### 4. Mô hình
![Model Diagram](link_to_your_image)

### 5. Tổng quan kịch bản
- **Footprinting**: Sử dụng Zenmap để thu thập thông tin các máy trong mạng và phát hiện ra các máy và các dịch vụ trong AD.
- **Tấn công ARP Spoofing, DNS Spoofing, Mail Phishing**: Tấn công máy client2 có IP 192.168.244.139 nhằm lừa máy này tải về PDF có chứa malware và chứng chỉ Mitmproxy để chiếm quyền kiểm soát và thu thập thông tin xã hội cũng như các file quan trọng trong máy client2 (bao gồm thông tin tài khoản MXH như LinkedIn, mail, Facebook, v.v.).
- **Chiếm quyền kiểm soát mail client2**: Sau khi có được username và password mail của client2, attacker sử dụng mail của client2 để gửi mail giả mạo đến Administrator nhằm lừa Administrator nhập sai địa chỉ IP trong phần File Sharing, sau đó thực hiện tấn công LLMNR Poisoning để lấy được Hash NTLMv2 và giải mã với Hashcat để có được password của máy Administrator.
- **Truy cập máy Administrator**: Sau khi có được password, attacker sử dụng PsExec để kết nối đến CMD của máy Administrator với quyền cao nhất, sau đó sử dụng Mimikatz để khai thác dữ liệu như thông tin trong AD bao gồm username, password của tất cả user trong AD, thông tin group, và dữ liệu lưu trữ local.

## II. Demo
- **Video Demo:** [Link YouTube](link_to_your_video)
- **Report:** [Link PDF](link_to_your_report)
