# Data-from-XML

Import from XML function is used to get data from an XML file format.
SheetKraft contains the **Data From XML** option which can be accessed by the **Import From** button present in the **SheetKraft** tab as shown in the following figure:

<p align="center">Fig 1.1: Import from XML option</p>
There is no UI support for XML as of now, and you will be directed to functions UI of Excel as shown in the following figure:

<p align="center">Fig 1.2: DataFromXML function</p>

**DataFromXml.SK()** function has the following arguments: 
+ **File_location**: Data from single / multiple file(s) with similar structure can be imported by selecting the Excel range that specifies the file paths. \
 **For example**: DataFromXml.SK(**$B$2**) 
+ **Root**: A parent root which contains all the elements and attributes which are required in the import. \
In the following example, **catalog** is the parent root:   

    ```
    <catalog xmlns="http://www.w3.org/TR/html4/">
        <book id="bk101">
            <author>Gambardella, Matthew</author>
            <title>XML Developer's Guide</title>
            <genre>Computer</genre>
            <price>44.95</price>
            <publish_date>2000-10-01</publish_date>
            <description>In-depth look at creating applications with XML.</description>
        </book>
    </catalog>
    ```      

  To further tabulate the data in the proper form, you can separate the parent object and the child object with a forward slash (**/**) \
  **For example**: DataFromXml.SK($B$2,"**catalog/book**")
 
+ **Pattern**: Arrangement of all the field names which will be required from the XML file and it acts as the header when sorted as a tabular data. \
In the following example, **author**, **title**, **genre**, **price**, **publish_date**, **description** are the headers which can be provided as values for **Pattern** field. 

```
<book id="bk101">
    <author>Gambardella, Matthew</author>
    <title>XML Developer's Guide</title>
    <genre>Computer</genre>
    <price>44.95</price>
    <publish_date>2000-10-01</publish_date>
    <description>In-depth look at creating applications with XML.</description>
</book>
```

+ **Exclude Column Headers**: Specifies whether the column header must be included or not. **TRUE** excludes the column headers, **FALSE** includes column header into the imported data.
+ **Namespaces manager**: Selecting the Excel range that specifies the namespace and a corresponding key. This field is used when the XML file contains namespace
(<catalog xmlns="http://www.w3.org/TR/html4/">). 
In this case, while providing values to Pattern fields the column headers will have the namespace key prepended to it. (a:author, a:title, a:price)
``` 
<h3>Sample XML Format:</h3>
<catalog xmlns="http://www.w3.org/TR/html4/">
    <book id="bk101">
        <author>Gambardella, Matthew</author>
        <title>XML Developer's Guide</title>
        <genre>Computer</genre>
        <price>44.95</price>
        <publish_date>2000-10-01</publish_date>
        <description>In-depth look at creating applications with XML.</description>
    </book>
</catalog>
```
**Note**: The **Root** in this XML file is **catalog**.
Before selecting the option for DataFromXML, a root element must be selected which contains the elements and attributes required. Once the root is identified, the elements and attributes can be provided as patterns, and if no pattern is provided, it will reflect the entire data in a tabular form by itself with the column headers.
In the following XML example, author, title, genre, price, publish_date, description are the Pattern values:
<book id="bk101">
    <author>Gambardella, Matthew</author>
    <title>XML Developer's Guide</title>
    <genre>Computer</genre>
    <price>44.95</price>
    <publish_date>2000-10-01</publish_date>
    <description>In-depth look at creating applications with XML.</description>
</book>

If pattern is selected for the same, there should be an at symbol (@) before the Attributes. Both of them are case sensitive. In the preceding example, <book id="bk101"> code line has id as the attribute of book element.
 
For example: 
=DataFromXml.SK($B$2,"a:catalog/a:book",{"a:author","a:genre","@id"},FALSE,M12:N12)
For blank rows or comments which are not contained in elements should have a pattern column looking for text; it should be used with the TEXT function.
In a similar way, you can select only the required columns.
 
