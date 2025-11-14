# Digital-forensics-lab
--- 
## Common Windows Artifacts.
Trong hệ điều hành Windows thì nó chứa đựng lượng lớn các dấu vết bao gồm: các thư mục, các files, logs, registry, lịch sử browser, tài khoản người dùng và rất nhiefu những dữ liệu quan trọng khác rất cần thiết, để hoạt động đúng cách.
## Windows Registry
- Là một hệ thống phân cấp cơ sở dữ liệu, mà ở đó lưu trữ những cấu hình cho người dùng bao gồm ứng dụng và phần cứng thiết bị.
- Windows Registry nó bao gồm 5 cái khóa gốc chính , được hiểu là các hives đó là:
    - HKEY_CURRENT_USER (HKCU): hives này chứa các thông tin về nhật ký của người dùng bao gồm màu màn hình và cài đặt control panel.
    - HKEY_USER (HKU): hives này chứa toàn bộ thông tin hồ sơ người dùng hiện có trên máy tính.
    - HKEY_LOCAL_MACHINE (HKLM): hives này chứa các thông tin về cấu hình hệ thống.
    - HKEY_CLASSESS_ROOT (HKCR): hives này chứa các thông tin về các loại files và các chương trình liên quan của họ.
    - HKEY_CURRENT_CONFIG (HKCC): hives này chứa thông tin về hồ sơ phần cứng của hệ thống.
- Mỗi một khóa này sẽ chứa những khóa con phân cấp và giá trị lưu trữ những thông tin cụ thể của hệ thống và cấu hình của nó. Lấy vị dụ thì cấu hình của con chuột, như là độ nhạy và double click speed sẽ được lưu trữ bên trong Computer\HKEY_CURRENT_USER\Control Panel\Mouse . Chúng ta có thể nhận dạng nó
  dưới dạng cây như sau:
<img width="1629" height="224" alt="image" src="https://github.com/user-attachments/assets/5e4f9367-05c6-4b8d-b741-a5ba145c1651" />

- Khóa Registry có thể được xem và chỉnh sửa bên trong Registry Editor - một công cụ được phát triển bởi Windows Microsoft. Mở bằng Windows + R regedit

<img width="1258" height="639" alt="regedit" src="https://github.com/user-attachments/assets/483bc0b0-1f57-4cc8-8c2c-d58a5313c686" />
<img width="2847" height="1522" alt="image" src="https://github.com/user-attachments/assets/6d64ae7e-c384-483f-89b8-36f035294b11" />

## NTUSER.DAT
- Files NTUSER.DAT là một hồ sơ người dùng hive, nó là một phần của registry. Mỗi người dùng được lưu trữ bên trong `C:\Users\%USERNAME%\NTUSER.DAT`.
- Nội dung của file NTUSER.DAT có thể được xem bằng công cụ Registry Explorer bởi Eric Zimmerman:
    - Công cụ có thể được tải bằng đường link https://ericzimmerman.github.io/#!index.md.
<img width="1874" height="960" alt="image" src="https://github.com/user-attachments/assets/19b0b6eb-9fa0-40c0-8a76-54a4c952b5a4" />

### LNK Files
- Files LNK là một file shortcut mà nó cho phép truy cập một cách nhanh chóng vào các files, folder, hoặc các chương trình của hệ thống được sử dụng một cách thường xuyên. Những files này thường có phần mở rộng là `.lnk` và có thể được tìm thấy ở những nơi như desktop, start menu, và thư mục tài liệu gần đây.
- Bất cứ khi nào một file được truy cập lần đầu tiên, file `.lnk` được tạo trong Recent folder. Những thông tin này là một phần hữu ích trong việc xác minh các file vừa được truy cập.
- Những files đó có thể được tìm thấy ở trong

+ `C:\Users\%USERNAME%\Recent`
+ `C:\Users\%USERNAME%\AppData\Roaming\Microsoft\Windows\Recent`
+ `C:\Users\%USERNAME%\AppData\Roaming\Microsoft\Office\Recent`
+ `C:\Users\%USERNAME%\Desktop`

- Có một cách để khám phá file LNK và giải nén ra những thông tin hữu ích từ nó là sử dụng một công cụ gọi là LECmd. Chúng ta có thể sử dụng nó để giải nén đầy đủ đường dẫn gốc của một file, ngày và giờ file được tạo, sửa đổi mới nhất, lần truy cập gần nhất, desktop name và địa chỉ MAC.
- Tools có thể được tải từ: https://github.com/EricZimmerman/LECmd
<img width="2555" height="1309" alt="image" src="https://github.com/user-attachments/assets/7e4839e5-de7d-47fd-87c1-2f48e26eb667" />

### Web Browsers

- Trình duyệt web được sử dụng rộng rãi trên toàn cầu. Trong bối cảnh của digital forensics, trình duyệt web cung cấp rất nhiều những thông tin về lịch sử trình duyệt người dùng, cookies, file downloads, mật khẩu được lưu, và nhiều hơn. Những thông tin này có thể được dùng để xác minh cái mà người dùng vừa ở đó, xác minh bất cứ hành động bất thường nào.
- Có rất nhiều trình duyệt web, nhưng tạm thời chúng ta chỉ đề cập đến Firefox và Chrome.
--- 
1. Firefox
   - Firefox lưu trữ dữ liệu mà có thể nó có giá trị trong quá trình điều tra digital forensics trong thư mục `C:\Users\%USERNAME%\AppData\Roaming\Mozilla\Firefox\Profiles`. bao gồm cookies, lưu thông tin đăng nhập, lịch sử trình duyệt và những thông tin khác về `.sqlite` và `.json`
   - Để xem được 1 file `.json` chúng ta có thể sử dụng bất cứ phần mềm text-editor nào.
   - Nhưng để xem nội dung của file `.sqlite` chúng ta cần một công cụ đặc trưng đó là: `Sqlitebroswer`

      `sqlitebrowser places.sqlite`
2. Save Login
   - Firefox mã hóa để lưu lại những lần đăng nhập sử dụng master key bên trong file `key4.db` được nằm ở trong hồ sơ của thư mục. Để giải nén tên người dùng và passwords, chúng ta có thể sử dụng một công cụ gọi là `firefox_encrypt` có thể được tải từ: https://github.com/unode/firefox_decrypt
   - Cách để tải tools đó về: 

          $ git clone https://github.com/unode/firefox_decrypt 
          Cloning into 'firefox_decrypt'...
          remote: Enumerating objects: 1163, done.
          remote: Counting objects: 100% (275/275), done.
          remote: Compressing objects: 100% (40/40), done.
          remote: Total 1163 (delta 250), reused 238 (delta 233), pack-reused 888
          Receiving objects: 100% (1163/1163), 414.55 KiB | 1.14 MiB/s, done.
          Resolving deltas: 100% (732/732), done.

           $ python3 firefox_decrypt.py hxdvwqnb.default-release 

          Website:   https://www.facebook.com
          Username: 'john.doe@example.com'
          Password: 'my_password123'
          
          Website:   https://twitter.com
          Username: 'john_doe'
          Password: 'my_twitter_password123'
          
          Website:   https://google.com
          Username: 'john.doe@gmail.com'
          Password: 'some_random_p4ssw0rd'
  3. Chrome
     - Chrome thì nó lưu trữ dữ liệu bao gồm mật khẩu được lưu, cookies và một số những thông tin hữu ích bên trong thư mục sau `C:\Users\%USERNAME%\AppData\Local\Google\Chrome\User Data\Default`. Những dữ liệu được mã hóa theo default, nhưng chìa khóa thì có thể được tìm thấ bên trong thư mục sau `C:\Users\%USERNAME%\AppData\Local\Google\Chrome\User Data\Local State`
  4. Event Logs
     - Event logs cung cấp một đoạn ghi vô cùng quan trọng cho hệ thống, bảo mật và các events của ứng dụng. Những logs này sẽ được tạo một cách tự động bởi Windows. và có thể cung cấp những thông tin có giá trị trong suốt quá trình điều tra.
     - Event logs được lưu trữ bên trong thư mục `C:\Users\System32\winevt\Logs` và có thẻ xem và phân tích bằng cách sử dụng Event Viewer, một công cụ được tạo bởi windows.
     - Có 3 dạng chính của Event logs của windows là system, security, application thì trong đó chúng ta chỉ quan tâm đến security là chủ yếu. The logs file có thể chứa đựng những thông tin sau:
        - `Security.evtx`
        - `Microsoft-Windows-Windows Defender%4Operational.evtx`
        - `Microsoft-Windows-Windows Firewall With Advanced Security%4Firewall.evtx`
        - `Microsoft-Windows-Powershell%4Operational.evtx`
      - Mỗi một event trong event logs đều có 1 con số đặc trưng cho event đó và chúng ta có một vài ví dụ như:
        
        <img width="858" height="620" alt="image" src="https://github.com/user-attachments/assets/67eb1545-0bba-4e58-ab2c-01f003204e4c" />

      - Here’s an example of event ID 1117 in the file Microsoft-Windows-Windows Defender%4Operational.evtx, viewed using the built-in Event Viewer
        <img width="1707" height="1181" alt="image" src="https://github.com/user-attachments/assets/2438513c-9ade-47d2-a5fb-1794fc79ad99" />




# Exercise
## 1. Sử dụng file registry của một hệ thống đã bị xâm nhập, và trả lời
### i.  mouse double-click speed : 500
### ii. The most recent typed path accessed as recorded in the registry is: 

`C:\Windows\System32\calc.exe`. Bởi vì recent typed path accessed là đường dẫn gần đây nhất mà người dùng nhập trên thanh (addressed bar) của File Explorer 
<img width="3821" height="2088" alt="image" src="https://github.com/user-attachments/assets/52f83668-6cfd-4efe-8639-40de478d7885" />

### iii. The new value added to the registry by the malware in order to establish persistence over the system?
  Bởi vì kẻ tấn công muốn thiết lập sự duy trì của malware trong hệ thống của người dùng một cách lâu dài, thì 1 trong số những khả năng mà kẻ tấn công có thể đặt malware đó chỉnh là trong phần `HKCU\SoftWare\Microsoft\Windows\CurrentVersion\Run\RunOnce` trong thư mục này thì mỗi lần khởi động máy tính thì malware sẽ đều được kích hoạt đảm bảo cho nó được tồn tại lâu dài trong hệ thống

<img width="3832" height="2159" alt="image" src="https://github.com/user-attachments/assets/5ff6a2a5-18ea-4c6b-90d2-15649df00e8a" />
<img width="2415" height="631" alt="image" src="https://github.com/user-attachments/assets/8fe1330c-2b5c-47cb-abe8-c1b178780c11" />

Đây là vị trí giá trị mà malware được thêm vào
