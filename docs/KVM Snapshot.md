# KVM Snapshot
[1.  Snapshot là gì ?](#snapshotlagi?)
    
-   [Internal Snapshot](#internalsnapshot)
-   [External Snapshot](#externalsnapshot)

[2. Lab](#Lab)

<a name="snapshotlagi"></a>
## 1. Snapshot là gì ?
Snapshot là một tính năng ghi lại tất cả trạng thái của máy ảo tại một thời điểm nhất định. Tức có nghĩa là bạn có thể quay lại trạng thái của máy ảo trước lúc Snapshot. Snapshot sử dụng không gian lưu trữ tối thiểu và đem tới khả năng khôi phục các phiên bản của máy ảo tại một thời điểm nhất định thay vì phải khôi phục hoàn toàn máy ảo.

Snapshot rất hữu ích trong trường hợp chúng ta phục vụ cho công việc vá lỗi, test một tính năng nào đó của máy ảo

Trong KVM có 2 loại Snapshot là Internal (chụp ảnh nhanh nội bộ), External (chụp nhanh bên ngoài).

- Internal Snapshot: Các bản snapshot được tạo ra sẽ nằm bên trong file disk của VM. Với cách này sẽ dễ dàng để tạo nhưng có trở ngại khi file disk của ta bị giới hạn. Chính vì vậy ta khi tạo snapshot kiểu này ta nên pause VM để nó ko phải lưu lại trạng thái của VM mà nó chỉ lưu thông tin trên disk điều này sẽ làm giảm sự lãng phí dung lượng cho VM.

Mặc dù vậy ở chế độ intetnal snapshot vẫn có vài hạn chế như sau: chỉ hỗ trợ định dạng qcow2, VM sẽ bị ngừng lại khi tiến hành snapshot, không hoạt động với LVM storage pools
- External Snapshot: Dựa theo cơ chế copy-on-write. Khi snapshot được tạo, ổ đĩa ban đầu sẽ có trạng thái “read-only” và có một ổ đĩa khác chồng lên để lưu dữ liệu mới