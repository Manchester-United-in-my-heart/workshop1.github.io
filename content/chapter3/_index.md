+++
title = 'Tạo CI/CD pipeline với Buddy'
date = 2024-03-13T22:44:06+07:00
pre = '3. '
weight = 3
+++

Tiếp theo, chúng ta sẽ tạo một pipeline CI/CD với Buddy để tự động build và deploy app lên S3 bucket mỗi khi có thay đổi trên branch master (có thể sử dụng CodePipeline và CodeBuild, cũng là 2 dịch vụ của AWS để gói gọn dự án trong khuôn khổ AWS, tuy nhiên, CodeBuild không thích hợp sử dụng vì chính sách Limitation với tài khoản mới của AWS).

1. Đầu tiên, push code của bạn lên github

    Tạo một repo public trên Github
    
![create-repo](/create-repo.png)

Push code từ local repo lên remote repo bằng câu lệnh

```
git remote add origin <REPO_URL>
git branch -M main
git push -u origin main
```

2. Đầu tiên, truy cập vào website <a href="https://buddy.works/">Buddy</a> và đăng nhập bằng tài khoản github đang chứa repo vừa push

![buddy-signin](/buddy-signin.png)

Chọn "Add Project"

![add-project](/add-project.png)

Chọn GitHub Provider và xác nhận ủy quyền truy cập

![authorize](/authorize.png)

Chọn repo vừa push và chọn "Sync"

![sync](/sync.png)

Chọn "New Pipeline"

![new-pipeline](/new-pipeline.png)

Tạo một pipeline mới như sau:

![add-pipeline](/add-pipeline.png)

Ở mục "Run Container" chọn Node.js

![run-container](/run-container.png)

Tạo command để install các thư viện và build app

![npm-run-build](/npm-run-build.png)

3. Tiếp theo, chúng ta tạo một IAM user để Buddy có thể upload file lên S3.
   Truy cập vào dịch vụ IAM, Chọn "Create user", điền thông tin như sau:

![IAM-1](/IAM-1.png)
![IAM-2](/IAM-2.png)

Thêm Permission "AmazonS3FullAccess" cho IAM user.
![Permission](/permission.png)

4. Quay trở lại màn hình của Buddy, nhấn vào dấu "+" để thêm Action
   
![add-action](/add-action.png)
![s3-transfer](/s3-transfer.png)


![add-target](/add-target.png)
Tạo access key cho IAM user vừa tạo
![create-access-key](/create-access-key.png)
![access-key](/access-key.png)
![paste-access-key](/paste-access-key.png)

Chọn nguồn file cần upload

![source](/source.png)

Chọn Bucket nơi code build sẽ được upload
![select-bucket](/select-bucket.png)

Ta chạy thử pipeline vừa tạo 

![test-run](/test-run.png)

5. Ta thử thay đổi source code và push lên remote repo, đợi vài phút để xem pipeline của chúng ta có hoạt động không

![change](/change.png)
![result](/result.png)



