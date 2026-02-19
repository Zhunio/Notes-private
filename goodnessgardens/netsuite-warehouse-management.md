# Netsuite Warehouse Management

## Netsuite WMS setup

- [x] 1. Installing the Netsuite WMS SuiteApps
  - [x] Go to Customization > SuiteBundler > Search & Install Bundles
  - [x] Install the following bundles:
    - [x] SCM Mobile - **572631**
    - [x] Oracle Netsuite WMS - **572325**
- [ ] 2. Enabling Prerequisite Features for Netsuite WMS
  - [ ] Company
    - Multiple Units of Measure
  - [ ] Transactions
    - Advanced Shipping
    - Pick, Pack, and Ship
  - [ ] Items & Inventory
    - Basic Inventory Management
    - Multi-Location Inventory
    - Bin Management
    - Advanced Bin / Numbered Inventory Management
    - Advanced Inventory Management
  - [ ] SuiteCloud
    - Custom Records
    - Advanced PDF/HTML Templates
    - Client SuiteScript
    - Server SuiteScript
  - [ ] Additional Features for Netsuite WMS
    - [ ] Transactions
      - Inbound Shipment Management
      - Advanced Receiving
    - Intercompany Cross-Subsidiary Fulfillment
    - [ ] Items & Inventory
      - Bar Coding and Item Labels
      - Assembly Items
      - Work Orders
      - Serialized Inventory (disabled; not required for our current process)
      - Lot Tracking
      - Inventory Status
      - Inventory Count
      - Advanced Item Location Configuration
- [ ] 3. Activate the Enable Warehouse Management system rule
  - Using the **WMS Warehouse Manager** role, go to WMS Configuration > Configure Warehouse -> System Rules
  - Activate the following rules:
    - Enable Warehouse Management
- [ ] 4. Warehouse Management Roles and Permissions
  - **Administrator** - To enable features, install SuiteApps, and create or manage records for NetSuite WMS
  - **Mobile Administrator** - To customize and configure mobile processes and mobile printing
  - **WMS Web Services Admin** - To access and use the NSWMS Printer Driver Application
  - **WMS Warehouse Manager** - To perform setup procedures for mobile processes, such as activating system rules and creating item aliases or cycle count plans
    - **WMS Inbound Manager** - For inbound processing records and tasks only
    - **WMS Outbound Manager** - For outbound processing records and tasks only
  - **WMS Mobile Operator**
    - **WMS Inbound Operator** - For inbound processing tasks and outbound picking through mobile
    - **WMS Outbound Operator** - For outbound processing tasks only
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

## Netsuite WMS post-setup

- [ ] Warehouse Management Records and Templates
- [ ] Setting Warehouse Management Preferences
- [ ] Warehouse Management Strategies
- [ ] Setting Up Bin Block for Order Picking
- [ ] Mobile App Setup
- [ ] System Rules for Netsuite WMS
- [ ] Creating a Wave Release Schedule
- [ ] Netsuite WMS Shipping Integration

### Configuring Netsuite WMS for Location With No Bins

### Netsuite WMS Setup with Ship Central
