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
### Lợi ích của ảo hóa

-   Tiết kiệm: Việc sử dụng nhiều máy ảo trên những server vật lý giúp tiết kiệm không gian, hạ tầng và tiết kiệm điện. Ảo hóa cũng cung cấp được chính xác CPU, RAM, và bộ nhớ lưu trữ cho từng máy ảo không gây lãng phí tài nguyên phần cứng của máy chủ.
-   Cô lập dịch vụ: Khi mỗi dịch vụ được chạy trên một máy ảo khác nhau thì khi gặp sự cố, sẽ có thể không làm ảnh hưởng đến các dịch vụ khác, thêm vào đó cúng giúp người dùng quản lý dễ dàng hơn các dịch vụ.
Cung cấp máy chủ nhanh chóng: Việc tạo máy ảo nhanh hơn nhiều so với việc mua, thiết lâp, chạy một máy chủ vật lý. Ví dụ như không phải quan tâm đến vị trí, tủ rack để đặt máy chủ mới.
- Dễ dàng dịch chuyển và sao lưu: Ảo hóa hỗ trợ tính năng giúp tạo snapshot để lưu lại trạng thái máy ảo để có thể triển khai máy ảo về đúng trạng thái tạo snapshot. Nó cũng hỗ trợ tính năng migrate giúp di chuyển các máy ảo dễ dàng trong datacenter.


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
Trong kiến trúc CPUx86 có một khái niệm về Ring ta có thể hiểu đơn giản là Ring giúp cách ly người dùng với hệ hành bằng các cấp đặc quyền nhất định. Cơ chế của nhằm bảo vệ dữ liệu và chức năng của một chương trình tránh khỏi nguy cơ lỗi hoặc bị truy cập trái phép bởi các chương trình khác.
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
-  Full Virtualization

Full Virtualization có nghĩa là ảo hóa toàn phần. Đây là loại ảo hóa mà không cần chỉnh sửa hệ điều hành khách (Guest OS), cũng như các phần mềm đã được cài đặt trên nó để chạy trong môi trường hệ điều hành chủ. Nhìn vào mô hình của ảo hóa toàn phần thì ta có thể thấy lớp *Hypervisor* được cài trực tiếp trên lớp Ring 0 đều đó đồng nghĩa với việc khi cài đặt *Hypervisor* trên lớp này nó sẽ đặc quyền tương tác với lớp vật lý dưới cùng của máy chủ như CPU, RAM, Memory...

 ![Full Virtualization](https://i.imgur.com/xam2zt0.png)
 Còn ở trên lớp Ring 1 chính là hệ điều hành khách (Guest OS) thì Guest OS này chỉ chạy trên quyền user lever mà không chạy trên quyền privilege theo như cách thức hoạt động của lớp Ring trong kiến trúc CPUx86 nên nó không trực tiếp chạy trên thằng hardware. Nhưng vì các OS cài trên VM không bị sửa đổi nên ở Guest OS nó không biết được điều đó và nó làm việc bình thường như trên máy thật, nhưng thực chất nó đang làm việc với VMM.

 ![Full Virtualization](https://i.imgur.com/3tk2SMx.png)
 Còn ở lóp Ring 3 có thể các chỉ thị của người trức tiếp tương tác trên lớp Hypervisor thông một driver được tích ở lớp Ring 0 từ đó xuống các chỉ thị của người dùng xuống lớp hardware ở dưới.

 -  Paravirtualization

Paravirtualization là việc chỉ tiến hành ảo hóa một số phần cứng nhất định nên nó không đủ tài nguyên để vận hành một số hệ điều hành ảo hoàn chỉnh, thay vào đó nó chỉ cho phép chạy một số phần mềm để tránh lãng phí tài nguyên.

![Paravirtualization](https://i.imgur.com/jasCKEJ.png)

Nhìn vào mô hình trên ta có thể thấy ý định của việc thực hiện ảo hóa này là việc chúng ta chạy Guest OS trên lớp Ring 0 việc đó để tương thích ở lớp Ring 0 này thì các OS (hệ điều hành) chạy trên máy khách (Guest) sẽ phải chỉnh sửa một chút để nó chạy tương thích với lớp Ring 0. Nếu điều đó xảy ra thì lớp Ring 0 chỉ cài được đúng một hệ điều hành khách nhưng việc của chúng ta là muốn chạy được nhiều Guest OS thì càng tốt nên vì giải pháp là xây dựng một lớp Virtualization Layer ở dưới Ring 0 nó như là một Hypervisor các chỉ thị từ lớp Ring 0 ở đây là các Guest OS sẽ một qua *hypercalls* để thực hiện chỉ thị các thực thi cung cấp CPU, RAM từ Guest OS.

![Paravirtualization](https://i.imgur.com/NuVsylW.png)