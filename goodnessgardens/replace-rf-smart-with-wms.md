# Replacing RF-Smart with Netsuite WMS

I want to replace RF-Smart with Netsuite WMS. The main reason for this switch is pricing.

One caveat

- We tried switching WMS, but it seems we need to enable Pick, Pack, and Ship feature Netsuite. I don't know what Pick, Pack, and Ship feature is. But from more experience users, it seems Pick, Pack, and Ship feature is not needed for our use case. So, enabling it won't be an option for us.
- Can you explain what that is, and if we actually need to turn it on?
- From higher ups, it seems we can only use WMS if Pick, Pack, and Ship feature is enabled. And that won't be an option. 
- I'm still new and need to understand why, but we will not enable Pick, Pack, and Ship feature.
- I'm Software Engineer, so another option, would be to develop custom web app (angular, vue, react) to talk to REST API of Netsuite and develop only the features we need.
- Can you advise here what's best approach? also filling in the gaps in my understanding?

Here is a list of what we use RF-Smart for:

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
