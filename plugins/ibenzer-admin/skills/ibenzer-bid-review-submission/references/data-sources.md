# Google Drive Data Sources

## Primary folder
- `6, Virtual Assistant`
- Folder ID: `1bhAtBWxyg4oe60SIXMjg9KeTItMY1Yn7`

## Primary tracker
- Spreadsheet: `Bid - VA`
- Spreadsheet ID: `1PjcdyV0BScNda9xNT_f7xaPpguvs1gHuTnW46BSBkm4`

### Important tabs
- `2026 Bid List`: active/current bid pipeline.
- `2026 Bid Result`: submitted bid outcomes and result follow-up.
- `2025 Bid List`, `2025 Bid Result`, `2024 Bid List`, `2024 Bid Result`, `2023Bid List`: historical comparison.
- `CRM`: customer history, communication, school background.
- `Account Info `: platform account information. Access only when needed; never reveal credentials.
- `Competitor`: competitor/market pricing history.
- `Contract`: contract-specific tracking.

### 2026 Bid List columns observed
Date Issued; School Name; Bid Documents; Submit documents; Relevant; Expected Submit Date; Submit Date; Due Date; Tracking Number; Required Product; Quantity; Reason; Way of Submission; Submit List; Alternation or not; Sample(Demo)?; Lead time; All or none?; Question Sent?; Required Bid Package; Products we can offer; Special Requirement; Submit SKU & Quote; Result.

### 2026 Bid Result columns observed
Entity; Bid Date Sent; Progress; Product; Quantity; Link; Total Amount; Respond; Result; Tabulation Link; Remarks.

## Bid folders
Use the current-year folder first:
- `2026 Bid Docs - Directly and Indirectly Relevant`

Other useful folders:
- `Submitted Document - Directly and Contract`
- `Bid Results (Document and Tabulation)`
- `Bid Reference`
- `Bid Documents`

## Internal SOP
- `BID SOP for VA.docx`
- File ID: `1v-F5KuFPmXV5uymV0bH2zSDPgnI0PXS5`

## Connector behavior
Use Google Drive search/list/fetch and Google Sheets range reads to gather facts. Write to tracker cells only when facts are verified. Preserve existing sheet structure, formulas, naming, and conventions.
