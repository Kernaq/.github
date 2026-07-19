# Kevik

Enterprise identity verification infrastructure for fintech, banking, crypto, payroll, and healthcare.

---

## Repositories

<table>
<tr>
<td width="50%" valign="top">

**[Identity](https://github.com/Kevik-Ltd/Identity)**

KYC pipeline, document OCR, face matching, and liveness detection.
Built in Go with Gin, PostgreSQL, MinIO, and AWS Textract + Rekognition.

```
POST /v1/verifications
POST /v1/documents/extract
POST /v1/documents/validate
POST /v1/face/detect
POST /v1/face/match
POST /v1/liveness/check
```

`Go 1.25` `PostgreSQL` `Redis` `MinIO` `AWS`

</td>
<td width="50%" valign="top">

**[Platform](https://github.com/Kevik-Ltd/Platform)**

Tenant management, API key provisioning, JWT auth, and the admin interface.
Keys are scoped per project with live and test environments.

```
POST /v1/auth/register
POST /v1/auth/login
POST /v1/projects
POST /v1/projects/:id/keys
GET  /v1/admin/stats
GET  /v1/admin/tenants
```

`Go 1.25` `PostgreSQL` `Redis`

</td>
</tr>
<tr>
<td width="50%" valign="top">

**[Website](https://github.com/Kevik-Ltd/Website)**

Marketing site, documentation hub, and the client and admin dashboard.
Docs are generated from the OpenAPI spec via Scalar.

- `/` — marketing
- `/docs` — guides and API reference
- `/dashboard` — client portal
- `/admin` — internal admin console

`React 19` `Vite` `TypeScript` `Tailwind v4`

</td>
<td width="50%" valign="top">

**SDKs** — coming soon

Node.js, Python, and Go clients wrapping all identity endpoints.
Includes multipart upload helpers and async polling for the KYC pipeline.

`Node.js` `Python` `Go`

</td>
</tr>
</table>

---

## Architecture

```
                 kevikltd.com (Website)
                        |
          +-------------+-------------+
          |                           |
   Platform :8090              Identity :8080
   Auth, Projects               KYC, OCR
   API Keys, Admin              Face, Liveness
          |                           |
          +----------+----------------+
                     |
               PostgreSQL
         kevik_platform | kevik_identity
                     |
              Redis  +  MinIO (AES-256)
```

Identity reads `api_keys` directly from Postgres — no HTTP hop to Platform on the request path.
Tokens are stored as `HttpOnly` cookies. Biometric files are TTL-purged (documents 7yr, biometrics 1yr).

---

## Local setup

```bash
cd identity  && make docker-up && make migrate-up && make run   # :8080
cd platform  && make migrate-up && make run                     # :8090
cd website   && npm install && npm run dev                      # :5173
```

---

support@kevik.com — security@kevik.com — [kevikltd.com](https://kevikltd.com)
