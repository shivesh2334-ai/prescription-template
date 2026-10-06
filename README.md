# Prescription template pack — 6 October 2026

## Deployment (Vercel)

This repository is a static site, ready for zero-config deployment on Vercel:

- `index.html` — the printable/readable catalogue (site entry point).
- `data/prescription-templates.json`, `data/prescription-options.csv`, `data/validation-summary.json` — source data files.
- `vercel.json` — static deployment configuration (clean URLs).

To deploy: import this repository into Vercel (no build command or output directory needed; the project root is served as-is), or run `npx vercel` / `npx vercel --prod` from the repository root with the Vercel CLI.


This is a portable content catalogue for a clinician-facing prescription platform. It has not been installed in a repository or production platform. It contains all 39 diagnoses requested, preserves the user's serial numbering, and distinguishes 18A (AF with CVR) from 18B (PSVT).

## Files

- `prescription-templates.json`: authoritative normalized catalogue, medicine references, 39 templates, required inputs, selection groups, follow-up, merge rules and source links.
- `prescription-options.csv`: flat option/ingredient mapping for spreadsheet review or import mapping. Rows are alternatives or components of an option, NOT a list to prescribe together.
- `prescription-template-catalogue.html`: readable, printable catalogue with an index and linked references. Open in a browser; print to PDF if needed.
- `validation-summary.json`: structural checks run on this content pack.

## Import contract

Import sources and the medicine catalogue, then templates in the supplied order. All options have `selected:false`. Preserve `selection_mode`: `choose_one` means mutually exclusive alternatives; `select_compatible` requires compatibility review; `review_only` never emits an order. Each option's `medication_ids` is one regimen branch, which may contain several medicines. When the same medicine ID is chosen by multiple diagnosis templates, reconcile rather than add quantities/doses. `adult_reference_dose` is information for the clinician, not a value to populate an order. `prescription_values` is intentionally blank. Hospital/emergency drug suggestions must remain behind a setting-aware workflow.

Before signing, fill dose, units, route, frequency in plain language, timing, duration or ongoing status, quantity, product identity and follow-up. Brand selection comes from the platform's verified local formulary. Expand fixed combinations into component strengths and cumulative ingredient doses. Chronic supply length is distinct from treatment duration. The curated rules are descriptive integration requirements, not an executable complete contraindication or interaction engine.

## Clinical review decisions

Adult examples assume that patient-specific eligibility, allergy, pregnancy/lactation, organ function and interacting medicines have been reviewed. Indian local product approval and antimicrobial susceptibility remain necessary. No paediatric extrapolation. Acute bronchitis/viral URI do not have default antibiotics. Bacterial URI requires a syndrome. CAP duration follows stability/severity; the 2025 ATS update permits shorter courses in selected stable nonsevere cases. HAP is a hospital/antibiogram workflow.

Hypertension 21/22 explicitly uses ACC/AHA 2025 stage definitions. The requested stage 3/4 entries remain classification/triage workflows, rather than invented additional ACC/AHA stages. Grade 3 thresholds are shown only under explicitly selected traditional ESH classification. Peripartum care requires obstetric context. CHF requires EF phenotyping. Post-PCI antithrombotics require ACS/elective indication and bleeding/OAC context, not time since PCI alone.

Diabetes counts describe selectable regimen branches and medication review, not a mandate to add drugs. Four-agent regimens require justification and five-agent therapy is a specialist reconciliation workflow. Insulin doses are deliberately blank. Individual initiation/titration plans, concentration/device, meals, monitoring and hypoglycaemia rescue are required. Ryzodeg and Mixtard are different products and are not silently substituted.

Samples informed layout and familiar choices only. No names, MRNs, visit IDs, phone numbers or copied patient-specific dose bundles are retained. Ambiguous or inconsistent sample brand/formulation fields were not imported as established mappings.

## Review status

Sources were checked on 6 October 2026. Clinical recommendations and labels are linked in the JSON and HTML. This is a draft clinical content pack requiring local clinical/formulary validation before production; it has structural validation but no prospective clinical validation or live prescribing-platform test.
