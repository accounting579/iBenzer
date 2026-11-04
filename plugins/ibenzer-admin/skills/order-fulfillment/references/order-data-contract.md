# Order data contract

Use this reference when reconciling a PO, Nutshell Lead, shipping order, and QuickBooks document.

## Required match fields

| Source | Required facts |
| --- | --- |
| PO/email | PO number, buyer/reseller, ship-to, SKU, quantity, commercial total, conditions |
| Nutshell Lead | Invoice Number, customer/reseller, PO Number, current stage, tracking fields |
| QuickBooks | exact document number, customer, lines/SKUs, quantities, total, status |
| Shipping system | recipient/address, SKU/quantity, carrier, tracking, ship/delivery date |

## Identity rules

- **Invoice Number** is the intended unique cross-system key.
- **PO Number** identifies the buyer's authorization, but is not sufficient to choose a Nutshell Lead or QBO document by itself.
- **Tracking Number** belongs to the physical shipment, not a payment or invoice. Write it only after the carrier confirms it.
- A quote or a PDF titled “Quotation” has no QuickBooks status until matched through QBO.

## Minimum update payload

On an exact match, keep these fields on the one Nutshell Lead:

`Invoice Number | PO Number | Carrier | Tracking Number | Tracking Link | Estimated Delivery Date | current stage / next activity`

If a required fact is unknown, preserve it as blank and report the missing fact; never invent a placeholder.
