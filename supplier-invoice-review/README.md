# Supplier invoice review worksheet

Published by [Calitem](https://www.calitem.com/en/).

A CSV starting point for checking supplier invoice lines against purchasing and receiving evidence. The examples are entirely synthetic and do not describe a customer, a supplier relationship or recovered savings.

## Files

* [invoice-review-template.csv](invoice-review-template.csv): column headings for your own internal review.
* [invoice-review-example.csv](invoice-review-example.csv): three illustrative situations: a price difference, a quantity difference and missing receipt evidence.

The CSV files contain no formulas. Example values are precomputed; enter and verify calculations in your own spreadsheet. Prepared with AI assistance and arithmetic checks of the three synthetic examples.

## How to use it

1. Identify the supplier, invoice, order and line references from the actual documents.
2. Align currency and units before comparing quantities and net unit prices. Record any documented conversion or discount that changes the comparison.
3. For the simple examples, calculate `expected_net_amount` as `invoiced_quantity * agreed_net_unit_price`. This uses the invoiced quantity so a partial invoice is not compared with the value of the entire order.
4. Calculate `net_price_variance` as `invoiced_net_amount - expected_net_amount`.
5. Where receiving evidence is available and the units agree, calculate `quantity_variance` as `invoiced_quantity - received_quantity`. Preserve an unknown received quantity as blank. It is not zero and is not proof of a quantity difference.
6. Assign a review owner and record the evidence, resolution and decision date. Follow your purchasing, approval and accounting rules before posting.

The example calculations exclude tax, additional charges, rebates and rounding. Apply the appropriate rules for those items in a real review. A detected variance requires investigation and does not by itself establish an overcharge or recovered savings. This worksheet does not post accounting entries or initiate payments.

Read the [supplier invoice review checklist](https://telegra.ph/Supplier-invoice-review-checklist-11-05) for the broader process, including recurring services and partial deliveries.

## Publisher

Calitem provides AI for purchasing and supplier cost control, invoice checks, configured approvals and accounting preparation for an existing ERP. Connector coverage and workflows depend on the agreed configuration. This is a Calitem educational resource, not an independent product review.
