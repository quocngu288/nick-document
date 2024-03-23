# Các khái niệm cần biết khi tham gia dự án có sử dụng Login Channel

- Provider: Đơn vị sở hữu và cung cấp công khai hệ thống app đến người dùng. Như ở đây là Megumilk

- Channel: Cổng cung cấp dịch vụ của LINE cho hệ thống app của một Provider

- Login Channel: Cổng chức năng đăng ký vào hệ thống App bằng LINE Account của User
  -- User có thể dùng LINE Account để đăng ký mới cũng như login vào hệ thống app như một user bình thường của hệ thống app đó
  -- Đồng thời, User khi đã đi ngang qua LINE Login, cũng đã ghi danh vào Provider và được cấp LINE UserID cho riêng Provider đó
  -- Cùng một User, nhưng sẽ có UserID khác nhau cho Provider khác nhau

- LINE Messaging API: Cổng chức năng hỗ trợ Official Account tương tác với LINE User. Gồm hai chức năng:
  -- Sending (LINE Message): Gửi message đến LINE User
  -- Webhook: Nhận request báo hiệu đến hệ thống app mỗi khi có một event được thực hiện bởi User, đồng thời có thể lấy thông tin mà User đã gửi cho OA

- Official Account (OA): LINE Account đặc biệt dành cho doanh nghiệp, không phải LINE Account của user thường
  -- Ngoài tương tác với LINE account khác như một LINE Account bình thường, thì có rất nhiều chức năng hỗ trợ về mặt Business

# Các logic cần biết về các tính năng

- Một Login Channel chỉ có thể được sử dụng bởi một hệ thống (do có yêu cầu settings về URL để redirect về hệ thống App sau khi Login)

- Một Messaging API Webhook được sử dụng bởi một hệ thống (cũng là do có yêu cầu settings về URL để nhận báo hiệu

- Một Messaging API Sending có thể được sử dụng bởi nhiều hệ thống (Không có yêu cầu về URL)

- Một Official Account sẽ chỉ có 1 Messaging API, cũng như chỉ có thể settings 1 Webhook
  -- Như vậy, nhiều hệ thống có thể gửi messaging đến User bằng cùng 1 Official Account
  -- Nhưng chỉ có một hệ thống là có thể nhận tín hiệu báo (Webhook) về mỗi khi có tương tác của User với Official Account đó

- Một LINE UserID được cấp cho Provider, nên tất cả Channel thuộc Provider đó đều share chung thông tin về UserID đó sẽ tương ứng với LINE Account nào
  -- Do đó, hai hệ thống không liên quan với nhau vẫn sẽ cùng chung LINE UserID cho cùng một LINE Account, nếu Login Channel thuộc chung 1 Provider
  -- Do cùng một LINE UserID, nên khi một trong hai hệ thống có thông tin của LINE UserID của hệ thống còn lại, vẫn sẽ gửi message cho User bình thường (thậm chí dù khác Official Account)
  -- Vì vậy, mỗi một End-Client phải có một Provider khác nhau, tránh TH râu ông nọ cắm cằm bà kia
