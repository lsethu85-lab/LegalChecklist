# Property Legal Checklist — Tamil Nadu Title Verification

A browser-based Tamil Nadu property due-diligence tool for comparing key land/property documents such as Sale Deed, Encumbrance Certificate, Patta/Chitta, Mother Deed, FMB Sketch, Layout Approval, and Seller ID.

The tool helps identify potential mismatches in owner name, survey number, extent, land classification, encumbrances, layout approval, and chain of title.

> ⚠️ Disclaimer: This tool is for preliminary screening only. It is not a legal opinion, certified translation, or government verification. Always verify documents with a licensed property lawyer, surveyor, and official Tamil Nadu e-Services / SRO records.

---

## Features

### Document Intake

Upload or drag-and-drop documents directly in the browser:

- Encumbrance Certificate, preferably 30+ years
- Patta / Chitta
- Current Sale Deed / Title Deed
- Mother / Parent Deed
- FMB Sketch
- Layout Approval, DTCP / CMDA
- Seller ID

Supported upload types include:

```text
PDF, JPG, JPEG, PNG, WEBP, TXT, HTML
```

---

## Cross-Comparison Matrix

The tool compares key fields across:

```text
Sale Deed ↔ EC ↔ Patta / Chitta
```

Compared parameters include:

- Owner Name
- Survey / Sub-division Number
- Total Extent / Area
- Boundaries

---

## Owner Name Matching Logic

The tool supports common Tamil Nadu document name variations.

Example:

```text
Sale Deed: L. Sethuraman
EC:        L. சேதுராமன்
Patta:     சேதுராமன்
Father:   லட்சுமிநாராயணன்
```

The tool can treat the above as a match because:

- `Sethuraman` and `சேதுராமன்` refer to the same core name
- `L` is derived from father name `லட்சுமிநாராயணன்`
- Address fragments like `at No. 74` are removed from Sale Deed owner extraction
- Punctuation and spacing are normalized

Examples handled:

```text
L. Sethuraman
L Sethuraman
L.Sethuraman
L. சேதுராமன்
சேதுராமன், Father: லட்சுமிநாராயணன்
```

---

## Survey Number Matching

The tool normalizes survey and sub-division numbers.

Example:

```text
472/23
472 23
Survey No. 472/23
```

The Patta OCR issue where `472 23` could be incorrectly interpreted as `4722/3` is handled by normalization logic.

---

## Extent / Area Comparison

The tool attempts to compare property extent across documents using approximate square-feet conversion.

Supported units include:

```text
sq.ft
sft
square feet
acre
cent
hectare
ares
சதுரடி
ச.அடி
```

Example:

```text
Sale Deed: 0 acre and 6.2 cents
EC:        2713 sq.ft
Patta:     0-2.50 hectare/ares approx
```

The tool flags mismatches when calculated values exceed the tolerance range.

---

## Encumbrance Detection

The tool checks EC text for possible encumbrance-related terms such as:

```text
Mortgage
Simple Mortgage
Equitable Mortgage
Attachment
Lis Pendens
Court Order
Release
Receipt
Discharge
Cancellation
```

If mortgage entries and release entries are detected, the tool flags them for manual verification.

---

## Land Classification Check

The Patta / Chitta text is scanned for land classification terms such as:

```text
Natham
Punjai
Nanjai
Poramboke
Anadheenam
```

General risk classification:

```text
Natham / Punjai         → usually safer for residential verification
Nanjai                  → restricted / conversion may be required
Poramboke / Anadheenam  → high-risk / government or unassigned land
```

Always verify classification with the Revenue Department.

---

## Scenario Modes

The tool supports two verification scenarios.

### 1. Planning to Purchase

Focuses on fraud prevention before payment:

- 30-year EC chain
- Layout approval status
- Land classification
- Encumbrance checks
- TN e-Services lookup

### 2. Already Purchased

Focuses on title maintenance:

- Fresh EC after registration
- Patta mutation status
- Rectification deed requirements
- Annual EC renewal reminder

---

## Generated Report

The tool can generate a structured report containing:

- Property master details
- Owner comparison
- Survey number comparison
- Extent comparison
- Encumbrance details
- Chain-of-title findings
- Missing document checklist
- Scenario-based action plan

---

## How to Use

### Option 1: Open Locally

Clone or download this repository.

```bash
git clone https://github.com/YOUR-USERNAME/property-legal-checklist.git
cd property-legal-checklist
```

Open the file in a browser:

```bash
index.html
```

No backend server is required.

---

### Option 2: Use with VS Code Live Server

Install the Live Server extension in VS Code, then right-click:

```text
index.html → Open with Live Server
```

---

## File Structure

```text
property-legal-checklist/
│
├── index.html
├── README.md
└── screenshots/
    └── cross-comparison-matrix.png
```

---

## Suggested Screenshot

Add a screenshot of the app here:

```markdown
![Cross-comparison matrix](screenshots/cross-comparison-matrix.png)
```

---

## Browser Compatibility

Recommended browsers:

- Microsoft Edge
- Google Chrome
- Mozilla Firefox

PDF text extraction depends on browser support and the availability of embedded text inside PDFs. Scanned PDFs may require OCR before upload.

---

## Important Limitations

This tool cannot guarantee legal correctness.

Manual verification is still required for:

- Original registered Sale Deed
- SRO Encumbrance Certificate
- Patta / Chitta from official TN e-Services
- FMB Sketch
- Layout Approval from DTCP / CMDA
- Court cases, attachments, lis pendens
- Boundary and physical survey verification
- Revenue classification and land-use restrictions

---

## Recommended Legal Workflow

Before purchasing a property in Tamil Nadu:

1. Get a 30-year EC from the SRO.
2. Verify current owner in Sale Deed, EC, and Patta.
3. Confirm survey number and sub-division number.
4. Cross-check extent in Sale Deed, EC, Patta, and FMB.
5. Verify layout approval with DTCP / CMDA.
6. Check land classification.
7. Confirm there are no unreleased mortgages or court attachments.
8. Ask a licensed property lawyer to review all documents.
9. Conduct a physical survey with FMB sketch.
10. Verify latest Patta and EC immediately before registration.

---

## Name Matching Examples

### Match

```text
Sale Deed: L. Sethuraman
EC:        L. சேதுராமன்
Patta:     சேதுராமன்
Father:   லட்சுமிநாராயணன்
```

Reason:

```text
Core name matches.
Father name supports initial L.
```

---

### Partial Match

```text
Sale Deed: L. Sethuraman
Patta:     Sethuraman
Father:   Not available
```

Reason:

```text
Core name matches, but initial proof is missing.
```

---

### Mismatch

```text
Sale Deed: L. Sethuraman
Patta:     R. Sethuraman
Father:   Ramasamy
```

Reason:

```text
Initial and father name do not support the same identity.
```

---

## Roadmap

Planned improvements:

- Better OCR support for scanned Tamil PDFs
- Export report as PDF
- Export report as Word document
- Confidence score for name matching
- Manual override for verified matches
- Side-by-side document evidence viewer
- Separate mismatch, partial match, and confirmed match categories
- Better Tamil-English transliteration dictionary
- FMB boundary comparison support

---

## Tech Stack

This is a single-page browser app built with:

- HTML
- CSS
- JavaScript
- PDF.js for browser PDF text extraction

No backend server is required.

---

## Privacy

All document processing is intended to happen in the browser.

If using this project locally, uploaded files are not sent to a backend server by this app. However, always review the code and hosting platform before uploading sensitive legal documents.

---

## Legal Disclaimer

This project is a document screening helper only.

It does not replace:

- Licensed advocate legal opinion
- Certified land survey
- SRO verification
- Revenue Department verification
- DTCP / CMDA approval verification
- Court case search

Use this tool only as an initial checklist and comparison assistant.

---

## License

Specify your preferred license.

Example:

```text
MIT License
```

---

## Author

Created by Sethu Lakshminarayanan.

For Tamil Nadu property document pre-screening and title verification support.
