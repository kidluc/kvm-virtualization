# Setting Up Standalone KVM Virtualization
## Host System Requirements
- Intel or AMD 64-bit CPU that has virtualizatino extension  
- 2GB RAM  
- 8GB free disk on KVM hypervisor after Linux OS installation  
- 100Mbps network.  

### Physical CPU
Intel hoặc AMD 64-bit CPU có hỗ trợ virtualization. Có thể kiểm trả bằng lệnh xem CPU có hỗ trợ không bằng lệnh  
```
grep --color -Ew 'svm|vmx|lm' /proc/cpuinfo
```
Nếu có svm nghĩa là CPU có AMD-V, vmx nghĩa là CPU có VT-x, và lm nghĩa là hỗ trợ 64 bit.  
Kiểm tra xem các module đã được nạp tự động hay chưa  
```
lsmod | grep kvm
```
### Physical memory
Nếu không có ý định overcommitting (sử dụng tài nguyên ảo nhiều hơn tài nguyên vật lý): RAM - 2GB = Số lượng RAM dùng cho VM.  
Nếu bạn định overcommitting: RAM - (2GB + .5 * (RAM/64)) = Số lượng RAM dùng cho VM.  
### SWAP
- 2GB nếu có <= 4GB RAM  
- 4GB nếu có 4-16GB RAM  
- 8GB nếu có 16-64GB RAM  
- 16GB nếu có 64-256GB RAM  

Nếu có ý định overcommitting: SWAP = (RAM * 0.5) + SWAP for OS  

## Setting up the environment
### Kiểm tra cấu hình hệ thống KVM
Sử dụng lệnh dưới để kiểm tra để xác nhận host có đủ khả năng đẻ chạy các trình điều khiển hypervisor libvirt.  
```
virt-host-validate
```
