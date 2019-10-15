---
description: AX 自动生成 XML
---

# Auto Generate XML From AX

## 新建查询

组织需要输出的数据，新建一个Query。注意新建的表需要有Index。

![](../../../.gitbook/assets/image.png)

## 文档服务

路径：工具 -&gt; 开发工具 -&gt; AIF -&gt; 创建、更新文档服务

![](../../../.gitbook/assets/image%20%284%29.png)

![](../../../.gitbook/assets/image%20%2812%29.png)

![](../../../.gitbook/assets/image%20%282%29.png)

### 自动创建Pravite Project

通过系统工具可以自动创建下图中的所有类，其中Job可以生成XML的XSD，CIG\_ICTradeOrderService是对应的文档服务名称

![](../../../.gitbook/assets/image%20%283%29.png)

## XML文件

如下代码描述了如何在服务器指定位置生成对应XML文件，执行如下程序可以把CIG\_ICTradeOrderTable中的指定数据根据Query中的数据结构生成对应的XML文件

```text
static void ExportOrderXml(CIG_ICTradeOrderTable    _tradeOrderTable)
{
    AxdCIG_ICTradeOrder                 TradeOrder;

    AifEntityKey                        key;

    Map                                 map;

    AifPropertyBag                      bag;

    XmlDocument                         xmlDocument = new XmlDocument();

    FileIoPermission                    perm;

    CIG_ICTradeOrderTable                          tradeOrderTable;// = CIG_ICTradeOrderTable::find(_transRefId);

    CIG_ICTradeOrderLine                           tradeOrderLine;



    filename                            filename;// = strfmt("//editest/AX-TEST/%1_%2.xml",strrem(strrem(salesTable.SalesId,'/'),'-'),timenow());

    Boolean                             loadStatus;
    ;

    if(_tradeOrderTable)
    {
        filename = strfmt("//edilive/edi_live/FileSystem/Root/Inbound/ORDER/ORDER_%2.xml",strrem(strrem(_tradeOrderTable.SalesPurchOrderId,'/'),'-'),_tradeOrderTable.EDIGUID);


        perm = new FileIoPermission(fileName,"wr");

        perm.assert();

        map = new Map(Types::Integer, Types::Container);

        map.insert(fieldnum(CIG_ICTradeOrderTable, EDIGUID), [_tradeOrderTable.EDIGUID]);

        map.insert(fieldnum(CIG_ICTradeOrderTable, OrderType), [_tradeOrderTable.OrderType]);

        key = new AifEntityKey();

        key.parmTableId(tablenum(CIG_ICTradeOrderTable));

        key.parmKeyDataMap(map);

        try
        {
            tradeOrder = new AxdCIG_ICTradeOrder();

            loadStatus = xmlDocument.loadXml(tradeOrder.read(key, null, new AifEndPointActionPolicyInfo(), new AifConstraintList(), bag));

            if(loadStatus)
            {
                xmlDocument.save(filename);

                CIG_QueueManager::createQueueManagerData(_tradeOrderTable
                                                        ,xmlDocument.xml()
                                                        ,""
                                                        ,AifMessageDirection::Outbound
                                                        ,filename);

                CIG_TradeInterCompany_EDI::updateStatus(_tradeOrderTable,"Sent");
            }

            CodeAccessPermission::revertAssert();


        }
        catch
        {
            throw error('Error in document service outbound');
        }
    }
}
```

