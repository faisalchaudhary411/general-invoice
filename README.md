# Invoice App (white-label)

A blank invoice generator with no business name, logo or branding built in. Everything printed on the invoices comes from **🏢 Business details** at the top of the page:

- Business name, tagline, address, city, phone numbers, owner name
- Payment details (one per line) — printed on the invoice and used in the QR code on the normal invoice
- Footer text, main colour and accent colour (the whole app and invoices follow them)
- Logo and signature pictures (white background removed automatically)
- The round stamp is drawn from the business name, city and tagline

Business details are saved on the phone as you type. On first open the section is expanded; once a name is saved it stays collapsed.

## Items
No built-in item list. Type an item name, then choose:
- **Qty × Price** — amount = qty × price
- **Lumpsum** — just a qty and an amount; nothing is multiplied

Items you add with **+ Custom Item** (or "Save as default price") are saved to your list and can be edited under **Manage Item Prices**.

## Deploy
Upload all files to a GitHub Pages repo (or any static host) and open the link. Customers, backups, cloud sync and printing work as usual; cloud sync data file defaults to `customers.json`.

## License
- 7-day free trial from first use, then the app locks until a license key is entered.
- The customer opens Customers > License (or the lock screen), copies their Device ID and sends it to you.
- You make a key in `license-keygen.html` (PRIVATE, never upload it) and send it back; they paste it and tap Activate.
- Keys are signed (ECDSA) so they cannot be invented without your private key. Keys can be locked to one device, or work on any device, and can be lifetime or expire.
- To show a WhatsApp button on the lock screen, set `LIC_CONTACT_WA` (e.g. '923001234567') near the top of the license script. Change `LIC_TRIAL_DAYS` for a different trial length.

## Suppliers
Suppliers tab: add the people you buy from, save slips (photo, date, amount, paid/unpaid/part). Photos stay on the phone; use "Save backup" regularly.

## Billing, stock and profit (v c)
- **Stock tab**: products with barcode, sale price, cost price, stock, unit, category, low-stock alert, expiry/batch/generic name (medicines). Add one by one, paste a list (Name, Price, Cost, Stock, Barcode, Category) or import a CSV. Export CSV, change all prices by %, add stock when goods arrive, make EAN-13 barcode labels.
- **Scanning**: camera button on the bill (continuous - every scan is added, same item again = quantity +1), or a USB/Bluetooth scanner gun. Unknown barcode opens "Add product" with the code filled in. Uses the phone's built-in scanner when available, otherwise `zxing.min.js` (keep that file next to index.html).
- **Bills**: empty customer name = Walk-in Customer. "Paid in full (cash)" button. Saving a bill reduces stock; deleting/re-saving a bill puts it back.
- **Profit tab**: daily and monthly sales, cost of goods, gross profit, expenses, net profit, cash received, credit given, top items. Profit uses the cost price saved on each bill line; items without a cost price are left out of profit and flagged.
- Products, stock and expenses live on the phone (backup button in the Stock tab). Bills/customers keep their own backup and cloud sync.

## Business type + barcode labels
- **Business details > Business type** (General store, Grocery, Pharmacy, Electric & Hardware, Mobile, Garments, Cosmetics, Stationery, Other). Asked once. It decides which product fields appear (pharmacy: expiry, batch, generic name; grocery/general/cosmetics: expiry; others: none) and the default unit. There is no per-item category box any more (a category column can still be imported from CSV).
- **Stock > Print barcode labels**: pick products or make custom labels (any text), set copies (or copies = stock), barcode type (Auto, Code 128, EAN-13, EAN-8, Code 39, QR), size (58mm roll 48x25 / 48x35 / 38x20, or A4 sheets 3x8, 4x10, 5x13, 2x7), what to show (business name, product name, price, code number, extra line), cut lines. Print on the Bluetooth printer, or download PNG (roll) / PDF + system print (A4).
- Keep `jsbarcode.min.js` and `zxing.min.js` next to index.html.

## Selling rules
- A bill with an out-of-stock or not-enough-stock item cannot be saved, printed, downloaded or shared, and the scanner will not add it. Expired items are blocked the same way. Both can be allowed in Stock > Options & backup (not recommended).
