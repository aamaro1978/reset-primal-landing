# 🚀 Reset Primal - Free Tier Integration Setup Guide

**Date:** February 4, 2026
**Status:** Step-by-Step Configuration
**Cost:** $0 (All free tier services)
**Timeline:** ~60 minutes for complete setup

---

## Overview

This guide walks through setting up the complete free tier tech stack for Reset Primal:

| Service | Free Tier | Primary Use | Status |
|---------|-----------|------------|--------|
| **Brevo** | 300 emails/day | Email sending | ✅ Setup here |
| **Airtable** | Unlimited records (free tier) | CRM & lead database | ✅ Setup here |
| **Zapier** | 1 zap + 100 tasks/month | Webhook automation | ✅ Setup here |
| **Google Analytics 4** | 100% free | Traffic & conversion tracking | ✅ Setup here |

---

## Part 1: Brevo Email Service Setup (15 min)

### Step 1.1: Create Brevo Account

1. Go to **https://www.brevo.com/sign-up/**
2. Choose: **Sign up for free**
3. Fill in:
   - Email: `suporte@resetprimal.com.br` (or your email)
   - Password: Create strong password
4. Click **Create my free account**
5. **Verify email** - Brevo sends verification link

### Step 1.2: Complete Brevo Setup

1. Select **Email marketing** as primary use
2. Company info:
   - Company name: `Reset Primal`
   - Industry: `Health & Wellness`
   - Website: `https://aamaro1978.github.io/reset-primal-landing/`
3. Accept terms
4. Dashboard ready ✅

### Step 1.3: Create Sender Email & Add Contacts List

**Create Sender:**
1. Go to **Senders** (left menu)
2. Click **Add sender**
3. Email: `suporte@resetprimal.com.br`
4. Sender name: `Reset Primal Support`
5. Verify sender email (confirmation sent)

**Create Contact List:**
1. Go to **Contacts** (left menu)
2. Click **Create a list**
3. Name: `Reset Primal Leads`
4. Folder: `Main folder`
5. Create ✅

### Step 1.4: Generate API Key

1. Go to **Settings** (bottom left) → **Users & access**
2. Select your user account
3. Scroll to **API Keys section**
4. Click **Generate new key** (Master access)
5. **COPY THIS KEY** - You'll need it for Zapier

**⚠️ Save this:** Your Brevo API Key looks like:
```
key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

---

## Part 2: Airtable Lead Database Setup (15 min)

### Step 2.1: Create Airtable Workspace

1. Go to **https://www.airtable.com/signup**
2. Sign up with email
3. Workspace name: `Reset Primal`
4. Create workspace ✅

### Step 2.2: Create Base & Table

1. Click **Create** (top left)
2. Name: `Reset Primal Leads`
3. Start from scratch ✅

### Step 2.3: Configure Table Schema

The table should have these fields (columns):

| Field Name | Type | Notes |
|-----------|------|-------|
| Nome | Single line text | User's full name |
| Email | Email | Contact email |
| WhatsApp | Phone number | +55 format |
| Idade | Single select | 35-40, 41-50, 51+ |
| Avatar | Single select | mental, peso, síndrome |
| Scores | JSON | {"m": 34, "p": 8, "s": 5} |
| Created | Date | Auto-fill on record creation |
| LP Clicked | Checkbox | Track LP engagement |
| Email Sent | Checkbox | Track email delivery |
| Status | Single select | New, Engaged, Converted |

**How to add fields:**
1. Click **+** next to last column
2. Enter field name
3. Select field type
4. Configure options (if Single select or Checkbox)
5. Done ✅

### Step 2.4: Generate API Key

1. Click your profile (top right) → **Account**
2. Go to **API tokens** tab
3. Click **Create new token**
4. Token name: `Zapier Integration`
5. Permissions:
   - ✅ data.records:create
   - ✅ data.records:read
   - ✅ data.records:update
   - ✅ schema.bases:read
6. Scopes: Select `Reset Primal Leads` base
7. Create token ✅

**⚠️ Save this:** Your Airtable API Token looks like:
```
patxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

### Step 2.5: Get Base & Table IDs

1. Open your `Reset Primal Leads` base
2. URL looks like: `https://airtable.com/appXXXXXXXXXXXXXX/tblYYYYYYYYYYYYYY/...`
3. Extract:
   - **Base ID:** `appXXXXXXXXXXXXXX`
   - **Table ID:** `tblYYYYYYYYYYYYYY`

**⚠️ Save these IDs** - You'll need them for Zapier

---

## Part 3: Zapier Workflow Setup (20 min)

### Step 3.1: Create Zapier Account

1. Go to **https://zapier.com/sign-up**
2. Sign up with email
3. Choose: **Getting started with Zapier**
4. Click **Create a Zap** ✅

### Step 3.2: Set Up Trigger - Webhook

**Configure Trigger:**
1. Search for: **Webhooks by Zapier**
2. Select: **Catch Raw Hook**
3. Account: `My Account`
4. Continue ✅
5. **COPY THE WEBHOOK URL** (you'll use this in quiz.html)

**Webhook URL format:**
```
https://hooks.zapier.com/hooks/catch/YOUR_WEBHOOK_ID/
```

**⚠️ Save this webhook URL** - You'll add it to quiz.html

### Step 3.3: Add Action 1 - Send Brevo Email

**Configure Action 1:**
1. Click **+** to add action
2. Search: **Brevo (Sendinblue)**
3. Action: **Send Email**
4. Account: Click to connect
   - Paste your **Brevo API Key** from Part 1.4
   - Authorize ✅

**Map Brevo Fields:**
1. To Email: Select `email` from webhook data
2. Subject line:
   - IF avatar = mental → `{nome}, aqui está sua solução personalizada 🎯`
   - IF avatar = peso → `{nome}, descobrimos como você pode eliminar aquela barriga 🎯`
   - IF avatar = síndrome → `{nome}, seus exames podem normalizar 🎯`
3. From Email: `suporte@resetprimal.com.br`
4. HTML Body: (Use email template from `email-templates.md`)
5. Contact list: `Reset Primal Leads` ✅

### Step 3.4: Add Action 2 - Save to Airtable

**Configure Action 2:**
1. Click **+** to add another action
2. Search: **Airtable**
3. Action: **Create Record**
4. Account: Click to connect
   - Paste your **Airtable API Token** from Part 2.4
   - Authorize ✅

**Map Airtable Fields:**
1. Base: `Reset Primal Leads`
2. Table: `Reset Primal Leads` (the table you created)
3. Map webhook fields to table columns:
   - Nome → `nome`
   - Email → `email`
   - WhatsApp → `whatsapp`
   - Idade → `idade`
   - Avatar → `avatar`
   - Scores (JSON) → `scores`
   - Created → Auto-populate with today's date ✅

### Step 3.5: Test the Zap

1. Click **Test & Review**
2. Use Zapier's **Send Test** feature
3. Fill sample data:
   ```
   {
     "nome": "João Silva",
     "email": "joao@email.com",
     "whatsapp": "+55 11 98765-4321",
     "idade": "41-50",
     "avatar": "mental",
     "scores": {"m": 34, "p": 8, "s": 5}
   }
   ```
4. Verify:
   - ✅ Email sent in Brevo
   - ✅ Record created in Airtable
5. Click **Publish Zap** ✅

**⚠️ Important:** Your zap is now LIVE

---

## Part 4: Update quiz.html with Zapier Webhook

### Step 4.1: Edit quiz.html

1. Open: `/Users/acacioamaro/reset-primal-landing/quiz.html`
2. Find this line (~line 580):
```javascript
const zapierWebhookUrl = 'https://hooks.zapier.com/hooks/catch/YOUR_WEBHOOK_ID/';
```
3. Replace `YOUR_WEBHOOK_ID` with your actual webhook URL from Part 3.2
4. Save file

### Step 4.2: Test Quiz → Form → Brevo/Airtable Flow

1. Open: `https://aamaro1978.github.io/reset-primal-landing/quiz.html`
2. Complete quiz (pick Mental bias: answer "a" for most questions)
3. Fill Phase 1 form:
   - Nome: Your test name
   - WhatsApp: +55 11 98765-4321
   - Email: Your email
   - Idade: 41-50
4. Submit form
5. **Verify:**
   - ✅ Redirected to LP (Mental)
   - ✅ Email received in your inbox (Brevo)
   - ✅ Record appears in Airtable

---

## Part 5: Google Analytics 4 Setup (10 min)

### Step 5.1: Create GA4 Property

1. Go to **https://analytics.google.com/**
2. Sign in with Google account
3. Click **Start measuring** (or create new account)
4. Account name: `Reset Primal`
5. Property name: `Reset Primal Landing`
6. Website: `https://aamaro1978.github.io/reset-primal-landing/`
7. Industry: `Health & Wellness`
8. Create account ✅

### Step 5.2: Add Measurement ID to Pages

1. In GA4, click **Admin** (bottom left)
2. Find **Data Streams** section
3. Select your data stream (web)
4. **COPY Measurement ID** - Format: `G-XXXXXXXXXX`

### Step 5.3: Add GA4 Tracking to All Pages

**For quiz.html:**
Add this before closing `</head>` tag:
```html
<!-- Google Analytics 4 -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX', {
    'page_path': '/quiz.html',
    'page_title': 'Reset Primal Quiz'
  });
</script>
```

**For landing pages:**
Replace the `<script>` section in each LP with:
```html
<script>
  // Google Analytics 4
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX', {
    'page_path': window.location.pathname,
    'page_title': document.title
  });

  // Track custom events
  gtag('event', 'lp_viewed', {
    'avatar': new URLSearchParams(window.location.search).get('avatar'),
    'user_name': new URLSearchParams(window.location.search).get('nome')
  });
</script>
```

**Replace** `G-XXXXXXXXXX` with your actual Measurement ID

### Step 5.4: Track Form Submission Event

In quiz.html, find the `sendToZapier()` function and add:
```javascript
// Track form submission
gtag('event', 'form_submit', {
  'avatar': avatar,
  'nome': nome,
  'email': email,
  'idade': idade,
  'scores_mental': scores.m,
  'scores_peso': scores.p,
  'scores_sindrome': scores.s
});
```

---

## Part 6: Integration Testing (10 min)

### Test Scenario 1: Mental Avatar Flow

**Step 1:** Complete quiz
- Answer questions biased toward Mental (answer "a" mostly)
- Expected score: ~m=30, p=5, s=5

**Step 2:** Fill form
- Nome: `Test Mental User`
- Email: `test-mental@email.com`
- WhatsApp: `+55 11 98765-0001`
- Idade: `41-50`

**Step 3:** Verify completeness
- [ ] Redirected to reset-primal-final.html (Mental LP)
- [ ] Greeting shows "Olá, Test Mental User!"
- [ ] Email received in inbox within 2 minutes
- [ ] Record appears in Airtable with all fields
- [ ] GA4 shows event in real-time

### Test Scenario 2: Peso Avatar Flow

**Step 1:** Complete quiz (Peso bias)

**Step 2:** Fill form
- Nome: `Test Peso User`
- Email: `test-peso@email.com`
- WhatsApp: `+55 21 987654-0002`
- Idade: `35-40`

**Step 3:** Verify completeness
- [ ] Redirected to lp-emagrecimento.html (Peso LP)
- [ ] Email received
- [ ] Airtable record created

### Test Scenario 3: Síndrome Avatar Flow

**Step 1:** Complete quiz (Síndrome bias)

**Step 2:** Fill form
- Nome: `Test Síndrome User`
- Email: `test-sindrome@email.com`
- WhatsApp: `+55 85 999888-0003`
- Idade: `51+`

**Step 3:** Verify completeness
- [ ] Redirected to lp-sindrome.html (Síndrome LP)
- [ ] Email received
- [ ] Airtable record created

---

## Part 7: Monitoring & Next Steps

### Monitor These Metrics

**In Airtable:**
- New leads per day
- Avatar distribution (should follow your targeting)
- Email delivery status

**In Brevo:**
- Email open rate (target: >20%)
- Email click rate (target: >5%)
- Unsubscribe rate (should be <0.5%)

**In Google Analytics 4:**
- Quiz completion rate
- Form submission rate
- LP view count
- Avatar distribution
- Traffic source

### Scaling Beyond Free Tier

When you reach limits:

**Brevo:**
- Free: 300 emails/day
- Paid: Starting $50/month for unlimited

**Airtable:**
- Free: Unlimited records, 100GB storage
- Paid: Starting $50/month for more users

**Zapier:**
- Free: 100 tasks/month (≈3/day)
- Paid: Starting $20/month for 750 tasks

**Google Analytics 4:**
- Free: Unlimited forever

---

## Quick Reference - Your Credentials

**Save these somewhere safe (encrypted file recommended):**

```
BREVO:
- Email: suporte@resetprimal.com.br
- API Key: key_xxxxxxx...
- Sender List: Reset Primal Leads
- From Email: suporte@resetprimal.com.br

AIRTABLE:
- Base ID: app...
- Table ID: tbl...
- API Token: pat...

ZAPIER:
- Webhook URL: https://hooks.zapier.com/hooks/catch/YOUR_ID/

GOOGLE ANALYTICS 4:
- Measurement ID: G-...
```

---

## Troubleshooting

### Email not arriving
1. Check Brevo spam folder
2. Verify sender email is verified in Brevo
3. Check Zapier zap run history for errors
4. Retry from Airtable (Zapier history tab)

### Airtable record not created
1. Verify Airtable API token permissions
2. Check Zapier zap is "On" (toggle switch)
3. Review field mappings match your table schema
4. Check Zapier run history for errors

### GA4 not tracking
1. Verify Measurement ID is correct (G-XXXXXXXX)
2. Check browser console for errors
3. View real-time events in GA4 dashboard
4. Clear browser cache and reload

### Quiz not redirecting
1. Verify Zapier webhook URL is correct in quiz.html
2. Check browser console (F12) for errors
3. Verify localStorage has quiz responses
4. Test Zapier webhook independently

---

## Next Steps (Optional Upgrades)

1. **Phase 2 Widget** - Optional form on LP to capture more data
2. **Email Sequence** - 7-day follow-up series (requires paid Zapier)
3. **A/B Testing** - Different LP copy variations
4. **SMS Follow-up** - WhatsApp integration (separate service)
5. **Lead Scoring** - Calculate lead value (0-100 score)

---

**Status:** ✅ Free tier stack ready for production
**Cost:** $0
**Emails/Day:** 300 (Brevo free limit)
**Records:** Unlimited (Airtable free limit)
**Monthly Tasks:** 100 (Zapier free limit)

Ready to go live! 🚀
