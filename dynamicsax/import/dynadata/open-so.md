---
description: 期初的Open销售订单导入
---

# Open SO

### 预览

首先导入中间表校验数据正确性

![&#x6570;&#x636E;&#x5F85;&#x5BFC;&#x5165;](../../../.gitbook/assets/image%20%284%29.png)

{% code-tabs %}
{% code-tabs-item title="示例" %}
```text
//PO NUMBER 35
//Line Number 5
//Item Number 30
//Request Date 14
//Quantity 10
//Unit Price 10
void ImportDataTmpTable()
{
    str                 custAccount;

    str                 custPO;

    str                 itemNumber;

    str                 site;

    str                 warehouse;

    str                 location;

    str                 version;

    str                 RequestDate;

    str                 quantity;

    str                 unit;

    str                 currency;

    str                 price;

    str                 priceInclTax;

    str                 taxPer;

    str                 tradeId;

    str                 department;

    str                 costcenter;

    str                 purpose;

    str                 orderpool;

    str                 SAPRef;

    container           conData;

    int                 i;

    str                 curLine;
//
//    str                 PONumber;
//
//    str                 LineNumber;
//
//    str                 RequestDate;
//
//    str                 Quantity;
//
//    str                 UnitPrice;
//
//    str                 conStr;
//
    container           conLine;

    SalesTable          curSalesTable;

    SalesLine           curSalesLine;

    InventDim           curInventDim;

    InventDimParm       curInventDimParm;

    InventOnhand        curInventOnHand;

    InventQty           curStockOnHand;

    LineNum             linenum;

    NumberSeq           numberSeq;

    Str                 strError;

    CIG_ICTradeLine         CIG_ICTradeLine;

    CIG_ICTradeTable        CIG_ICTradeTable;// = CIG_ICTradeTable::findLastVersion(SalesTable.CIG_TradeId);

    ;
    if(fileName)
    {
        conData = element.ReadTextFile(fileName);
    }
    else
    {
        conData = element.ReadTextFile();
    }

    set = new set(types::String);

    enoughOnhand = true;

    for(i=2;i<=conlen(conData);i++)
    {
        strError = '';

        curLine = conpeek(conData,i);//Customer account,Customer PO number,Item number,Site,Warehouse,Location,Delivery date,Quantity,Unit,Currency,Price ,Prices incl. sales tax,Sales tax percentage,TradeId,Department,Cost center,Purpose,

        conLine = str2con(curLine,',');

        custAccount = conpeek(conLine,1);

        if(!custTable::find(custAccount))
        {
            strError   += strError + strfmt("Customer Account isn`t exist");
        }

        custPO = conpeek(conLine,2);

        itemNumber = conpeek(conLine,3);

        if(!inventTable::find(itemNumber))
        {
            strError   += strError + strfmt("Item Number isn`t exist");
        }

        site    = conpeek(conLine,4);

        warehouse    = conpeek(conLine,5);

        location = "001";//conpeek(conLine,6);

        version = conpeek(conLine,7);

        RequestDate = conpeek(conLine,8);

        quantity = conpeek(conLine,9);

        unit = conpeek(conLine,10);

        currency = conpeek(conLine,11);

        price = conpeek(conLine,12);

        priceInclTax = conpeek(conLine,13);

        taxPer = conpeek(conLine,14);

        tradeId = conpeek(conLine,15);

        department = conpeek(conLine,16);

        costCenter = conpeek(conLine,17);

        purPose = conpeek(conLine,18);

        orderpool = conpeek(conLine,19);

        SAPRef = conpeek(conLine,20);

        CIG_ICTradeTable = CIG_ICTradeTable::findLastVersion(tradeId);

        CIG_ICTradeLine = CIG_ICTradeLine::find(tradeId,CIG_ICTradeTable::findLastVersion(tradeId).Version,"SALES","ORDER",curext());

        if(!set.in(custPO))
        {

            SalesTable.setTmp();

            SalesTable.clear();

            SalesTable.salesId                       = custPO;

            SalesTable.CustAccount                   = custAccount;

            SalesTable.CurrencyCode                  = custTable::find(SalesTable.CustAccount).Currency;

            SalesTable.InventSiteId                  = site;

            SalesTable.InventLocationId              = warehouse;

            SalesTable.ShippingDateRequested         = str2date(strRtrim(RequestDate),321);

            SalesTable.ReceiptDateRequested          = SalesTable.ShippingDateRequested;

            SalesTable.CIG_PurchaseOrderNum          = custPO;

            SalesTable.CIG_TradeId                   = tradeId;

            SalesTable.CIG_ICVersion                 = CIG_ICTradeTable::findLastVersion(tradeId).Version;

            SalesTable.CIG_isEditPrice              = (CIG_ICTradeLine.IsEditPrice == "YES") ? NoYes::Yes:NoYes::No;

            SalesTable.CIG_isEditQty                = (CIG_ICTradeLine.isEditQty == "YES") ? NoYes::Yes:NoYes::No;

            SalesTable.CIG_isPriceAgreement         = (CIG_ICTradeLine.isPriceAgreement == "YES") ? NoYes::Yes:NoYes::No;

            SalesTable.CIG_SalesPricePercent        = CIG_ICTradeLine.PricePercent;

            SalesTable.CIG_SalesPricePercentOrig    = CIG_ICTradeLine.PricePercent;

            SalesTable.CIG_SourceType               = "Source";

            salesTable.CIG_CUDType          = "Insert";

            salesTable.CIG_RefGUID          = guid2str(newguid());

            SalesTable.Dimension[1]                  = department;

            SalesTable.Dimension[2]                  = costCenter;

            SalesTable.Dimension[3]                  = purPose;

            SalesTable.InclTax                       = ( priceInclTax == "Yes" ) ? NoYes::Yes : Noyes::No;

            SalesTable.SalesPoolId                   = orderpool;

            SalesTable.CIG_Reference                 = SAPRef;

            SalesTable.doInsert();
        }

        set.add(custPO);

        SalesLine.setTmp();

        linenum++;

        SalesLine.clear();

        SalesLine.salesId                        = SalesTable.salesId;

        SalesLine.LineNum                        = linenum;

        SalesLine.CurrencyCode                   = SalesTable.CurrencyCode;

        SalesLine.initValue();

        SalesLine.ItemId                         = ItemNumber;

        SalesLine.initFromSalesTable(SalesTable);

        curInventDim.inventLocationid               = warehouse;

        curInventDim.InventSiteId                   = site;

        curInventDim.wmsLocationId                  = location;

        if(InventDImSetup::find(inventTable::find(ItemNumber).DimGroupId,9).Active == NoYes::Yes)
        {
            curInventDim.InventColorId              = version;
        }

        curInventDim                                = inventDim::findOrCreate(curInventDim);

        SalesLine.InventDimId                    = curInventDim.inventDimId;

        SalesLine.salesQty                       = str2num(Quantity);

        SalesLine.remainSalesPhysical            = SalesLine.SalesQty;

        SalesLine.remainInventPhysical           = SalesLine.SalesQty;

        SalesLine.salesUnit                      = InventTable::find(ItemNumber).inventTableModuleSales().UnitId;

        SalesLine.ShippingDateRequested          = SalesTable.ShippingDateRequested;

        SalesLine.ReceiptDateRequested           = SalesTable.ReceiptDateRequested;

        SalesLine.SalesPrice                     = any2real(price);

        SalesLine.LineAmount                     = SalesLine.calcLineAmountForced(SalesLine.SalesQty);

        SalesLine.TaxGroup                          = taxPer;

        numberSeq   = NumberSeq::newGetNum(InventParameters::numRefInventTransId());

        SalesLine.InventTransId                  = numberSeq.num();

        if(strError)
        {
            SalesLine.CIG_ErrorMSG   = strError;
            SalesLine.CIG_Mark       = NoYes::No;
        }
        else
        {
            SalesLine.CIG_ErrorMSG   = "";
            SalesLine.CIG_Mark       = NoYes::Yes;
        }

        SalesLine.doinsert();
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 程序代码

{% file src="../../../.gitbook/assets/form\_cig\_tmpimportopenso.rar" %}

### 数据模板

{% file src="../../../.gitbook/assets/csag\_openso.rar" %}

