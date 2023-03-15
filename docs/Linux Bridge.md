# Linux Bridge
[1. Giới thiệu về Linux Bridge](#gioithieuvelinuxbridge)

[2. Isolated Virtual Network (Host-Only)](#Isolatedvirtualnetwork)

[3. Routed Virtual Network (Bridge)](#routedvirtualnetwork)

[4. NATed Virtual Network (NAT)](#natedvirtualnetwork)

<a name="gioithieuvelinuxbridge"></a>
## 1. Giới thiệu về Linux Bridge

- Linux Bridge là một mô-đun trong nhân kernel nó hoạt động như một switch ảo, giúp chuyển tiếp các gói tin giữ interface với switch ảo nhằm giải quyết các vấn đề ảo hóa network bên trong các máy vật lý.
-   Linux Bridge sẽ tạo ra các switch layer 2 kết nối với các VM để các VM đó giao tiếp được với nhau và có thế kết nối ra mạng ngoài. Linux Bridge thường sử dụng kết hợp với hệ thống ảo hóa KVM-QEMU