SSL

SSL là gì ? - 

Có bao nhiêu cách chứng thực SSL ?

CSR file dùng làm gì trong quá trình tạo SSL

Sử dụng OpenSSL để gen file CSR sau đó request SSL cho domain <name>.techtraining.zonecloud.tech


# 1. Kiểm tra OpenSSL

Trước khi thực hiện việc khởi tạo CSR chúng ta cần phải kiểm tra OpenSSL đã được cài đặt trên máy chủ của mình chưa
```
openssl version
```

![image](https://github.com/eggsy3011/ZONECLOUD-Train-3/assets/108015833/45deba28-bd1a-4a04-b7a7-7f61d5877160)


# 2. Tiến hành tạo private key và CSR

Khởi tạo file private key
```
mkdir thai.techtraining.zonecloud.tech
```
```
cd thai.techtraining.zonecloud.tech
```
```
openssl genrsa -out thai.techtraining.zonecloud.tech.key 2048
```
![image](https://github.com/eggsy3011/ZONECLOUD-Train-3/assets/108015833/54dfbd5a-95aa-4b7d-bee9-6fb83ad38893)



# 3. Khởi tạo CSR với input private key vừa tạo
```
openssl req -new -key thai.techtraining.zonecloud.tech.key -out  thai.techtraining.zonecloud.tech.csr
```

![image](https://github.com/eggsy3011/ZONECLOUD-Train-3/assets/108015833/7922287d-ba23-4a77-a374-47d32e79f4d5)


    Country Name (2 letter code) []: Mã quốc gia theo chuẩn ISO 3166-1 alpha-2 (2 ký tự : VN, UK, US)
    State or Province Name (full name) []: Tên tỉnh thành
    Locality Name (eg, city) []: Tên thành phố/quận huyện
    Organization Name (eg, company) []: Tên công ty, doanh nghiệp
    Organizational Unit Name (eg, section) []: Lĩnh vực hoạt động
    Common Name (eg, fully qualified host name) []: Domain của website cần chứng thực ( Ví dụ: vietnix.cloud )
    Email Address []: Địa chỉ Email


# Pem file là gì ?

là định dạng phổ biến nhất cho X, 509 giấy chứng nhận, CSRs và khóa mật mã. Tệp PEM là tệp văn bản chứa một hoặc nhiều mục trong mã hóa Base64 ASCII, mỗi mục có đầu trang và chân trang văn bản đơn giản (ví dụ: -----BEGIN CERTIFICATE----- và -----END CERTIFICATE-----). Một tệp PEM duy nhất có thể chứa một chứng chỉ thực thể cuối, một khóa riêng tư hoặc nhiều chứng chỉ tạo thành một chuỗi tin cậy hoàn chỉnh. Hầu hết các tệp chứng chỉ được tải xuống từ SSL.com sẽ ở định dạng PEM.


# Private key ssl là gì ?

Mỗi khi ta đăng ký một SSL, nhà cung cấp SSL sẽ cho chúng ta Certificate, Private Key và root CA.
Để có được một SSL bạn phải tạo một Certificate Signing Request (CSR) trên máy chủ, quá trình này sẽ tạo ra một khóa riêng và khóa công khai trên máy chủ

PFX file là gì ? Cách chuyển từ file crt file sang PFX file.

File .pfx sử dụng để bạn cài đặt ssl lên server IIS của Windows hoặc các dịch vụ hỗ trợ như: Firewall Kerio,…

Câu lệnh:
```
pkcs12 -export -out domain.pfx -inkey domain.key -in domain.crt
```
Trong đó: (Sửa chuỗi domain thành tên bạn muốn xuất ra (với .pfx) và tên file đang có trên thư mục bin của OpenSSL).

    domain.pfx là tên file và đuôi mở rộng .pfx bạn muốn xuất ra.
    domain.key là tên file và đuôi mở rộng .key có trên thư mục bin của OpenSSL.
    domain.crt là tên file mà đuôi mở rộng .crt của Certificate có trên thư mục bin của OpenSS

Chuyển đổi .pfx sang crt (Certificate):
```
pkcs12 -in certname.pfx -nokeys -out cert.pem
```
Hoặc xuất bao gồm cả khóa key:
```
pkcs12 -in certname.pfx -out cert.pem
```
    Sửa certname thành tên file .pfx bạn muốn chuyển đổi.
    Sửa cert thành tên file .pem bạn muốn xuất ra.

File cert.pem sẽ chưa nội dung của CA, Root,… bạn cần copy chuỗi Certificate để lưu lại thành 1 file riêng theo định dạng cert.crt. Thông thường, chuỗi Certificate nằm ở đầu file .pem được đánh dấu theo subject=tenmien. Nếu bạn cần sử dụng cả các file CA, Root,… bạn copy chuỗi CA, Root,… ra 1 file riêng. Phần mở rộng cũng là .crt.

Bài tập: Trả lời các câu hỏi bên trên và thực hiện yêu cầu sau đó note vào file markdown tại: <name>/hosting-webserver/basic/ssl.md

Domain

Domain là gì ?

Domain được coi như địa chỉ chính của một website trên internet, bao gồm phần tên và phần đuôi, ví dụ: tenmien.com, wikipedia.org,...

Các trạng thái của domain.

    Available: Tên miền có sẵn để đăng ký.
    Registered: Tên miền đã được đăng ký bởi một cá nhân hoặc tổ chức.
    Active: Tên miền đã được cấu hình và đang hoạt động trên mạng.
    Expired: Tên miền đã hết hạn và không được gia hạn kịp thời.
    Redemption: Tên miền đã hết hạn và đang trong giai đoạn gia hạn đặc biệt (thường kéo dài 30 ngày) trước khi bị xóa.
    Pending Deletion: Tên miền đã qua giai đoạn redemption và sắp bị xóa khỏi cơ sở dữ liệu đăng ký.
    Deleted: Tên miền đã bị xóa và sẽ trở lại trạng thái có sẵn để đăng ký.


# Subdomain là gì?

-Subdomain là một phần mở rộng của Domain chính, được tạo ra để phân chia website thành các khu vực riêng biệt. Subdomain nằm trước Domain chính và được phân cách bằng dấu chấm. Ví dụ: blog.google.com, shop.wikipedia.org,..
Ví dụ về Subdomain

-Giả sử bạn có một tên miền chính là example.com, bạn có thể tạo các subdomain khác nhau như:

    blog.example.com: Dùng cho blog.
    shop.example.com: Dùng cho cửa hàng trực tuyến.
    support.example.com: Dùng cho trang hỗ trợ khách hàng.

# Virtual Hosts là gì?

Virtual Hosts là một phương thức lưu trữ cho phép lưu nhiều tên miền khác nhau trên cùng một máy chủ Server. Virtual Hosts có thể được xem như một giải pháp cho phép bạn nhúng rất nhiều tên miền trên một địa chỉ IP của một Server duy nhất.

Có 2 loại chính Virtual Hosts: 
     
     Name-based Virtual Hosts: Sử dụng tên miền (hoặc tên miền thứ cấp) của yêu cầu để phân biệt các trang web khác nhau. Đây là phương pháp phổ biến nhất và cho phép một máy chủ duy nhất phục vụ nhiều tên miền khác                   nhau trên cùng một địa chỉ IP. Apache HTTP Server và Nginx đều hỗ trợ Name-based Virtual Hosts.

     IP-based Virtual Hosts: Sử dụng các địa chỉ IP khác nhau để phân biệt các trang web. Mỗi địa chỉ IP sẽ được sử dụng để phục vụ một trang web riêng biệt. Đây là phương pháp hiệu quả cho các trang web yêu cầu riêng tư hoặc         yêu cầu nhiều cấu hình bảo mật khác nhau. Apache HTTP Server, Nginx và Microsoft IIS đều hỗ trợ IP-based Virtual Hosts




Mail Server

Tìm hiểu MX Record

Tìm hiểu DKIM, SPF, PTR

Debug khi khách hàng không nhận được email.




DNS

DNS là gì ?

Các loại recored DNS

Nguyên tắc làm việc của DNS

Cách phân giải địa chỉ DNS


