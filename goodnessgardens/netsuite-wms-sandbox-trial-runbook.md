# NetSuite WMS Sandbox Trial Runbook

## Goal

- Run a controlled NetSuite WMS trial in sandbox.
- Produce a repeatable checklist for production rollout with minimal risk.

## Scope

- Features:
  - Pick, Pack, and Ship
  - Warehouse Management
- Bundles:
  - SCM Mobile (`572631`)
  - Oracle NetSuite WMS (`572325`)

## Sandbox Trial Checklist

### 1. Baseline Capture

- Record current fulfillment flow screenshots and settings.
- Record current warehouse roles used by operations users.
- Select 3 test scenarios:
  - Standard sales order
  - Larger/multi-line order
  - Edge case (short pick, missing bin, or partial fulfillment)

### 2. Bundle Verification

- Confirm both bundles are installed in sandbox:
  - SCM Mobile (`572631`)
  - Oracle NetSuite WMS (`572325`)
- Record bundle versions and install status.

### 3. Enable Features

- Enable `Pick, Pack, and Ship` under Transactions.
- Enable `Warehouse Management` under Items & Inventory.
- Save changes and log:
  - Date/time
  - User who changed settings

### 4. Limit Blast Radius

- Do not assign WMS roles to all warehouse users.
- Restrict trial to:
  - One pilot location
  - One small pilot user group

### 5. Minimal WMS Activation

- Enable system rule: `Enable Warehouse Management`.
- Assign only needed pilot roles:
  - `WMS Warehouse Manager`
  - `WMS Mobile Operator` (or inbound/outbound operator as needed)

### 6. Execute End-to-End Tests

- Outbound:
  - Create sales order
  - Pick
  - Pack
  - Ship
- Inbound (if in scope):
  - Receipt flow
  - Putaway/bin behavior
- Inventory controls:
  - Inventory status handling
  - Bin-based movement/selection
- Printing:
  - Labels/documents (if applicable)
- Exception:
  - Short pick or missing-bin scenario

### 7. Validate Results

- Verify transaction statuses are correct through full lifecycle.
- Verify non-pilot users can continue their normal sandbox flow.
- Verify no broken downstream dependencies (invoicing/integrations/reports in scope).

### 8. Exit Criteria

- No critical blockers.
- No data integrity issues.
- Pilot users complete full flow without manual workaround.

## Evidence to Capture

- Feature toggles enabled (with screenshots).
- System rules enabled (with screenshots).
- Roles assigned (who/which role).
- Records/forms changed.
- Test transaction IDs and outcomes.
- Defects found + resolution status.

## Production Replication Plan

### 1. Pre-Cutover

- Schedule low-traffic deployment window.
- Confirm sandbox checklist passed and evidence is complete.
- Confirm rollback owner and communication channel.

### 2. Cutover Steps

- Repeat only the exact changes validated in sandbox.
- Enable features/system rules in the same order used in sandbox.
- Start with:
  - One location
  - Pilot users only

### 3. Hypercare Monitoring

- Monitor first live orders end-to-end.
- Track:
  - Pick/pack/ship completion time
  - Error rates
  - User-reported blockers

### 4. Rollback Triggers

- Critical transaction failure
- Data inconsistency
- Repeated blocking user errors

### 5. Rollback Actions

- Remove pilot role assignments from non-essential users.
- Pause WMS process usage at pilot location.
- Revert to pre-defined fallback process for affected orders.

## Sign-Off Template

- Date:
- Environment:
- Change owner:
- Features enabled:
- System rules enabled:
- Pilot location:
- Pilot users:
- Test evidence links:
- Risks accepted:
- Go/No-Go:
