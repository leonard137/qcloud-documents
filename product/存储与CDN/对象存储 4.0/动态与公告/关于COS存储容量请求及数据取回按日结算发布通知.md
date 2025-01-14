## 概述

自2022年7月1日起，COS **存储容量、请求及数据取回**计费项将由**按月结算**陆续升级为**按日结算**，便于您通过日结账单做更精细的费用管理。本次发布将按用户分批升级，具体升级时间，以您收到的通知（站内信、邮件及短信）为准。您已出账的账单不变，不会受到影响，您无须做任何操作。关于计费模式与账单统计周期，请见 [账单介绍](https://cloud.tencent.com/document/product/555/30250#.E8.AE.A1.E8.B4.B9.E6.A8.A1.E5.BC.8F.E4.B8.8E.E8.B4.A6.E5.8D.95.E7.BB.9F.E8.AE.A1.E5.91.A8.E6.9C.9F)。

>? 计费模式与账单统计周期：COS 默认按量计费（后付费）。
> - 按月结算的资源：在1月1日00:00 - 1月31日23:59产生的消耗，实际扣费时间在2月1日。若按扣费周期，该记录归属到2月账单；若按计费周期，该记录归属到1月账单。 
> - 按日结算的资源：在1月31日00:00 - 23:59产生的消耗，实际扣费时间在2月1日。若按扣费周期，该记录归属到2月账单；若按计费周期，该记录归属到1月账单。
> 

## 发布时间

自2022年7月1日起，按月结算将陆续升级为按日结算。具体升级时间，请以通知（站内信、邮件及短信）中的升级时间为准。升级完成后，将在次日出上一天的账单，请您留意账单变化。

## 升级前后变更点

### 计费周期

| 计费项                               | 升级前                          | 升级后                         |
| ------------------------------------ | ------------------------------- | ------------------------------ |
| 存储容量费用、请求费用及数据取回费用 | 按月结算，每月1号结算上月一整月产生的费用，并出账单 | 按日结算，次日结算上一天产生的费用，并出账单       |
| 流量费用、管理功能费用               | 按日结算，次日结算上一天产生的费用  | 不变   |


### 计费项单价

本次升级后，具体说明如下：

<table>
<thead>
<tr>
<th width="10%">计费项</th>
<th>计费项说明</th>
<th>价格说明</th>
<th>计费周期</th>
</tr>
</thead>
<tbody><tr>
<td>存储容量</td>
<td>按存储容量和存储时长计算</td>
<td>价格“元/GB/月”与计费周期有关。其中，价格中的“月”指的是 30 天。按日结算价格需要换算，换算公式为：日单价 = 月单价 / 30。例如，北京地域的标准存储容量的月单价为0.118 元/GB/月，则日单价为 0.118 / 30 = 0.00393333 元/GB/日。</td>
<td>按日结算</td>
</tr>
<tr>
<td>请求</td>
<td>按发送到COS的请求次数计算</td>
<td>价格“元/万次”与计费周期无关，按日结算价格无须换算。例如，北京地域的标准存储读写请求价格为0.01元/万次，无论按日结算还是按月结算，请求价格不变。</td>
<td>按日结算</td>
</tr>
<tr>
<td>数据取回</td>
<td>按实际取回数据量的大小计算</td>
<td>价格“元/GB”与计费周期无关，按日结算价格无须换算。例如，北京地域的低频存储数据取回价格为0.02元/GB，无论按日结算还是按月结算，数据取回价格不变。</td>
<td>按日结算</td>
</tr>
</tbody></table>

>?
>- 存储容量费用：若按月结算，按照**每个月30天**计费。若按日结算，按照**每个月的实际天数**计费。
>- 账单波动说明：在每个月用量不变的情况下，存储容量账单会产生一定的波动。若您使用一整个月，1月会按照31天计费，2月会按照28（或29）天计费，4月会按照30天计费。
>

### 计费公式

本次升级后，计费项不同结算周期的计费公式，详情如下：

<table>
   <tr>
      <th>计费项</th>
      <th>子计费项</th>
      <th>计费公式</th>
      <th>计费周期</th>
   </tr>
   <tr>
      <td rowspan=2>存储容量费用</td>
      <td rowspan=2>存储容量费用</td>
      <td>存储容量费用 = 月存储容量单价 × 月存储量</td>
      <td>按月结算</td>
   </tr>
   <tr>
      <td>存储容量费用 = 日存储容量单价 × 日存储量 = 月存储容量单价 / 30 x 当日“每5分钟存储容量”之和 / 288</td>
      <td>按日结算</td>
   </tr>
   <tr>
      <td rowspan=8>请求费用</td>
      <td rowspan=2>读请求费用</td>
      <td>读请求费用 = 每万次请求单价 × 月累计请求次数 / 10000</td>
      <td>按月结算</td>
   </tr>
   <tr>
      <td>读请求费用 = 每万次请求单价 × 日累计请求次数 / 10000</td>
      <td>按日结算</td>
   </tr>
   <tr>
      <td rowspan=2>写请求费用</td>
      <td>写请求费用 = 每万次请求单价 × 月累计请求次数 / 10000</td>
      <td>按月结算</td>
   </tr>
   <tr>
      <td>写请求费用 = 每万次请求单价 × 日累计请求次数 / 10000</td>
      <td>按日结算</td>
   </tr>
   <tr>
      <td rowspan=2>取回请求费用</td>
      <td>取回请求费用 = 每万次请求单价 × 月累计请求次数 / 10000</td>
      <td>按月结算</td>
   </tr>
   <tr>
      <td>取回请求费用 = 每万次请求单价 × 日累计请求次数 / 10000</td>
      <td>按日结算</td>
   </tr>
   <tr>
      <td rowspan=2>对象监控费用</td>
      <td>对象监控费用 = 每万个对象监控单价 × 月累计对象个数 / 10000</td>
      <td>按月结算</td>
   </tr>
   <tr>
      <td>对象监控费用 = 每万个对象监控单价 / 30 × 日累计对象个数 / 10000</td>
      <td>按日结算</td>
   </tr>
   <tr>
      <td rowspan=2>数据取回费用</td>
      <td rowspan=2>数据取回费用</td>
      <td>数据取回费用 = 每 GB 单价 × 月数据取回量</td>
      <td>按月结算</td>
   </tr>
   <tr>
      <td>数据取回费用 = 每 GB 单价 × 日数据取回量</td>
      <td>按日结算</td>
   </tr>
</table>

## 相关指引

### 如何查看账单

您可登录腾讯云官网控制台，在费用中心的 [费用账单](https://console.cloud.tencent.com/expense/bill/overview) 中查看及下载账单。关于账单的介绍，请查看 [账单介绍](https://cloud.tencent.com/document/product/555/30250#.E8.AE.A1.E8.B4.B9.E6.A8.A1.E5.BC.8F.E4.B8.8E.E8.B4.A6.E5.8D.95.E7.BB.9F.E8.AE.A1.E5.91.A8.E6.9C.9F)。

**操作步骤**

1. 登录 [腾讯云控制台](https://console.cloud.tencent.com/)。
2. 在右上方导航栏**费用**中，单击 **[费用中心](https://console.cloud.tencent.com/expense)**，进入费用中心总览页面。
3. 单击 **费用账单** > **[账单详情](https://console.cloud.tencent.com/expense/bill/summary)**，进入账单详情页面。
4. 在“资源 ID 账单”选项卡页面，下拉列表中选择 COS 对象存储，可按照地域、计费模式和交易类型等维度查看您的 COS 消费情况。
5. 在 **[账单下载中心](https://console.cloud.tencent.com/expense/bill/downloadCenter)** 可下载账单。

### 如何查看价格

关于 COS 的按量计费（后付费）的定价，请参见 [产品定价](https://buy.cloud.tencent.com/price/cos)。您也可以通过 [价格计算器](https://buy.cloud.tencent.com/price/cos/calculator) 进行费用预估。

### 如何查看计费项信息

关于 COS 的计费项您可通过[按量计费（后付费）](https://cloud.tencent.com/document/product/436/36522)了解。本次变更的计费项的更多信息，请查看文档：
- [存储容量费用](https://cloud.tencent.com/document/product/436/53482)
- [请求费用](https://cloud.tencent.com/document/product/436/53861)
- [数据取回费用](https://cloud.tencent.com/document/product/436/53862)


## 遇到问题？

若您对本次升级有疑问，请 [联系我们](https://cloud.tencent.com/document/product/436/37708)，我们将为您解答。
