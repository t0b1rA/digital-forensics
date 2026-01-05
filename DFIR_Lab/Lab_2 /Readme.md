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
## Exercise
1. A phishing attack has been reported in your organization, where an employee received a malicious Word document in an email that appeared to come from a trusted source. The employee opened the document which had macros in it, resulting in the attacker gaining access to the employee’s computer. A secret which will reveal the attacker's identity, is embedded inside the macro code. You are tasked with analyzing the macro code and extracting the embedded secret. The secret has the format flag{s0me_str1ng}.

The Word document can be downloaded from [https://github.com/vonderchild/digital-forensics-lab/blob/main/Lab 03/files/YearlyBonus.docm].

- Ở bài đầu tiên này thì tình huống ở đây là một nhân viên đã bị xâm nhập vào máy tính của mình thông qua một docm có chứa macross độc hại, việc của em bây giờ là sẽ bắt đầu phân tích file `.docm`
- Đầu tiên em dùng oleid để kiểm tra xem file `.docm` có chứa loại vba macross không.
<img width="1409" height="716" alt="image" src="https://github.com/user-attachments/assets/d292accd-89db-4ffa-b9a0-dfd8ab995320" />

Ta thấy được trong file `.docm` chứa một vba macross ở mức HIGH và nó kêu em nên dùng olevba để kiểm tra nội dung đoạn mã vba kia thực hiện làm gì
```
Sub ConvertByteArrayToString(byteArray() As Byte)
    Dim str As String
    str = "Oh, and almost forgot, here's something little cryptic for you: " + StrConv(byteArray, vbUnicode)
    MsgBox str
End Sub


Sub doShenanigans()
    Dim byteArray(0 To 100) As Byte
    byteArray(0) = 77
    byteArray(1) = 101
    byteArray(2) = 109
    byteArray(3) = 34
    byteArray(4) = 22
    byteArray(5) = 111
    byteArray(6) = 101
    byteArray(7) = 107
    byteArray(8) = 22
    byteArray(9) = 104
    byteArray(10) = 91
    byteArray(11) = 87
    byteArray(12) = 98
    byteArray(13) = 98
    byteArray(14) = 111
    byteArray(15) = 22
    byteArray(16) = 97
    byteArray(17) = 100
    byteArray(18) = 101
    byteArray(19) = 109
    byteArray(20) = 22
    byteArray(21) = 111
    byteArray(22) = 101
    byteArray(23) = 107
    byteArray(24) = 104
    byteArray(25) = 22
    byteArray(26) = 109
    byteArray(27) = 87
    byteArray(28) = 111
    byteArray(29) = 22
    byteArray(30) = 87
    byteArray(31) = 104
    byteArray(32) = 101
    byteArray(33) = 107
    byteArray(34) = 100
    byteArray(35) = 90
    byteArray(36) = 22
    byteArray(37) = 87
    byteArray(38) = 22
    byteArray(39) = 76
    byteArray(40) = 56
    byteArray(41) = 55
    byteArray(42) = 22
    byteArray(43) = 99
    byteArray(44) = 87
    byteArray(45) = 89
    byteArray(46) = 104
    byteArray(47) = 101
    byteArray(48) = 22
    byteArray(49) = 89
    byteArray(50) = 94
    byteArray(51) = 87
    byteArray(52) = 98
    byteArray(53) = 98
    byteArray(54) = 91
    byteArray(55) = 100
    byteArray(56) = 93
    byteArray(57) = 91
    byteArray(58) = 36
    byteArray(59) = 0
    byteArray(60) = 0
    byteArray(61) = 79
    byteArray(62) = 101
    byteArray(63) = 107
    byteArray(64) = 104
    byteArray(65) = 22
    byteArray(66) = 92
    byteArray(67) = 98
    byteArray(68) = 87
    byteArray(69) = 93
    byteArray(70) = 22
    byteArray(71) = 95
    byteArray(72) = 105
    byteArray(73) = 48
    byteArray(74) = 22
    byteArray(75) = 92
    byteArray(76) = 98
    byteArray(77) = 87
    byteArray(78) = 93
    byteArray(79) = 113
    byteArray(80) = 105
    byteArray(81) = 107
    byteArray(82) = 89
    byteArray(83) = 94
    byteArray(84) = 85
    byteArray(85) = 99
    byteArray(86) = 42
    byteArray(87) = 89
    byteArray(88) = 104
    byteArray(89) = 38
    byteArray(90) = 85
    byteArray(91) = 99
    byteArray(92) = 107
    byteArray(93) = 89
    byteArray(94) = 94
    byteArray(95) = 85
    byteArray(96) = 109
    byteArray(97) = 38
    byteArray(98) = 109
    byteArray(99) = 23
    byteArray(100) = 115

    For iter = 0 To 100
        byteArray(iter) = byteArray(iter) + 3
    Next

    Call ConvertByteArrayToString(byteArray)
End Sub

Sub AutoOpen()

    Dim str As String
    str = "You have been hacked!"
    MsgBox str

    Call doShenanigans

End Sub
```
Đây là toàn bộ đoạn mã vba bên trong file `.docm`, giờ em sẽ phân tích một tí qua đoạn mã trên.
- Đầu tiên nó thực hiện gọi một hàm:
```
Sub ConvertByteArrayToString(byteArray() As Byte)
    Dim str As String
    str = "Oh, and almost forgot, here's something little cryptic for you: " + StrConv(byteArray, vbUnicode)
    MsgBox str
End Sub
```
Hàm này thực hiện tạo một biến str và in ra dòng tin nhắn cùng với một mãng byte đã được chuyển thành string.
Sau đó nó tạo ra một hàm `doShenanigans()` thực hiện tạo ra mảng byte gồm 100 vị trí, với mỗi vị trí tương ứng với một giá trị số từ 0 - 100, sau đó nó dùng vòng lặp for, với mỗi giá trị tương ứng với vị trí từ 0 - 100 sẽ cộng thêm 3, và sau đó gọi hàm `ConvertByteArrayToString(byteArray)` để chuyển các giá trị đó thành dạng strings và kết thúc vòng lặp.
Cuối cùng là tạo một hàm `AutoOpen()` in ra biến `str` và gọi hàm `doShenanigans`.
- Vậy bây giờ em nắm được công việc của mình là sẽ viết script với mỗi giá trị + thêm giá trị 3 và ghép chúng lại thành 1 mảng chuyển thành dạng strings.
```python
  GNU nano 6.2                                            decode.py
byte_array = [ 77, 101, 109, 34, 22, 111, 101, 107, 22, 104, 91, 87, 98, 98, 111, 22,
    97, 100, 101, 109, 22, 111, 101, 107, 104, 22, 109, 87, 111, 22, 87, 104,
    101, 107, 100, 90, 22, 87, 22, 76, 56, 55, 22, 99, 87, 89, 104, 101, 22,
    89, 94, 87, 98, 98, 91, 100, 93, 91, 36, 0, 0, 79, 101, 107, 104, 22,
    92, 98, 87, 93, 22, 95, 105, 48, 22, 92, 98, 87, 93, 113, 105, 107, 89,
    94, 85, 99, 42, 89, 104, 38, 85, 99, 107, 89, 94, 85, 109, 38, 109, 23, 115
]
decode_strings = ""
for byte in byte_array:
        if byte == 0:
                continue
        decode_strings += chr(byte + 3)
print(decode_strings)
```
Khi chạy code này thì đoạn mã được in ra ở dạng không đọc được. Em thấy được trong các mảng byte có một giá 22 được lặp lại khá nhiều lần ở các vị trí (4,8,15,20,..) và nếu em sử + 3 vào 22 và xét trong bảng ASCII [https://www.ascii-code.com/], thì giá trị 25 là một giá `end of medium` một kí tự điều khiển báo hiệu cho sự kết thúc của một "phương tiện" lưu trữ hoặc truyền tải dữ liệu. Khi nhìn kĩ hơn trong bảng em cũng để ý thấy giá trị 32 có nghĩa là space và cũng tình cờ là các giá trị 22 trong bảng cũng xuất hiện rất nhiều nên em nghĩ đây là vị trí cho một khoảng trống (space), vì 22 + 10 sẽ là 32(space), nên giờ em chỉnh lại là byte sẽ + với 10.
```python
byte_array = [ 77, 101, 109, 34, 22, 111, 101, 107, 22, 104, 91, 87, 98, 98, 111, 22,
    97, 100, 101, 109, 22, 111, 101, 107, 104, 22, 109, 87, 111, 22, 87, 104,
    101, 107, 100, 90, 22, 87, 22, 76, 56, 55, 22, 99, 87, 89, 104, 101, 22,
    89, 94, 87, 98, 98, 91, 100, 93, 91, 36, 0, 0, 79, 101, 107, 104, 22,
    92, 98, 87, 93, 22, 95, 105, 48, 22, 92, 98, 87, 93, 113, 105, 107, 89,
    94, 85, 99, 42, 89, 104, 38, 85, 99, 107, 89, 94, 85, 109, 38, 109, 23, 115
]
decode_strings = ""
for byte in byte_array:
        if byte == 0:
                continue
        decode_strings += chr(byte + 10)
print(decode_strings)
```
```
t0b1ra@tobiraNduy:/mnt/d/kali-linux/CTF/Task_KCSC/Digital_Forensics_Lab/Lab_3$ python3 decode.py
Wow, you really know your way around a VBA macro challenge.Your flag is: flag{such_m4cr0_much_w0w!}
```
Ở đây em ra được flag, **flag{such_m4cr0_much_w0w!}**

2. A mole within the government has leaked top secret information to a spy. The mole, aware of spycraft techniques, used steganography to hide the information within an image, which he then slipped to his handler. The spy received the image and pasted it into a PowerPoint document, covering it with multiple random images to conceal it. One of our spies has gained access to the enemy spy's computer and recovered the PowerPoint document. Your mission is to extract the first image, extract the top secret information as well as the name and location of his source inside the government.

The PowerPoint document can be downloaded from [https://github.com/vonderchild/digital-forensics-lab/blob/main/Lab 03/files/Presentation.pptx].

3. Provided with the audio file from the Audio Steganography section, figure out how you can view the spectogram and recover the flag using Audacity. Submit a screenshot.
The audio file can be downloaded from [https://github.com/vonderchild/digital-forensics-lab/blob/main/Lab 03/files/super_secret_audio.wav].
