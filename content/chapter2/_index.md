+++
title = 'Tạo và cấu hình S3 bucket'
date = 2024-03-13T20:57:01+07:00
pre = '2. '
weight = 2
+++

Sau khi chạy được app trên localhost, chúng ta sẽ build app rồi deploy nó trên một s3 bucket.

1. Trước hết, chạy câu lệnh sau để build app: 
```
npm run build
```


![sau khi build](/built.png)

Chúng ta sẽ khởi tạo một s3 bucket cho phép truy cập public đến các file, thư mục vừa được build.

2. Tạo S3 Bucket

    Tìm dịch vụ S3 và tạo mới 1 bucket
    
    Đặt tên cho bucket 
![s3-name](/s3-name.png)

Bỏ tick ở mục block all public access

![remove-block](/public-access.png)

Tick "I acknowledge that the current settings might result in this bucket and the objects within becoming public."

Chọn "Create Bucket"

3. Config S3 Bucket
   Chọn s3 bucket vừa tạo

![select-s3](/s3-preconfig.png)

Vào tab "Properties", kéo xuống dưới mục "Static Web Hosing", chọn "Edit":

![s3-properties](/s3-properties.png)

![s3-edit-static](/s3-edit-static.png)

Ở mục "Static Website Hosting", tick chọn "Enable" và điền default page là "index.html", rồi nhấn "Save Changes".

![s3-static-config](/s3-static-config.png)

Thử truy cập vào đường dẫn của website ta, thấy được lỗi 403, tức là ta không được quyền truy cập đến tài nguyên này.

![403](/403.png)

Ta sẽ thiết lập quyền truy cập vào tài nguyên S3 bucket này từ mọi nơi.

Vào tab "Permission", ở mục "Bucket Policy", chọn edit

![select-permission](/select-permission.png)

![edit-policy](/edit-policy.png)

Điền đoạn policy sau, sau đó nhấn "Save Changes":
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "<BUCKET_ARN>/*"
        }
    ]
}
```

![paste-policy](/paste-policy.png)

Truy cập lại đường dẫn đến static web, lúc này ta thấy hiện lên lỗi 404, tức là do static web không thể tìm thấy được trang index.html:

![404](/404.png)

4. Upload file, folder lên S3

Vào tab "Objects" chọn "Upload", upload toàn bộ file và folder trong thư mục "build" trong react app của chúng ta.

![upload-file-folder](/upload-file-folder.png)

Sau khi upload xong, chúng ta truy cập vào website và thấy nó đã có thể xem được nội dung.

![uploaded](/uploaded.png)
