MS Office hỗ trợ một số định dạng tài liệu; tuy nhiên, cốt lõi của hầu hết các tài liệu là XML. Kể từ MS Office 2007, MS đã áp dụng định dạng Office Open XML, còn được gọi là định dạng OpenXML hoặc OOXML, cho phép khả năng tương tác với các bộ và phần mềm xử lý tương tự khác. Định dạng Office Open XML dựa trên XML và đã được ECMA International áp dụng với tên gọi ECMA-376 (Ecma International, 2006) và trở thành tiêu chuẩn quốc tế (ISO / IEC 29500) (International Organization for Standardization, 2016).

- https://www.loc.gov/preservation/digital/formats/fdd/fdd000397.shtml
- http://officeopenxml.com/anatomyofOOXML.php
- https://docs.microsoft.com/en-us/office/open-xml/structure-of-a-wordprocessingml-document

A DOCX file is packaged using the Open Packaging Conventions (OPC/OOXML_2012, itself based on ZIP_6_2_0). The package can be explored, by opening with ZIP software, typically by changing the file extension to .zip. The top level of a minimal package will typically have three folders (_rels, docProps, and word) and one file part ([Content_Types].xml). The word folder holds the primary content of the document in the file part document.xml. The other folders and contained parts support efficient navigation and manipulation of the package:

_rels is a Relationships folder, containing a single file .rels (which may be hidden from file listings, depending on operating system and settings). It lists and links to the key parts in the package, using URIs to identify the type of relationship of each key part to the package. In particular it specifies a relationship to word/document.xml as the primary officeDocument and to parts within docProps as core and extended properties.
docProps is a folder that contains properties for the document as a whole, typically including a set of core properties, a set of extended or application-specific properties, and a thumbnail preview for the document.
[Content_Types].xml is a file part, a mandatory part in any OPC package, that lists the content types (using MIME Internet Media Types as defined in RFC 6838) for parts within the package.
The word folder contains at a minimum document.xml and files and subsidiary folders that support presentation styles and themes. Headers and footers are stored in separate parts if present. The minimal structure for document.xml will include a nested set of elements:

<w:body> --- text body
<w:p> --- paragraph
<w:r> --- run, text having a given set of formatting parameters, e.g., font face and size, regular, bold or italic, etc.
<w:t> --- textual characters, allowing any Unicode character allowed by XML
Optional elements <w:pPr> and <w:rPr> define the formatting properties of a particular paragraph or run.
