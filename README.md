# docs-hisab-kitab-application
- backend application webapi ref: https://api-cloud.restroorder.com/swagger/index.html

## Build ERP Application in flutter Application with different types of users: OrgAdmin, Finance and General.
Application will focus on: 
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

## Outlet Mgmt
- Max no of outlets are defined by tenant subscription
- so before creating new outlets the limitations need to be checked

## outlet settings
- default cash ledger to be mapped
- default bank ledger to be mapped
- Shift Open/Close Required for Txn

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
