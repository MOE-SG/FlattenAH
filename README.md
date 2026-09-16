# FlattenAH

Flatten Airhang (QADR / COMRES) HTML reports into a CSV file that opens directly in Excel. One row is produced per report.

## Use

1. Open `index.html` in a modern browser.
2. Drop one or more `.htm`/`.html` Airhang reports onto the page, or click to browse. Files are queued in a list - remove any you don't want with the **✕** button next to it.
3. Select **Process files** to flatten every queued report.
4. Review the **Flattened data preview** table, then select **Download CSV**. A dialog suggests a filename, which you can edit before saving.
5. Use **Clear all** to reset and start over with a new batch.

The parser runs entirely in the browser - report contents are never uploaded anywhere.

## Options

- **Include empty / na values** - when unchecked, a column is dropped from the output only if it is empty (or `na`) across *every* processed file.
- **Transpose (fields as rows)** - ticked by default. Shows the preview with fields down the left and one column per file, which is easier to scan when there are many fields but only a few files. Untick to see files as rows and fields as columns instead. This only affects the on-screen preview; the downloaded CSV always uses files-as-rows.

## Format checks

QADR and COMRES reports share the same underlying Airhang report format and can be indistinguishable by filename alone, so this tool treats them as one family for naming purposes. ResiStar reports use a different, unsupported report structure.

A warning banner appears above the file list whenever:
- A queued file's name doesn't contain "Airhang" (worth double-checking it's actually a QADR/COMRES report).
- A queued file's name contains "ResiStar" (a different format this tool doesn't parse).
- The current batch mixes more than one detected format, since flattening them together won't produce consistent rows.

These are warnings, not hard blocks - files can still be processed regardless.

## Output filename

Downloads default to:

```
yymmdd-hhmmss-key-product-flattenAH.csv
```

- `yymmdd-hhmmss` - the date and time the CSV was saved.
- `key` - for a single file, the report's own Tool ID (read from inside the HTML, not the filename). For multiple files, this is replaced with the file count (e.g. `3files`).
- `product` - `ADR` for Airhang-format (QADR/COMRES) files, `ResiStar` for ResiStar-named files. If a batch mixes both, both are listed (e.g. `ADR+ResiStar`).

You can freely rename the suggested filename in the save dialog before confirming - nothing is saved until you do.
