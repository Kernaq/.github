<div align="center">
  <h1>Kernaq</h1>
  <p><strong>Identity verification infrastructure for Africa.</strong></p>
  <p>
    Document OCR · Face matching · Liveness detection · Full KYC pipeline<br>
    One API call. Synchronous results. Nothing stored after processing.
  </p>
  <p>
    <a href="https://kernaq.com">kernaq.com</a> ·
    <a href="https://documentation.kernaq.com/identity">Docs</a> ·
    <a href="https://kernaq.com/dashboard">Dashboard</a>
  </p>
</div>

---

## What we build

Kernaq provides a KYC API purpose-built for East African financial services — banks, fintechs, SACCOs, payroll platforms, and healthcare providers. The pipeline runs document OCR, face matching, and liveness detection in a single synchronous HTTP call, returning a structured verdict in under 10 seconds.

**Core principle:** process and forget. No biometrics, no PII, and no documents are retained after a verification completes. Compliance proof is delivered via a tamper-evident RS256-signed audit receipt that your system stores permanently — Kernaq never needs to be online to verify it.

---

## SDKs

All official SDKs are published in the [Kernaq/SDKs](https://github.com/Kernaq/SDKs) repository.

| SDK | Install | Registry |
|-----|---------|----------|
| Node.js / TypeScript | `npm install @kernaq/identity` | [npmjs.com](https://www.npmjs.com/package/@kernaq/identity) |
| Python | `pip install kernaq-identity` | [PyPI](https://pypi.org/project/kernaq-identity) |
| Go | `go get github.com/Kernaq/SDKs/identity/go@v1.0.2` | Public repo |
| Java | `com.github.Kernaq:SDKs:v1.0.2` | [JitPack](https://jitpack.io/#Kernaq/SDKs) |
| Verify — Web | `npm install @kernaq/verify` | [npmjs.com](https://www.npmjs.com/package/@kernaq/verify) |
| Verify — React Native | `npm install @kernaq/verify-react-native` | [npmjs.com](https://www.npmjs.com/package/@kernaq/verify-react-native) |

### Quick start — Node.js

```typescript
import Kernaq from '@kernaq/identity'

const kernaq = new Kernaq({ apiKey: process.env.KERNAQ_API_KEY })

const result = await kernaq.verify.run({
  document:     fs.createReadStream('national_id.jpg'),
  selfie:       fs.createReadStream('selfie.jpg'),
  video:        fs.createReadStream('liveness.mp4'),
  documentType: 'national_id',
  country:      'KEN',
  reference:    'user_abc123',
})

console.log(result.verdict)          // "pass" | "fail" | "review"
console.log(result.documentFields)   // name, DOB, document number, ...
```

### Drop-in UI — Web

```html
<script src="https://unpkg.com/@kernaq/verify/dist/index.esm.js" type="module"></script>

<kernaq-verify
  api-key="k_test_..."
  country="KEN"
  reference="user_abc123"
></kernaq-verify>
```

---

## Repositories

| Repo | Description |
|------|-------------|
| [Kernaq/Identity](https://github.com/Kernaq/Identity) | Core KYC API — document OCR, face match, liveness, audit receipts (Go) |
| [Kernaq/Platform](https://github.com/Kernaq/Platform) | Developer platform — auth, projects, API keys, billing, M-Pesa top-up (Go) |
| [Kernaq/SDKs](https://github.com/Kernaq/SDKs) | Official SDKs and drop-in UI components |
| [Kernaq/Website](https://github.com/Kernaq/Website) | Marketing site and developer documentation (React) |
| [Kernaq/ml](https://github.com/Kernaq/ml) | Local ML inference service — OCR, face, liveness (Python) |

---

## Stack

`Go 1.23` `Python 3.11` `React 19` `TypeScript 7` `PostgreSQL 16` `Redis 7`  
`AWS Textract` `AWS Rekognition` `PaddleOCR` `InsightFace` `ONNX Runtime`

---

## Pricing

New projects get **50 free live verifications** — no card required.

| Plan | Price |
|------|-------|
| Pay as you go | $0.25 / verification |
| Startup | from $0.18 / verification |
| Growth | from $0.12 / verification |
| Enterprise | from $0.08 / verification |

Sandbox mode is free and unlimited with `k_test_` keys.

---

## Security

Found a vulnerability? Email **security@kernaq.com**. We respond within 48 hours.  
Do not open a public issue for security reports.

---

<div align="center">
  <sub>
    <a href="https://kernaq.com">kernaq.com</a> ·
    <a href="mailto:support@kernaq.com">support@kernaq.com</a> ·
    <a href="mailto:security@kernaq.com">security@kernaq.com</a>
  </sub>
</div>
