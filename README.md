# Overview
The intent of this repo is to validate an approach for Kaspa block/transaction analysis.

# Included Data Sets
To help produce consistent results, this repo includes two data sets.

### `blocks-<date>.json`
A snapshot of blocks (including transactions). This file was created using `save_blocks.ipynb`.
- from block 959c77c5fbf3cdeb0b1f730041a06ac02cf4086711fe648e6866faa7ef4c88bd (December 12, 2023 14:25:48.666) 
- to block 7ca2f4224dfd2260ee21c81506e0fe056f14c38f0f9b3296c1e00573e529ff6e (December 14, 2023 18:50:21.968)

### `spent-outputs.json`
Output data (tx_id, index, address, amount) for outputs spent in blocks in `blocks.json`. Included so we can analyze tx inputs.

# Steps to Run
**To analyze the included data set:**
1. Unzip all `blocks-<date>.json.gz` files and `spent-outputs.json.gz`
1. Run `main.ipynb`


**To analyze a newer data set:**
1. Run `save_blocks.ipynb` to produce a new `blocks.json` file. The new file will include blocks from the current pruning point to selected tip.
2. Figure out how you want to handle spent outputs:
   - Optionally, you can try to get all spent outputs from some data source like api.kaspa.org. Though rate limits exist and this will take some time.  
   - This data is not required though, `SPENT_OUTPUTS` variable can be set to `False` in `main.ipynb`. This will cause the analysis code in `main.ipynb` to ignore inputs.

# Thank You
A thank you to IameR1 for the [kaspa-db-filler](https://github.com/lAmeR1/kaspa-db-filler/tree/main). It provided the general approach used here, as well as the gRPC client code.