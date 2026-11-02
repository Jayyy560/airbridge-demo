# Client requirement traceability — 2026-11-02

Legend: **Demo functional** = local UI interactions and calculations work in this browser. **Demo representation** = flow is visible but has no automated external action, secure backend or production guarantee. **Build phase** = needs production engineering, vendor approval or integrations.

The client document (three pages, ten numbered sections) takes precedence over feature assumptions derived from third-party screenshots.

| No. | Client requirement | Demo location / interaction | Coverage |
|---:|---|---|---|
| 1 | Unique shipment/job ID | New shipment creates a Job ID and linked records | Demo functional |
| 1 | Customer, shipper, consignee, origin, destination, airline/agent | Shipment details | Demo functional |
| 1 | MAWB/HAWB, flight, pieces, weight, dimensions, commodity and notes | Shipment details and Flight & AWB | Demo functional |
| 1 | Upload and store per-shipment AWB/supporting docs | Airline documents / Document centre | Demo functional locally |
| 1 | Search Job ID, AWB, HAWB, customer | Job register / global search | Demo functional |
| 1 | Multiple assigned people and status/pending actions | Shipment collaborators, assigned owner and linked follow-up tasks | Demo functional locally |
| 2 | Enter selling revenue and individual cost heads | Shipment Rates & costs | Demo functional |
| 2 | Profit, margin and total costs automatically calculated | Live profitability panel | Demo functional |
| 2 | Freight, handling, documentation, transport, agent, customs, other | Cost head grid | Demo functional |
| 2 | Multiple currencies and exchange rates | Revenue currency/FX plus per-cost-head currency/FX to INR | Demo functional |
| 2 | Profit by shipment/customer/lane/airline/salesperson/period | Reports, shipment and partner views | Demo functional |
| 3 | Multiple people on one lane/project | Profit & Partner Sharing | Demo functional |
| 3 | Configurable split e.g. 40/30/20/10 | Create/edit rule | Demo functional |
| 3 | Per-lane/project split and authorised shipment override | Default vs shipment scope, management role demo | Demo functional / demo role only |
| 3 | Each share amount and remaining company profit | Distribution tables | Demo functional |
| 3 | Monthly/quarterly/yearly partner reports | Reporting period and partner summary | Demo functional local calculation |
| 3 | Secure authorisation and financial approval history | Role switch and audit event | Demo representation — secure controls build phase |
| 4 | Quotation, proforma, invoice, credit/debit notes | Quote register and invoice editor type picker | Demo functional |
| 4 | Link invoice to customer and shipment | Invoice Job ID & customer selectors | Demo functional |
| 4 | Configurable numbering, tax/GST, bank, company details and terms | Invoice lines + settings + notes | Demo functional; compliance verification build phase |
| 4 | Professional PDF download | Invoice preview → browser Print → Save as PDF | Demo functional via browser |
| 4 | Direct email sending | Prepare draft in local mail app | Demo representation; sending build phase |
| 5 | Store payment reminder recipient emails | Invoice editor | Demo functional |
| 5 | Automatic emails before/on/after due until paid | Settings + reminder queue | Demo representation; scheduler/email build phase |
| 5 | Part payment updates outstanding balance | Record payment and invoice balance | Demo functional |
| 5 | Stop reminder when paid in full | Reminder action blocked for settled invoices | Demo functional locally |
| 5 | Maintain reminder history | Invoice preview simulated reminder log | Demo functional locally; actual sends build phase |
| 6 | Assigned follow-ups with due date, priority, notes | Follow-ups & Reminders | Demo functional |
| 6 | Automated reminders to team members | Due/overdue dashboard and calendar export | Demo representation; push/email build phase |
| 6 | Today / upcoming / overdue views | Follow-ups KPI | Demo functional |
| 6 | Management visibility of responsible person | Dashboard and tasks table | Demo functional |
| 7 | AWB copies stored per shipment | Airline documents | Demo functional locally |
| 7 | MAWB, HAWB, invoice, packing list, shipping bill, POD, rate confirmation, credit/debit note | Upload category picker | Demo functional locally |
| 7 | Search/access files from job | Job document tab / document centre | Demo functional |
| 7 | Appropriate document permissions by role | Role preview | Demo representation — production RBAC build phase |
| 7 | Document version history | Same filename/category uploaded again increments version | Demo functional locally |
| 8 | Revenue, counts/status, profit/margin, customers, lanes, partner allocation | Overview, Reports and Profit Sharing | Demo functional |
| 8 | Outstanding & overdue, payment ageing, follow-ups | Receivables and Reports | Demo functional |
| 8 | Unbilled and financially incomplete shipments | Reports: unbilled section | Demo functional (unbilled) / partial (completeness) |
| 8 | Excel/PDF export | CSV for Excel, Print-to-PDF | Demo functional; native XLSX build phase |
| 9 | Roles management/sales/operations/docs/finance | Top role switch | Demo representation |
| 9 | Restrict sensitive cost, profit and partner data | Limited views for selected role | Demo representation; server-side enforcement build phase |
| 9 | Audit trail on finance and sharing changes | Settings > Audit log | Demo functional locally; immutable log build phase |
| 9 | Management business visibility | Overview and reports | Demo functional |
| 10 | Additional branches/users/customers/lanes/projects | Sample branch selection, parties and extensible data records | Partial UI; administration build phase |
| 10 | Integration options Tally, GST/e-invoice, WhatsApp/email, logistics APIs | Architecture and design notes | Build phase (intentionally disconnected) |
| 10 | Transparent one-time fees, hosting, AMC and customization rates | Requires separate commercial proposal | Not a software UI feature; no invented rates |
| 10 | Data access, ownership and full export | Settings > Export demo data JSON / CSV reports | Demo functional for structured records; stored binary files individually downloaded |

## Other screens referenced (not all mandated by the client requirements)

| Source | Workflow concepts brought into UI | What is deliberately not represented as real |
|---|---|---|
| SmartKargo/AFCOM images | Booking consignment, route/date, screening, ad-hoc charges, MAWB/HAWB and airline document handoff | Live carrier booking/rate confirmation, airline stock, AWB issuance and actual API submission |
| D-Solution screenshots | Rate centre, quotations, air documents, sea documents, receivables/payables, bank cheque register, overseas FX view, journal view | Complete Tally-grade bookkeeping and live freight/sea compliance integrations |
| Refrens screenshots | Invoice editor, line items, HSN/GST, payable bank settings, totals, email draft and reminder UI | GST validation, e-invoice IRN, real online payment links, true automation |
| Kargo360 PDF | GSA quotation/booking, AWB stock, airline document e-pouch, dashboards, revenue controls, allotments | GSA-to-airline integrations, schedule/capacity engines, AI predictive insight, e-AWB protocols |
| Etihad AWB specimen | Shipper/consignee, origin/destination, airway bill numbers, chargeable weight, declared values, freight terms, handling codes | Reproduction of carrier-owned legally binding AWB template, e-signatures, customs transmission |

## Important questions before production

1. Is the company acting as a forwarder, a GSA for one/multiple airlines, or both, and which station/airline integrations are actually contractually available?
2. Should partner profit share be based on invoiced profit, accrued profit, collected profit or realised profit after vendor settlement? How are losses and adjustments handled?
3. Which GST treatment, place-of-supply rules, export exemptions and e-invoice thresholds apply to each client and service?
4. What documents are airline-mandatory by carrier, lane and cargo type, and should airline submission use portal API, email, SFTP or manual pack download?
5. What is the target hierarchy for organisation, multi-branch access, user approval limits and data retention, and who owns/controls the production host and data export?
