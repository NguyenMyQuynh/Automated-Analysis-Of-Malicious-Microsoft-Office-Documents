## XML
https://www.w3schools.com/xml/default.asp

- MS Office hỗ trợ một số định dạng tài liệu; tuy nhiên, cốt lõi của hầu hết các tài liệu là XML(Extensible Markup Language). 
- XML là một dạng ngôn ngữ đánh dấu, để xác định cú pháp mã hóa tài liệu giúp con người, máy móc có thể đọc được. Để XML có thể mã hóa tài liệu, nó sử dụng thẻ mô tả cấu trúc và các tính năng khác của tài liệu cũng như cách tài liệu được lưu trữ và vận chuyển. 
- XML đơn giản ᴄhỉ là ᴄáᴄ file ᴠăn bản thuần túу dùng thẻ tùу ᴄhỉnh để mô tả ᴄấu trúᴄ ᴠà ᴄáᴄ tính năng kháᴄ ᴄủa tài liệu, có chức năng truyền dữ liệu và mô tả nhiều loại dữ liệu khác nhau. Mục đích chính của XML là đơn giản hóa việc chia sẻ dữ liệu giữa các platform và các hệ thống được kết nối với mạng Internet. Chính vì vậy, XML có tác dụng rất lớn trong việc chia sẻ, trao đổi dữ liệu giữa các hệ thống. Ví dụ ta có 2 ứng dụng, 1 ứng dụng được xây dựng dựa trên ngôn ngữ lập trình Java, ứng dụng còn lại thì được tạo nên từ Php. Vậy thì hai ứng dụng này hoàn toàn không thể kết nối với nhau được. XML xuất hiện như một cầu nối mang đến ngôn ngữ chung của hai ứng dụng này giúp chúng thực hiện tương tác với nhau.
- So sánh XML với HTML: 
  - Ngôn ngữ XML không có thẻ được xác định trước. Các thẻ trong ví dụ bên dưới (như <to> và <from>) không được định nghĩa trong bất kỳ tiêu chuẩn XML nào. Các thẻ này được "phát minh" bởi tác giả của tài liệu XML. HTML hoạt động với các thẻ được xác định trước như `<p>`, `<h1>`, `<table>`, ... Với XML, tác giả phải xác định cả thẻ và cấu trúc tài liệu.
  - XML được thiết kế để chuyển tải và lưu trữ dữ liệ, HTML được thiết kế để hiển thị dữ liệu


- Ví dụ mã XML:
```
<?xml version="1.0" encoding="UTF-8"?>
<note>
  <to>Tove</to>
  <from>Jani</from>
  <heading>Reminder</heading>
  <body>Don't forget me this weekend!</body>
</note>
```

```
<?xml version="1.0" encoding="UTF-8"?>
<breakfast_menu>
<food>
    <name>Belgian Waffles</name>
    <price>$5.95</price>
    <description>
   Two of our famous Belgian Waffles with plenty of real maple syrup
   </description>
    <calories>650</calories>
</food>
<food>
    <name>Strawberry Belgian Waffles</name>
    <price>$7.95</price>
    <description>
    Light Belgian waffles covered with strawberries and whipped cream
    </description>
    <calories>900</calories>
</food>
<food>
    <name>Berry-Berry Belgian Waffles</name>
    <price>$8.95</price>
    <description>
    Belgian waffles covered with assorted fresh berries and whipped cream
    </description>
    <calories>900</calories>
</food>
<food>
    <name>French Toast</name>
    <price>$4.50</price>
    <description>
    Thick slices made from our homemade sourdough bread
    </description>
    <calories>600</calories>
</food>
<food>
    <name>Homestyle Breakfast</name>
    <price>$6.95</price>
    <description>
    Two eggs, bacon or sausage, toast, and our ever-popular hash browns
    </description>
    <calories>950</calories>
</food>
</breakfast_menu>
```

<br>

##  Open XML(OpenXML/OOXML):
  
Kể từ MS Office 2007, MS đã áp dụng định dạng Office Open XML, còn được gọi là định dạng OpenXML hoặc OOXML, cho phép khả năng tương tác với các bộ và phần mềm xử lý tương tự khác. Định dạng Office Open XML dựa trên XML và đã được ECMA International áp dụng với tên gọi ECMA-376 (Ecma International, 2006) và trở thành tiêu chuẩn quốc tế (ISO / IEC 29500) (International Organization for Standardization, 2016).

- https://www.loc.gov/preservation/digital/formats/fdd/fdd000397.shtml
- http://officeopenxml.com/anatomyofOOXML.php
- https://docs.microsoft.com/en-us/office/open-xml/structure-of-a-wordprocessingml-document

*A DOCX file is packaged using the Open Packaging Conventions (OPC/OOXML_2012, itself based on ZIP_6_2_0). The package can be explored, by opening with ZIP software, typically by changing the file extension to .zip. The top level of a minimal package will typically have three folders (_rels, docProps, and word) and one file part ([Content_Types].xml). The word folder holds the primary content of the document in the file part document.xml. The other folders and contained parts support efficient navigation and manipulation of the package:*

- *_rels is a Relationships folder, containing a single file .rels (which may be hidden from file listings, depending on operating system and settings). It lists and links to the key parts in the package, using URIs to identify the type of relationship of each key part to the package. In particular it specifies a relationship to word/document.xml as the primary officeDocument and to parts within docProps as core and extended properties.*
- *docProps is a folder that contains properties for the document as a whole, typically including a set of core properties, a set of extended or application-specific properties, and a thumbnail preview for the document.*
- *[Content_Types].xml is a file part, a mandatory part in any OPC package, that lists the content types (using MIME Internet Media Types as defined in RFC 6838) for parts within the package.*
- *The word folder contains at a minimum document.xml and files and subsidiary folders that support presentation styles and themes. Headers and footers are stored in separate parts if present. The minimal structure for document.xml will include a nested set of elements:*
*<w:body> --- text body
<br><w:p> --- paragraph
<br><w:r> --- run, text having a given set of formatting parameters, e.g., font face and size, regular, bold or italic, etc.
<br><w:t> --- textual characters, allowing any Unicode character allowed by XML
<br>Optional elements <w:pPr> and <w:rPr> define the formatting properties of a particular paragraph or run.*
