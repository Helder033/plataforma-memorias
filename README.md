# Para Sempre V5 — MVP comercial online

Esta versão fecha o ciclo principal do produto: criação online, edição protegida por token, armazenamento de fotos em Cloudflare R2, publicação por slug e estrutura de pagamento Pagar com confirmação por webhook.

## Stack
- Cloudflare Workers + Assets
- Cloudflare D1
- Cloudflare R2
- Pagar API (M-Pesa/e-Mola; checkout pode devolver URL para cartão quando disponível)

## Configuração
1. Crie o D1 `para-sempre` e coloque o ID em `wrangler.toml`.
2. Crie o R2 bucket `para-sempre-media`.
3. Execute `wrangler d1 execute para-sempre --remote --file=schema.sql`.
4. Configure secrets: `PAGAR_API_KEY`, `PAGAR_SIGNING_SECRET`, `PAGAR_WEBHOOK_SECRET`.
5. No Pagar, configure o webhook para `https://SEU-DOMINIO/api/pagar/webhook`.
6. `wrangler deploy`.

## Importante
- O pagamento ainda não é LIVE até as credenciais/KYC do Pagar serem configuradas.
- O token de edição é um mecanismo MVP para proteger a página; antes de escalar, substituir por autenticação completa/magic link.
- Não colocar chaves do Pagar no frontend.
- O backend define os preços.
