# Hướng dẫn sử dụng
## Giải thích về các thành phần trong repository này
1. file package.json và file package-lock.json
*Đó là 1 câu chuyện dài :))) Vui lòng đọc hết đoạn văn dưới đây để hiểu*
- Khi code ứng dụng, chắc chắn sẽ có lúc chúng ta cần sử dụng các thư viện bên ngoài, các thư viện đó cũng là các đoạn code HTML, CSS và javascript đã được build và đóng gói lại thành các package sau đó share ra bên ngoài theo các con đường khác nhau như: github, gitbucket, gitlab, npm, ... (Cách build và cách sử dụng thư viện sẽ được trình bày sau)
  - Trong đó github, gitbucket, gitlab thì do nó là các kho quản lý và lưu trữ mã nguồn nên người ta thường lưu rất nhiều thứ lên đó, có những mã nguồn rất hay, rất có giá trị, nhưng cũng có nhiều mã nguồn rác, không dùng được, thậm chí, không thể install và chạy được (Thật đấy, không đùa đâu :3). Chưa kể, github, gitbucket và gitlab không chỉ hỗ trợ lưu mã nguồn javascript mà còn lưu mã nguồn của những ngôn ngữ khác nữa, nên việc tìm kiếm 1 thư viện hay để sử dụng trong github, gitbucket và gitlab không khác gì bới đống rác tìm vàng (Nếu vẫn muốn tìm thì hãy dựa trên số sao được người dùng vote, dự án nào càng được nhiều sao thì dự án đó càng nhận được sự công nhận)
  - Còn npm thì cũng là kho, nhưng nó không để lưu trữ mã nguồn mà thường là để lưu những thư viện javascript (Không dành cho các ngôn ngữ khác) đã thành phẩm (Tức là thư viện đã code xong, chạy được, sau đó được build sẵn - hoặc được setup để được tự động build sau khi mình install), mình chỉ cần install về là dùng được luôn
  - Vậy nên, nếu thư viện chúng ta cần dùng tìm thấy trên npm, thì thường người ta dùng npm để install về dùng luôn chứ không ai dại gì tìm mã nguồn rồi bê mã nguồn của thư viện đó trên github, gitbucket, gitlab,... về build cả.
- Giới thiệu sơ qua về npm:
  - npm là viết tắt của node package manager: Tức là mục đích ban đầu của nó là để quản lý và chia sẻ các thư viện javascript dành cho nodejs thôi (nói dễ hiểu thì nodejs là 1 Javascript runtime, nó hỗ trợ chạy javascript trực tiếp trên máy tính mà không cần thông qua browser, nó giúp chúng ta code được backend bằng javascript - Đây lại là 1 câu chuyện dài :v Sẽ được nói cụ thể sau). Tuy nhiên, sau này cứ cái thư viện nào sử dụng javascript (Cả nodejs và cả js cho browser) thì hầu như đều dùng npm để quản lý. Thành ra là hiện tại trên npm sẽ có cả các thư viện chỉ chạy được ở phía Backend (Tức là nodejs) và sẽ có cả các thư viện chỉ chạy được ở phía Frontend (Tức là js dùng chạy trên browser), cụ thể thì từng thư viện mà người ta sẽ nói rõ là code của họ chạy được ở đâu.
  - npm đã được đóng gói sẵn trong node.js, vậy nên để sử dụng npm thì ta cần cài đặt node.js
- npm thì liên quan quái gì tới package.json và package-lock.json?
*Chúng ta đã nói rất nhiều về npm rồi, tuy nhiên chưa nói gì về sự liên quan của chúng với npm*
  - Muốn install và sử dụng được các thư viện từ npm thì trước hết ở root của project (Ví dụ với project này thì root của project cùng cấp với file Readme.md này) ta cần tạo ra 1 file tên là package.json. File này sẽ được đọc bởi npm mỗi khi chúng ta gọi lệnh nào đó liên quan đến npm (Ví dụ như npm install tên_package_muốn_install). File này chứa các thông tin về:
    - Tên thư viện của chúng ta
    - Version
    - Tác giả
    - description
    - Vị trí file main của thư viện (main giống như cái cổng nhà ấy, cứ vào nhà phải đi qua cái cổng, nó sẽ là file đầu tiên của thư viện được gọi khi mà thư viện của chúng ta được import vào 1 chỗ khác)
    - scripts: Các scripts để chạy, test, build, fix,... thư viện'
    - dependencies: Thông tin về các thư viện được install và sử dụng trong thư viện của chúng ta
    - ...
  - Còn về file package-lock.json thì sao? 
    - Các thư viện được chúng ta bê về dùng thì cũng hầu như đều kết hợp cả mã họ tự viết với sử dụng các thư viện khác nữa, chứ chẳng có ai viết chay 100% cả, tạm gọi những thư viện đó là thư viện con của thư viện. Để tránh việc các thư viện con cập nhật dẫn đến thư viện chúng ta bê về không còn chạy được nữa thì npm cần lưu cả phiên bản của chúng vào.
    - nếu package.json chứa thông tin tổng quan về thư viện của chúng ta thì package-lock.json chứa thông tin chi tiết về các thư viện được sử dụng và các thư viện con của chúng. Những thông tin này bao gồm:
      - tên thư viện
      - link tải thư viện
      - mã xác thực (hàm băm)
      - phiên bản node hỗ trợ (code có chạy hay không còn tùy thuộc vào phiên bản nodejs nữa, vì khi nodejs cập nhật thì sẽ có nhiều logic đằng sau nó được cập nhật theo, dẫn đến code của chúng ta chạy không còn đúng nữa)
      - ...
    - file package-lock.json sẽ được tạo tự động khi chúng ta gọi lệnh npm install và sẽ được cập nhật tự động khi chúng ta install hoặc uninstall 1 thư viện nào đó. Nên là: **Đừng sửa gì vào file này nhé :v Anh giải thích cho hiểu thôi**

2. folder node_modules
- folder này sẽ được tạo tự động sau khi các em gọi npm install. 
- Sau khi install các thư viện trên kho thư viện npm về thì code của chúng sẽ được lưu và quản lý trong folder node_modules này

3. file index.js
- file này chứa code js để anh bê thư viện five-server về dùng làm server examples cho các em thôi

4. file .gitignore
- Sau học về git thì em sẽ rõ cái file này
- Nó là 1 file để git biết được file nào, folder nào cần được bỏ qua, không cần đẩy lên git server
- Thường thì chúng ta chỉ đẩy source code, package.json, package-lock.json, Readme.md hay các file liên quan đến việc install và chạy code thôi chứ không đẩy những cái liên quan đến bảo mật và những cái tự install được như node_modules nha (Vì package.json và package-lock.json chứa hết thông tin về phiên bản của các thư viện rồi nên ai cần thì bê code mình về mà tự install thôi, chứ mình không đẩy lên nữa cho nặng).

## Yêu cầu
1. Cài đặt Node.js
- Cài version nào cũng được
- Để cài Node.js thì chúng ta có 2 cách chính (Còn nhiều cách nữa nhưng biết 2 cách đủ rồi):
  - Cách 1: Tải trực tiếp về trên trang chủ của Node.js và cài đặt: [Download Node.js](https://nodejs.org/en/download). Với cách này thì được cái nhanh và dễ, nhưng sẽ có lúc chúng ta cần thay đổi phiên bản của node.js. Trong trường hợp chạy những thư viện cũ, chỉ hỗ trợ Node.js phiên bản cũ hơn chẳng hạn, trong trường hợp này thì chúng ta không dùng cách 1 được mà phải dùng cách 2 (Mới học thì cứ dùng cách 1 cũng được, chạy được là tốt rồi)
  - Cách 2: Sử dụng nvm (Node Version Manager), nó là 1 thư viện chuyên hỗ trợ chúng ta cài đặt và chuyển qua lại giữa các phiên bản Node.js khác nhau, hướng dẫn cài đặt đây: [How to install nvm guide](https://www.freecodecamp.org/news/node-version-manager-nvm-install-guide/). Nó cũng không khó đâu :v Cũng dễ, cũng nhanh, chỉ là không dễ bằng cách 1 thôi.

## Hướng dẫn cài đặt và chạy
1. Nhập lệnh `npm install` vào terminal rồi nhấn enter để install các thư viện được sử dụng trong repository này
2. Nhập lệnh `npm start` rồi nhấn enter để start server example
3. Lúc này 1 tab browser sẽ tự động mở hiển thị explores file trong repo này, em truy cập vào đúng example rồi chọn vào file index.html là được
