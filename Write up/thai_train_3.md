# SSL

# SSL là gì ? - 

# Có bao nhiêu cách chứng thực SSL ?

# CSR file dùng làm gì trong quá trình tạo SSL

# Sử dụng OpenSSL để gen file CSR sau đó request SSL cho domain <name>.techtraining.zonecloud.tech


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

-Là định dạng phổ biến nhất cho X, 509 giấy chứng nhận, CSRs và khóa mật mã. Tệp PEM là tệp văn bản chứa một hoặc nhiều mục trong mã hóa Base64 ASCII, mỗi mục có đầu trang và chân trang văn bản đơn giản (ví dụ: -----BEGIN CERTIFICATE----- và -----END CERTIFICATE-----). Một tệp PEM duy nhất có thể chứa một chứng chỉ thực thể cuối, một khóa riêng tư hoặc nhiều chứng chỉ tạo thành một chuỗi tin cậy hoàn chỉnh. Hầu hết các tệp chứng chỉ được tải xuống từ SSL.com sẽ ở định dạng PEM.


# Private key ssl là gì ?

-Mỗi khi ta đăng ký một SSL, nhà cung cấp SSL sẽ cho chúng ta Certificate, Private Key và root CA.
Để có được một SSL bạn phải tạo một Certificate Signing Request (CSR) trên máy chủ, quá trình này sẽ tạo ra một khóa riêng và khóa công khai trên máy chủ

# PFX file là gì ? Cách chuyển từ file crt file sang PFX file.

-File .pfx sử dụng để bạn cài đặt ssl lên server IIS của Windows hoặc các dịch vụ hỗ trợ như: Firewall Kerio,…

# Câu lệnh:
```
pkcs12 -export -out domain.pfx -inkey domain.key -in domain.crt
```
Trong đó: (Sửa chuỗi domain thành tên bạn muốn xuất ra (với .pfx) và tên file đang có trên thư mục bin của OpenSSL).

    domain.pfx là tên file và đuôi mở rộng .pfx bạn muốn xuất ra.
    
    domain.key là tên file và đuôi mở rộng .key có trên thư mục bin của OpenSSL.
    
    domain.crt là tên file mà đuôi mở rộng .crt của Certificate có trên thư mục bin của OpenSS

-Chuyển đổi .pfx sang crt (Certificate):
```
pkcs12 -in certname.pfx -nokeys -out cert.pem
```
-Hoặc xuất bao gồm cả khóa key:
```
pkcs12 -in certname.pfx -out cert.pem
```
    Sửa certname thành tên file .pfx bạn muốn chuyển đổi.
    
    Sửa cert thành tên file .pem bạn muốn xuất ra.

-File cert.pem sẽ chưa nội dung của CA, Root,… bạn cần copy chuỗi Certificate để lưu lại thành 1 file riêng theo định dạng cert.crt. Thông thường, chuỗi Certificate nằm ở đầu file .pem được đánh dấu theo subject=tenmien. Nếu bạn cần sử dụng cả các file CA, Root,… bạn copy chuỗi CA, Root,… ra 1 file riêng. Phần mở rộng cũng là .crt.


# Domain

# Domain là gì ?

-Domain được coi như địa chỉ chính của một website trên internet, bao gồm phần tên và phần đuôi, ví dụ: tenmien.com, wikipedia.org,...

# Các trạng thái của domain:

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

-Virtual Hosts là một phương thức lưu trữ cho phép lưu nhiều tên miền khác nhau trên cùng một máy chủ Server. Virtual Hosts có thể được xem như một giải pháp cho phép bạn nhúng rất nhiều tên miền trên một địa chỉ IP của một Server duy nhất.

Có 2 loại chính Virtual Hosts: 
     
     -Name-based Virtual Hosts: Sử dụng tên miền (hoặc tên miền thứ cấp) của yêu cầu để phân biệt các trang web khác nhau. Đây là phương pháp phổ biến nhất và cho phép một máy chủ duy nhất phục vụ nhiều tên miền khác                   nhau trên cùng một địa chỉ IP. Apache HTTP Server và Nginx đều hỗ trợ Name-based Virtual Hosts.

     -IP-based Virtual Hosts: Sử dụng các địa chỉ IP khác nhau để phân biệt các trang web. Mỗi địa chỉ IP sẽ được sử dụng để phục vụ một trang web riêng biệt. Đây là phương pháp hiệu quả cho các trang web yêu cầu riêng tư hoặc         yêu cầu nhiều cấu hình bảo mật khác nhau. Apache HTTP Server, Nginx và Microsoft IIS đều hỗ trợ IP-based Virtual Hosts




# Mail Server

-Mail Server (hay còn gọi là Email Server hay máy chủ thư điện tử) là một hệ thống máy tính hoặc máy chủ được thiết lập để quản lý và xử lý các dịch vụ liên quan đến thư điện tử email. Chức năng chính của Server Mail là quản lý và lưu trữ email số lượng lớn (business email), cho nhân viên dùng gửi và nhận thư điện tử thông qua mạng

#Tìm hiểu MX Record

-MX Record được viết tắt của từ Mail Exchange Record, có nghĩa là record giúp xác định được địa chỉ của một hoặc nhiều mail server đang chịu trách nhiệm xử lý mail cho chính tên miền đó. Hiểu đơn giản hơn, việc ra đời của MX record này nhằm mục đích dùng để xác định được mail server cho một tên miền cụ thể.

![image](https://github.com/eggsy3011/ZONECLOUD-Train-3/assets/108015833/74740215-e6d0-4bb3-b48d-d12ec1eb68f9)


# Tìm hiểu DKIM, SPF, PTR

DKIM (DomainKeys Identified Mail):

    DKIM là một phương pháp xác thực email bằng cách ký số các email gửi từ một miền nhất định.
    Khi một email được gửi đi, máy chủ email của người gửi sẽ tạo một chữ ký số bằng thuật toán mã hóa và thêm vào phần tiêu đề của email dưới dạng một ghi chứng nhận DKIM.
    Máy chủ email của người nhận sau đó có thể kiểm tra chữ ký này với khóa công khai của miền gửi để xác minh tính hợp lệ của email.

SPF (Sender Policy Framework):

    SPF là một cơ chế xác định xem máy chủ email nào được ủy quyền để gửi email từ một miền cụ thể.
    Chủ sở hữu miền có thể thiết lập một bản ghi SPF trong bản ghi DNS của miền để chỉ định các máy chủ IP được phép gửi email từ miền đó.
    Máy chủ nhận có thể kiểm tra bản ghi SPF để xác định xem email được gửi từ một máy chủ IP có được phép hay không.

PTR (Pointer):

    Ghi PTR là một phần của cơ sở hạ tầng Internet được sử dụng để ánh xạ địa chỉ IP về tên miền và ngược lại.
    Đặc biệt, ghi PTR thường được sử dụng để xác định tên miền của một địa chỉ IP cụ thể.
    Ghi PTR thường được sử dụng trong việc kiểm tra đảm bảo rằng địa chỉ IP của máy chủ email có phản hồi bằng tên miền hợp lệ.

    

Debug khi khách hàng không nhận được email.

Email đến
Tệp nhật ký Postifx (máy chủ SMTP):

```
    / var / log / maillog
```

Từ đuôi bắt đầu shell trên tệp nhật ký bằng cách sử dụng lệnh này

```
    tail -f / var / log / maillog
```
Sau khi bạn đã đặt đuôi trên tệp nhật ký, hãy thử gửi email kiểm tra và trong màn hình khác theo dõi tệp nhật ký.

Email gửi đi
Từ đuôi bắt đầu shell trên tệp nhật ký bằng cách sử dụng lệnh này

```
    tail -f / var / log / maillog
```
Sau khi bạn đã đặt đuôi trên tệp nhật ký, hãy thử gửi email kiểm tra và trong màn hình khác theo dõi tệp nhật ký.

- Thử kiểm tra danh tiếng MailServer (IP)

Webmail
Tệp nhật ký (roundcube)

```
    / usr / local / cwpsrv / var / services / roundcube / logs /
```
# Các vấn đề phổ biến nhất:


    - cổng SMTP được đóng bởi nhà cung cấp máy chủ (giải pháp: cố gắng liên hệ với nhà cung cấp máy chủ của bạn)
    - rDNS / PTR chưa được đặt (giải pháp: yêu cầu nhà cung cấp thiết lập nó làm tên máy chủ của bạn)
    - tên máy chủ không có tập hợp bản ghi A hợp lệ (giải pháp: đảm bảo tên máy chủ của bạn đã hoạt động Bản ghi A)



# DNS

# DNS là gì ?

-DNS (Domain Name System – hệ thống phân giải tên miền) là một hệ thống giúp con người và máy tính giao tiếp dễ dàng hơn. Con người sử dụng tên, còn máy tính sử dụng số, DNS chính là một hệ thống giúp biên dịch tên website hay hostname thành số để máy tính có thể hiểu được. 

# Các loại recored DNS

    +A Record
    -Là DNS record đơn giản nhất và được dùng nhiều nhất dùng để trỏ tên website tới một địa chỉ IP cụ thể. Bạn có thể thêm tên mớo, TTL (Time to Live, thời gian tự động tải lại bản ghi), Points to (trỏ tới IP nào).
    
    +CNAME record
    -Là bản ghi đóng vai trò như đặt một hoặc nhiều tên khác cho tên miền chính, bạn có thể tạo một tên mới, trỏ tới tên gốc là gì, đặt TTL.
    
    +MX record
    -MX record là một bản ghi chỉ định server nào quản lý các dịch vụ email của tên miền đó. Bạn có thể trỏ tên miền tới mail server, đặt mức độ ưu tiên (priority), đặt TTL.
   
    +TXT record
    -Là record giúp bạn chứa các thông tin dạng text (văn bản) của tên miền, bạn có thể thêm Host mới, Giá trị TXT, TTL (Time to Live), Points to.
    
    +AAAA record
    -Cũng là A record, nhưng dùng để trỏ domain tới một địa chỉ IPV6 address. Bạn có thể thêm host mới, IPv6, TTL.
    
    +NS record
    -Là DNS server records của tên miền giúp bạn chỉ định nameserver cho từng tên miền phụ. Bạn có thể tạo host mới, tên nameserver (NS), TTL (Time to Live).
    
    +SRV record
    -Là bản ghi đặc biệt trong Domain Name System dùng để xác định chính xác dịch vụ nào chạy port nào, tại đây bạn có thể thêm Priority, Name, Weight, Port, Points to, TTL.


# Nguyên tắc làm việc của DNS

-DNS hoạt động theo từng bước theo cấu trúc của DNS. Bước đầu tiên gọi là DNS query, một truy vấn để lấy thông tin.

- Ta sử dụng tình huống tìm kiếm website bằng cách gõ tên miền vào trong web browser (ví dụ, www.google.com). Đầu tiên, DNS server sẽ tìm thông tin phân giải trong filehosts
– một file text trong hệ điều hành chịu trách nhiệm chuyển hostname thành địa chỉ IP. Nếu không thấy thông tin, nó sẽ tìm trọng cache 
– bộ nhớ tạm của phần cứng hay phần mềm. Nơi phổ biến nhất lưu thông tin cache này là  bộ nhớ tạm của trình duyệt và bộ nhớ tạm của Internet Service Providers (ISP). Nếu không nhận được thông tin, bạn sẽ thấy mã lỗi hiện lên.

# Cách phân giải địa chỉ DNS

![image](https://github.com/eggsy3011/ZONECLOUD-Train-3/assets/108015833/b040b4bc-fbb4-4351-8b80-5cee0f77f8aa)

-Khi người dùng muốn truy cập vào một website, hay kiểm tra email, hay bất kỳ một tác vụ nào liên quan đến tên miền, sẽ có vài công đoạn kết nối:

    Máy tính sẽ gửi một câu lệnh phân giải tên miền, DNS query, để tìm máy chủ cần thiết. Câu lệnh này được gửi đến cấu hình phân giải tên miền, DNS resolver ở máy tính người dùng, hoặc ISP cung cấp dịch vụ Internet cho ngườ dùng.
    
    Các máy chủ DNS resolver này hoặc kiểm tra mới, hoặc tìm trong cache lưu trữ name server của tên miền, và sẽ gửi chuyển tiếp câu lệnh phân giải tên miền đến các máy chủ chứa các bản ghi DNS của tên miền.
    
    Các máy chủ name server của tên miền tìm trong cơ sở dữ liệu của mình thông tin về tên miền, nếu có thì trả về giá trị địa chỉ IP về cho thiết bị của người dùng.Từ đó, thiết bị của người dùng có thể tiếp tục gửi các câu lệnh giao tiếp khác trực tiếp đến server hosting.




