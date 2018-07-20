# Network and Storage
## Virtual Netwworking
Thành phần chính của mạng libvirt là mạng chuyển mạch ảo, còn được gọi là bridge. Trên Linux Bridge có thể sử dụng không giới hạn các port ảo. Tương tự như switch vật lý, bridge tìm hiểu địa chỉ MAC từ các gói nhận được và lưu các địa chỉ MAC đó vào bảng MAC. Các quyết định chuyển tiếp gói tin được lấy dựa trên địa chỉ MAC mà nó đã học và được lưu trữ trong bảng MAC.  
Các interface được gắn vào các port của bridge được gọi là TAP. TUN là "tunnel" mô phỏng thiết bị và hoạt động lớp 3 trong mô hình OSI, TAP mô phỏng thiết bị và hoạt động ở lớp 2.  
### Virtual networking using libvirt
libvirt có một số tùy chọn mạng ảo trong libvirt.  
1. Isolated Virtual Network  
Ở mode này, chỉ các VM được thêm vào mạng mới có thể giao tiếp với nhau.  
2. Routed Virtual Network  
Mạng ảo sẽ được kết nối với mạng vật lý bằng cách sử dụng các tuyến IP được chỉ định tren hypervisor. Các tuyến IP này được sử dụng để định tuyến lưu lượng truy cập từ các VM tới mạng kết nối với hypervisor.  
3. NATed Virtual Network  
Mode này cho phép các VM giao tiếp với mạng bên ngoài mà không cần sử dụng bất kỳ cấu hình bổ sung nào.  
4. Bridge network  
VM sẽ hoạt động như một hệ thống nằm trong cùng một mạng với NIC vật lý.  
5. MacVTap  
MacVTap sử dụng khi không muốn tạo normal bridge nhưng vẫn muốn người dùng trong mạng cục bộ truy cập vào VM.  

## Storage 
### Creating a disk image
Có 2 loại disk  
- Preallocated: Loại disk này sẽ gán toàn bộ không gian ổ đĩa ngay khi tạo, nó có tốc độ ghi nhanh.  
- Thin-Provisioned: Loại disk này không gian sẽ chỉ được phân bổ khi cần, nó giúp tiết kiệm không gian đĩa.  

Tạo disk image Preallocated
```
dd if=/dev/zero of=dbvm_disk2.img bs=1G count=10
```
Tạo disk image Thin
```
dd if=/dev/zero of=dbvm_disk2_seek.img bs=1G seek=10 count=0
```

