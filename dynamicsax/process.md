---
description: 标准的AX项目实施流程
---

# Process

### Kick off

项目组成员，沟通方式，汇报方式，现场支持方式的确立

### BPA

业务流程分析

{% file src="../.gitbook/assets/sum\_qa \(1\).rar" %}

### CRP

业务流程模型、Gap List、项目计划的建立

![](../.gitbook/assets/image%20%287%29.png)

{% file src="../.gitbook/assets/businessprocess.rar" %}

{% file src="../.gitbook/assets/gap-list.xlsx" %}

{% file src="../.gitbook/assets/projectplan.rar" %}

### System Preparation

系统基础参数配置

在这个阶段，我们需要创建新的系统环境：Live 、Stage、Test、Dev，并且为新的环境配置系统参数。

{% file src="../.gitbook/assets/sysconf\_systemconfiguration.rar" %}

### System development

系统开发、测试

### UAT and KU training

关键用户培训

* General 总帐 
* Order-to-Cash 应收账款
* Purchase-to-pay 应付账款
* Finance-to-Manage 财务管理
* Warehouse management 仓库管理
* Demand-to-Supply 计划管理
* Production management 生产

### Data migration

期初数据整合

#### 静态数据

* COA 财务科目
* Dimension 财务维度
* Currency 币种、汇率
* Sales Tax税组
* Customer 客户
* Vendor 供应商
* Site Warehouse 站点、仓库
* Item 物料
* BOM
* Trade Agreement 协议价
* ...

{% page-ref page="import/stadata.md" %}

#### 动态数据

* Open PO 未结采购订单
* Open SO 未结销售订单
* Opening Transation\(AR\AP\) 应收、应付
* Fixed Assets 固定资产
* Opening Balance 期初余额

{% page-ref page="import/" %}

### Go-live

