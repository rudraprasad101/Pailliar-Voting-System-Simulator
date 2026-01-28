# Secure E-Voting Platform (Demo)

This folder contains a self-contained front-end demo of a Paillier homomorphic e‑voting system.

> NOTE: This repository file (`version2.html`) is an educational demo only. It demonstrates homomorphic aggregation with Paillier-style operations but is not secure for real elections. See "Security Caveats" below.

## Contents
- `version2.html` — Single-file demo: HTML, CSS and JavaScript implementing a Paillier-like cryptosystem, simulated voters, encrypted ballots, homomorphic aggregation and decryption of final tallies.
- (Other files in the workspace belong to different modules of the project.)

## Features (what the demo shows)
- Generates a Paillier-style keypair (demo implementation).
- Allows manual voting (15 voters by default) or automated simulations (10 or 25 voters).
- Encrypts each ballot as a one-hot vector (one ciphertext per candidate).
- Aggregates ciphertexts homomorphically and decrypts the aggregates to get counts.
- UI with voter cards, progress bar, logs, results and a simple bar chart.
- Button to reveal public key parameters used in the demo.

## How to run (quick)
1. Open the file directly in a browser by double-clicking `version2.html`.
2. Or run a simple local server (recommended if you want console/network-friendly behavior):

PowerShell (Windows):

```powershell
Set-Location 'D:\Desktop\5th_sem_proj\CNS'
# If Python 3 is installed as `py`:
py -3 -m http.server 8000
# or if `python` is available:
python -m http.server 8000
# Then open in your browser:
# http://localhost:8000/version2.html
```

## Demo usage
- Quick Demo (10 Voters) / Full Demo (25 Voters): runs an automated simulation that casts votes at short intervals then auto-tallies.
- Manual Voting Mode: creates 15 voter cards; click candidate buttons to cast encrypted votes.
- Tally All Votes: becomes available after all registered voters have cast votes (or you can manually invoke it).

## Security caveats (important)
This is a demonstration and contains several insecure or simplified implementations:

- Prime generation is stubbed: the code picks small primes from a static array. Not secure.
- Randomness is produced with `Math.random()` and `Number(this.n)`, which is not cryptographically secure and not suitable for large BigInt keys.
- Conversions between BigInt and Number (`Number(m)`) may overflow or lose precision for large values.
- `hashBallot()` is a simple substring and not a real cryptographic hash.
- No authentication, signature, or tamper-evidence for voters or ballots — UI-level checks only.

Do NOT use this for any real voting system. Use established cryptographic libraries and audited protocols for production systems.

## Suggested improvements (if you want to harden the demo)
- Use secure prime generation and large primes (or rely on a vetted library implementing Paillier).
- Use the Web Crypto API (`crypto.getRandomValues`) for secure randomness.
- Avoid converting large BigInt to Number; preserve BigInt arithmetic for decryption results or use a bigint-friendly library.
- Replace `hashBallot()` with a real digest (SHA-256 via SubtleCrypto).
- Add digital signatures or authentication to prevent forged ballots.
- Move cryptographic operations server-side or use audited client libraries when appropriate.
- Add unit tests for encryption/decryption and homomorphic operations.

## Developer notes / internals
- Main class: `PaillierCryptosystem` (in `version2.html`) — contains `encrypt`, `decrypt`, `addEncrypted`, `multiplyEncrypted`, and key generation helpers.
- Voting flow: `createVoters()` -> `castVote()` stores `encryptedVotes` -> `tallyVotes()` homomorphically aggregates and decrypts.
- UI elements are created dynamically under `#votersGrid`, results shown in `#resultsGrid` and `#barChart`.

## License & attribution
This is a demo file for learning and experimentation. No license file is provided in this folder; if you incorporate this into a larger project, add your preferred license.

## Next steps (if you'd like me to proceed)
- Replace insecure prime/random generation with a safer implementation (I can add a library or use WebCrypto patterns).
- Extract the JS into modules and add unit tests for the crypto and tallying logic.
- Harden the demo to demonstrate a more realistic secure workflow.

If you want one of these, tell me which and I will implement it next.