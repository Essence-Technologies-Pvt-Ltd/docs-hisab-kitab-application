# docs-hisab-kitab-application
- backend application webapi ref: https://api-cloud.restroorder.com/swagger/index.html


## Build ERP Application in flutter Application with different types of users: OrgAdmin, Finance and General.
Application will focus on: 
- Login/Register Authentication
- General Accounting, Multiple outlets, Multiple Currency
- Product Items with Multiple Units, Child Items
- Customers, Supplier, Financial Balance Snapshot
- Inventory Modules 
	- Purchase 
	- Sales
	- Sales Return
	- Purchase Return
	- Stock Transfer [between outlets]
	- Stock Adjustment
- General Expenses
- Accounting Vouchers
- Profit and Loss Reports
- Focus over mobile app designs and user experience
- general settings
	- Add Vat to sales
	- Default Currency
	- 
- Additional Expenses Categories + Sub Categories[Staff Salary -> Ram, Shyam, Hari, Utilities -> Rent, Internet, Lunch, Electricity, etc]
- Accounting Ledgers [Assets, Liabilities, Income, Expenses]
- Outlet Management
- Staff Management
- Payroll Expenses
- Payment methods
- Cash & Bank Ledgers
- Inventory Stock Report

## Organization Settings
- VAT Application Yes/No should be there
- If VAT is applicable, VAT Percent to be setup
- Admin Email Id which will receive all email updates
- Organization Name, Logo, Address, Email which can be updated
- Default Currency
- Information related to package subscribed
- Backup and Restore Whole Data
- Active Fiscal year

## Outlet Mgmt
- Max no of outlets are defined by tenant subscription
- so before creating new outlets the limitations need to be checked

## outlet settings
- default cash ledger to be mapped
- default bank ledger to be mapped
- Shift Open/Close Required for Txn

## Fiscal year
- Code [pk, string, 10], start date, end date, last bill no, last receipt no

## Fiscal year Acc Voucher Config
- tracks last voucher no of different types of voucher types


## Cost Center [Billing Counters]
- Used in Restaurant POS for matching Billing Counter, BAR, KTICHEN
- Billing Counter should open shift before making sales billing, if outlet has shift open/close

## Staff/user Mgmt
- User Roles mainly: Org Admin, Finance, Cashier
- Cashier should be linked to Outlet and Billing Counter
- Finance can have access to single outlet or multiple outlets
- Org Admin can reset password or any related users

## Cash & Bank
- Easy to use accounting ledgers mapped and marked as cash and bank
- Multiple ledgers can be marked as Cash ledger like petty cash, main cash
- Multiple Bank Ledgers will be there in system. Bank Ledgers will be common for all outlets

## Customer Mgmt
- Customer CRUD with receivable snapshot and opening balance
- Check Statment, Email Statement, Collect Payments

## Supplier Mgmt
- Supplier CRUD with payable snapshot and opening balance
- Check Statement, Email Statement, Make Payments

## Payment Methods
- CRUD Operation
- May be of type: Cash, Credit, QR, Bank, Cheque, Credit Card.
- QR, Bank, Credit Card are linked with bank ledger

## Inventory modules features
- Products, Categories, Units CRUD Operation
- products can be marked taxable/non taxable, Track Stock Yes/No
- Inventory Products may have multiple child items [child items are also product]
- Inventory Products may have multiple units out of which 1 will be default
- Units has conversion ratio like 12 for dozen, 2 for pairs
- while making purchase, sales etc item rates can be changed by users if item has prop -> fixed rate as false
- discounts and taxes are applicable to each purchase, sales etc modules
- purchase invoices should have option to mark tax claimable yes/no
- purchase, sales should have payment log matching payment method and amount. This will enable us to mark out of 10,000/- in bill amount, 3,000/- has been paid into bank, 3500 has been paid via online QR, 2,000 has been paid in cash, rest is marked as credit payable/receivable to party ledger
- Inventory Stock Report [Outletwise]

## Accounting Module
- Journal Vouchers
- Ledger Statement
- Trial Balance
- Balance Sheet
- Profit and Loss
- Cash Flow

## Other Modules + Accounting Module Link
- Each Customer, Supplier, Cash & Bank must sync up with accounting module ledgers.
- customer sync up sundry debtors ledger category should be linked and mapped via default ledger settings
- supplier sync up sundry creditors ledger category should be linked and mapped via default ledger settings
- cash ledgers should be mapped from default ledger settings
- bank ledgers should also be mapped from default ledger settings
- staff salary ledger category should be linked and mapped via default ledger settings
- 


# Hisab-Kitab Ledger Integration: Hisab-Kitab ERP Mobile

An offline-first, multi-currency ledger bookkeeper and credits management extension built for **Hisab-Kitab ERP Mobile**. This system merges traditional micro-merchant credit ledgers ("Udhar Book") with automated enterprise accounting and double-entry voucher journals list structures.

---

## 🎨 Core Architectural Features

### 1. Traditional Khata Ledger Books ("Hisab Kitab")
- **Active Ledger Timeline:** View sorted ledger lines showing specific credits, payments, dates, and item remarks.
- **Red "You Gave / Udhar" Records:** Log credit issued to customers or payments forwarded to suppliers.
- **Green "You Got / Jama" Records:** Log collections received from customers or bills received from suppliers.
- **Auto-Balance Synchronizer:** Balance deltas cascade directly to accounts receivable or payable directories upon entry.

### 2. Settle & Sync Toolkit
- **One-Tap Settle:** Clear out outstanding client balances through automatic offset transaction logs.
- **SMS/WhatsApp Reminders:** Copy friendly, personalized payment reminder templates populated with current balances to the clipboard.
- **Interactive Reversals:** Support row-level transaction deletions that safely reverse current balances.

### 3. High-Contrast PDF Statements
- **Printable Statements:** Generates high-fidelity preview sheets matching professional invoice templates.
- **Aesthetic Page Design:** Formatted with top watermarks, terminal locations, clear party blocks, and hand-written sign-offs.
- **Running Ledger Table:** Chronologically lists dates, particulars, debits, credits, and progressive running balance columns.
- **System Print Ingress:** Direct trigger to interface with standard browser system printers.

---

## 📱 Interactive User Experience

### Recording an Udhar/Credit (You Gave)
1. Navigate to the **Partners Dashboard** tab.
2. Select any active Financial Partner to expand their ledger profile options.
3. Tap **🔴 YOU GAVE**.
4. Enter the amount option, details (such as invoice number or itemized menu details), and transaction date.
5. Tap **Book Entry** to play the high-frequency scan tone and capture the entry.

### Generating PDF Reports
1. Expand the target Customer/Supplier.
2. Under the actions row, tap **📄 PDF Report**.
3. Review the high-contrast printed preview sheet containing summaries and running ledger balances.
4. Tap **🖨️ Print Document** to trigger standard browser print dialogs.

---

## 🗃️ Under the Hood: Data Schema

```typescript
interface FinancialPartner {
  id: string;
  type: 'Customer' | 'Supplier';
  name: string;
  code: string;
  balanceCurrency: 'AED' | 'USD' | 'GBP';
  balance: number; // Positive (+) for Receivable Debit, Negative (-) for Payable Credit
  creditLimit: number;
}

interface PartnerTransaction {
  id: string;
  partnerId: string;
  type: 'Credit' | 'Payment'; // Credit (You Gave - Udhar) or Payment (You Got - Jama)
  remarks: string;
  amount: number;
  date: string;
}
