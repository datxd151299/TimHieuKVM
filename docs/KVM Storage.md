# KVM Storage
1. KVM Storage là gì?
2. Định dạng ổ đĩa trong KVM



# 1. KVM Storage là gì?
KVM Storage được dùng để lưu trữ các đĩa ảo của các VM trong KVM. Có thể quản các nhóm lưu trữ này bằng nhiều cách khác nhau sau đây do thư viện libvirt cung cấp

- Filesystem Directory (local)
- LVM Volume Group (local)
- NFS Storage Pool
- iSCSI backed (shared)

Trong KVM có 2 cơ chế lưu trũ Thin-Thick

1.1 Thick

Với cơ chế này khi ta tạo một disk ảo cho VM nó sẽ nhận nguyên dung lượng disk đó làm disk của nó dù cho nó chưa sử dụng hết dung lượng disk đó. Thick có 2 loại là:

Thick Lazy khi tạo một disk cho VM nó sẽ ánh xạ đến một phân vùng trên disk thật. Nó nhận đủ dung lượng disk mà ta tạo cho VM và nó sẽ không xóa dữ liệu cũ trên disk (nếu có) khi chúng ta ghi cái ghì lên đó thì nó mới xóa dữ liệu đó đi. Chính vì vậy nên việc tạo đĩa ảo sẽ rất nhanh nhưng sẽ mất nhiều thời gian cho lần ghi đầu tiên do phải xóa dữ liệu cũ(nếu có)

Thick Eager cũng gần giống như thick lazy có cũng nhận toàn bộ dung lượng mà ta tạo disk cho VM. Nó sẽ ghi toàn bộ bit 0 lên phần dung lượng chưa được sử dụng của disk ảo(giống như ta tạo file với câu lệnh dd). Vì vậy khi tạo disk cho VM ở kiểu này sẽ lâu hơn so với thick lazy nhưng với lần ghi đầu tiên sẽ nhanh hơn


Như ta thấy thì nó sẽ rất lãng phí disk. Ví dụ ta có 100G dung lượng disk và ta tạo 5 máy ảo mỗi máy 20G disk và ta không thể tạo thêm một máy nào khác cho dù 5 VM kia chưa sử dụng hết 20G. Như vậy dung lượng bị lãng phí là rất lớn. Nhưng nó sẽ đảm bảo sự độc lập giữa các VM

1.2 Thin

Với cơ chế này sẽ tránh được sự lạng phí dung lượng ổ cứng so với thick. Cơ chế này thì VM chỉ chiếm dung lượng bằng đúng phần dung lượng mà nó đang lưu trữ. Vì vậy với phần dung lượng còn trống ta vẫn có thể làm việc khác.



Với cơ chế này ta có thể tận dụng được hết dung lượng disk nhưng nó có nhược điểm là nếu dung lượng đĩa cứng bị hết thì tất cả các VM trên đó sẽ gặp vấn đề vì không còn dung lượng disk để sử dụng.

2. Định dạng ổ đĩa trong KVM

3. Thao tác và làm việc với Storage
virsh pool-define-as --name vmdisks --type dir --target /vmdisks
virsh pool-list --all
virsh pool-start --build vmdisks
vish pool-autostart vmdisks
virsh pool-info vmdisks

tạo các volume tronng storage pool sử dụng Command Line
ví dụ tạo một volume trong storage vmdisks
virsh vol-create-as vmdisks raw-disk.img 10G --format raw
trên là một image định dạng ở raw

tạo volume định dạng qcow2
virsh vol-create-as vmdisks qcow2-disk.qcow2 10G --format qcow2

Ta có thể xem lại thông tin volume vừa tạo sử dụng lệnh như sau

virsh vol-info --pool vmdisks qcow2-disk.qcow2
Thực hiện cài đặt VM
virt-install \
-- name vm-centos \
-- memory 2048 \
-- vcpus 2 \
-- disk pool=vmdisks,size=20,format=qcow2\
-- location /var/lib/libvirt/images/Centos-7.0-x86_64-Mininal.iso\

KVM hỗ trợ add disk ngay cả khi VM đang chạy
virsh attach-disk vm-centos /vmdisks/add-disk.qcow vdb --live --config