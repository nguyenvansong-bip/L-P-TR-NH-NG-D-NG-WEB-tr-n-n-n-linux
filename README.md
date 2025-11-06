Nguyễn Văn Song

k215480106043

k57KMT

Bài Tập 3

Yêu cầu     : LẬP TRÌNH ỨNG DỤNG WEB trên nền linux
1. Cài đặt môi trường linux: SV chọn 1 trong các phương án
 - enable wsl: cài đặt docker desktop
 - enable wsl: cài đặt ubuntu
 - sử dụng Hyper-V: cài đặt ubuntu
 - sử dụng VMware : cài đặt ubuntu
 - sử dụng Virtual Box: cài đặt ubuntu
2. Cài đặt Docker (nếu dùng docker desktop trên windows thì nó có ngay)
3. Sử dụng 1 file docker-compose.yml để cài đặt các docker container sau: 
   mariadb (3306), phpmyadmin (8080), nodered/node-red (1880), influxdb (8086), grafana/grafana (3000), nginx (80,443)
4. Lập trình web frontend+backend:
 SV chọn 1 trong các web sau:
 4.1 Web thương mại điện tử
 - Tạo web dạng Single Page Application (SPA), chỉ gồm 1 file index.html, toàn bộ giao diện do javascript sinh động.
 - Có tính năng login, lưu phiên đăng nhập vào cookie và session
   Thông tin login lưu trong cơ sở dữ liệu của mariadb, được dev quản trị bằng phpmyadmin, yêu cầu sử dụng mã hoá khi gửi login.
   Chỉ cần login 1 lần, bao giờ logout thì mới phải login lại.
 - Có tính năng liệt kê các sản phẩm bán chạy ra trang chủ
 - Có tính năng liệt kê các nhóm sản phẩm
 - Có tính năng liệt kê sản phẩm theo nhóm
 - Có tính năng tìm kiếm sản phẩm
 - Có tính năng chọn sản phẩm (đưa sản phẩm vào giỏ hàng, thay đổi số lượng sản phẩm trong giỏ, cập nhật tổng tiền)
 - Có tính năng đặt hàng, nhập thông tin giao hàng => được 1 đơn hàng.
 - Có tính năng dành cho admin: Thống kê xem có bao nhiêu đơn hàng, call để xác nhận và cập nhật thông tin đơn hàng. chuyển cho bộ phận đóng gói, gửi bưu điện, cập nhật mã COD, tình trạng giao hàng, huỷ hàng,...
 - Có tính năng dành cho admin: biểu đồ thống kê số lượng mặt hàng bán được trong từng ngày. (sử dụng grafana)
 - backend: sử dụng nodered xử lý request gửi lên từ javascript, phản hồi về json.
 4.2 Web IOT: Giám sát dữ liệu IOT.
 - Tạo web dạng Single Page Application (SPA), chỉ gồm 1 file index.html, toàn bộ giao diện do javascript sinh động.
 - Có tính năng login, lưu phiên đăng nhập vào cookie và session
   Thông tin login lưu trong cơ sở dữ liệu của mariadb, được dev quản trị bằng phpmyadmin, yêu cầu sử dụng mã hoá khi gửi login.
   Chỉ cần login 1 lần, bao giờ logout thì mới phải login lại.
 - hiển thị giá trị mới nhất của các thông số đang giám sát, khi click vào thì hiển thị đồ thị lịch sử quá trình thay đổi (gọi grafana iframe để hiển thị)
 - backend: Sử dụng nodered để đọc dữ liệu từ các cảm biến (có thể dùng api online để lấy dữ liệu theo giời gian thực), 
   nodered sẽ lưu dữ liệu mới nhất (dạng update) vào cơ sở dữ liệu mariadb (sử dụng phpmyadmin để tạp table và quản trị lần đầu)
   nodered sẽ lưu dữ liệu (insert) vào influxdb để lưu giá trị lịch sử, để cho grafana dùng để hiển thị biểu đồ.
5. Nginx làm web-server
 - Cấu hình nginx để chạy được website qua url http://fullname.com  (thay fullname bằng chuỗi ko dấu viết liền tên của bạn)
 - Cấu hình nginx để http://fullname.com/nodered truy cập vào nodered qua cổng 80, (dù nodered đang chạy ở port 1880)
 - Cấu hình nginx để http://fullname.com/grafana truy cập vào grafana qua cổng 80, (dù grafana đang chạy ở port 3000)
 - 
Bài Làm

Cài đặt môi trường linux

PHẦN 1: BẬT WSL VÀ CÀI UBUNTU

Bước 1: Bật WSL và Virtual Machine Platform

<img width="842" height="506" alt="Ảnh chụp màn hình 2025-10-24 193914" src="https://github.com/user-attachments/assets/2eba272e-d6d3-4f44-bf7c-cb44a92e012a" />
Bước 2: Cài đặt WSL2

<img width="771" height="472" alt="Ảnh chụp màn hình 2025-10-24 195049" src="https://github.com/user-attachments/assets/fe5b03b6-84e0-40fe-826e-91d587277945" />
Bước 3: Cài Ubuntu

<img width="520" height="397" alt="Ảnh chụp màn hình 2025-10-24 195324" src="https://github.com/user-attachments/assets/e44042b2-1d74-438f-906e-c89c0e80589b" />
Bước 4: Cập nhật Ubuntu

<img width="954" height="1026" alt="Ảnh chụp màn hình 2025-10-24 203538" src="https://github.com/user-attachments/assets/595ec0dd-9f9c-4436-a24d-7f7cec2ec628" />
PHẦN 2: CÀI ĐẶT DOCKER DESKTOP

Bước 1: Tải Docker Desktop

<img width="1920" height="1080" alt="Ảnh chụp màn hình 2025-10-24 204024" src="https://github.com/user-attachments/assets/801624a5-7c2c-4b9e-8ed6-4478170ddf8a" />
Bước 2: Cài đặt

<img width="705" height="485" alt="Ảnh chụp màn hình 2025-10-24 204519" src="https://github.com/user-attachments/assets/4081be5b-502c-428a-9212-6dcb808ff09e" />
Bước 3: Kiểm tra WSL integration trong Docker

<img width="957" height="1003" alt="Ảnh chụp màn hình 2025-10-24 210613" src="https://github.com/user-attachments/assets/7bc19b17-9442-4b08-9243-60e43d429896" />
Bước 4: Kiểm tra Docker hoạt động

<img width="849" height="509" alt="Ảnh chụp màn hình 2025-10-24 223410" src="https://github.com/user-attachments/assets/82b9c417-f2c7-46ba-af44-2de54542a7d7" />
<img width="777" height="610" alt="Ảnh chụp màn hình 2025-10-24 223420" src="https://github.com/user-attachments/assets/12a7c94d-28f1-4523-88ec-cd52dfbfecc5" />
<img width="923" height="507" alt="Ảnh chụp màn hình 2025-10-27 203221" src="https://github.com/user-attachments/assets/d06ee9b1-9b03-4f49-94f9-b77c24189a80" />

3. Sử dụng 1 file docker-compose.yml để cài đặt các docker container sau: 

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1586e91b-640a-477e-b07c-1a7f4b665bba" />

4. Lập trình web frontend+backend:

Web IOT: Giám sát dữ liệu IOT.

Tạo web dạng Single Page Application (SPA), chỉ gồm 1 file index.html, toàn bộ giao diện do javascript sinh động:

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/57111daa-a1f3-4b5c-ab2d-dd74487e8366" />

Có tính năng login, lưu phiên đăng nhập vào cookie và session Thông tin login lưu trong cơ sở dữ liệu của mariadb, được dev quản trị bằng phpmyadmin, yêu cầu sử dụng mã hoá khi gửi login.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8963934e-c13b-422b-ba46-4f2ca6432ecf" />

: Chuẩn bị môi trường

<img width="1107" height="615" alt="Ảnh chụp màn hình 2025-10-27 210032" src="https://github.com/user-attachments/assets/672c51e8-7694-4999-9a2a-02479a70a98f" />

: Tạo cơ sở dữ liệu
<img width="870" height="509" alt="Ảnh chụp màn hình 2025-10-31 221610" src="https://github.com/user-attachments/assets/4db77cf6-9ee7-4d59-b043-67baa7d2b7be" />
<img width="875" height="501" alt="Ảnh chụp màn hình 2025-10-31 221634" src="https://github.com/user-attachments/assets/cd5f2272-5cdd-464b-8651-a9c20c96ab24" />
<img width="874" height="506" alt="Ảnh chụp màn hình 2025-10-31 221645" src="https://github.com/user-attachments/assets/e86f4dd6-d6d8-404c-af3b-b90bd7c203a2" />

5. Nginx làm web-server

Cấu hình nginx để chạy được website qua url http://nguyenvansong2003.com
   
<img width="1920" height="1080" alt="Ảnh chụp màn hình 2025-11-06 201753" src="https://github.com/user-attachments/assets/44bd7545-dcc8-4903-a66e-6d0aed443f26" />

Cấu hình nginx để http://nguyenvansong2003/.com/nodered/ truy cập vào nodered qua cổng 80

<img width="1920" height="1080" alt="Ảnh chụp màn hình 2025-11-06 201804" src="https://github.com/user-attachments/assets/5815afb2-4249-42ee-9205-ecf054ca7aaa" />

Cấu hình nginx để http://nguyenvansong2003/grafana.com/grafana truy cập vào grafana qua cổng 80

<img width="1920" height="1080" alt="Ảnh chụp màn hình 2025-11-06 201417" src="https://github.com/user-attachments/assets/201602ee-a63d-4a8b-bb69-d1f630c00f32" />








