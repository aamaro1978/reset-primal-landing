# Reset Primal - N8N Cloud Migration

**Date:** February 10, 2026
**Status:** In Progress - Webhook Setup Phase
**Migration From:** Zapier
**Migration To:** N8N Cloud (Singullarco workspace)

---

## Overview

Migrando da arquitetura Zapier para N8N Cloud para centralizar todas as automacoes em um unico lugar, alinhado com o squad que ja usa N8N para WhatsApp.

---

## Current Architecture

### Before (Zapier)
```
Sales Page Form
    ↓
    ├→ Zapier Webhook 1 (RP-Leads-Sheets) → Google Sheets
    └→ Zapier Webhook 2 (RP-Leads-Email) → Brevo Email
```

### After (N8N Cloud)
```
Sales Page Form
    ↓
    ├→ N8N Webhook 1 (RP-Leads-Sheets) → Google Sheets
    └→ N8N Webhook 2 (RP-Leads-Email) → Brevo Email
```

---

## Workflows Created

### Workflow 1: RP-Leads-Sheets

**Status:** ✅ Created & Active

**Configuration:**
- **Platform:** N8N Cloud (Singullarco)
- **Webhook URL:** `https://singullarco.app.n8n.cloud/webhook/515504c7-1bbb-468a-9324-15f2096fe635`
- **Method:** POST
- **Trigger:** Webhook (Capture eventos do Webhook)
- **Next Step:** Google Sheets integration (pending)

**Fields Received:**
```json
{
  "nome": "string",
  "email": "string",
  "whatsapp": "string",
  "source": "sales-page",
  "timestamp": "ISO-8601"
}
```

### Workflow 2: RP-Leads-Email

**Status:** ⏳ Pending Setup

**Configuration:**
- **Platform:** N8N Cloud (Singullarco)
- **Webhook URL:** (to be generated)
- **Method:** POST
- **Trigger:** Webhook
- **Action:** Send Email via Brevo
- **Fields:** Same as RP-Leads-Sheets

---

## Code Changes

### Sales Page (`sales.html`)

**Updated Webhooks Configuration:**

```javascript
// N8N Cloud webhooks (migrado de Zapier)
const N8N_LEADS_SHEETS = 'https://singullarco.app.n8n.cloud/webhook/515504c7-1bbb-468a-9324-15f2096fe635';
const N8N_LEADS_EMAIL = '';  // RP-Leads-Email (em configuracao)
```

**Updated Form Handler:**
- Changed from `Promise.all()` (sending to 2 endpoints) to single webhook
- Still sends all 3 fields: `nome`, `email`, `whatsapp`
- Added `source` and `timestamp` automatically

**Deployment:**
- ✅ Committed to GitHub
- ✅ Pushed to main branch
- ✅ Live on GitHub Pages: `https://aamaro1978.github.io/reset-primal-landing/sales.html`

---

## Next Steps

### Immediate (Today)
1. ✅ Create RP-Leads-Sheets webhook in N8N Cloud
2. ✅ Update sales page with N8N webhook URL
3. ✅ Deploy to GitHub Pages
4. ⏳ **Test webhook:** Send form submission and verify N8N receives data

### Phase 2 (Tomorrow)
1. ⏳ Add Google Sheets node to RP-Leads-Sheets workflow
2. ⏳ Configure sheet mapping (Nome, Email, WhatsApp, Source, Data)
3. ⏳ Test end-to-end: Form → N8N → Google Sheets

### Phase 3 (Week 1)
1. ⏳ Create RP-Leads-Email workflow in N8N Cloud
2. ⏳ Add Brevo email node
3. ⏳ Configure email templates
4. ⏳ Test end-to-end: Form → N8N → Brevo

### Phase 4 (Week 2)
1. ⏳ Decommission Zapier workflows
2. ⏳ Cancel Zapier account
3. ⏳ Add Stripe payment automation to N8N (replace custom code)

---

## Testing Checklist

### Webhook Connectivity
- [ ] Form submission triggers webhook
- [ ] N8N receives POST request
- [ ] All fields populated correctly
- [ ] Timestamp auto-generated
- [ ] Source field = "sales-page"

### Google Sheets Integration
- [ ] Data flows from N8N to Google Sheets
- [ ] Row created for each submission
- [ ] Fields mapped correctly
- [ ] No duplicate rows

### Email Integration
- [ ] Email sent automatically after form submission
- [ ] Email received in inbox
- [ ] Template renders correctly
- [ ] User name personalized

---

## Advantages of N8N Cloud Migration

| Aspect | Zapier | N8N Cloud |
|--------|--------|-----------|
| **Cost** | $20+/month (paid plan) | Free tier generous |
| **Scalability** | Limited free tier (100 tasks/month) | Unlimited workflows |
| **Customization** | Limited | Full control |
| **Centralization** | Separate from WhatsApp automation | Single workspace for all |
| **Team Access** | Requires paid plan | Free collaboration |
| **Self-hosted Option** | Not available | Available later |

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│ Reset Primal - Lead Capture & Automation (N8N Cloud)         │
└─────────────────────────────────────────────────────────────┘

                    Landing Pages
                         │
        ┌────────────────┼────────────────┐
        │                │                │
    Quiz Page        Sales Page      WhatsApp Bot
        │                │                │
        └────────────────┼────────────────┘
                         │
                    Form Submit
                         │
        ┌────────────────┴────────────────┐
        │                                 │
   N8N WEBHOOK                    N8N WEBHOOK
   (RP-Leads-Sheets)             (RP-Leads-Email)
        │                                 │
        ├─→ Google Sheets               ├─→ Brevo
        │   (Lead Database)             │   (Email Automation)
        │                              │
        └──→ Airtable                  └──→ WhatsApp (future)
            (CRM)                           (Existing Squad)
```

---

## Credentials & Access

### N8N Cloud Account
- **Workspace:** Singullarco
- **URL:** https://singullarco.app.n8n.cloud
- **Access:** Squad team members

### Google Sheets
- **Spreadsheet:** Reset Primal Leads
- **Schema:** Nome | Email | WhatsApp | Source | Data

### Brevo
- **Account:** suporte@resetprimal.com.br
- **From Email:** suporte@resetprimal.com.br
- **List:** Reset Primal Leads

---

## Troubleshooting

### Webhook Not Receiving Data
1. Verify webhook is **Active** in N8N
2. Check Sales Page has **correct webhook URL**
3. Verify form submission **reaches webhook** (check N8N execution history)
4. Check browser console for JavaScript errors

### Data Not Going to Google Sheets
1. Verify Google Sheets node is configured
2. Check sheet name matches configuration
3. Verify column headers match field names
4. Check API credentials are valid

### Email Not Sending
1. Verify Brevo node is configured
2. Check API key is valid
3. Verify sender email is verified in Brevo
4. Check email template for errors

---

## Rollback Plan

If N8N has issues, we can quickly revert to Zapier:

1. Update `sales.html` webhooks back to Zapier URLs
2. Reactivate Zapier zaps
3. Push to GitHub
4. Rollback complete (2 min)

---

## Documentation Links

- **Sales Page:** `/Users/acacioamaro/reset-primal-landing/sales.html`
- **GitHub Repo:** https://github.com/aamaro1978/reset-primal-landing
- **N8N Workspace:** https://singullarco.app.n8n.cloud
- **Design System:** `DESIGN-SYSTEM.md`

---

## Status Summary

| Component | Status | Notes |
|-----------|--------|-------|
| N8N Cloud Account | ✅ Active | Singullarco workspace |
| RP-Leads-Sheets Workflow | ✅ Created | Webhook active |
| Sales Page Update | ✅ Deployed | GitHub Pages live |
| Google Sheets Integration | ⏳ Pending | Next step |
| Brevo Integration | ⏳ Pending | After Sheets |
| Testing | ⏳ Pending | Full end-to-end |
| Zapier Decommission | ⏳ Later | After N8N validated |

---

**Last Updated:** February 10, 2026
**Next Update:** After Google Sheets integration completes

