# IMEI Check

A lightweight, offline IMEI checker that runs entirely in your browser. No install, no server, no account — nothing you paste leaves your machine.

## What it does

Paste one IMEI per line (dashes, spaces and dots are ignored) and each number is checked as you type:

| Input | Result |
| --- | --- |
| 15 digits | Validates the Luhn check digit. If it is wrong, shows the corrected number. |
| 14 digits | Computes the missing check digit and shows the full IMEI. |
| 16 digits | Treated as an IMEISV; the software version is split off and the equivalent IMEI is shown. |

For every well-formed number it also shows:

- **TAC and serial** — the 8-digit Type Allocation Code and the 6-digit serial.
- **Make / model** — looked up from the TAC in the bundled database.
- **Allocated by** — the reporting body identified by the first two digits.
- **Placeholder warning** — numbers such as all zeros that pass the checksum but are not real device identities.

A summary shows how many numbers are valid, and **Copy as CSV** puts the results on the clipboard (`input, status, tac, serial, make, model, note`).

## What it does not do

It cannot tell you whether a phone is **blacklisted, stolen or carrier-locked**. That information only exists in paid provider databases and is not part of this tool.

Make and model coverage is limited. The bundled database is community-collected, dates from around 2016 and is thin on recent phones, so newer devices will often show "Not in database".

## Usage

🖼️ **[View the Live Website](https://wv-web-developers.github.io/imei-check/)**

Download or clone the repository and open `index.html` in any modern browser. Keep `tacdb.js` in the same folder — without it the tool still works, but make and model are not shown.

To find a phone's IMEI, dial `*#06#`.

If you prefer to serve it locally:

```bash
python -m http.server 8765
```

Then open `http://localhost:8765`.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole tool: markup, styles and logic. |
| `tacdb.js` | TAC to make/model lookup table (about 650 KB, 22,524 entries). |

## Licence

The code (`index.html`) is released under the [MIT License](LICENSE).

The data is licensed separately: `tacdb.js` is derived from the [Osmocom TAC database](http://tacdb.osmocom.org/), © Harald Welte 2016, licensed under [CC-BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/). If you redistribute it, keep the attribution and share any changes to the data under the same licence.
