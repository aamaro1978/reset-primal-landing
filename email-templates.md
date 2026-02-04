# Email Templates - Reset Primal (Story 6.1)

## Template 1: Mental Avatar

**Subject:** {nome}, aqui está sua solução personalizada 🎯

**From:** suporte@resetprimal.com.br

**Body:**

```
Olá {nome},

Com base nas suas respostas ao nosso diagnóstico, identificamos que seu principal desafio é recuperar CLAREZA MENTAL e PRODUTIVIDADE.

Você relatou dificuldade de concentração, nevoeiro mental que não deixa pensar direito, e aquela sensação de cansaço que vem 2-3 horas após comer.

Desenvolvemos um protocolo específico para:
✓ Eliminar o nevoeiro mental completamente
✓ Recuperar foco e produtividade
✓ Ter energia estável o dia todo

[BOTÃO: Ver Seu Protocolo Personalizado]
(Link: {lp_url}?nome={nome}&email={email}&avatar=mental)

**Sua Garantia:**
7 dias de acesso completo por R$ 97.
Se não acordar mais claro e com energia restaurada, seu dinheiro volta integral.

Você não tem nada a perder. Tudo a ganhar.

Abraços,
Time Reset Primal
```

---

## Template 2: Peso Avatar

**Subject:** {nome}, descobrimos como você pode eliminar aquela barriga 🎯

**From:** suporte@resetprimal.com.br

**Body:**

```
Olá {nome},

Você respondeu que ganhou bastante peso nos últimos anos, principalmente na barriga.
E o pior: não se reconhece mais no espelho.

Sabemos o que é isso. Tentou dietas. Nada funcionou.

A verdade? O problema não é você. É que toda dieta que existe não funciona para corpos como o seu.

Desenvolvemos um protocolo que:
✓ Faz você perder peso teimoso (principalmente barriga)
✓ Sem dieta radical
✓ Sem exercício impossível

[BOTÃO: Acessar Seu Protocolo]
(Link: {lp_url}?nome={nome}&email={email}&avatar=peso)

**Sua Garantia:**
Comece agora por R$ 97.
Siga por 7 dias. Se não notar diferença, dinheiro de volta.

Simples assim.

Abraços,
Time Reset Primal
```

---

## Template 3: Síndrome Avatar

**Subject:** {nome}, seus exames podem normalizar 🎯

**From:** suporte@resetprimal.com.br

**Body:**

```
Olá {nome},

Seus exames revelam síndrome metabólica.
Glicemia alta. Pressão elevada. Colesterol ruim.

Você sabe o que isso significa: se não fazer nada, vai virar como aquele parente que ficou diabético.

Mas há uma boa notícia: síndrome metabólica é REVERSÍVEL.

Temos o protocolo exato que já ajudou centenas de homens a:
✓ Normalizar glicemia
✓ Estabilizar pressão
✓ Recuperar vitalidade

[BOTÃO: Começar a Reverter Agora]
(Link: {lp_url}?nome={nome}&email={email}&avatar=sindrome)

**Sua Garantia:**
R$ 97 agora. 7 dias de protocolo completo.
Se seus exames não começarem a melhorar, dinheiro de volta total.

Você vence essa.

Abraços,
Time Reset Primal
```

---

## Zapier Integration Instructions

### Workflow Trigger:
- **Event:** Phase 1 Form submitted → sendToZapier()
- **Webhook received in Zapier**

### Zapier Actions:

1. **Parse JSON Payload**
   - Input: POST from quiz.html
   - Extract: nome, email, avatar, scores

2. **Determine Template**
   - IF avatar == "mental" → Use Template 1
   - IF avatar == "peso" → Use Template 2
   - IF avatar == "síndrome" → Use Template 3

3. **Send Email via Brevo/Mailchimp**
   - To: {email}
   - Subject: From template (replace {nome})
   - Body: From template (replace {nome}, {email}, {lp_url})
   - From: suporte@resetprimal.com.br
   - Delay: Send within 2 minutes of form submit

4. **Save to CRM**
   - Save email sent timestamp
   - Mark as "Phase 1 Complete"
   - Link to Phase 2 form response (Story 4.1)

5. **Add to Email List**
   - Provider: Brevo or Mailchimp
   - List: "Reset Primal Leads"
   - Tags: [avatar, month_submitted]

### Testing:
- Test with 3 emails (one per avatar)
- Verify delivery within 2 minutes
- Check email content rendering
- Verify LP link has correct params

### Monitoring:
- Track: Email sent timestamp
- Track: Email open rate
- Track: LP click rate
- Track: Conversion from LP

---

## Variables Reference

| Variable | Source | Example |
|----------|--------|---------|
| {nome} | phase1Data.nome | João Silva |
| {email} | phase1Data.email | joao@email.com |
| {avatar} | determineAvatar(scores) | mental/peso/síndrome |
| {lp_url} | window.location.origin | https://reset-primal.example.com |

---

## Performance Requirements

- Email send latency: <2 minutes
- Email delivery success: >98%
- Email rendering: No broken layouts
- CTA click tracking: Required
- Unsubscribe option: Required (LGPD)

---

## LGPD Compliance

✓ Explicit opt-in via Phase 1 form
✓ Email contains unsubscribe link
✓ Data retention: 30 days after unsubscribe
✓ Privacy policy linked in email footer
✓ Data processing agreement with email provider
