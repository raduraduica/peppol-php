## BIS Order only 3.2

##  Principles and prerequisites

This BIS describes a process comprising a Buyer to issue an electronic order without an order confirmation by the Seller.
The main activities supported by this profile are:

**Structured Ordering**

The Order transaction should support the structured ordering of goods or services, using free text or use of identifiers. 

**Accounting**

The ordering process must support the allocation of budgets, so the value amounts of the ordered products may be stated.

**Invoice Verification**

The buyer may provide some information that the seller is required to place on the invoice for aiding and automation of invoice approval.

**TAX reporting**

TAX reporting is not a general requirement on orders. In this context the term TAX is used as a generalization of taxes such as VAT, GST or Sales Tax.

**Transport and delivery**

Only limited support is in scope for transport related information, but it is recognized that the buyer needs to be able to provide some information about requested delivery location, some basic term, time and contact persons for a delivery of an order.

**Inventory**

Supporting inventory management is not in scope, but structured orders based on catalogues can be used to automate picking at supplier warehouses.

## Parties and roles

The **customer** is the legal person or organization who is in demand of a product or service.Examples of customer roles: buyer, consignee, delivery partu, debtor, contracting authority, originator.

The **supplier** is the legal person or organization who provides a product or service. Examples of supplier roles: seller, consignor, creditor, economic operator.

<img src="https://github.com/pondersource/peppol-php/blob/main/docs/pics/order-bis-1.PNG?raw=true"/>

## Benefit

Based on success with automation of invoicing, there is a growing interest in automation of ordering also. This approach has two dimensions: Support further automation of invoicing and using structured catalogues as basis for ordering. Implementing this BIS is an important step for many companies and government agencies towards full procurement automation.

For the sellers, the approval, picking and invoicing can be automated significantly.

For the procuring agency, approval and accounting of invoices can be automated and ordering can be structured by use of catalogues.


## Process flow

The Order process flow can be described as follows:

- A Buyer submits an Order to the Seller requesting for delivery of goods or services

- An Order may refer to a framework agreement for its terms and conditions; otherwise the Buyer’s terms and conditions apply.

- An Order may contain items (goods or services) with item identifiers or items with free text description.

<img src="https://github.com/pondersource/peppol-php/blob/main/docs/pics/bmpn.PNG?raw=true"/>

## Ordering including consignee and delivery party

An order for numbered items with allowance and charges both on order level, line level and price.

**Parties involved**
- Buyer
- Seller
- Consignee
- Delivery party

**Assumptions**
 	
The buyer has a catalogue or list of products to order.
The catalogue contains the item numbers, names and type of unit of measure.

**The flow**

The buyer creates an order with 3 different lines and items.
The seller receives the order.
At time for delivery the seller packs all items, print goods labels which are put on and all packages and a transport label put on the plastic wrapping that holds all the packages.
The wrapped packages are delivered to and unloaded at the location of the consignee.
The packages are reloaded and delivered by internal transport to the delivery party.

**Result**

The buyer and the seller have reached an agreement.
The delivery party has received the ordered items.
If the invoice has an order reference, the invoice can be matched automatically.

**XML example file**
* [Use case Example file](https://github.com/pondersource/peppol-php/blob/as4-testing-1/rules/use-case-examples/order/UC-Order.xml)

## References
* [BIS Order only 3.2](https://docs.peppol.eu/poacc/upgrade-3/profiles/3-order-only/)    
* [Universal Business Language Version 2.1](http://docs.oasis-open.org/ubl/UBL-2.1.html)



