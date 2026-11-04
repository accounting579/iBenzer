---
name: ab-order-processing
description: "处理 AB / Office Depot 非批发订单：核对 PO、Excel、ShipStation、QuickBooks 与 Fishbowl 数据，并准备出货与发票步骤。适用于用户明确要求处理、核对或更新 AB 订单时。"
---

# AB 订单处理

## 公司固定执行与错误闭环
开始此工作流前，先读取 [公司固定规则](../../references/company-operating-rules.md)。该规则适用于本 Skill 的所有步骤；如与当前用户明确指令冲突，以用户当次明确指令为准。


用于 AB / Office Depot 的非批发客户订单。当前权威参考为《出货&退货:AB订单流程》：
https://docs.google.com/document/d/1QM8bfYkG1eKRIzZrj56bVcOuKpcp_HWk7g-KcwRMUNQ/edit

## 适用范围

- 处理来自 Accounting 邮箱的 AB 订单。
- 核对 PO、Excel、ShipStation、QuickBooks、Fishbowl 或准备相应的出货与发票资料。
- 不用于批发客户订单或未标明为 AB / Office Depot 的订单；遇到此类情况，先询问适用流程。

## 核对与处理顺序

1. 查看新订单及历史邮件，避免漏单。
2. 从 PO 提取并核对：PO 编号、收货地址、SKU/产品、数量、订单日期、价格。
3. 确保 PO、Excel 和 Fishbowl 中的对应资料一致。任何缺失或不一致都要清晰列出，不要自行猜测或改写。
4. 若商品数量超过 2 件，先请求仓库称重；在收到重量前停止后续需要运费或标签的步骤。
5. 在 ShipStation 准备订单时，使用 Excel 中收货地址首行作为 Name，将 Fishbowl Number 作为 Order #，并在 Line Items 填写 Order SKU，供仓库拣货。
6. 使用 Third Party 运费方式；创建标签后复核 Billing 仍为 Third Party，并把 Tracking Number 回填 Excel。
7. 在 AB Invoice 记录中保留 SKU、Fishbowl SO #、PO #、承运商追踪信息、数量、日期和 Subtotal。
8. 在 QuickBooks 发票中，使客户、Bill To/Ship To、SO #、PO 与追踪信息、金额、数量及 Subtotal 与订单和 Excel 一致；填写运输方式与发货日期。
9. 在 Fishbowl 建立 New Sales Order，核对 Customer、SKU、价格、数量、Bill To 和 Ship To；完成后将 SO No. 回填 Excel，并进行最终订单与库存核实。

## AB SKU 与当日表格规则

- 只有电脑硬壳 SKU 才须以 `+1` 结尾；包、内胆包、sleeve 等非硬壳产品不得机械添加 `+1`。录入 Excel、Fishbowl、ShipStation Line Items 和 AB Invoice 时必须按产品类别保持一致。
- 已确认映射：PO Mfg Number `LC-NPT-T14CYCL+1` 对应订单 SKU `MT14-CYCL+1`。不得写成 `MAT14-CYCL+1`，也不得省略 `+1`。
- 已确认映射：PO Mfg Number `LC-NPT-T16X-CYCL+1` 对应订单 SKU `MT16X-CYCL+1`。不得把供应商 PO 的 `LC-NPT-` 前缀原样写入 AB 出货 SKU。
- 已确认映射：PO Mfg Number `LS-SLD-0115BK`（包／sleeve）对应订单 SKU `LS-SLD15-BK`，不加 `+1`。不得保留 PO 中的 `-0115BK` 编码形式。其他 `LS-SLD` 款式必须先核实是否为包／sleeve，再决定是否可加 `+1`；没有确认时不得猜测。
- 已确认映射：AB PO 所列 `LS-BPS-0213BK` 对应订单／出货 SKU `LS-BPS-13BK`。这是包／sleeve SKU，**不加 `+1`**；录入 Excel、Fishbowl、ShipStation Line Items 和 AB Invoice 时均使用 `LS-BPS-13BK`。
- 当日 AB 页的 `Platform PO` 栏默认留空；客户 PO、终端用户 PO、LAB 或其他 PO 文本不得填入该栏，除非用户明确要求填写。
- 写入当日 AB 页前，逐项将 PO Mfg Number 与既有 AB SKU 映射核对；存在 `LC-NPT-` 等供应商前缀时，必须写入对应的订单 SKU，不能仅机械保留 PO 原文。映射不明确时停止并询问，不得猜测。
- Delivery Address 必须按历史 AB 页的多行格式写入并居中：收件单位／姓名、街道地址（必要时第二地址行）、`城市 州`、ZIP（ZIP+4 使用连字符）、联系人 ` / ` 电话。不得使用逗号把地址压成单行；写入后开启换行并按内容适配行高。
- 同一 AB PO 的多个 SKU 必须保留为各自独立的明细行。共享的 Fishbowl Number、Delivery Address、Order Date、Tracking、CRM Update 和 Memo 单元格须跨这些明细行纵向合并；整组订单（而非仅首行）使用黄色底色。SKU、Quantity、PO Number、Price 和 Subtotal 保持逐行单元格。合并后视觉复核，确保 Fishbowl、地址和日期只显示一次且每项金额清晰可见。
- 每日新建的 AB 日期页应置于 `Template` 页之后，作为最靠前的日期页；不要追加到历史日期页之后。
- 新增或更新当日页时，应保持模板的边框、金额公式及颜色，并使标题、地址、Fishbowl Number 和 Tracking 栏在正常缩放下完整可读。完成后进行视觉复核；不得仅写入数据而不处理明显的截断或不协调的行列尺寸。
- 每次 AB 标签生成并取得 Tracking 后，除回填当日《2025 线下散单 - AB》外，必须同步更新《invoice葵花宝典 & AB DISTRIBUTING 2021.xlsx》中对应的 AB 记录；以 PO #、Fishbowl SO #、SKU/数量交叉定位，写入相同 Tracking，并在两个表复核一致后才报告完成。

## 完成前检查

- SKU、数量、价格、地址、PO #、Fishbowl SO # 与 Tracking Number 在相关系统/表格中均一致。
- Subtotal 与 Excel 计算结果一致。
- 标签 Billing 是 Third Party。
- 发票和订单已按当前任务要求完成保存、打印或发送。

## 批量 Get Rate 防漏检查

当用户要求对待发订单进行 Get Rate 时，先完整浏览当前列表，并按已确认的产品重量、规格和服务要求分组。不得只完成首个清晰分组后停止：须继续完成所有可由既有规则确定的同类订单，并保留已成功 Get Rate 的订单勾选状态，供用户后续打印标签。

- 此规则针对 EzeeShip 的线上散单，不适用于 AB 线下散单表格或 ShipStation 打单。开始前必须完整扫描当前待发列表（包括继续向下浏览的可见订单），把所有已知重量的订单一次性归入相应重量组；不得只处理列表顶部、用户已勾选的少数订单，或在得到一两个费率后结束。

- **批次清单闸门：** 在首次勾选、以及每次切换重量组之前，先在当前页面建立可见订单的“SKU／订单号 → 已知重量 → 本批归属”清单。只有清单中该重量的全部非暂缓订单都已勾选，才可修改服务、规格或点击 Get Rate；不得因为一个订单已有绿色费率、另一个订单服务为空、或某行排在后面，就将同重量组拆开处理。完成一组后必须回看清单，继续下一组，直到所有可按现有规则判定的订单都有绿色费率并保持勾选。用户明确要求暂缓的订单（例如指定号码或 577 开头）从清单中标作“跳过”，不得混入批次。

- 手机相关产品统一按 4 oz；单件 13/14 英寸电脑壳统一按 10 oz；MAT15 为 12 oz（包括 `E-LC-HPE-MAT15-BK+2`，须与其他 12 oz 的 MAT15 订单同批处理）；MA11 为 8 oz。
- 两个 13/14 英寸电脑壳为 15 oz；15 与 16 的组合为 2 lb；数量超过 5 件时必须等仓库称重。
- 电脑壳 SKU 标记为 `+3` 时统一为 2 lb（例如 `MR13-CYCL+3SP`）；不得沿用单件 13/14 的 10 oz 规则。
- 下列单件产品也统一为 15 oz，且遇到时必须与当批其他 15 oz 订单一并处理：`W-T16X-CL+1TC`、`MR15-QUGN+1`、`MMP15T-NVBL+1A`、`LC-HPE-LNV100E4-BK`、`LC-HPE-DL-PB14250-BK`、`LC-HPA-HP14EB6-G1i-BK`、`E-MT16-MTGN+1TC`、`E-MR15-BK+1`、`W-T16X-CL+1 FBW`、`W-MT16-QUGN+1 FBW`、`W-MT16-CYCL+1TC FBW`、`W-LC-HPE-MS-LSE-CL FBW`、`W-LC-HPE-LNV300E3-BK FBW`、`MMP16T-GY+1TC`、`E-MT16X-CYCL+1`、`E-MT16-CYBK`、`E-MT16-BK`、`E-MT15-CL+2TC`、`E-MT15-BK+2TC`、`E-MR15-NVBL+1`、`E-LS-EVA11P-BK`、`E-LS-BG15-BK`。
- 批量处理时，先完整勾选同一重量组，再点 `Change Service`，明确选择 `USPS Ground Advantage` 并点 `OK` 保存；不能只看列表中已有的服务文字就跳过此步骤。服务变更完成后，才进入尺寸/重量与 Get Rate。
- 再点 `Change Dimensions And Weight`：必须选择对应的保存规格预设，不手工填写尺寸。单件 13/14 英寸电脑壳使用 `MT13 (10*13*3)` 预设并设为 `0 lb 10 oz`。其他重量组也须先选其规定预设、再填该组重量并保存。
- 每个组保存服务和尺寸/重量后再点 `Get Rate`，等待页面回传。仅出现绿色美元金额才算成功；红色感叹号、空白或 `-` 均不算完成，须单独重试并记录为页面错误。不得把不同重量的订单混在同一次服务/尺寸/费率操作中。
- 结束前逐项核对：当前可按规则处理的订单均已有运费结果；不同重量订单未混选；成功订单仍被勾选；任何真正需要额外信息或仓库称重的订单单独列出。
- 最终状态以页面为准：每一笔已知重量订单必须同时满足 `(1)` 已实际保存 USPS Ground Advantage、`(2)` 已实际保存对应预设与重量、`(3)` Get Rate 栏出现绿色美元金额、`(4)` 仍保持勾选。只显示服务名称、刷新图标、`-`、空白或红色感叹号都不是完成；须先针对该订单/该重量组重试，再报告异常。

### Get Rate 操作防火墙（强制）

- 用户说“Get Rate”时，授权范围仅为：选择订单、修改服务／预设／重量、点击 **Get Rate(s)**、读取绿色费率并保留成功勾选。**绝不**点击 `Create Label(s)`、`Create Label`、`Print`、`Shipment Actions`、`Save Draft`、`Cancel Order(s)` 或任何生成、打印、作废、保存订单的按钮；这些动作必须有用户单独、明确的指令。
- 每次批量动作前，重新读取当前页面并确认：(1) 当前勾选订单数与本批清单相等，(2) 工具栏目标按钮文字准确为 `Change Service`／`Change Dimensions And Weight`／`Get Rate(s)`，(3) 没有打开 `Create Label(s)` 对话框。不得沿用旧页面元素索引、旧坐标、旧勾选状态或旧截图执行点击。
- 点击 `Get Rate(s)` 后，等待结果并逐项检查绿色金额；若出现任何标签创建／费用合计／`Created` 状态对话框，立即停止，不继续处理其他订单，保留页面供用户核对，并如实报告已创建数量和可见总额。不得把标签创建当作 Get Rate 成功。
- 线上 EzeeShip 散单与 AB 线下散单是两个独立工作流：开始前必须复述并在页面确认当前系统与任务范围。不得因用户同时提及 AB、Fishbowl、ShipStation 或 EzeeShip 而将一方的数据、重量、标签动作或表格写回带入另一方。

## 授权与异常

- 默认只读取、核对、整理并报告结果。
- 创建/修改/保存订单、生成或打印标签、发送 Invoice、Issue Fishbowl 订单、修改库存或写回 Excel 前，必须获得用户对该具体动作的确认。
- 不暴露或复述账户号、客户敏感资料或其他凭据；如需填写，直接使用用户授权的系统中的既有资料。
- 若流程文件与用户当次指示冲突，以用户当次指示为准，并说明差异。

