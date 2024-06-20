SSL

SSL là gì ?

Có bao nhiêu cách chứng thực SSL ?

CSR file dùng làm gì trong quá trình tạo SSL

Sử dụng OpenSSL để gen file CSR sau đó request SSL cho domain <name>.techtraining.zonecloud.tech


1. Kiểm tra OpenSSL

Trước khi thực hiện việc khởi tạo CSR chúng ta cần phải kiểm tra OpenSSL đã được cài đặt trên máy chủ của mình chưa

openssl version

Tiến hành tạo private key và CSR

Khởi tạo file private key

mkdir thai.techtraining.zonecloud.tech

cd thai.techtraining.zonecloud.tech

openssl genrsa -out thai.techtraining.zonecloud.tech.key 2048




Khởi tạo CSR với input private key vừa tạo

openssl req -new -key thai.techtraining.zonecloud.tech.key -out  thai.techtraining.zonecloud.tech.csr


Pem file là gì ?

Private key ssl là gì ?

PFX file là gì ? Cách chuyển từ file crt file sang PFX file.

Bài tập: Trả lời các câu hỏi bên trên và thực hiện yêu cầu sau đó note vào file markdown tại: <name>/hosting-webserver/basic/ssl.md

Domain

Domain là gì ?

Các trạng thái của domain

Subdomain là gì?

Virtual Hosts là gì?

Bài tập: Trả lời các câu hỏi bên trên và thực hiện yêu cầu sau đó note vào file markdown tại: <name>/hosting-webserver/basic/domain.md


Mail Server

Tìm hiểu MX Record

Tìm hiểu DKIM, SPF, PTR

Debug khi khách hàng không nhận được email.

Bài tập: Trả lời các câu hỏi bên trên và thực hiện yêu cầu sau đó note vào file markdown tại: <name>/hosting-webserver/basic/mail.md


DNS

DNS là gì ?

Các loại recored DNS

Nguyên tắc làm việc của DNS

Cách phân giải địa chỉ DNS

Bài tập: Trả lời các câu hỏi bên trên và thực hiện yêu cầu sau đó note vào file markdown tại: <name>/hosting-webserver/basic/dns.md
