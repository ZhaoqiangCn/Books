# Open SO

{% code-tabs %}
{% code-tabs-item title="ReadFile" %}
```text
container ReadTextFile(FileName _filename = @"C:\Users\zhaoqiang\Desktop\Japan_OpenSO_PROD_20190831.csv")
{
    TextIo file;

    container con;
    FileIoPermission permission;
    str             strXML;
    #File
    ;
    try
    {
        permission = new FileIoPermission(_filename, #io_read);
        permission.assert();

        file = new TextIo(_filename, #io_read);
        if (!file)
            throw Exception::Error;

        file.inRecordDelimiter('\n'); //For Next Record
        file.inFieldDelimiter('\t');

        con = file.read();
        while (file.status() == IO_Status::Ok)
        {        
            con += file.read();
        }

        //info(strfmt("%1",strXML));
        return con;
    }
    catch(Exception::Error)
    {
        error("You do not have access to write the file to the selected folder");
    }
    CodeAccessPermission::revertAssert();
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

