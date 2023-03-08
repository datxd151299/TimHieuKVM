# Tổng quan về Virtualization và Hypervisor
## Mục Lục
 [1. Virtualization?](#Virtualization)

 [2. Hypervisor/VMM](#Hypervisor/VMM)

- [Native](#Native)
- [Hosted](#Hosted)

[3. Ring](#Ring)

[4. Các loại ảo hóa](#cacloaiaohoa)
<a name="Virtualization"></a>
## 1. Virtualization?
-   Virualization, hay còn gọi là ảo hóa, là một công nghệ được thiết kế để tạo ra tầng trung gian giữa hệ thống phần cứng và phần mềm chạy trên nó. Ý tưởng của công nghệ ảo hóa máy chủ là từ một máy vật lý đơn lẻ có thể tạo thành nhiều máy ảo độc lập. Mỗi một máy ảo đều có một thiết lập nguồn hệ thống riêng rẽ, hệ điều hành riêng và các ứng dụng riêng. Ảo hóa có nguồn gốc từ việc phân chia ổ đĩa, chúng phân chia một máy chủ thực thành nhiều máy chủ logic. Một khi máy chủ thực được chia, mỗi máy chủ logic có thể chạy một hệ điều hành và các ứng dụng độc lập.

***NOTE: Tóm lại, ảo hóa là phương pháp để tạo ra phiên bản ảo hóa trên máy tính vật lý***

<a name="Hypervisor/VMM"></a>
## 2. Hypervisor/VMM
***Hypervisor là các phầm mềm công nghệ để tạo ra máy ảo và có chức năng chính là giám sát và điều khiển máy ảo***.Nó được sử dụng để tạo, startup, dừng và reset lại các máy ảo. Các hypervisor cho phép mỗi VM hoặc “guest” truy cập vào lớp tài nguyên phần cứng vật lý bên dưới, chẳng hạn như CPU, RAM và lưu trữ.


<a name="Native"></a>
### Native (Hypervisor 1)
Kiến trúc này lớp phần mềm hypervisor chạy trực tiếp trên nền tảng phần cứng của máy chủ, không thông qua bất kì một hệ điều hành hay một nền tảng khác. Qua đó các hypervisor này có khả năng điều khiển, kiểm soát phần cứng của máy.
![Hypervisor 1](https://i.imgur.com/usHF9PR.png)
<a name="Hosted"></a>
### Hosted (Hypervisor 2)
Kiến trúc sử dụng một lớp hypervisor chạy trên nề tảng hệ điều hành, sử dụng các dịch vụ được hệ điều hành cung cấp để phân chia tài nguyên tới các máy ảo. Ta xem hypervisor như một lớp riêng biệt, do đó các hệ điều hành khách của máy ảo sẽ nằm trên lớp hypervisor rồi đến hệ điều hành của máy chủ cuối và cuối cùng là phần cứng. Một số hypervisor phổ biến hiện nay là VmWare Workstation, Microsoft Hyper-V..
![Hypervisor 2](https://i.imgur.com/tREIUT5.png)
<a name="Ring"></a>
## 3. Ring
Trong kiến trúc CPUx86 có một khái niệm về Ring ta có thể hiểu đơn giản là Ring giúp cách ly người dùng với hệ hành bằng các cấp đặc quyền nhất định
![Ring](https://i.imgur.com/EaILVBA.png)
Có thể thấy các Ring có trọng số càng thấp thì có đặc quyền cao nhất như Ring 0 thì bao bọc lớp kernel nó có thể tương tác trực tiếp với CPU, Memory, RAM..
Các Ring có trọng số cao hơn thì đồng nghĩa có đặc quyền thấp hơn ví dụ như các ứng dụng ở Ring 3 đang chạy các ứng dụng muốn truy cập đến Ring 0 thì chúng cần có lời mời gọi hàm.
<a name="cacloaiaohoa"></a>
## 4. Các loại ảo hóa
Trong ảo hóa được chia làm các loại ảo hóa như sau:
1. RAM Virtualization
2. CPU Virtualization
3. Network Virtualization
4. Device I/O Virtualization

Chúng ta sẽ đi sâu vào đến CPU Virtualization chủ yếu vào 2 loại là
Full Virtualization và Para Virtualization