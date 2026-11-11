# AokChain mainnet blocks

Pre-packed AokChain **mainnet blocks** for a fast first synchronisation.

> **Status:** test stage. The wallet feature that reads these files ships with AokChain Core 3.1.0, which is not released yet.

Download: **[Releases → mainnet](https://github.com/AokChain/mainnet-blocks/releases/tag/mainnet)**

## What this is
A freshly installed AokChain node has to fetch about three million blocks from other nodes. There are few peers, so this takes hours. This repository offers the same blocks, in height order, as compressed archives. A node reads its blocks from here instead of from peers.

- Blocks 1 to 3,031,432 (mainnet)
- 15 compressed files, 1.4 GB in total (2.1 GB uncompressed)
- `manifest.json` (file list and hashes), `SHA256SUMS`

## Do I have to trust these files?
No. That is the point of the design.

- The node **validates every block itself**, exactly as it does for blocks received from peers.
- A wrong or damaged file is rejected and the node falls back to the normal peer-to-peer sync.
- The archives only replace the download path. They cannot change balances or transactions.

## How to use
**AokChain Core 3.1.0 and later (upcoming)**

- Wallet (GUI): on a first start with a long way to sync, it downloads and validates the archives automatically. This can be skipped in the sync screen.
- To set the address yourself, put this into `aokchain.conf`:
  ```
  bootstrapurl=https://github.com/AokChain/mainnet-blocks/releases/download/mainnet/
  ```
- To use a folder downloaded beforehand (servers, offline machines, slow links):
  ```
  bootstrapdir=/path/to/downloaded/folder
  ```
  The folder must contain all files of the release as they are, including `manifest.json`.
- `bootstrap=0` turns it off.

Option names may still change before the 3.1.0 release.

**3.0.x** cannot read these files.

## Download and verify by hand
```
# after downloading all release files into one folder
sha256sum -c SHA256SUMS
```

## File format
- Each `blocks-<first>-<last>.dat.gz` is a gzip-compressed file in the `bootstrap.dat` format: for every block the 4 network magic bytes, a 4 byte little-endian length and the raw block, in height order.
- `manifest.json` holds the format version, the network, and per file the height range, sizes and SHA-256, plus the height and hash of the last block.
- The files are produced with `contrib/aokchain/make_bootstrap.py` from the AokChain Core source.

## Updates
As the chain grows, new files are appended and `manifest.json` and `SHA256SUMS` are replaced. Files already published are not changed. Blocks newer than the archives come from peers as usual.

## Files
| File | Block heights | Size |
|---|---|---|
| `blocks-00000001-00230000.dat.gz` | 1 – 230,000 | 190 MB |
| `blocks-00230001-00249999.dat.gz` | 230,001 – 249,999 | 20 MB |
| `blocks-00250000-00425249.dat.gz` | 250,000 – 425,249 | 190 MB |
| `blocks-00425250-00499999.dat.gz` | 425,250 – 499,999 | 48 MB |
| `blocks-00500000-00749999.dat.gz` | 500,000 – 749,999 | 114 MB |
| `blocks-00750000-00999999.dat.gz` | 750,000 – 999,999 | 182 MB |
| `blocks-01000000-01249999.dat.gz` | 1,000,000 – 1,249,999 | 71 MB |
| `blocks-01250000-01499999.dat.gz` | 1,250,000 – 1,499,999 | 70 MB |
| `blocks-01500000-01749999.dat.gz` | 1,500,000 – 1,749,999 | 79 MB |
| `blocks-01750000-01999999.dat.gz` | 1,750,000 – 1,999,999 | 89 MB |
| `blocks-02000000-02249999.dat.gz` | 2,000,000 – 2,249,999 | 102 MB |
| `blocks-02250000-02499999.dat.gz` | 2,250,000 – 2,499,999 | 101 MB |
| `blocks-02500000-02749999.dat.gz` | 2,500,000 – 2,749,999 | 77 MB |
| `blocks-02750000-02999999.dat.gz` | 2,750,000 – 2,999,999 | 68 MB |
| `blocks-03000000-03031432.dat.gz` | 3,000,000 – 3,031,432 | 8 MB |

---

The block data is the public AokChain blockchain. Text and tooling in this repository are released under the MIT license.
