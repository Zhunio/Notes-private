# 📝 SuiteScript 2.x Reference Cheat Sheet

---

## 1️⃣ User Event Script

**Runs on server, tied to record lifecycle**

| Entry Point  | Fires                    | Context                          | Purpose                               |
| ------------ | ------------------------ | -------------------------------- | ------------------------------------- |
| beforeLoad   | Before record form loads | `newRecord`, `form`, `type`      | UI changes, buttons, read-only fields |
| beforeSubmit | Before record save       | `newRecord`, `oldRecord`, `type` | Validation, defaults, block save      |
| afterSubmit  | After record save        | `newRecord.id`, `type`           | Create/update other records, emails   |

---

## 2️⃣ Client Script

**Runs in browser (UI only)**

| Entry Point   | Fires                          | Context                                 | Return/Notes                    |
| ------------- | ------------------------------ | --------------------------------------- | ------------------------------- |
| pageInit      | Page load                      | `currentRecord`, `mode`                 | —                               |
| fieldChanged  | Any field change               | `currentRecord`, `fieldId`, `sublistId` | —                               |
| postSourcing  | After field sourcing completes | `currentRecord`                         | —                               |
| validateField | Leaving a field                | `currentRecord`                         | `true` = allow, `false` = block |
| validateLine  | Adding a line to sublist       | `currentRecord`, `sublistId`            | `true` = allow, `false` = block |
| saveRecord    | Before record save             | `currentRecord`                         | `true` = allow, `false` = block |

---

## 3️⃣ Suitelet

**Custom UI + HTTP endpoint**

| Entry Point | Fires               | Context               | Purpose                       |
| ----------- | ------------------- | --------------------- | ----------------------------- |
| onRequest   | On HTTP GET or POST | `request`, `response` | Build forms, return HTML/JSON |

**Common Modules**: `N/ui/serverWidget`, `N/record`, `N/search`, `N/file`

---

## 4️⃣ Scheduled Script

**Background / batch jobs**

| Entry Point | Fires          | Context   | Purpose                        |
| ----------- | -------------- | --------- | ------------------------------ |
| execute     | When scheduled | `context` | Nightly jobs, batch processing |

---

## 5️⃣ Map/Reduce Script

**Mass data processing, scalable**

| Entry Point  | Fires                    | Context   | Purpose                                |
| ------------ | ------------------------ | --------- | -------------------------------------- |
| getInputData | Start, provide data      | —         | Return search, array, or dataset       |
| map          | Per input record         | `context` | Transform/process individual data      |
| reduce       | Per group of map outputs | `context` | Aggregate data, process group results  |
| summarize    | End of script            | `summary` | Log results, errors, governance checks |

---

## 6️⃣ RESTlet

**External API endpoint**

| Entry Point | HTTP Method | Context/Params  | Purpose     |
| ----------- | ----------- | --------------- | ----------- |
| get         | GET         | `requestParams` | Return data |
| post        | POST        | `requestBody`   | Create data |
| put         | PUT         | `requestBody`   | Update data |
| delete      | DELETE      | `requestParams` | Delete data |

---

## 7️⃣ Workflow Action Script

**Triggered by Workflows**

| Entry Point | Fires                  | Context   | Purpose               |
| ----------- | ---------------------- | --------- | --------------------- |
| onAction    | When workflow executes | `context` | Custom workflow logic |

---

## 8️⃣ Portlet Script

**Dashboard widget**

| Entry Point | Fires          | Context   | Purpose                    |
| ----------- | -------------- | --------- | -------------------------- |
| render      | Dashboard load | `context` | Show KPIs, charts, widgets |

---

## 9️⃣ Mass Update Script

**Triggered by Mass Update (UI)**

| Entry Point | Fires               | Context   | Purpose             |
| ----------- | ------------------- | --------- | ------------------- |
| each        | Per selected record | `context` | Bulk update records |

---

## 🔑 Notes / Tips

- **Only functions returned are executed**:

```javascript
return { beforeSubmit: beforeSubmit };
```
