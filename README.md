# AirBridge — Unified Freight Operations & Finance Prototype

**Purpose:** A working browser-based UI prototype for a freight forwarder that currently switches between cargo booking, airline airway-bill management, D-Solution logistics operations, and Refrens-style billing. This is an original interface integrating the *workflow concepts*, not the vendors' code or proprietary APIs.

## Open the demonstration

**Easiest:** Open `AirBridge_Standalone_Demo.html` (provided separately). This contains all HTML, CSS and JavaScript in one file and needs no build step.

**Editable source:** Open `index.html` with `style.css` and `app.js` in the same directory. Use a static HTTP host for the most consistent local-file behaviour.

**Navigation:** Overview → Shipments & Jobs → open any Job ID → use six tabs for shipment details, flight & AWB, airline documents, rates & costs, profit sharing, and billing. The left navigation contains the other business modules.

**Demo records:** Four example shipments and sample financial records are preloaded. They are fictional workflow examples (not real carrier inventory or invoicing data). For a clean starting point use **Settings & Audit → Reset sample data**. Records stay in your browser's local storage. Uploaded files use browser IndexedDB where available, with a session-only fallback if the browser blocks it. Uploaded files do **not** travel to an airline, a client or a server.

## Modules built in the demo

| Workspace module | Representative functioning interactions |
|---|---|
| Management Overview | Dashboard metrics, shipment statuses, overdue actions, links into jobs |
| Shipments & Jobs | Create jobs, Job ID, search by AWB/customer, change route/cargo/priority, assign owner/team, statuses, edit weights/dimensions |
| Airline Bookings & AWB | Record flight legs, booking status, MAWB/HAWB, allotment types, airway-bill declarations, screening status, handling codes |
| Airline Document Centre | Upload actual local files, category, per-job document checklist, versions, retrieve local file, prepare checklist and manifest |
| Sea Freight | Basic MBL/HBL/vessel/voyage/container/port/ETD/ETA register, linked to Job ID and document centre |
| Quotes & Tariffs | Add contract/spot/ad-hoc rates, create quotes, approve and convert quote to job |
| AWB Stock & Allocation | Add carrier serial ranges, track used/free numbers, allocate MAWB to a job |
| Invoicing & Receivables | Create tax invoices, proformas, quotations, credit/debit notes; item lines, HSN, GST, dues, payments, preview, browser PDF print, email draft |
| Accounts Payable | Record vendor bills, classify cost heads, link job, settle balances |
| Ledger & Bank | Illustrative journal generated from finance records; record cheques, payment register, overseas exchange view |
| Profit & Partner Sharing | Lane default and shipment-specific overrides, 40/30/20/10 style splits, company retained %, reporting period selector |
| Follow-ups | Task owner, due date, priority, notes, completion, invoice reminder log, calendar export |
| Reports | Customer/lane/airline/owner/month/branch grouping, financial metrics, ageing, unbilled jobs, partner allocation, export CSV/print PDF |
| Customers & Vendors | Shared lookup derived from operational records and manual party addition |
| Settings & Audit | Company/GST/bank defaults, reminder policy, role preview, local audit trail, data export/reset |

## Design distinction: upload instead of print AWB

The supplied SmartKargo screenshot included a **Print AWB** action. This prototype intentionally prioritises **Airline documentation pack → upload AWB / invoice / packing list / shipping bill / other attachments → per-job checklist → version history → download manifest**. It does not send anything to an airline. A production delivery method (email/API/e-AWB/ePouch approved by airline) must be agreed and integrated later.

## Implementation and integrity notes

- Data is browser-local with no database backend and no authentication. The role switch illustrates **intended** permission boundaries, not real server-side security.
- Invoices use **browser Print → Save as PDF**; this is a PDF workflow, not a server-generated or e-invoice compliant PDF engine.
- Email compose is a `mailto:` draft; payment reminder logs are simulated. No mail, SMS or WhatsApp is sent.
- Airline booking confirmation, capacity inventory, rates, AWB submission/e-AWB transmission, Customs, screening, Tally, GSTN, automated e-invoicing and payment processing **are not connected**.
- Local version metadata is maintained for replacement document filenames within a category. Production document storage needs secure object storage, immutable audit records and role checks.
- The financial journal is **illustrative only**. Multi-currency shipping profits use explicit INR FX rates. Posting, tax treatment, GST location rules, recognition timing and foreign exchange gains/losses require accounting specifications.
- The demo's profit share uses **positive gross profit** and unallocated profit remains with the company. Distributions on negative profits, timing of payouts, collection-based sharing, approvals and reversals must be clarified.
- CSV files open in Excel; a native XLSX export would be part of a backend or enhanced frontend version.
- The source is plain HTML/CSS/JavaScript and can be deployed to any static hosting provider. A fully deployed multi-user product needs an authenticated backend, SQL database, object storage, queue/scheduler, logs, tests, and integration adapters.

## Suggested production architecture

Frontend: React / Next.js with typed form validation, accessible component library and role-aware navigation. Backend: API server (Django / FastAPI or Node), PostgreSQL for jobs/finance/shares, encrypted object storage for AWB files, Redis jobs for notifications, durable event/audit log, RBAC with server-side enforcement. Use modular integration adapters for airline platforms, customs, GST, Tally, email, WhatsApp and other carriers.

## Launching on a public domain

Deploy this directory as a static project on a hosting service such as Vercel, Netlify, Cloudflare Pages or GitHub Pages. Publish the folder containing `index.html`, `style.css` and `app.js` (or upload the standalone HTML as `index.html`). Since the app has no backend, uploaded documents and local demo data will not sync across users. **Do not enter production or sensitive customer data.**

### GitHub Pages deployment

Live demo: https://jayyy560.github.io/airbridge-demo/

Repository: https://github.com/Jayyy560/airbridge-demo

GitHub Pages publishes the repository root from the `main` branch. No build step is required; `.nojekyll` keeps the files served directly. To update the deployed demo, commit and push changes from this directory to `main`.

## Reference material consulted

1. `Custom_Freight_Software_Requirements.pdf` — primary 10-section client requirements.
2. `360 Kargoscape - GSA Solution by Kargo360 Sep 2026.pdf` — GSA airline operations, quotation, booking, stock, e-pouch, revenue and finance concepts.
3. `DOC-20261014-WA0000.pdf` — specimen airway bill, metadata fields, declared values, chargeable weight and supporting documents.
4. Supplied screenshots — SmartKargo/AFCOM, D-Solution International Logistic Software and Refrens invoice screens.
5. Public manufacturer/product descriptions where available: SmartKargo official, Kargo360 official and Refrens official. The exact software identity called “Cargo Expert” could not be conclusively matched to a verified cargo software vendor; no unverified functionality was attributed to it.

**Disclaimer:** This original design is a proof-of-concept UX and workflow prototype, not a substitute for a regulated or audited cargo/finance system.
