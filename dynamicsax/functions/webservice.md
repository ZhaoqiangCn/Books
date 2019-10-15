---
description: webservice WCF
---

# Webservice

## Using webservice to connect with Dynamics AX

### SystemConnector

### Consume SystemConnector in VS

![](../../.gitbook/assets/image%20%281%29.png)

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Xml;
using SystemConnector.DynamicsAX;

namespace CIG_WCF4AgileAX
{
    public partial class WebForm1 : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            string ret = "";
            //string _XMLStr = GetXmlDocument(@"D:/AgileXml/HDC000076-utf.xml");
            //string _XMLStr = GetXmlDocument(@"E:/AgileXml/test1014/UPD-1014-33-01.xml");
            string _XMLStr = GetXmlDocument(@"E:/AgileXml/test1014/CIG000780.xml");
            //string _XMLStr = "AX-MES-RDIF-Go";
            try
            {
                AXServiceProvider axServiceProvider = new AXServiceProvider();
                //ret = axServiceProvider.handleRFIDData("cig", _XMLStr);
                ret = axServiceProvider.handleAgileData("cig", _XMLStr);
               
            }
            catch (Exception ex)
            {
                ret= ex.ToString();
            }
            Response.Write(ret);
        }

        private static string GetXmlDocument(string xmlPath)
        {
            try
            {
                XmlDocument doc = null;
                if (File.Exists(xmlPath))
                {
                    doc = new XmlDocument();
                    doc.Load(xmlPath);               
                }
                return doc.InnerXml;
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.Write(ex.Message);
            }
            return null;
        }
    }
}
```

{% file src="../../.gitbook/assets/cig\_wcf4agileax.zip" %}

