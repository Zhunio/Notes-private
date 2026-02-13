# Netsuite Warehouse Mangement

## Netsuite WMS setup

- [x] 1. Installing the Netsuite WMS SuiteApps
  - Go to Customization > SuiteBuilder > Search & Install Bundles
  - Install the following bundles:
    - SCM Mobile - **572631**
    - Oracle Netsuite WMS - **572325**
- [x] 2. Enabling Prerequisite Features for Netsuite WMS
  - [x] Company
    - Multiple Units of Measure
  - [x] Transactions
    - Advanced Shipping
    - Pick, Pack, and Ship
  - [x] Items & Inventory
    - Basic Inventory Management (missing)
    - Multi-Location Inventory
    - Bin Management
    - Advanced Bin / Numbered Inventory Mangement
    - Advanced Inventory Management
  - [x] SuiteCloud
    - Custom Records
    - Advanced PDF/HTML Templates
    - Client SuiteScript
    - Server SuiteScript
  - [x] Additional Features for Netsuite WMS
    - [x] Transactions
      - Inbound Shipment Management
      - Advanced Receiving
    - Intercompany Cross-Susidiary Fullfillment
    - [x] Items & Inventory
      - Bar Coding and Item Labels
      - Assembly Items
      - Work Orders
      - Serialized Inventory **(disabled**)
      - Lot Tracking
      - Invetory Status
      - Inventory Count
      - Advanced Item Location Configuration
- [x] 3. Activate the Enable Warehouse Management system rule
  - Using the **WMS Warehouse Manager** role, go to WMS Configuration > Configure Warehouse -> System Rules
  - Activate the following rules:
    - Enable Warehouse Management
- [x] 4. Warehouse Management Roles and Permissions
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
