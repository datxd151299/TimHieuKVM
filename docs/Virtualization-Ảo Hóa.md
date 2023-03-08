# Virtualization - Ảo Hóa
## Mục Lục
 [1. Virtualization?](#Virtualization)

 [2. Các loại ảo ảo hóa](#cacloaiaohoa)
<a name="Virtualization"></a>
## 1. Virtualization?
-   Virualization, hay còn gọi là ảo hóa, là một công nghệ được thiết kế để tạo ra tầng trung gian giữa hệ thống phần cứng và phần mềm chạy trên nó. Ý tưởng của công nghệ ảo hóa máy chủ là từ một máy vật lý đơn lẻ có thể tạo thành nhiều máy ảo độc lập. Mỗi một máy ảo đều có một thiết lập nguồn hệ thống riêng rẽ, hệ điều hành riêng và các ứng dụng riêng. Ảo hóa có nguồn gốc từ việc phân chia ổ đĩa, chúng phân chia một máy chủ thực thành nhiều máy chủ logic. Một khi máy chủ thực được chia, mỗi máy chủ logic có thể chạy một hệ điều hành và các ứng dụng độc lập.

***NOTE: Tóm lại, ảo hóa là phương pháp để tạo ra phiên bản ảo hóa trên máy tính vật lý***

<a name="cacloaiaohoa"></a>
## 2. Các loại ảo hóa
-   Có các loại ảo hóa cơ bản như sau
    1. Server Virtualization
    2. Desktop Virtualization
    3. Application Virtualization
    4. Network Virtualization
    5. Storage Virtualization

- Nhưng trong phần bài viết này chúng ta chủ yếu tìm hiểu về ảo hóa hệ thống  máy chủ (Server Virtualization)
- Ảo hóa hệ thống máy chủ cho phép chúng ta chạy nhiều máy ảo (VM) trên một máy vật lý, đem lại nhiều lợi ích như tăng tính di động, dễ dàng thiết lập với các máy chủ ảo, giúp việc quản lý chia sẻ tài nguyên tốt hơn, quản lý luồng làm việc phù hợp với nhu cầu, tăng hiệu suất làm việc của một máy chủ vật lý
- Xét về kiến trúc mô hình ảo hóa hệ thống máy chủ có thể hai dạng sau ***Host-based*** và ***Hypervisor-based***
- Trước hết đi vào tìm hiểu kiến trúc của 2 mô hình thì chúng ta cần tìm hiểu về khái niệm của Hypervisor như sau
```
Hypervisor là các phầm mềm công nghệ để tạo ra máy ảo và có chức năng chính là giám sát và điều khiển máy ảo.Nó được sử dụng để tạo, startup, dừng và reset lại các máy ảo. Các hypervisor cho phép mỗi VM hoặc “guest” truy cập vào lớp tài nguyên phần cứng vật lý bên dưới, chẳng hạn như CPU, RAM và lưu trữ
```
### Hypervisor-based (Hypervisor 1)
Kiến trúc này lớp phần mềm hypervisor chạy trực tiếp trên nền tảng phần cứng của máy chủ, không thông qua bất kì một hệ điều hành hay một nền tảng khác. Qua đó các hypervisor này có khả năng điều khiển, kiểm soát phần cứng của máy.
![Hypervisor 1](https://i.imgur.com/usHF9PR.png)
### Host-based (Hypervisor 2)
Kiến trúc sử dụng một lớp hypervisor chạy trên nề tảng hệ điều hành, sử dụng các dịch vụ được hệ điều hành cung cấp để phân chia tài nguyên tới các máy ảo. Ta xem hypervisor như một lớp riêng biệt, do đó các hệ điều hành khách của máy ảo sẽ nằm trên lớp hypervisor rồi đến hệ điều hành của máy chủ cuối và cuối cùng là phần cứng. Một số hypervisor phổ biến hiện nay là VmWare Workstation, Microsoft Hyper-V..
![Hypervisor 2](https://i.imgur.com/tREIUT5.png)