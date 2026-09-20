# Synthetic interactive estimate calculator

AI-created portfolio demonstration, not client work. All bicycle services and prices are fictional. This is one self-contained HTML file with CSS and JavaScript, no external dependencies, account, backend, booking or payment flow. It requests no personal information and includes no application network requests or storage.

## Try the sample

Download `estimate-calculator.html` from the public portfolio and open it in a modern browser. GitHub's file view shows source rather than executing the page. The local authoring file is `index.html`. Direct file opening is intended but was not independently browser-tested: the automation browser's URL policy blocked file URLs. Chrome UI verification used a local HTTP preview instead; no bypass was attempted.

Select quantities from 0 to 5 for four fictional services: basic tune-up $45, chain clean $15, tire fitting $20, brake adjustment $25. Calculation uses integer cents. Invalid, empty, fractional or out-of-range values suppress the total and disable printing. Reset clears both quantities and the displayed estimate.

## Verified on September 20, 2026

- Chrome UI: one tune-up plus one chain clean produces $60 with two itemized rows.
- Chrome UI: two tune-ups plus three tire fittings produce $150.
- Maximum quantities (five of each service) produce $525, with line amounts $225, $75, $100 and $125.
- Inputs `-1`, `1.5`, `6` and blank show the validation message, suppress the total and disable Print.
- Reset from a nonzero estimate returns $0, shows the empty-state message and disables Print. An initial reset timing defect was found and corrected before publication.
- Keyboard ArrowUp on the tune-up quantity increases the estimate by $45.
- Desktop and narrow-screen layouts were visually inspected. At the narrow viewport, document client width and scroll width were both 375 CSS pixels, with no horizontal overflow.
- Source was inspected for external dependencies, requests and storage; none are included. JavaScript syntax was checked with Node.

The print stylesheet and browser Print control are included, but the print dialog, PDF export and physical printing were not verified. No screen-reader audit, comprehensive accessibility certification or cross-browser guarantee is claimed. This is a small example, not a production quotation or tax engine.

## Cover

`estimate-preview.png` is an illustrative code-rendered cover showing fictional $45 + $15 = $60 line items. It is explicitly labeled as a schematic, not a browser screenshot. The local authoring cover is `cover.png`.
