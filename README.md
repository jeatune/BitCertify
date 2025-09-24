# BitCertify 📜

## Bitcoin-Native Academic Credential Verification Platform

BitCertify is a decentralized academic credential verification system built on **Stacks**, leveraging **Bitcoin’s security and immutability**. It enables educational institutions to issue tamper-proof digital certificates while maintaining **full transparency, verifiability, and decentralization**.

---

## 🚀 Features

* **Decentralized Institution Registry**

  * Stake-based institution onboarding
  * Multi-signature and delegate-based authority management
  * Suspension and reputation tracking

* **Tamper-Proof Credential Management**

  * Single and batch issuance of digital credentials
  * Expiry and revocation handling
  * On-chain storage of metadata references

* **Reputation & Endorsement System**

  * Weighted endorsements with comments and categories
  * Institutional reputation growth through endorsements
  * Extended endorsement details for transparency

* **Transferable Credentials**

  * Secure ownership transfers (e.g., student → employer)
  * Pending/approved transfer states
  * Expiry enforcement on transfer requests

* **Enterprise-Scale Capabilities**

  * Batch credential issuance (up to 50 per transaction)
  * Delegate authority with custom permissions
  * Reputation-based governance

---

## 🏗️ Smart Contract Overview

### Constants

* `MINIMUM-STAKE` – Required STX stake for institution registration
* `MAX-BATCH-SIZE` – Maximum credentials per batch issuance

### Core Data Maps

* **institutions** – Registered schools/universities with stake, reputation, and status
* **credentials** – Issued credentials linked to students with metadata & expiry
* **endorsements** – Endorsements with weight, comment, and type
* **institution-delegates** – Delegate assignments with permissions & expiry
* **transfer-requests** – Credential ownership transfer requests

---

## 🔑 Key Functions

### Institution Management

* `register-institution (name)` → Register a new institution (stake required)
* `add-delegate (delegate permissions expiry)` → Assign delegate with permissions

### Credential Management

* `issue-credential (...)` → Issue a single credential
* `batch-issue-credentials (...)` → Issue up to 50 credentials in one transaction

### Endorsements

* `endorse-credential-extended (...)` → Endorse a credential with weight, comment & type

### Transfers

* `request-credential-transfer (...)` → Initiate a credential transfer request

### Read-Only Queries

* `get-institution-info (institution)`
* `get-credential-info (id student)`
* `get-endorsement-info (id endorser)`
* `get-delegate-info (institution delegate)`
* `is-credential-valid (id student)`
* `get-validation-level (id student)`

---

## ⚠️ Error Codes

| Code   | Meaning               |
| ------ | --------------------- |
| `u100` | Not authorized        |
| `u101` | Already registered    |
| `u102` | Insufficient stake    |
| `u103` | Credential not found  |
| `u104` | Already verified      |
| `u105` | Invalid status        |
| `u106` | Credential expired    |
| `u107` | Batch issuance failed |
| `u108` | Transfer failed       |
| `u109` | Invalid batch size    |
| `u110` | Invalid delegation    |
| `u111` | Already endorsed      |
| `u112` | Invalid expiry        |
| `u113` | Invalid input         |
| `u120` | Empty string input    |

---

## 🔒 Security Considerations

* Institutions must stake `MINIMUM-STAKE` STX to prevent spam registrations
* Delegation requires explicit expiry dates to avoid indefinite privileges
* Transfers are **time-bound** with expiry enforcement
* All inputs validated (non-empty strings, expiry dates, weight ranges, etc.)
* Batch issuance includes size and input consistency checks

---

## 🛠️ Deployment

1. Ensure you have a Stacks environment set up (`clarinet` or `stacks-cli`)
2. Clone the repository and enter project directory
3. Deploy using:

```bash
clarinet contract deploy bitcertify
```

4. Interact with contract functions using Clarinet console or a frontend client

---

## 📌 Example Usage

### Register Institution

```clarity
(contract-call? .bitcertify register-institution "University of Bitcoin")
```

### Issue Credential

```clarity
(contract-call? .bitcertify issue-credential "BSC-2025-001" 'SP123... "B.Sc. Computer Science" u2025 "ipfs://metadata-hash" u120000 "Undergraduate")
```

### Endorse Credential

```clarity
(contract-call? .bitcertify endorse-credential-extended "BSC-2025-001" 'SP123... u10 "Verified by peer institution" "University")
```

---

## 📖 License

MIT License. Free to use, modify, and distribute under open-source terms.
