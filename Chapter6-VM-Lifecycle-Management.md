# Migrate
Migrate là quá trình move 1 VM từ host này sang host khác với downtime nhỏ.
## Offline Migrate
Offline Migrate tạm dừng VM rồi di chuyển VM đến host đích sau đó được bật lại tại host đích.  
## Live Migrate
Trong kiểu migrate này, VM được di chuyển đến host đích trong khi nó đang chạy trên host nguồn. Quá trình này vô hình với người dùng đang sử dụng VM. 
## Các lưu ý khi Migrate
- VM nên sử dụng storage pool được tạo trong 1 vùng share storage  
- Virtual network được sử dụng bởi các VM nên có sẵn trên cả 2 Host  
- Thời gian của host nguồn và đích nên được đồng bộ  

