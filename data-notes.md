# JSON to CSV transformation sample

This AI-created synthetic example contains fictional product records. It demonstrates a small output-only data transformation, not customer work, sales results or a testimonial.

## Files

- `source.json`: eight original records, including deliberate data-quality cases.
- `cleaned.csv`: five retained records with normalized text and explicit quantity status.
- `exceptions.csv`: two records requiring a source decision, including each unchanged original record as JSON.

The product name `=SUM(1,1)` is deliberately fictional test text. It is not intended to run as a spreadsheet formula.

## Rules applied

1. Number source records from 1 in their original order. Keep these positions in both output files.
2. Remove only an exact repeated JSON record, comparing every field and preserving value types and whitespace. Source record **5** exactly matches record **1** and is removed. No other duplicate rule is applied.
3. Preserve each SKU as its original five-character digit string, including leading zeroes. Do not infer or renumber identifiers.
4. Trim surrounding whitespace, collapse internal whitespace, and use title case for ordinary product names and categories. The formula-like test name retains its original case, with one leading apostrophe added for safe text handling. `product_name_escaped=true` records that change.
5. A quantity may be a nonnegative JSON integer or `null`. Preserve **zero as `0` with status `known`**. Preserve **null as an empty CSV field with status `missing`**. Missing quantity is allowed in the cleaned output, remains explicitly unresolved, and is never replaced by zero.
6. Unit prices must be strings with a decimal point and exactly two decimal places, such as `12.50`. Preserve numeric zero as `0.00`. Do not interpret a comma as either a decimal mark or a thousands separator.
7. Route invalid or ambiguous records entirely to exceptions. Record **6**, SKU `00105`, has quantity `ten`; record **7**, SKU `00106`, has price `1,299`. Both need confirmation. Neither is included in the cleaned output.
8. Write UTF-8 CSV with a header, quoted fields, and CRLF line endings. Quote embedded commas and JSON correctly. Preserve originals in `source.json`.

## Reconciliation and checks

**8 source records = 5 cleaned + 2 exceptions + 1 exact duplicate removed.** The sets of source positions are disjoint and cover all eight records. The cleaned records are positions 1, 2, 3, 4 and 8. Exceptions are positions 6 and 7. Position 5 is the duplicate.

The five retained SKUs are `00101`, `00102`, `00103`, `00104`, and `00107`. Four quantities are known and sum to 17. One quantity is missing, so 17 is a known-quantity subtotal, not a complete inventory count.

Both exported CSV files were read back with an independent CSV parse and checked against the original JSON. Checks covered record counts, source coverage, the exact duplicate, original exception payloads, leading-zero SKUs, zero versus missing quantity, zero price, quoted commas, and neutralization of the one formula-like name. The source value `=SUM(1,1)` becomes the literal output text `'=SUM(1,1)`; no expression is evaluated.

## Opening the CSV

CSV stores text fields but cannot enforce spreadsheet cell types. The SKU strings are preserved in the file. **Import the SKU and product-name columns as Text** in a spreadsheet application to avoid automatic type conversion; quoting alone does not prevent a viewer from stripping leading zeroes. Depending on the importer, the defensive leading apostrophe may remain visible. It is recorded explicitly rather than silently discarded.

The sample was validated as CSV data. Native Excel or Google Sheets import behavior was not tested, and no workbook is included. For actual client work, agree the schema, duplicate definition, null policy, date/number conventions, and expected output before transformation. Do not infer ambiguous values.

Public sample files are `source.json`, `cleaned.csv`, `exceptions.csv`, and this README. Internal builder code is not part of the output-only service or portfolio publication set.
