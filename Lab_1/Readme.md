
# Common Windows Artifacts.
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

## 2. Given the Firefox profile of a suspect, answer the following:
### i. What’s the username and password stored in the saved logins
Đầu tiên chúng ta cần phải biết là, các phần thuộc về credentials information đều bị Firefox chuyển hóa thành dạng không thể đọc được để tăng tính bảo mật trong file `login.json`, thế nên để đọc được username và password thì chúng ta cần sử dụng một công cụ đó gọi là **Firefox_Decrypt** được build sẳn trên github, đầu tiên chúng ta cần thực hiện thao tác tải về bằng lệnh:
```
git clone https://github.com/unode/firefox_decrypt 
Cloning into 'firefox_decrypt'...
remote: Enumerating objects: 1163, done.
remote: Counting objects: 100% (275/275), done.
remote: Compressing objects: 100% (40/40), done.
remote: Total 1163 (delta 250), reused 238 (delta 233), pack-reused 888
Receiving objects: 100% (1163/1163), 414.55 KiB | 1.14 MiB/s, done.
Resolving deltas: 100% (732/732), done.
```
Sau đó chúng ta chỉ cần chay lệnh firefox_decrypt là sẽ thấy được username và password trong file `login.json`
<img width="1908" height="438" alt="Screenshot 2025-11-21 151852" src="https://github.com/user-attachments/assets/9936300b-8814-4e0b-ab2b-989e6bb90a05" />

### ii. What’s the most frequently visited website?
Để tìm được trang web mà người dùng truy cập vào nhiều nhất, chúng ta có thể sử dụng 2 cách:
- Cách đầu tiên là dùng phần Browser Data của sqlitebrowser để thực hiện xem phần moz_places và tìm kiếm phần visitcount để suy ra được mục mà người dùng xem nhiều nhất như sau
  <img width="1912" height="1035" alt="Screenshot 2025-11-18 233111" src="https://github.com/user-attachments/assets/fa599986-9be7-4173-af40-5a5910901ad1" />

  Đầu tiên vào **places.sqlite**, đây là nơi chúng ta sẽ thực hiện xem các thông tin mà liên quan đến người dùng nhiều nhất.
  Sau đó vào phần **Browser Data**
  <img width="1386" height="916" alt="Screenshot 2025-11-18 234602" src="https://github.com/user-attachments/assets/357fc607-b2ea-4d7a-9bc4-a8bace267715" />

  ở đây chúng ta sẽ thấy được visitcount vào trang web https://amazon.com là nhiều nhất với nhiều lần truy cập trang web đó.
- Cách thứ 2 là dùng Execute SQL để thực hiện chay nhanh hơn.
  Đầu tiên di chuyển qua ô Execute SQL cùng hàng với mục Browser Data.
  <img width="3838" height="1723" alt="image" src="https://github.com/user-attachments/assets/63d01638-01e7-4b72-87c9-71ecfc8bda46" />

  Chạy lệnh Execute SQL sau:
  ```
  SELECT 
    url, 
    title, 
    visit_count
    FROM moz_places 
    ORDER BY visit_count DESC 
    LIMIT 10;
  ```
  Vậy chúng ta cũng có thể xác định được trang web được truy cập qua cách này
### iii. What’s the name of the file downloaded by the suspect?
Tương tự như trên thì chúng ta sẽ chạy 1 lệnh trong Execute SQL để tìm ra được file đã download về
<img width="1371" height="978" alt="Screenshot 2025-11-18 235528" src="https://github.com/user-attachments/assets/a58c5b66-d7fd-45c7-b000-9c677f82eb11" />

<img width="3839" height="1248" alt="image" src="https://github.com/user-attachments/assets/e15c99ab-a9bb-407a-9ab0-b000e92eaea5" />

Khi dùng Browser Data chúng ta cũng sẽ thấy có một đường dẫn của https://www.python.org/ftp/python/3.11.1/python-3.11.1-amd64.exe
Vậy file được tải về chinh là python-3.11.1-amd64.exe

## 3. Given the PowerShell Event logs of a compromised system, answer the following:
### i. What’s the command executed by the attacker to download a file on the system?
Trong bài này, chúng ta được đề cung cấp cho 1 file event được PowserShell, tức là kẻ tấn công đã dùng các lệnh độc để cố gắng cài mã độc vào hệ thống. Đầu tiên khi mở file SaveLog của PowerShellevent lên thì chúng ta có thể thấy được có 1 event xuất hiện lệnh prompt được mở lên.
<img width="1306" height="674" alt="Screenshot 2025-11-19 134524" src="https://github.com/user-attachments/assets/66ba890a-d8c0-468d-871e-45490641566d" />

Sau đó khi tìm các event sau chúng ta có thể thấy được 1 event rất đáng ngờ như sau.
<img width="1299" height="665" alt="Screenshot 2025-11-19 142025" src="https://github.com/user-attachments/assets/1cee9700-9b4a-40f2-bbe1-8a6e48aaac3e" />

Đây dường như là một lệnh cài đặt 1 cái gì đó về máy từ internet. Chúng ta sẽ phân tích câu lệnh này qua từng phần nhỏ
`Invoke-WebRequest -UseBasicParsing -Uri ... -OutFile "file.ps1"` đầu tiên đây là câu lệnh tìm thấy bên trong event. chia nhỏ nó ra thành từng phần để hiểu hơn
    - `Invoke-WebRequest`: (viết tắt là wget - iwr) đây là lệnh yêu cầu máy tính gửi một request HTTP ra ngoài internet, để tải về một tệp gì đó trong trường hợp này.
    - `-UseBasicParsing`: tham số này bảo PowerShell dùng bộ phận phân tích cơ bản nhất, bỏ qua Internet Explorer engine. Nó thường được dùng trong các script của các hacker dùng để tránh lỗi không tương thích với máy chủ, hoặc máy không có giao diện GUI để có thể đảm bảo lệnh chạy mượt mà nhất.
    - `-URI https://www.google.com/search?q=raw.githubusercontent.com//Lab 2/files/file.ps1` đây là địa chỉ nguồn trên internet.Kẻ tấn công dường như đang tải một file độc hại từ github về
    - Cuối cùng lệnh Output sẽ lưu file được tải vào "file.ps1"
### ii. Can you analyze the downloaded file and understand what’s the purpose of that file?
File được tải về là `file.ps1`, giờ hãy xem nội dung của file ấy là gì.
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/5da4372f-ffde-4ce9-994b-655d7f10105c" />

```
$data = "SGVsbG8sIHVzZSBmbGFne2V2M250X2wwZ3NfZjByX3RoM193MW59IGFzIHRoZSBhbnN3ZXIgdG8gdGhlIG9yaWdpbmFsIHF1ZXN0aW9uLg=="
$flag = [System.Text.Encoding]::ASCII.GetString([System.Convert]::FromBase64String($data))
Write-Output $flag
```
Đây là nội dung của file khi được tải về. Ở đây chúng ta có 1 biến data dường như nó đã được mã hóa theo dạng base64 theo những kí tự in hoa, in thường, số, và dấu bằng đặc trưng ở cuối, tiếp đó là biến flag cho thấy lệnh được giải mã ra và ghi output nó vào biến flag mới. Vậy ở đây chúng ta chỉ cần tập trung vào biến data với nội dung mã hóa là gì.
Đây là nội dung của đoạn base64 sau khi decode ra:
<img width="1721" height="937" alt="image" src="https://github.com/user-attachments/assets/490a99c4-96c6-49b5-bf22-f52aa76e3e72" />

Vậy Flag là: flag{ev3nt_l0gs_f0r_th3_w1n}

# Document Analysis and Steganography
Tài liệu là một cách phổ biến để gửi và lưu trữ các thông tin như là tin nhắn, báo casco, videos, hoặc là các ý tưởng. MS Office documents, Images và audio files là các format mà chúng ta sử dụng phổ biến nhất qua mỗi ngày. Tuy nhiên, Bên cạnh những gì chúng ta viết trong tài liệu word hoặc nghe từ các file audio, thì những tài liệu trên còn có thể chứa đựng các tin nhắn ẩn, hoặc các đoạn code độc hại, và có thể thực thi khi chúng ta mở nó lên. Trong lab này chúng ta sẽ khám phá các kỹ thuật để phân tích và luyện tập với tài liệu trên.
# Microsoft Office Documents
Có 2 loại format file chính được sử dụng bởi Microsoft Office documents:
- OLE (Object Linking and Embedding)
- OOXML (Office Open XML)
## OLE(Object Linking and Embedding)
OLE là một format file được sử dụng trong các phiên bản đầu tiên như Microsoft Office giữa 1997 và 2003. Nó được định nghĩa là "file within a file" tức là sẽ có 1 file khác bên trong 1 file cấu trúc này cho phép có thể nhúng 1 file khác bên trong 1 file.Lấy ví dụ là 1 trang Excel bên trong 1 trang pdf Word.
Nó hỗ trợ cho file có phần mở rộng như: `.rtf`, `.doc`, `.ppt`, và `.xls` hoặc hơn.
## OOXML(Office Open XML)
OOXML là loại format file được sử dụng cho các phiên bản Micorsoft Office hiện tại, cái được dựa trên XML - là loại format dựa trên office document.
Phần mở rộng của tài liệu này bao gồm `.docx`, `.pptx`, và `.xlsx` và các cái khác.
Phần quan trọng khác là format của OOXML là được lưu trữ tài liệu dưới dạng Container ZIP. Có nghĩa là những tài liệu như Word.Excel,PPt, là một file zip. Bằng cách thay đổi tên của nó từ `.docx`, `.xlsx` hoặc `.pptx` thành `.zip`, bạn có thể giải nén các nội dung của tệp và xem phần bên trong của XML files. Điều này có ý nghĩa rất lớn trong pháp y kĩ thuật số, nó cho phép các nhà điều tra có thể phân tích nội dung của tài liệu mà không phải thay đổi nó.
## Giải phẫu tài liệu OOXML(Word Document - Docx)
Khi giải nén một tài liệu `.docx`, chúng ta thu được một cấu trúc thư mục tiêu chuẩn, nơi mỗi thành phần(văn bản, hình ảnh, cài đặt) được lưu trữ trong cái file XML riêng biệt.
Cấu trúc thư mục ví dụ:
```
$ unzip Doc1.docx                       
Archive:  Doc1.docx
  inflating: [Content_Types].xml     
  inflating: _rels/.rels             
  inflating: word/document.xml       
  inflating: word/_rels/document.xml.rels  
  inflating: word/theme/theme1.xml   
  inflating: word/settings.xml       
  inflating: word/styles.xml         
  inflating: word/webSettings.xml    
  inflating: word/fontTable.xml      
  inflating: docProps/core.xml       
  inflating: docProps/app.xml
```
Đây là cấu trúc của 1 file Word document trông như thế này:
```
.
├── [Content_Types].xml
├── docProps
│   ├── app.xml
│   └── core.xml
├── _rels
│   └── .rels
└── word
    ├── document.xml
    ├── fontTable.xml
    ├── _rels
    │   └── document.xml.rels
    ├── settings.xml
    ├── styles.xml
    ├── theme
    │   └── theme1.xml
    └── webSettings.xml
```
### [Content-Typed].xml
File này chứa đựng những thông tin về loại nội dung hiện có trong tài liệu và phần mở rộng tập tin tương ứng của họ.
### 📂 docProps
Folder này chứa đựng 2 files chính là: **core.xml** và **app.xml**
- `app.xml` - chứa thông tin về các ứng dụng được sử dụng để tạo nên document trên.
```xml
 <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<Properties xmlns="http://schemas.openxmlformats.org/officeDocument/2006/extended-properties" xmlns:vt="http://schemas.openxmlformats.org/officeDocument/2006/docPropsVTypes">
  <Template>Normal.dotm</Template>
  <TotalTime>0</TotalTime>
  <Pages>1</Pages>
  <Words>1</Words>
  <Characters>12</Characters>
  <Application>Microsoft Office Word</Application>
  <DocSecurity>0</DocSecurity>
  <Lines>1</Lines>
  <Paragraphs>1</Paragraphs>
  <ScaleCrop>false</ScaleCrop>
  <Company/>
  <LinksUpToDate>false</LinksUpToDate>
  <CharactersWithSpaces>12</CharactersWithSpaces>
  <SharedDoc>false</SharedDoc>
  <HyperlinksChanged>false</HyperlinksChanged>
  <AppVersion>16.0000</AppVersion>
</Properties>
```
- `core.xml` - chứa các thông tin metadata của các tài liệu, như là author's name, ngày tạo, ngày sửa gần nhất.
```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<cp:coreProperties xmlns:cp="http://schemas.openxmlformats.org/package/2006/metadata/core-properties" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:dcterms="http://purl.org/dc/terms/" xmlns:dcmitype="http://purl.org/dc/dcmitype/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <dc:title/>
  <dc:subject/>
  <dc:creator>Saad Javed</dc:creator>
  <cp:keywords/>
  <dc:description/>
  <cp:lastModifiedBy>Saad Javed</cp:lastModifiedBy>
  <cp:revision>2</cp:revision>
  <dcterms:created xsi:type="dcterms:W3CDTF">2023-02-04T15:44:00Z</dcterms:created>
  <dcterms:modified xsi:type="dcterms:W3CDTF">2023-02-04T15:44:00Z</dcterms:modified>
</cp:coreProperties>
```
### 📂 _rels
Folders này chứa những tên file như `.rels`
- `.rels` - chứa các thông tin về các mối quan hệ giữa các phần khác nhau trong tài liệu như à `app.xml` và `core.xml`.
### 📂 word
Folder này chứa những nội dung hiện có của tài liệu.
- `document.xml` - chứa những đoạn text hiện tại của tài liệu.
```xml 
<!-- SNIP -->
  <w:body>
    <w:p w14:paraId="68F74602" w14:textId="442B891B" w:rsidR="00D473D4" w:rsidRPr="00B20485" w:rsidRDefault="00B20485">
      <w:pPr>
        <w:rPr>
          <w:lang w:val="en-US"/>
        </w:rPr>
      </w:pPr>
      <w:r>
        <w:rPr>
          <w:lang w:val="en-US"/>
        </w:rPr>
        <w:t>Hello World!</w:t>
      </w:r>
    </w:p>
    <w:sectPr w:rsidR="00D473D4" w:rsidRPr="00B20485">
      <w:pgSz w:w="11906" w:h="16838"/>
      <w:pgMar w:top="1440" w:right="1440" w:bottom="1440" w:left="1440" w:header="708" w:footer="708" w:gutter="0"/>
      <w:cols w:space="708"/>
      <w:docGrid w:linePitch="360"/>
    </w:sectPr>
  </w:body>
</w:document>
```
- `fontTable.xml` - chứa những thông tin về font được sử dụng bên trong tài liệu.
- **📂 _rels —** chứa 1 file `document.xml.rels`
    - `document.xml.rels` - chứa những thông tin về các mối quan hệ giữa các phần khác nhau trong tài liệu, như là styles, themes, settings và các URIs cho các link bên ngoài.
- `setting.xml` - chứa các cài đặt của tài liệu và cấu hình thông tin.
- `styles.xml` - chứa thông tin về styles sử dụng trong tài liệu.
-  **📂 theme —** chứa các file về theme được sử dụng trong tài liệu
    - `theme1.xml` - chứa các theme hiện có trong nội dung.
- `webSettings.xml` - chứa thông tin về các cài đặt cụ thể của web cho tài liệu, như là khung cài đặt HTML và cũng nhuwlamf thế nào mà tài liệu có thể xử lí khi lưu một HTML.
## Macro-Enabled Documents
Macro-Enabled documents là tài liệu chứa macro, cái có thể thiết lập nên các hướng dẫn để hoàn thành các tác vụ một cách tự động. Macros có thể được viết bởi Visual Basic for Applications (VBA) và có thể được sử dụng để thực hiện nhiều tác vụ cùng lúc. như là formating text, thực hiện tính toán và tự động hóa các tiến trình phức tạp. Tuy nhiên, những kẻ tấn công cũng thường sử dụng tiện ích của chức năng cho Office document với phishing attack và nhúng các macros độc hịa và để thực hiện các hành động độc hại và tải malware về.

Phần mở rộng của tài liệu này bao gồm `.docm`, `.pptm` và `.xlsm` và hơn nữa.

Để lấy ví dụ, chúng ta hãy tạo ra một tài liệu trống và theo các bước sau.
1. Nhấn vào View -> Macros -> View macros.
<img width="405" height="224" alt="image" src="https://github.com/user-attachments/assets/830d834e-6141-4a69-be56-ca1fcceb03a8" />

2. Đặt cho nó cái tên vdu HelloWorld. chọn vào Document1 (document hiện tai) bên dưới Macros in và chọn create.
<img width="445" height="362" alt="image" src="https://github.com/user-attachments/assets/ca58a798-126f-4482-9a19-73a25af921da" />

3. Dán vào trong ô đó đoạn code sau:
```
Sub HelloWorld()

Dim doc As Document
Set doc = Word.ActiveDocument
doc.Content.InsertAfter ("Hello, World!")

End Sub
```
<img width="872" height="538" alt="image" src="https://github.com/user-attachments/assets/634e4569-121b-4db2-a6a3-e6fff943f98d" />

4. Đóng Microsoft Visual Basic for Application tab.
5. Lặp lại bước 1 và chọn vào HelloWorld macro và nhấn vào chạy.
6. Hiện thì `Hello, World` đã được viết trong tài liệu.
7. Lưu trong tài liệu tại `.docm`
Theo việc giải phẫu OOXML file, thì macro hiện được lưu trữ bên trong word/vbaProject.bin, tuy nhiên, chúng ta sẽ không thể đọc được nó vì nó ở dạng nhị phân. Nhưng, chúng ta có thể sử dụng một tập hợp các tools gọi là oletools để phân tích các macros từ OLE files.
Để tải được tools thì chúng ta sử dụng lệnh `sudo -H pip install -U oletools`.
và bây giờ sẽ sử dụng `oleid` để xem những thứ được nhúng bên trong:
```
$ oleid HelloWorld.docm   
XLMMacroDeobfuscator: pywin32 is not installed (only is required if you want to use MS Excel)
oleid 0.60.1 - http://decalage.info/oletools
THIS IS WORK IN PROGRESS - Check updates regularly!
Please report any issue at https://github.com/decalage2/oletools/issues

Filename: HelloWorld.docm
WARNING  For now, VBA stomping cannot be detected for files in memory
--------------------+--------------------+----------+--------------------------
Indicator           |Value               |Risk      |Description               
--------------------+--------------------+----------+--------------------------
File format         |MS Word 2007+ Macro-|info      |                          
                    |Enabled Document    |          |                          
                    |(.docm)             |          |                          
--------------------+--------------------+----------+--------------------------
Container format    |OpenXML             |info      |Container type            
--------------------+--------------------+----------+--------------------------
Encrypted           |False               |none      |The file is not encrypted 
--------------------+--------------------+----------+--------------------------
VBA Macros          |Yes                 |Medium    |This file contains VBA    
                    |                    |          |macros. No suspicious     
                    |                    |          |keyword was found. Use    
                    |                    |          |olevba and mraptor for    
                    |                    |          |more info.                
--------------------+--------------------+----------+--------------------------
XLM Macros          |No                  |none      |This file does not contain
                    |                    |          |Excel 4/XLM macros.       
--------------------+--------------------+----------+--------------------------
External            |0                   |none      |External relationships    
Relationships       |                    |          |such as remote templates, 
                    |                    |          |remote OLE objects, etc   
--------------------+--------------------+----------+--------------------------
```

Trong kết quả chúng ta thấy được rằng nó kêu chúng ta sử dụng olevba để xem xét cái macro bên trong 
```
$ olevba HelloWorld.docm
XLMMacroDeobfuscator: pywin32 is not installed (only is required if you want to use MS Excel)
olevba 0.60.1 on Python 3.10.8 - http://decalage.info/python/oletools
===============================================================================
FILE: HelloWorld.docm
Type: OpenXML
WARNING  For now, VBA stomping cannot be detected for files in memory
-------------------------------------------------------------------------------
VBA MACRO ThisDocument.cls 
in file: word/vbaProject.bin - OLE stream: 'VBA/ThisDocument'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
(empty macro)
-------------------------------------------------------------------------------
VBA MACRO NewMacros.bas 
in file: word/vbaProject.bin - OLE stream: 'VBA/NewMacros'
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
Sub HelloWorld()

Dim doc As Document
Set doc = Word.ActiveDocument
doc.Content.InsertAfter ("Hello, World!")

End Sub
No suspicious keyword or IOC found.
```
# Web Attack Forensics
Ứng dụng web là một phần không thể thiếu trong cuộc sống hiện nay và đã được sử dụng trong phần lớn các hoạt động, từ mua hàng online, dùng để thanh toán hoặc là mạng xã hội. Tuy nhiên, việc sử dụng rộng rãi sẽ mở ra một bề mặt tấn công lớn cho các tác nhân xấu khai thác và giành được chỗ đứng ban đầu vào hệ thống.
Trong lab này, chúng ta sẽ tìm hiểu về các loại tấn công khác nhau phổ biến đối với web applications và khám phá về các kĩ thuật để xác nhận các cuộc tấn công bằng cách phân tích web application logs và web application firewall logs để tìm ra điểm chính của attack, và truy tìm các nguyên nhân gốc rễ bằng cách xác định lỗ hổng đã bị khai thác.
## Thiết lập môi trường
Trước khi đi sâu vào chủ đề của tấn công webs và forensics, hãy bắt đầu thiết lập một môi trường Docker. Điều này cho phép chúng ta có thể thực hành và hiểu toàn diện về tài liệu được đề cập.
```
git clone https://github.com/vonderchild/digital-forensics-lab && cd digital-forensics-lab/Lab\ 4/files/app
```
### Tải về Docker
```
sudo apt-get update
sudo apt-get install -y docker.io
sudo service docker start
```
### Xây dựng & Và chạy Docker Image
```
docker build -t app:latest .
docker run -p 9090:80 app:latest
```
# Web Attack & Forensics
### Web Application & WAF Logs
Web application logs đóng một vai trò quan trọng trong digital forensics vì nó giúp chúng ta xem lại các hành động của người dùng, xác nhận các mối đe dọa tiềm năng, truy tìm nguồn gốc của cuộc tấn công và xác định mức độ ảnh hưởng của nó. Trong lab này, chúng ta sẽ tập trung vào Apache, một máy chủ web rộng rãi được dùng để lưu trữ các ứng dụng web. Một nhật ký được tạo bởi Apache sẽ chứa access logs và error logs. Access logs chứa những thông tin về những yêu cầu đến như là Ip address của client, thời gian và ngày của yêu cầu, công cụ của yêu cầu (vdu GET, POST), những yêu cầu URI, những mã trạng thái phản hồi(200, 403, 404) và tác nhân của người dùng. Error logs, là một trường hợp khác, chứa những thông tin về các lỗi được đếm bởi server, như là các yêu cầu thất bại, các sự kiện không mong đợi đã xảy ra trong suốt quá trình của yêu cầu. Nhật ký này được tìm thấy trong `/var/log/apache2` trong hệ thống Linux.

Web Application firewalls (WAFs) là một khía cạnh quan trọng của bảo mật ứng dụng web. WAF cung cấp các lớp bảo mật cho ứng dụng bởi chặn tất cả những lưu lượng độc hại
trước khi nó ảnh hưởng đến các ứng dụng. Trong lab này, chúng ta sẽ sử dụng Modsecurity làm tường lửa cho ứng dụng web của chúng ta. Vị trí mặc định cho audit logs là `/var/log/apache/modsec_security_audit.log`. Khi một lỗi hay bất cứ nỗ lực độc hại sẽ bị đếm bởi server và ghi vào `/var/log/apache2/error.log`.
```
var
└── log
    └── apache2
        ├── access.log
        ├── error.log
        ├── modsec_audit.log
        └── other_vhosts_access.log
```
## Các kiểu tấn công web phổ biến & Logs
Có rất nhiều lỗ hổng có thể bị khai thác trong web application có thể đi từ các lỗ hổng có tác động chưa lớn đến các lổ hổng thật sự nguy hiểm nếu kẻ tấn công có thể khai thác được vào và có một ví trí trong đặc quyền của server. Một số lỗ hổng như mà chúng ta chú ý trong phiên này bao gồm: Path Traversal, Remote Control Executions (RCE), SQL Injections.
### Path Traversal
Là một lỗ hổng cho phép kẻ tấn công truy cập vào file/folder nằm ngoài thư mục của web/root, nó thường được thực hiện bằng cách thao tác với các "enter field" đường dẫn tệp trong ứng dụng web để truy cập các tệp mà ứng dụng có quyền truy cập, nhưng kẻ tấn công thì không, nói dễ hơn là kẻ tấn công sẽ nhập vào các đường dẫn mà khiến hắn có thể truy cập vào các tệp mà những người dùng bình thường không thể truy cập chẳng hạn như truy cập vào các tệp cấu hình hoặc mã nguồn.
Ví dụ: bạn đang ở thư mục chính là `/home/kali/`. Để thay đổi bạn quay trở về `/home/` thì bạn sẽ dùng lệnh `cd ../`. Tương tự như vậy, kẻ tấn công cũng có thể sử dụng cách này để đi vào phần gốc/các tệp bên ngoài ứng dụng web. 
```
Lưu ý: Thuật ngữ Path Traversal thường được sử dụng thay thế cho nhau với Local File inclusion (LFI), tuy nhiên cả hai đều là những lỗ hổng khác nhau; path traversal được giới han trong việc đọc các files, còn LFI cho phép thực thi các files đó trên server.
```
<img width="852" height="1378" alt="image" src="https://github.com/user-attachments/assets/5307f545-adf0-47ee-8a38-611af4258884" />

Đây là giao diện bình thường, nhưng nếu chúng ta không nhập vào những tấm hình, mà muốn xâm nhập vào các thông tin /etc/passwd/. Rõ ràng sau vài lần thử với `../`, thì chúng ta đã thấy mình đã khai thác được, các thông tin chung về người dùng, và tên người dùng trong root. Đó là một ví dụ của Path traversal, khi các attacker đã sử dụng lỗ hổng này để khai thác các thông tin chung
Nhận dạng bằng các chuỗi kí tự: ../../ , ..2%,..
<img width="849" height="1321" alt="image" src="https://github.com/user-attachments/assets/583cd1e1-397f-4a75-acf6-72c2fdaec5d0" />

Bây giờ chúng ta đã quen với phương pháp khai thác lỗ hổng này, hãy tiến hành tìm hiểu cách phát hiện nó trong nhật ký của chúng ta. Để truy cập nhật kí bên trong docker, thì chúng ta sử dụng lệnh `docker ps -q` để in ra được id của container hiện tại, và dùng lệnh `docker exec -it <ID_container> bash` để truy cập vào giao diện bash của linux trong container của id đó.
```
t0b1ra@tobiraNduy:~$ docker ps -q
5988a9297d1e

t0b1ra@tobiraNduy:~$ docker exec -it 5988a9297d1e bash
root@5988a9297d1e:/#
```
Bây giờ chúng ta truy cập vào thư mục chứa nhập ký truy cập và in chúng ta 
```
root@5988a9297d1e:/var/log/apache2# cat access.log
172.17.0.1 - - [02/Dec/2025:13:39:36 +0500] "GET /view.php?image=/../../../../../etc/passwd HTTP/1.1" 200 633 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
172.17.0.1 - - [02/Dec/2025:13:39:36 +0500] "GET /favicon.ico HTTP/1.1" 404 489 "http://127.0.0.1:9090/view.php?image=/../../../../../etc/passwd" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
172.17.0.1 - - [02/Dec/2025:13:49:42 +0500] "GET /view.php?image= HTTP/1.1" 200 203 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
172.17.0.1 - - [02/Dec/2025:13:52:19 +0500] "GET /images.php HTTP/1.1" 200 1114 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
172.17.0.1 - - [02/Dec/2025:13:52:19 +0500] "GET /images/starry_night.jpg HTTP/1.1" 304 250 "http://127.0.0.1:9090/images.php" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
172.17.0.1 - - [02/Dec/2025:13:52:19 +0500] "GET /images/red_vineyards.jpg HTTP/1.1" 304 251 "http://127.0.0.1:9090/images.php" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
172.17.0.1 - - [02/Dec/2025:13:52:19 +0500] "GET /images/almond_blossom.jpg HTTP/1.1" 304 251 "http://127.0.0.1:9090/images.php" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
172.17.0.1 - - [02/Dec/2025:14:29:24 +0500] "GET /images=? HTTP/1.1" 404 490 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
172.17.0.1 - - [02/Dec/2025:14:29:36 +0500] "GET /images=%C3%A1d HTTP/1.1" 404 490 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
172.17.0.1 - - [02/Dec/2025:14:29:59 +0500] "GET /etc/passwd HTTP/1.1" 404 490 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
172.17.0.1 - - [02/Dec/2025:14:31:24 +0500] "GET /view.php?image= HTTP/1.1" 200 203 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
172.17.0.1 - - [02/Dec/2025:14:31:40 +0500] "GET /view.php?image=/../../../../etc/passwd HTTP/1.1" 200 633 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
```
Như chúng ta thấy được rằng, logs hiển thị đầy đủ các yêu cầu được thực hiện đến máy chủ `172.17.0.1` sử dụng trình duyệt Mozilla/Firefox để truy cập vào `/view.php`, `/image.php`. Chúng ta còn thấy các logs ghi lại việc mà ban nãy chúng ta đã khai thác path traversal của trang web này in ra `/etc/passwd`
Bước tiếp theo là kiểm tra nhật ký Modsecurity WAF tạo ra.
- Rude ID: `930100` hoặc `930110`
- Message: Path traversal attack (/../)
- Matched Data: /../ found within Request_URI
- Severity CRITICAl - mức độ nguy hiểm cấp cao nhất.
## Remote Control Execution(RCE)
Trong một cuộc tấn công RCE(Remote Control Execution), kẻ tấn công có thể thực thi các lệnh độc hại trên máy chủ, tương tự như thực thi các lệnh trong thiết bị đầu cuối. Trong một số trường hợp nhất định, điều này cũng có thể được gọi là lỗ hổng Command Insert.

Ví dụ: Nếu một trang web cho phép người dùng nhập lệnh để tìm kiếm tệp, kẻ tấn công tệp có thể nhập lệnh xóa tất cả tệp trên máy chủ bằng cách chèn các lệnh bổ sung như `; rm -rf /` vào trường input. Điều này có khả năng có thể làm tổn hại đến toàn bộ hệ thống nếu trang web có các quyền cần thiết để thực thi các lệnh đó.

Bây giờ chúng ta sẽ đi vào thực hành thử trên web đã dựng:

1.  `id`
2.  `cat /etc/passwd`
3.  `cat /etc/shadow`
```
Bây giờ chúng ta truy cập vào `access.log`:
172.17.0.1 - - [02/Dec/2025:15:21:11 +0500] "POST /command.php HTTP/1.1" 200 1033 "http://127.0.0.1:9090/command.php" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
172.17.0.1 - - [02/Dec/2025:15:22:50 +0500] "POST /command.php HTTP/1.1" 200 1045 "http://127.0.0.1:9090/command.php" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
172.17.0.1 - - [02/Dec/2025:15:23:08 +0500] "POST /command.php HTTP/1.1" 200 1051 "http://127.0.0.1:9090/command.php" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
172.17.0.1 - - [02/Dec/2025:15:24:12 +0500] "POST /command.php HTTP/1.1" 200 1376 "http://127.0.0.1:9090/command.php" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
172.17.0.1 - - [02/Dec/2025:15:24:31 +0500] "POST /command.php HTTP/1.1" 200 1020 "http://127.0.0.1:9090/command.php" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
172.17.0.1 - - [02/Dec/2025:15:24:32 +0500] "POST /command.php HTTP/1.1" 500 1087 "http://127.0.0.1:9090/command.php" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
172.17.0.1 - - [02/Dec/2025:15:24:32 +0500] "POST /command.php HTTP/1.1" 500 1087 "http://127.0.0.1:9090/command.php" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
172.17.0.1 - - [02/Dec/2025:15:24:32 +0500] "POST /command.php HTTP/1.1" 500 1087 "http://127.0.0.1:9090/command.php" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36"
```
Có thể thấy các logs trên đều ghi lại các yêu cầu đến và không tiết lộ các lệnh người dùng nhập vì đó là yêu cầu POSR. Đây là nơi WAF phát huy tác dụng vì nó có thể hiển thị cả nội dung và yêu cầu và phản hồi. Để xem người dùng đã nhập gì chúng ta vào logs WAF.
```
<SNIP>

Message: Warning. Matched phrase "etc/passwd" at ARGS:cmd. [file "/usr/share/modsecurity-crs/rules/REQUEST-930-APPLICATION-ATTACK-LFI.conf"] [line "97"] [id "930120"] [msg "OS File Access Attempt"] [data "Matched Data: etc/passwd found within ARGS:cmd: cat /etc/passwd"] [severity "CRITICAL"] [ver "OWASP_CRS/3.3.2"] [tag "application-multi"] [tag "language-multi"] [tag "platform-multi"] [tag "attack-lfi"] [tag "paranoia-level/1"] [tag "OWASP_CRS"] [tag "capec/1000/255/153/126"] [tag "PCI/6.5.4"]
Message: Warning. Matched phrase "etc/passwd" at ARGS:cmd. [file "/usr/share/modsecurity-crs/rules/REQUEST-932-APPLICATION-ATTACK-RCE.conf"] [line "500"] [id "932160"] [msg "Remote Command Execution: Unix Shell Code Found"] [data "Matched Data: etc/passwd found within ARGS:cmd: cat/etc/passwd"] [severity "CRITICAL"] [ver "OWASP_CRS/3.3.2"] [tag "application-multi"] [tag "language-shell"] [tag "platform-unix"] [tag "attack-rce"] [tag "paranoia-level/1"] [tag "OWASP_CRS"] [tag "capec/1000/152/248/88"] [tag "PCI/6.5.2"]

<SNIP>

Apache-Error: [file "apache2_util.c"] [line 271] [level 3] [client 172.17.0.1] ModSecurity: Warning. Matched phrase "etc/passwd" at ARGS:cmd. [file "/usr/share/modsecurity-crs/rules/REQUEST-930-APPLICATION-ATTACK-LFI.conf"] [line "97"] [id "930120"] [msg "OS File Access Attempt"] [data "Matched Data: etc/passwd found within ARGS:cmd: cat /etc/passwd"] [severity "CRITICAL"] [ver "OWASP_CRS/3.3.2"] [tag "application-multi"] [tag "language-multi"] [tag "platform-multi"] [tag "attack-lfi"] [tag "paranoia-level/1"] [tag "OWASP_CRS"] [tag "capec/1000/255/153/126"] [tag "PCI/6.5.4"] [hostname "127.0.0.1"] [uri "/command.php"] [unique_id "Y-rT-PsFa_lKkx8ckcXpMAAAAAQ"]
Apache-Error: [file "apache2_util.c"] [line 271] [level 3] [client 172.17.0.1] ModSecurity: Warning. Matched phrase "etc/passwd" at ARGS:cmd. [file "/usr/share/modsecurity-crs/rules/REQUEST-932-APPLICATION-ATTACK-RCE.conf"] [line "500"] [id "932160"] [msg "Remote Command Execution: Unix Shell Code Found"] [data "Matched Data: etc/passwd found within ARGS:cmd: cat/etc/passwd"] [severity "CRITICAL"] [ver "OWASP_CRS/3.3.2"] [tag "application-multi"] [tag "language-shell"] [tag "platform-unix"] [tag "attack-rce"] [tag "paranoia-level/1"] [tag "OWASP_CRS"] [tag "capec/1000/152/248/88"] [tag "PCI/6.5.2"] [hostname "127.0.0.1"] [uri "/command.php"] [unique_id "Y-rT-PsFa_lKkx8ckcXpMAAAAAQ"]

<SNIP>

Apache-Error: [file "apache2_util.c"] [line 271] [level 3] [client 172.17.0.1] ModSecurity: Warning. Operator GE matched 5 at TX:inbound_anomaly_score. [file "/usr/share/modsecurity-crs/rules/RESPONSE-980-CORRELATION.conf"] [line "91"] [id "980130"] [msg "Inbound Anomaly Score Exceeded (Total Inbound Score: 13 - SQLI=0,XSS=0,RFI=0,LFI=5,RCE=5,PHPI=0,HTTP=0,SESS=0): individual paranoia level scores: 13, 0, 0, 0"] [ver "OWASP_CRS/3.3.2"] [tag "event-correlation"] [hostname "127.0.0.1"] [uri "/command.php"] [unique_id "Y-rT-PsFa_lKkx8ckcXpMAAAAAQ"]

<SNIP>
```
Chúng ta chỉ có thể xem được các log ghi lại các lệnh như `/etc/passwd`, bởi vì WAF đã phát hiện nỗ lực phiên LFI và RCE.
Đối với lệnh `/etc/shadow` chúng ta không thấy máy chủ phản hồi là do máy chủ đang chạy với quyền người dùng và không có đặc quyền `www-data`, và quyền truy cập cần thiết để xem nội dung của `/etc/shadow` chúng ta có thể xác nhận điều này qua lỗi:
```
root@5988a9297d1e:/var/log/apache2# cat error.log | grep 'Permission denied'
cat: /etc/shadow: Permission denied
```
Nhưng máy chủ vẫn có thể xác định được đây là một nỗ lực khai thác LFI và RCE nên vẫn sẽ ghi nó lại bên trong modsec_audit.logs
```
<SNIP>

Message: Warning. Matched phrase "etc/shadow" at ARGS:cmd. [file "/usr/share/modsecurity-crs/rules/REQUEST-930-APPLICATION-ATTACK-LFI.conf"] [line "97"] [id "930120"] [msg "OS File Access Attempt"] [data "Matched Data: etc/shadow found within ARGS:cmd: cat /etc/shadow"] [severity "CRITICAL"] [ver "OWASP_CRS/3.3.2"] [tag "application-multi"] [tag "language-multi"] [tag "platform-multi"] [tag "attack-lfi"] [tag "paranoia-level/1"] [tag "OWASP_CRS"] [tag "capec/1000/255/153/126"] [tag "PCI/6.5.4"]
Message: Warning. Matched phrase "etc/shadow" at ARGS:cmd. [file "/usr/share/modsecurity-crs/rules/REQUEST-932-APPLICATION-ATTACK-RCE.conf"] [line "500"] [id "932160"] [msg "Remote Command Execution: Unix Shell Code Found"] [data "Matched Data: etc/shadow found within ARGS:cmd: cat/etc/shadow"] [severity "CRITICAL"] [ver "OWASP_CRS/3.3.2"] [tag "application-multi"] [tag "language-shell"] [tag "platform-unix"] [tag "attack-rce"] [tag "paranoia-level/1"] [tag "OWASP_CRS"] [tag "capec/1000/152/248/88"] [tag "PCI/6.5.2"]

<SNIP> 

Apache-Error: [file "apache2_util.c"] [line 271] [level 3] [client 172.17.0.1] ModSecurity: Warning. Matched phrase "etc/shadow" at ARGS:cmd. [file "/usr/share/modsecurity-crs/rules/REQUEST-930-APPLICATION-ATTACK-LFI.conf"] [line "97"] [id "930120"] [msg "OS File Access Attempt"] [data "Matched Data: etc/shadow found within ARGS:cmd: cat /etc/shadow"] [severity "CRITICAL"] [ver "OWASP_CRS/3.3.2"] [tag "application-multi"] [tag "language-multi"] [tag "platform-multi"] [tag "attack-lfi"] [tag "paranoia-level/1"] [tag "OWASP_CRS"] [tag "capec/1000/255/153/126"] [tag "PCI/6.5.4"] [hostname "127.0.0.1"] [uri "/command.php"] [unique_id "Y-rT_V10ftOo0AKdI-JC2gAAAAU"]
Apache-Error: [file "apache2_util.c"] [line 271] [level 3] [client 172.17.0.1] ModSecurity: Warning. Matched phrase "etc/shadow" at ARGS:cmd. [file "/usr/share/modsecurity-crs/rules/REQUEST-932-APPLICATION-ATTACK-RCE.conf"] [line "500"] [id "932160"] [msg "Remote Command Execution: Unix Shell Code Found"] [data "Matched Data: etc/shadow found within ARGS:cmd: cat/etc/shadow"] [severity "CRITICAL"] [ver "OWASP_CRS/3.3.2"] [tag "application-multi"] [tag "language-shell"] [tag "platform-unix"] [tag "attack-rce"] [tag "paranoia-level/1"] [tag "OWASP_CRS"] [tag "capec/1000/152/248/88"] [tag "PCI/6.5.2"] [hostname "127.0.0.1"] [uri "/command.php"] [unique_id "Y-rT_V10ftOo0AKdI-JC2gAAAAU"]

<SNIP>

Apache-Error: [file "apache2_util.c"] [line 271] [level 3] [client 172.17.0.1] ModSecurity: Warning. Operator GE matched 5 at TX:inbound_anomaly_score. [file "/usr/share/modsecurity-crs/rules/RESPONSE-980-CORRELATION.conf"] [line "91"] [id "980130"] [msg "Inbound Anomaly Score Exceeded (Total Inbound Score: 13 - SQLI=0,XSS=0,RFI=0,LFI=5,RCE=5,PHPI=0,HTTP=0,SESS=0): individual paranoia level scores: 13, 0, 0, 0"] [ver "OWASP_CRS/3.3.2"] [tag "event-correlation"] [hostname "127.0.0.1"] [uri "/command.php"] [unique_id "Y-rT_V10ftOo0AKdI-JC2gAAAAU"

<SNIP>
```
## SQL Injection
SQL injection hay SQLi là kẻ tấn công thao túng các trường đầu vào của trang web để gửi mã SQL độc hại, sau đó mã này được thực thi trên máy chủ.
Ví dụ: hãy xem xét một trang web có trang đăng nhập có tên người dùng và mật khẩu. Thông thường, trang web sẽ so sánh thông tin xác thực đã nhập với thông tin được lưu trữ trong cơ sở dữ liệu để xác định xem người dùng có được cấp quyền truy cập hay không. Nếu mã của trang web dễ bị tấn công bởi SQL injection, kẻ tấn công có thể dùng lệnh ` ' OR 1=1--` với tên người dùng của họ, về cơ bản sẽ lừa CSDL trả về tất cả các bản ghi và bỏ qua xác thực.
Thực thi lệnh:
1. `user1' and 1=1 #` -> đây là lệnh in ra thông tin user1 với tên và email.
2. `usser1' union select username, email, password from users #`
<img width="1696" height="1328" alt="image" src="https://github.com/user-attachments/assets/970418f8-8a2c-402f-954a-c3e4cba27b5b" />

Chúng ta sử dụng truy vấn đầu tiên để kiểm tra xem ứng dụng có cho phép chạy lệnh thực thi đến máy chủ không, và khi thấy có thể chúng ta sử dụng cách tấn công SQL injection để trích xuất mk và email người dùng.

Vì cả hai đều là yêu cầu POST nên chúng ta kiểm tra chúng trong `error.log`
```
[Tue Dec 02 15:39:27.418712 2025] [security2:error] [pid 268] [client 172.17.0.1:53096] [client 172.17.0.1] ModSecurity: Warning. detected SQLi using libinjection with fingerprint 's&1c' [file "/usr/share/modsecurity-crs/rules/REQUEST-942-APPLICATION-ATTACK-SQLI.conf"] [line "66"] [id "942100"] [msg "SQL Injection Attack Detected via libinjection"] [data "Matched Data: s&1c found within ARGS:search: user1' and 1=1 #"] [severity "CRITICAL"] [ver "OWASP_CRS/3.3.5"] [tag "application-multi"] [tag "language-multi"] [tag "platform-multi"] [tag "attack-sqli"] [tag "paranoia-level/1"] [tag "OWASP_CRS"] [tag "capec/1000/152/248/66"] [tag "PCI/6.5.2"] [hostname "127.0.0.1"] [uri "/users.php"] [unique_id "aS7B33S7D0Y-KGIb15sHhgAAAAg"], referer: http://127.0.0.1:9090/users.php

[Tue Dec 02 15:39:27.418931 2025] [security2:error] [pid 268] [client 172.17.0.1:53096] [client 172.17.0.1] ModSecurity: Warning. Operator GE matched 5 at TX:anomaly_score. [file "/usr/share/modsecurity-crs/rules/REQUEST-949-BLOCKING-EVALUATION.conf"] [line "94"] [id "949110"] [msg "Inbound Anomaly Score Exceeded (Total Score: 8)"] [severity "CRITICAL"] [ver "OWASP_CRS/3.3.5"] [tag "application-multi"] [tag "language-multi"] [tag "platform-multi"] [tag "attack-generic"] [hostname "127.0.0.1"] [uri "/users.php"] [unique_id "aS7B33S7D0Y-KGIb15sHhgAAAAg"], referer: http://127.0.0.1:9090/users.php

[Tue Dec 02 15:40:36.661509 2025] [security2:error] [pid 262] [client 172.17.0.1:42996] [client 172.17.0.1] ModSecurity: Warning. detected SQLi using libinjection with fingerprint 'sUEnk' [file "/usr/share/modsecurity-crs/rules/REQUEST-942-APPLICATION-ATTACK-SQLI.conf"] [line "66"] [id "942100"] [msg "SQL Injection Attack Detected via libinjection"] [data "Matched Data: sUEnk found within ARGS:search: user1' union select username, email, password from users #"] [severity "CRITICAL"] [ver "OWASP_CRS/3.3.5"] [tag "application-multi"] [tag "language-multi"] [tag "platform-multi"] [tag "attack-sqli"] [tag "paranoia-level/1"] [tag "OWASP_CRS"] [tag "capec/1000/152/248/66"] [tag "PCI/6.5.2"] [hostname "127.0.0.1"] [uri "/users.php"] [unique_id "aS7CJJhkNXIkhV-xBkb0ogAAAAI"], referer: http://127.0.0.1:9090/users.php

[Tue Dec 02 15:40:36.661560 2025] [security2:error] [pid 262] [client 172.17.0.1:42996] [client 172.17.0.1] ModSecurity: Warning. Pattern match "(?i:(?:[\\"'`](?:;?\\\\s*?(?:having|select|union)\\\\b\\\\s*?[^\\\\s]|\\\\s*?!\\\\s*?[\\"'`\\\\w])|(?:c(?:onnection_id|urrent_user)|database)\\\\s*?\\\\([^\\\\)]*?|u(?:nion(?:[\\\\w(\\\\s]*?select| select @)|ser\\\\s*?\\\\([^\\\\)]*?)|s(?:chema\\\\s*?\\\\([^\\\\)]*?|elect.*?\\\\w?user\\\\()|in ..." at ARGS:search. [file "/usr/share/modsecurity-crs/rules/REQUEST-942-APPLICATION-ATTACK-SQLI.conf"] [line "184"] [id "942190"] [msg "Detects MSSQL code execution and information gathering attempts"] [data "Matched Data: ' union s found within ARGS:search: user1' union select username, email, password from users #"] [severity "CRITICAL"] [ver "OWASP_CRS/3.3.5"] [tag "application-multi"] [tag "language-multi"] [tag "platform-multi"] [tag "attack-sqli"] [tag "paranoia-level/1"] [tag "OWASP_CRS"] [tag "capec/1000/152/248/66"] [tag "PCI/6.5.2"] [hostname "127.0.0.1"] [uri "/users.php"] [unique_id "aS7CJJhkNXIkhV-xBkb0ogAAAAI"], referer: http://127.0.0.1:9090/users.php

[Tue Dec 02 15:40:36.661600 2025] [security2:error] [pid 262] [client 172.17.0.1:42996] [client 172.17.0.1] ModSecurity: Warning. Pattern match "(?i)union.*?select.*?from" at ARGS:search. [file "/usr/share/modsecurity-crs/rules/REQUEST-942-APPLICATION-ATTACK-SQLI.conf"] [line "297"] [id "942270"] [msg "Looking for basic sql injection. Common attack string for mysql, oracle and others"] [data "Matched Data: union select username, email, password from found within ARGS:search: user1' union select username, email, password from users #"] [severity "CRITICAL"] [ver "OWASP_CRS/3.3.5"] [tag "application-multi"] [tag "language-multi"] [tag "platform-multi"] [tag "attack-sqli"] [tag "paranoia-level/1"] [tag "OWASP_CRS"] [tag "capec/1000/152/248/66"] [tag "PCI/6.5.2"] [hostname "127.0.0.1"] [uri "/users.php"] [unique_id "aS7CJJhkNXIkhV-xBkb0ogAAAAI"], referer: http://127.0.0.1:9090/users.php

[Tue Dec 02 15:40:36.661727 2025] [security2:error] [pid 262] [client 172.17.0.1:42996] [client 172.17.0.1] ModSecurity: Warning. Operator GE matched 5 at TX:anomaly_score. [file "/usr/share/modsecurity-crs/rules/REQUEST-949-BLOCKING-EVALUATION.conf"] [line "94"] [id "949110"] [msg "Inbound Anomaly Score Exceeded (Total Score: 18)"] [severity "CRITICAL"] [ver "OWASP_CRS/3.3.5"] [tag "application-multi"] [tag "language-multi"] [tag "platform-multi"] [tag "attack-generic"] [hostname "127.0.0.1"] [uri "/users.php"] [unique_id "aS7CJJhkNXIkhV-xBkb0ogAAAAI"], referer: http://127.0.0.1:9090/users.php
```
Khi chúng ta gõ lệnh `cat error.log | grep SQLi -i` chúng ta sẽ thấy modsec ghi lại tất cả các logs mà nó đã xác nhận đây là một phiên nỗ lực tấn công bằng SQL injection và thông qua các tags,severity chúng ta có thể thấy rõ.


# Exercise Web Application Forensics
### 1. What IP address does the attack seem to be originating from?
Chúng ta sử dụng lệnh `cat error.log | grep -i "sqli"` để liệt kê ra hết những log ghi lại quá trình kẻ tấn công thực hiện cuộc tấn công sql injection nếu có, và trong lần đầu kiểm tra xem kẻ tấn công sử dụng kiểu tấn công nào thì chúng ta đã có kết quả:
<img width="1911" height="475" alt="image" src="https://github.com/user-attachments/assets/f7c59017-412b-4858-9b2c-8a923f0e3842" />

Thấy dòng client di kèm theo 1 địa chỉ ip: **192.168.0.106** cùng với tags: "attack-sql" chúng ta có thể rút ra kết luận đây là một request sử dụng sql injection tấn công.
### 2. Which vulnerabilities do you think are being exploited, and what evidence do you have to support your findings?
Để biết được cách tấn công của attacker sử dụng để khai thác trang web, chúng ta sẽ đọc phần `access.logs` để biết được hắn đã thực thi những lệnh gì bằng lệnh `cat access.logs`
<img width="1910" height="798" alt="image" src="https://github.com/user-attachments/assets/56378b35-eb67-45f4-bfaa-9e881dff13b0" />

Qua output chúng ta sẽ thấy được các dòng 
```
192.168.0.106 - - [16/Feb/2023:01:35:27 +0500] "GET /view.php?image=../../../../etc/passwd HTTP/1.1" 200 650 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0"
192.168.0.106 - - [16/Feb/2023:01:35:30 +0500] "GET /view.php?image=../../../../etc/shadow HTTP/1.1" 200 202 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0"
192.168.0.106 - - [16/Feb/2023:01:35:39 +0500] "POST /command.php HTTP/1.1" 200 1143 "http://192.168.0.101:9090/command.php" "Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0"
192.168.0.106 - - [16/Feb/2023:01:36:07 +0500] "GET /database.php HTTP/1.1" 404 494 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0"
192.168.0.106 - - [16/Feb/2023:01:37:49 +0500] "GET /view.php?image=../../../../../../../../../important_note.txt HTTP/1.1" 200 501 "http://192.168.0.101:9090/images.php" "Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0"
192.168.0.106 - - [16/Feb/2023:01:36:19 +0500] "POST /users.php HTTP/1.1" 200 1115 "http://192.168.0.101:9090/users.php" "Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0"
192.168.0.106 - - [16/Feb/2023:01:38:53 +0500] "GET /users.php HTTP/1.1" 200 1117 "-" "sqlmap/1.6.11#stable (https://sqlmap.org)"
```
Chúng ta đã lọc ra những logs quan trọng nhất, và hãy bắt đầu phân tích từng log một để có thể hiểu hơn về intent của kẻ tấn công và hắn đã làm được gì:
- Dòng log đầu tiên và thứ 2 chúng ta thấy hắn đã thành công khai thác lỗ hổng **Path traversal** để tải về máy hắn về được 2 dữ liệu quan trọng là /etc/passwd và /etc/shadow, 
    - `/etc/passwd`: ở đây chứa các thông tin về danh sách người dùng, thông tin chung của các người dùng.
    - `/etc/shadow`: chứa các thông tin về mật khẩu của đã băm của các root và các user khác.
    => Khi kẻ tấn công lấy được 2 thứ này, hắn có thể sử dụng các công cụ bẻ khóa (crack) các hàm băm này và lấy mật khẩu.
- Dòng log thứ 3 kẻ tấn công đã thành công khai thác lỗ hổng RCE(Remote Control Execution) và upload lên server một file command.php mà chúng ta

# Disk Image Forensics
Các thiết bị lưu trữ số, như là ổ cứng, ổ cứng rắn, hoặc là USB nắm giữ lượng lớn dữ liệu có thể rất quan trọng với các cuộc điều tra pháp y kỹ thuật số. Disk image forensics là một quá trình phân tích các thiết bị và nội dung tìm kiếm có thể rất hữu ích trong quá trình điều tra.

Trong lab này chúng ta sẽ mở rộng hơn 1 tí, tìm hiểu về hai file system trước đây và hiện tại sử dụng nhiều của Windows Microsoft là FAT(File Allocation Table) và NTFS(New Technology File System):
## FAT (File Allocation Table)
Một cấu trúc dữ liệu của hệ thống tệp FAT: Hệ thống tệp FAT hỗ trợ các Cấu trúc dữ liệu sau:
- **Cluster(Cụm):** Một cluster là đơn vị lưu trữ cơ bản của hệ thống tệp FAT. Mỗi tệp được lưu trên thiết bị lưu trữ có thể được coi là một nhóm các cluster chứa các bit thông tin.
    - Cluster: là đơn vị lưu trữ nhỏ nhất trong hệ thống tệp mà hệ điều hành có thể quản lí.
    - Bản chất của ổ cứng có hàng tỷ ô nhỏ gọi là các Sector(thường là 512 byte). Tuy nhiên, quản lý từng ô nhỏ này quá phức tạp và tốn tài nguyên. Do đó, hệ thống gom nhiều Sector lại thành một Cluster để dễ hơn trong quá trình quản lý.
    - Ví dụ: Nếu bạn có một tệp tin rất nhỏ (vdu 1KB) nhưng kích thước Cluster là 4KB, tệp tin đó vẫn sẽ chiếm trọn 1 CLuster (chiếc hộp 4KB). Phần thừa 3KB còn lại bị lãng phí gọi là (Slack Space - không gian thừa). Nếu một tệp tin lớn hơn thì nó sẽ được chia cho nhiều cluster khác.
- **Directory(Thư mục):** Một thư mục chứa thông tin về nhận dạng tệp, chẳng hạn như tên tệp, cluster bắt đầu, các metadat,..
    - Directory: là cấu trúc tổ chức chứa thông tin về tệp.
    - Trong hệ thống tệp FAT, Directory không chứa nội dung của tệp, nó chứa các metadata của tệp bao gồm:
        - Tên tệp (file name)
        - Phần mở rộng của tệp (file extention)
        - Kích thước (size)
        - Thời gian tạo/sửa đổi (time create/modify)
        - Quan trọng nhất là con trỏ, trỏ tới cluster đầu tiên nơi tệp được lưu.
- **FAT(File Allocation Table):** Bảng phân bổ tệp tin, là một danh sách liên kết (linked list) của tất cả các cluster. Nó chứa trạng thái của cluster và con trỏ đến cluster tiếp theo của chuỗi.
    - FAT: Bảng phân bổ tệp tin.
    - Bản chất: hãy tưởng tượng rằng ổ cứng của bạn là một cuốn sách khổng lồ thì, FAT chính là mục lục cho cuốn sách chứa nhiều thông tin đó, nó sẽ ghi rõ trạng thái và con trỏ tiếp theo của cluster trỏ đến là ở đâu giúp bạn có thể định địa chỉ cho cluster dễ dàng
    - Trong một số trường hợp mà tệp FAT bị hỏng, nội dung trong ổ đĩa vẫn còn đó thế nhưng máy tính không còn thứ gì dẫn đường cho nó xử lí dữ liệu gây ra việc lạc mất dữ liệu.
- **FAT12, FAT16, FAT32**: các con số như là 12, 16, 32 là các bit được dùng để đặt địa chỉ định danh cho các cluster.
    - **FAT12** là hệ thống tệp đã cũ và không còn được sử dụng cho ngày nay nữa, ngày xưa nó được sử dụng cho các đĩa mềm (Floop disk). Số lượng địa chỉ quá ít nên chỉ quản lí một phần nhỏ ổ đĩa.
    - **FAT16** là hệ thống phổ biến thời MS-DOS và Windows 95. Hạ chế lớn là dung lượng phân vùng tối đa chỉ có 2GB ( hoặc 4GB). Ngày nay rất ít dùng.
    - **FAT32** tương thích cực tốt. Cắm USB FAT32 vào Windows, MAC, Linux TV máy game loa đều có thể dùng được. Nhưng nó cũng có nhược điểm là không thể lưu trữ tập tin nào lớn hơn 4GB, nếu có 1 bộ phim HD nặng 5GB, bạn không thể đưa nó vào một USB FAT32.
    - **exFAT**: là bảng phân bổ tệp tin mở rộng.
        - Dùng để khắc phục các hạn chế của FAT32 chỉ có thể chứa tối đa 4GB nhưng vẫn giữ được sự nhẹ nhàng không phức tạp như NTFS của Windows.
        - Đặc điểm:
            - Không giới hạn 4GB: Bạn có thể lưu trữ các tệp video 4k, 8k khổng lồ thoải mái
            - Tương thích cao: Hoạt động tốt trên cả Windows và MacOS (trong khi NTFS thì MacOS chỉ đọc được chứ mặc định không ghi được)
            - Tối ưu cho thẻ nhớ/USB: Được thiết kế để không ghi xóa quá nhiều lần không cần thiết, giúp tăng tuổi thọ cho bộ nhớ flash (thẻ nhớ máy ảnh, USB).
## NTFS (New Technology File System)
Hệ thống tệp FAT là một hệ thống tệp rất cơ bản. Nó hoàn thành công việc khi nói đến việc tổ chức dữ liệu của chúng ta, nhưng nó cung cấp rất ít khả năng về bảo mật, độ tin cậy và khả năng phục hồi, hạn chế về kích thước tệp và kích thước phân vùng cũng rất đáng nói. Thế nên Microsoft đã tạo ra một hệ thống tệp mới gọi là, Hệ thống tệp công nghệ mới (NTFS) nó đã khắc phục hết tất cả những nhược điểm mà hệ thống tệp FAT gặp phải và đồng thời còn tạo ra các tính năng mới như:
### Journaling (Ghi nhật ký hệ thống)
 - Hệ thống tệp NTFS lưu giữ một nhật ký về các thay đổi đối với metadata trong phân vùng. Tính năng này giúp hệ thống phục hồi sau sự cố hoặc khi di chuyển dữ liệu do chống phân mảnh. Nhật ký này được lưu trữ trong tệp `$LOGFILE` ở thư mục gốc của phân vùng. Do đó, hệ thống tệp NTFS được gọi là hệ thống tệp journaling.
 - Trong NTFS: Trước khi thực hiện thay đổi lên ổ cứng (như lưu file), NTFS ghi thông tin hành động đó vào `$LOGFILE`. Nếu máy tính bị sập nguồn dột ngột (crash), khi khởi động lại NTFS đọc `$LOGFILE` để sửa lỗi, giúp dữ liệu tránh bị hỏng.
### Access Control Lists(ACLs - Danh sách kiểm soát truy cập)
- Giải thích: NTFS cho phép gán quyền chi tiết (Read, Write, Execute) cho từng người dùng cụ thể. FAT32 không làm được điều này (ai vào được ổ đĩa là xem được hết). Đây là nền tảng bảo mật của Windows.
- Hệ thống tệp FAT không có kiểm soát truy cập dựa trên người dùng. Hệ thống tệp NTFS có các kiểm soát quyền truy cập vào tệp cho người dùng giúp đảm bảo tính bảo mật hơn.
### Volume Shadow Copy(Bản sao bóng phân vùng)
- Hệ thống tệp NTFS theo dõi các thay đổi được thực hiện đối với một tệp bằng tính năng gọi là Volume Shadow Copies. Sử dụng tính năng này, người dùng có thể khôi phục các phiên bản tệp trước đó để phục hồi dữ liệu hoặc khôi phục hệ thống. Trong các cuộc tấn công ransomware, các ransomware đã bị ghi nhận là xóa các shadow copies trên hệ thống của nạn nhân để ngăn họ khôi phục dữ liệu.
- Trong forensics: Đây là "mỏ vàng" cho điều tra viên. Kể cả khi hacker xóa file hoặc mã hóa file (ransomeware), VSS thường vẫn lưu trữ một bản san lưu (snapshot) của file đó tại thời điểm trong quá khứ. Hacker chuyên nghiệp thường chạy lệnh `vssadmin delete shadows/all/quiet` để xóa sạch các bản sao này trước khi tấn công.
### Alternate Data Stream(ADS-Luồng dữ liệu thay thế)
- Một tệp là một luồng dữ liệu được tổ chức trong một hệ thống tệp. Alternate Data Streams (ADS) là một tính năng trong NTFS cho phép các tệp có nhiều luồng dữ liệu được lưu trữ trong một tệp duy nhất. Internet Explorer và các trình duyệt khác sử dụng ADS để nhận dạng các tệp được tải xuống từ internet (sử dụng ADS Zone Identifier). Phần mềm độc hại (Malware) cũng đã được quan sát thấy ẩn mã độc của chúng trong ADS.
- Nói dễ hiểu hơn là nó cho phép bạn chạy kèm 1 file ẩn bên trong 1 file với tính năng đa luồng - tức là khi bạn có 1 tệp `report.txt` (hiển thi 10KB), bạn có thể dùng ADS giấu bên trong (`report.txt` một file `malware.exe` hiển thị (100mb) thì họ chỉ thấy tệp `.txt` và khi mở thì họ vô tình khởi động cả tệp `.exe`
- Zone Identifier: Khi bạn tải 1 file từ Internet, Windows sẽ gắn một "nhãn" ADS vào file đó để đánh dấu "File này đến từ Internet, hãy cẩn thận".
### $MFT, $MFTmirr, $LogFile, $UsnJrnl (Các tệp siêu dữ liệu)
- **$MFT**: The Master File table là một file quan trọng trong NTFS file system, nó lưu trữ những thông tin về tất cả các file và thư mục trên volume, bao gồm tên của nó, quyền, và thuộc tính. Nó chứa những thông tin về vị trí của file khác trên disk.
- **$MFTmirr**: File này là viết tắt của MFT mirror và nó đóng vai trò như là một file backup cho $MFT, nó rất cần thiết trong trường hợp $MFT gốc bị hỏng.
- **$LogFile**: File này ghi lại những nhật ký thông tin của metadata, và có thể dùng để khôi phục dữ liệu.

## Basic Terminology
**Disk Image**: là một bản sao kỹ thuật chính xác từng bit một (bit-for-bit copy) của một Disk hoặc một volume. Nó là một phần bảo tồn chính xác các nội dung hoặc cấu trúc của dữ liệu gốc. Nó bao gồm không chỉ các files và folders mà còn các không gian trống, metadata và các dữ liệu ẩn.

**Disk imaging** là quá trình tạo ra một bản sao forensics cho việc lưu trữ thiết bị, như là ổ cững hoặc là USB. Nó là một bước rất quan trọng trong pháp y kỹ thuật số bởi vì nó đảm bảo các dữ liệu gốc được duy trì nguyên vẹn và không bị thay đổi. Cryptographic hashes được sử dụng trong việc xác thực các bản sao đó trùng với bản gốc, đảm bảo không có sự thay đổi nào với dữ liệu gốc. Điều này cho phép nhà điều tra pháp y làm việc với bản sao mà không lo vô tình thay đổi dữ liệu.

**Disk image Forensics** là một quá trình phân tích các disk image để tìm kiếm các bằng chứng mình quan tâm. Nó bao gồm việc sử dụng các công cụ như Autopsy hay FTK Imager để lấy ra những thông tin hữu ích và phân tích nó với các dấu vết hệ thống như là windows registry, trình duyệt web, tệp `.LNK`, event logs, lịch sử cmd, ....

**Disk** là thiết bị phần cứng vật lý lưu trữ dữ liệu. Nó là cái mà bạn có thể cầm nắm được như (HDD, SSD, USB).

**Volume** là một phần của disk được chia ra và định dạng (format) bằng một hệ thống tệp gọi là (File System như NTFS, FAT32) để hệ điều hành có thể đọc và ghi dữ liệu. Hệ điều hành gán cho nó một ký tự (logical Drive Letter). Một disk có thể chứa một hoặc nhiều Volume.

**Case(Hồ sơ điều tra)** là một dự án hoặc một thùng chứa trong phần mềm điều tra như Autopsy,FTK,... Nó dùng để quản lý toàn bộ quá trình điều tra. Một file case có thể chứa:
- Các file Image (bằng chứng đầu vào như tệp `.ad1`, `.aut`,...
- Các ghi chú của điều tra viên
- Các bookmark những file khả nghi
- Các báo cáo kết quả.
