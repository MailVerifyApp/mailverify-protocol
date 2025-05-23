# MailVerify Protocol (v0.1 Draft)

MailVerify is a sender identity trust layer that uses signed tokens and verifiable headers to establish authenticity at the human level—complementing SPF, DKIM, and DMARC.

---

## 🔐 Token Structure (JWT)

Each email from a verified sender includes a signed JWT:

```
{
  "email": "jane@example.com",
  "verified": true,
  "methods": ["institutional", "social", "domain"],
  "issued": "2025-05-22T12:00:00Z",
  "expires": "2026-05-22T12:00:00Z",
  "signature": "..."
}
```

---

## ✉️ Header Injection

A custom header is included in outbound email:

```
X-MailVerify: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

---

## 🔁 Verification Flow

1. User verifies identity with MailVerify via an accepted method  
   (e.g., institutional ID, domain DNS, or validated social account)  
2. Token is issued and stored  
3. Token is added to outgoing email headers (manually, via SMTP relay, or via MailVerify tool)  
4. Receiving inbox or plugin validates token using public JWKS key  
5. Trust badge is displayed or trusted routing preference is applied

---

## 🧭 Future Considerations

- BIMI compatibility  
- DNS TXT-based trust registry  
- Trust tiering (Gold / Blue / Verified Org)  
- Feedback loop integrations with ESPs

