# Documentação Técnica - Sistema de Consultório Médico (2025)

## Arquitetura do Sistema

- **Frontend (Next.js + TypeScript):** Agendamento online, painel médico, painel paciente, administração
- **Backend (Fastify/Express):** Autenticação JWT, APIs REST de agendamento, orçamento, pagamentos e prontuários
- **Banco de Dados PostgreSQL/Prisma**
- **Integrações:** Stripe (PIX/cartão), Twilio WhatsApp, Resend/Sendgrid (email), ICP-Brasil, Atesta CFM
- **Compliance:** LGPD/SBIS nativo, trilha de auditoria, logs, criptografia, backup diário

## Principais Fluxos

### 1. Agendamento Online
- Disponibilidade médica
- Confirmação via email/WhatsApp
- Pagamento digital (PIX/cartão)

### 2. Orçamento
- Geração de orçamento PDF por serviço
- Envio automático WhatsApp/email
- Validade e histórico de acompanhamento

### 3. Pagamentos (Stripe API)
- PIX (1,19%), cartão nacional (3,99% + R$0,39)
- Processo auditável

### 4. Prontuário Eletrônico
- CRUD multi-especialidade
- Assinatura digital ICP-Brasil
- Logs e versionamento
- Compliance Retenção CFM/SBIS

## Compliance Regulatória

- **Atesta CFM:** obrigatório para atestados (março/2025)
- **LGPD:** consentimento digital, log de alterações, anonimização possível
- **SBIS:** NGS1/NGS2, backup automático, criptografia ponta-a-ponta
- **Telemedicina:** Resolução CFM 2.430/2025, autenticação e logs integrados

## Estrutura de Pastas

```
consultorio-medico/
├── app/
│   ├── api/
│   ├── dashboard/
│   ├── appointments/
│   └── patients/
├── components/
├── lib/
├── prisma/
│   ├── schema.prisma
│   └── migrations/
└── types/
```

## Principais Endpoints REST

- `POST /api/appointments` - Criação de agendamento
- `GET /api/appointments` - Listagem por usuário
- `POST /api/payments` - Geração pagamento Stripe
- `POST /api/quotes` - Solicitar orçamento
- `POST /api/medical_records` - Novo prontuário
- `GET /api/audit_logs` - Consultar alterações e acessos

## Regras Técnicas e Boas Práticas

- LGPD: consentimento obrigatório, log em toda alteração crítica
- SBIS: integração pronta para certificação (auditoria, backup, controles de acesso)
- Arquitetura escalável para N médicos/consultórios

## Integrações
- Stripe SDK (PIX/cartão)
- WhatsApp API via Twilio
- ICP-Brasil/Resend para assinatura digital/email
- Atesta CFM/api oficial para atestados

## Como rodar o projeto

1. Instale dependências: `npm install`
2. Configure `.env.local` (Stripe, Twilio, banco e e-mail)
3. Rode migrations: `npx prisma migrate deploy`
4. Inicie: `npm run dev` (local)
5. Deploy sugerido: Vercel (frontend), Railway/Supabase(PostgreSQL)

---

Para dúvidas ou fluxos detalhados por endpoint, solicite exemplos práticos ou diagramas específicos!
