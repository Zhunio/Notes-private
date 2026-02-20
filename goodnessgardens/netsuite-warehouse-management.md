# Netsuite Warehouse Management

## 1. Installing the Netsuite WMS SuiteApps

- [x] Go to Customization > SuiteBundler > Search & Install Bundles
- [x] Install the following bundles:
  - [x] SCM Mobile - **572631**
  - [x] Oracle Netsuite WMS - **572325**

## 2. Enabling Prerequisite Features for Netsuite WMS

- [x] Go to Setup > Company > Enable Features
  - [x] Company
    - [x] Multiple Units of Measure
  - [x] Transactions
    - [x] Advanced Shipping
  - [x] Items & Inventory
    - [x] Inventory (Basic Inventory Management)
    - [x] Multi-Location Inventory
    - [x] Bin Management
    - [x] Advanced Bin / Numbered Inventory Management
    - [x] Advanced Inventory Management
  - [x] SuiteCloud
    - [x] Custom Records
    - [x] Advanced PDF/HTML Templates
    - [x] Client SuiteScript
    - [x] Server SuiteScript
  - [x] Additional Features for Netsuite WMS
    - [x] Transactions
      - [x] Inbound Shipment Management
      - [x] Advanced Receiving
    - [x] Items & Inventory
      - [x] Warehouse Management
      - [x] Intercompany Cross-Subsidiary Fulfillment
      - [x] Bar Coding and Item Labels
      - [x] Assembly Items
      - [x] Work Orders
      - [ ] Serialized Inventory (disabled; not required for our current process)
      - [x] Lot Tracking
      - [x] Inventory Status
      - [x] Inventory Count
      - [x] Advanced Item Location Configuration

## 3. Add "WMS Mixed Items" fields to Custom Form

- [x] Go to Assembly/Inventory Item (i.e "ANCDPZ03GG", "2OZBASTUBE") > Edit > Customize > Custom Form
- [x] Go to Fields > NS WMS
- [x] Check the "Show" box for the following fields:
  - [x] WMS MIX LOTS IN BINS
  - [x] WMS MIX ITEMS IN BINS

## 4. Setup WMS Mass Update for Item records

- [x] Go to Lists > Mass Update > Mass Updates
- [x] Go to General Updates > Items > Assembly/Inventory Item
- [x] In the Results tab, add the following fields:
  - [x] WMS MIX LOTS IN BINS
  - [x] WMS MIX ITEMS IN BINS
- [x] In the Mass Update Fields tab, add the following fields:
  - [x] WMS MIX LOTS IN BINS - Set to "Yes"
  - [x] WMS MIX ITEMS IN BINS - Set to "Yes"

## 5. Enable Pick, Pack, and Ship Feature

- [x] Go to Setup > Company > Enable Features
  - [x] Transactions
    - [x] Pick, Pack, and Ship
- [x] Go to Setup > Accounting > Shipping
- [x] Change "Default Item Fulfillment Stage" to "Shipped"

## 6. Enable Warehouse Management Feature

- [ ] Go to Setup > Company > Enable Features
  - [ ] Items & Inventory
    - [ ] Warehouse Management

## 7. Setup Custom Label for WMS Mobile App

- [ ] Go to LPC Admin > Configuration > Label Design
- Edit the "3x2 ITEM RECEIPT LABEL (LOT QR)" template

## 8. Activate the Enable Warehouse Management system rule

- Using the **WMS Warehouse Manager** role, go to WMS Configuration > Configure Warehouse -> System Rules
- Activate the following rules:
  - Enable Warehouse Management

## 9. Warehouse Management Roles and Permissions

### Warehouse Management Roles

- **Administrator** - To enable features, install SuiteApps, and create or manage records for NetSuite WMS
- **Mobile Administrator** - To customize and configure mobile processes and mobile printing
- **WMS Web Services Admin** - To access and use the NSWMS Printer Driver Application
- **WMS Warehouse Manager** - To perform setup procedures for mobile processes, such as activating system rules and creating item aliases or cycle count plans
  - **WMS Inbound Manager** - For inbound processing records and tasks only
  - **WMS Outbound Manager** - For outbound processing records and tasks only
- **WMS Mobile Operator**
  - **WMS Inbound Operator** - For inbound processing tasks and outbound picking through mobile
  - **WMS Outbound Operator** - For outbound processing tasks only

### Warehouse Management Permissions

[NetSuite WMS Roles and Permissions](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_156520480478.html#subsect_156520614424)

## 10. Warehouse Management Records and Templates

- To create or update records for your warehouse configuration:
  - Creating Warehouse Locations
  - Configuring Records for Locations with Bins
  - Creating Item Stock Locations
- To create or update records for warehouse or shipping items and order types:
  - Creating Item Process Families
  - Creating Item Process Groups
  - Creating Inventory Statuses
  - Setting Up Units for Pick Decomposition
  - Creating Items for NetSuite WMS
  - Creating Item Aliases
  - Creating Order types
  - Defining a UCC Code Format
  - Creating Carrier Service Levels
- To customize outbound processing templates and forms according to your business requirements:
  - Creating Custom Wave Criteria Templates
  - Creating a Custom Pick Ticket Saved Search
  - Creating a Custom Advanced Templates for Pick Tickets
  - Creating Custom Wave Forms
  - Setting Up Custom Packing Lists

## 11. Setting Warehouse Management Preferences

## 12. Warehouse Management Strategies

## 13. Setting Up Bin Block for Order Picking

## 14. Mobile App Setup

## 15. Netsuite WMS Shipping Integration

## 16. Electronic Data Interchange (EDI) Integration Setup

## 17. Mobile Device for Netsuite WMS

### Accessing Bins on the App

### Inventory Status on Mobile Devices

### Multiple Units of Measure (UOM) on Mobile Devices

### Mobile Device Transactions
