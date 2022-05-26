---
description: Moving media manager from theme asset to dedicated environment(Shopify File)
---

# New media manager

<mark style="color:purple;">**Vấn đề:**</mark> \
&#x20;       PF hiện nay đang lưu image của merchant trong theme asset của họ. Việc này sẽ gây ra một vấn đề nghiêm trọng khi theme asset chứa các file image đó có thể bị xoá đi, khiến toàn bộ image sẽ bị mất. Do vậy cần tìm đến một môi trường khác để lưu data image của user => Shopify File Settings\
\
\
<mark style="color:purple;">**Mechanism:**</mark> \
&#x20;    PF sẽ sử dụng Shopify Graphql API để upload image và video lên Shopify. Sau đó lưu lại id của các file được upload lên bởi PF trong . Sở dĩ cần lưu lại id của media lại trên PF db vì Shopify File API khá là hạn chế khi không cho edit displayName của file, mà chỉ có thể update altText của media. \
\
&#x20;  \- Bắt buộc user phải accept  về `read_files` và `write_files`. \
\
&#x20;  \- Upload media file: Re-use lại component của a Cường viết trước đó cho Custom font feature. Bản chất việc upload files của font và media là giống nhau.\
&#x20; \
&#x20; \- Khi media manager được mở lên, sẽ cần 1 lần query file data từ Shopify để check xem các file của PF sẽ được xoá đi ko. VIệc đó sẽ được sử dụng nhờ việc Bulk Query của Shopify Graphql. Do Shopify ko hề cung cấp webhook để check được xem file có được thay đổi hay ko, nên sẽ cần 1 khoảng delay để sync data của PF và Shopify mỗi lần load vào page để query lấy ra data.\
&#x20;\
&#x20; \- Migrate data from theme to Shopify File Settings: Việc migrate data sẽ ko cần phải qua 1 bước upload file lên 1 server như quá trình upload bình thường, bời các file trong theme asset đã có sẵn link cdn. Do vậy quá trình migrate sẽ chỉ cần trải qua việc request`fileCreate` lên Shopify:\
&#x20;              fileCreate => check processingFile => get fileError and fileSuccess => update PF db\
&#x20;   \
&#x20;   Để tránh việc limit request của Shopify GraphQL, cũng như việc upload quá nhiều file lên Shopify dẫn đến việc một số file sẽ bị lỗi connect, Shopify ko thể download xuống được. Cụm file khi lớn hơn 50 sẽ được chia ra nhiều part để upload lên. Việc lấy fileError và fileSuccess ra cũng sẽ ko bị limit query từ Shopify\
&#x20;\
Trong quá trinh migrate, sẽ có thể có một số file ko thể migrate được, e.g: do resolution của image quá 20MP, do quá trình upload file lên của shopify bị lỗi,... => List error from Shopify: [https://shopify.dev/api/admin-graphql/2022-04/enums/FileErrorCode](https://shopify.dev/api/admin-graphql/2022-04/enums/FileErrorCode)\
&#x20;  \- Các file SVG, MOV, MP4 thuộc GenericFile theo Shop\
&#x20;  &#x20;

&#x20;<mark style="color:purple;">**Note dành cho design:**</mark> \
\
\- Việc migrate sẽ tạo ra 1 link cdn mới cho image\
\- File SVG vẫn có thể upload được lên Shopify cũng như PageFly thời điểm hiện tại, bài viết của Shopify bị outdate\
\- Với video thì chỉ cho user upload từ máy của họ, ko thể có option upload từ url\
\- Hiện tại Shopify chỉ cho update altText cho media, do vậy khi crop image, 1 image mới sẽ được tạo ra chứ ko thể thay thế image cũ \
\- Sẽ có một số trường hợp server của Shopify ko download được image xuống, buộc user sẽ phải retry lại quá trình migrate cho các image bị lỗi đó. \
\- Sẽ có case resolution của image quá 20MP, khiến cho image ko thể migrate được\
\
\- Hiện nay Shopify ko hề có webhook hay 1 trigger nào đưa ra tín hiệu có sự thay đổi của file settings . Do vậy để có thể sync được data media giữa PF và Shopify, sẽ buộc phải query đến Shopify để lấy ra thông tin tất cả các file trên Shopify, và cần một khoảng thời gian chạy ngầm để lấy ra thông tin đó. Sau đó so sánh với data của PF để biết được là liêu có image nào bị xoá đi ko.\
&#x20; \=> Ở đây Shopify File Settings và Theme Customizer đều sử dụng navigation để tránh việc query lượng lớn file, khác hẳn với cách mà Media Manager của PF đang hoạt động.\
\- Phần Trash của file sẽ có thời gian để xoá hẳn đi khỏi PF lẫn Shopify sau bao nhiêu ngày ko ?&#x20;

&#x20; <mark style="color:purple;">**Note dành cho developer:**</mark>\
\- **** Theo như thống nhất với designer, PageFly theme asset sẽ không bị xoá thời điểm hiện tại. Do PageFly theme asset còn lưu cả capture image từ page và section. Nếu trong lúc implement, team có phương án lưu trữ lượng ảnh capture đó ở 1 nơi khác thì có thể cân nhắc đến việc xoá PageFly theme asset   \
\- Please make sure you always read Shopify changelog to know which field is deprecated. This docs was written on version 2022-04 :) And update shopifyApiVersion on pfserver too&#x20;
