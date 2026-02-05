# Replace RF-Smart with Netsuite WMS

- Bin transfers
  - Bin transer per pound
    1. We scan QR code. QR code contains PO + line number of item in PO.
    2. We put quantity (i.e. 10 pounds)
    3. We select destination bin.
    4. We confirm transfer.
  - Bin transfer per each
    1. We scan QR code. QR codes contains Bin (I believe)
    2. We select item from list.
    3. We put quantity (i.e. 1,2,3)
    4. We scan destination bin.
    5. We confirm transfer.
- Receiving items
  1. We can Bar code from Vendor packing list. Bar code contains PO
  2. We verify each item and quantity against PO.
- Generate Item Receipt
  1. After receiving items, we generate item receipt via Receive button in PO
- Print labels
  1. Once Item Receipt is generated, we print labels for items received.
  2. The labels contain PO in QR code format, and Lot number, and other info.
