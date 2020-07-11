# BLOCKCHAIN

## Introducation

### Blockchain là gì?

- Nói một cách đơn giản, blockchain là một **digital ledger** (sổ cái số). Blockchain chứa danh sách các transactions tăng đều đặn được gọi là **blocks** – tất cả được kết nối một cách tuần tự với nhau (sequentially connected). Mỗi **block** đều có một liên kết (link) với một **block** trước đó trong danh sách.
- Một khi **block** đã được đưa vào **chain**, nó sẽ không thể bị xóa bỏ, và trở thành một phần của một CSDL cố định chưa tất cả các transactions đã từng diễn ra từ khi vận hành.
- Một trong những tính năng thú vị nhất về công nghệ blockchain chính là không có central authority hay một nguồn ledger duy nhất. Điều này có nghĩa mọi nodes đều có một bản sao hoàn chỉnh, đầy đủ của blockchain đó. Khi một block mới được thêm vào, mọi node đều sẽ biết đến nó. Phân bố phân tán và sự tin tưởng giúp đảm bảo sự minh bạch của hệ thống.

### Quy trình hoạt động

### Ưu và nhược điểm

## Keyconcept

### Digital ledger

- Dữ liệu trong các transaction được mã hóa và đóng khối **block** sau đó được liên kết với **block** trước đó thông qua mã băm  của khối **block** trước.

  

### Immutable

- **Tính bất biến của dữ liệu** nằm trên blockchain có lẽ là lý do mạnh mẽ và thuyết phục nhất để triển khai các giải pháp dựa trên blockchain cho một loạt các quy trình kinh tế xã hội hiện đang được ghi trên các máy chủ tập trung. Tính không thay đổi này làm cho blockchain hữu ích cho kế toán, giao dịch tài chính, quản lý nhận dạng và sở hữu tài sản, quản lý và chuyển giao. Một khi một giao dịch được ghi vào blockchain, không ai có thể thay đổi nó, hoặc, ít nhất, sẽ rất khó khăn để thay đổi nó.
- Về mặt kĩ thuật, rất khó để thay đổi các giao dịch trong một blockchain, bởi vì mỗi khối được **liên kết với các khối trước đó** bằng cách chứa **mã băm** của các **khối trước** đó. Do đó, nếu thay đổi 1 khối, ta phải thay cập nhật lại các **khối sau** nó để đảm bảo tính hợp lệ của chuỗi. Nếu một khói không hợp lệ nó sẽ bị loại khỏi chuỗi ngay.
- **Thời gian cần thiết để tính toán lại số nonce** cho khối sau sẽ tốn rất nhiều thời gian và công sức tính toán, do đó hầu như không thể thực hiện do các khối mới được tạo từ các máy tính khác sẽ được cập nhật liên tục vào chuỗi. Ví dụ: trong blockchain của bitcoin, một khối có 6 khối phía sau sẽ không thể thay đổi, bởi thời gian và công sức để thay đổi cho **6 khối liền sau** để tạo tính đồng thuận của mạng lưới là không thể thực hiện được (trừ khi chiếm 51% khả năng tính toán của mạng lưới).
- Ngoài ra, trong mỗi khối, mã băm của một giao dịch đơn lẻ còn bao gồm các mã băm của các giao dịch khác trong cùng 1 nhánh của [cây Merkle](https://kipalog.com/posts/Merkle-Tree). Việc thay đổi 1 giao dịch sẽ kéo theo yêu cầu thay đổi các giao dịch trước đó.

### Decentralize

- Cơ chế phi tập trung, **decentralized** sử dụng mạng ngang hàng (P2P), những người tham gia trong node có quyền lực như nhau (mining/miner/validator), được chia sẻ phần thưởng theo lý thuyết trò chơi (Game of Theory), hoạt động theo một tập luật được quy định sẵn (fixed set of rules), đồng thuận (consensus).