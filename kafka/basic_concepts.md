
# Apache Kafka — Topic, Partition, Offset & Broker  

## 1. Kafka là gì?  
Apache Kafka là một nền tảng xử lý streaming data theo thời gian thực, với các đặc điểm:  
- **Scalable**: dễ mở rộng bằng cách thêm broker hoặc partition  
- **Durable**: dữ liệu được ghi xuống đĩa, hạn chế mất mát  
- **Reliable**: hỗ trợ replication, đảm bảo hệ thống không ngừng hoạt động khi có node lỗi  
- **Hiệu năng cao**: throughput lớn, phù hợp truyền dữ liệu liên tục  

Kafka thường dùng cho log, event, tracking, real-time analytics, data pipeline,…

---

## 2. Topic, Partition và Offset  

### 2.1 Topic  
- Topic là “danh mục dữ liệu” nơi Producer gửi message và Consumer đọc message.  
- Có thể hiểu topic giống một bảng (table) — mỗi message là một bản ghi.  
- Dữ liệu trong topic được lưu dạng log, chia thành nhiều segment.

### 2.2 Partition  
- Một topic được chia thành nhiều **partition**.  
- Mỗi partition là một log được append liên tục.  
- Việc chia partition giúp Kafka xử lý song song nhiều luồng dữ liệu và dễ mở rộng.

### 2.3 Offset  
- Mỗi message trong partition có một **offset** — số thứ tự tăng dần từ 0.  
- Offset:  
  - Chỉ có ý nghĩa trong phạm vi *một partition*.  
  - Giúp Consumer biết đã đọc đến đâu.  
- Kafka **không sắp xếp thứ tự giữa các partition** — chỉ đảm bảo thứ tự trong nội bộ từng partition.

### 2.4 Tính chất quan trọng  
- Message **immutable** – ghi rồi không sửa.  
- Offset **không reset** dù dữ liệu cũ bị xóa theo thời gian lưu trữ.  
- Cần 3 thông tin để xác định 1 message:  
  `topic name + partition + offset`

---

## 3. Broker và Cluster  

### 3.1 Broker  
- Broker là một server Kafka.  
- Mỗi broker lưu nhiều partition của nhiều topic khác nhau.  
- Một cluster Kafka gồm nhiều broker.

### 3.2 Cluster & Replication  
- Để tránh mất dữ liệu, Kafka hỗ trợ **replication**.  
- Mỗi partition sẽ có:  
  - **Leader**: broker chính, nhận ghi/đọc  
  - **Followers**: bản sao, dùng khi leader lỗi  
- Điều này giúp Kafka chịu lỗi tốt (fault tolerance).

### 3.3 Nhiệm vụ của broker  
1. Nhận message từ Producer  
2. Ghi message vào log file của partition  
3. Cung cấp message cho Consumer  

### 3.4 Lợi ích  
- Hệ thống phân tán, dễ mở rộng  
- Chịu lỗi tốt nhờ replication  
- Hiệu năng cao  
- Hỗ trợ nhiều consumer group xử lý song song

---

## 4. Tóm tắt nhanh  
- **Topic** = luồng dữ liệu  
- **Partition** = cách Kafka chia nhỏ topic để tăng hiệu năng  
- **Offset** = vị trí message trong 1 partition  
- **Broker** = server Kafka  
- **Cluster** = nhiều broker, có replication để tăng độ tin cậy  

Kafka mạnh vì: bất biến, tốc độ cao, bền vững, mở rộng dễ và xử lý song song cực tốt.
