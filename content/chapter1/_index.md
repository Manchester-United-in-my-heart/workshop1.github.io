+++
title = 'Chuẩn bị React App'
date = 2024-03-13T15:27:25+07:00
pre = '1. '
weight = 1
+++

Trước tiên, chúng ta sẽ chuẩn bị một React App có thể chạy trên localhost. Hiện tại có nhiều repo React trên github, bạn có thể clone repo tôi đã chuẩn bị sẵn bằng câu lệnh sau:
```
git clone https://github.com/BuiDuongKham/my-mpa-react-app.git
```

Sau khi repo này được clone về, project có cấu trúc như sau:
![cấu trúc thư mục](/folder_structure.png)

Chúng ta chạy câu lệnh sau để download các package cần thiết:
```
npm install
```
![cấu trúc thư mục](/install.png)

Tiếp theo chúng ta chạy câu lệnh sau và truy cập vào localhost:3000 để xem kết quả: 
```
npm start
```

![demo](/local-demo.png)

Như vậy là chúng ta đã có một react app có thể chạy ổn định trên môi trường localhost.