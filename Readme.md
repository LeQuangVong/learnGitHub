# GitHub
## VCS (Version Control System):
Hệ thống quản lý phiên bản - Version Control System (VCS) là một hệ thống ghi nhận và lưu lại sự thay đổi của các file theo thời gian, từ hệ thống đó một file có thể phục hồi quay về trạng thái (phiên bản) ở một thời điểm trước đó. Ngoài ra bạn có thể theo dõi sự thay đổi của một file theo thời gian, ai đã thay đổi, thay đổi vào lúc nào .... Có nhiều hệ thống VCS mà bạn có thể chọn sử dụng như: Concurrent Versions System, Subversion, Git, Mercurial
- CVCS(Centralized Version Control Systems): Hệ thống quản lí phiên bản trung tâm.
- DVCS(Distributed Version Control Systems): Hệ thoóng quản lí phiên bản phân tán.

## VCS Git:
Git chính là hệ thống quản lý phiên bản phân tán (DVCS), với các ưu điểm: tốc độ, đơn giản, phân tán, phù hợp với dự án lớn nhỏ.

## How to save data in Git?
Git lưu dữ liệu dưới dạng một loạt "ảnh chụp" (snapshot) của một tập hợp các file, có nghĩa là mỗi khi bạn commit (lưu lại) thì Git tiến hành chụp lại hệ thống các file thời điểm đó và lưu giữ một tham chiếu đến ảnh chụp dó, nhớ rằng các file không có thay đổi thì Git sẽ không lưu lại file đó lần nữa mà chỉ có một liên kết đến file đã lưu ở lần trước.

## Work with Git:
Vì mỗi máy trạm có một Database Git nên hầu hết thao tác với Git như thêm mới, xem lại lịch sử ... đều không cần đến Server (trừ cần commit lên Server, lấy về một file do người khác đã cập nhật)

## Data in git is guaranteed
## Add to Git the data:
Các hành động trong Git hầu hết là các thao tác là thêm dữ liệu vào hệ thống Git. Rất khó để yêu cầu hệ thông thực hiện việc gì đó mà không phục hồi lại được, cũng như khó mà xóa hoàn toàn dữ liệu khỏi hệ thống.
## Status with Git:
- Với Git, các file của bạn có thể nằm ở một trong ba trạng thái: committed, modified, staged

    - committed: có nghĩa là dữ liệu đã lưu trữ an toàn trong Database (local).
    - modified có nghĩa là dữ liệu (file) có thay đổi nhưng chưa lưu trong Database (local)

    - staged có nghĩa đánh dấu các file sửa đổi modified chuẩn bị được commit tiếp theo
## Area:
- Thư mục làm việc (Working tree) - Chứa bản sao phiên bản cụ thể của dự án
- Khu vực sắp xếp (staging) - là một file, nằm trong thư mục Git chứa thông tin sẽ commit
- Thư mục Git (Git directory) - nơi Git lưu Database các file Metadata