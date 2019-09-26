---
description: 期初上线阶段的Open销售订单导入
---

# Open SO

#### 读取系统文件夹内待导入文件

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

#### 程序代码

{% file src="../../../.gitbook/assets/form\_cig\_tmpimportopenso.rar" %}

#### 数据模板

{% file src="../../../.gitbook/assets/csag\_openso.xlsx" %}

