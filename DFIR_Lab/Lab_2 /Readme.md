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
