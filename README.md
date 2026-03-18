# lead-capture-system

Sistema de captura de leads pensado para uso em link do Instagram Stories.

## Estrutura do projeto

- `/frontend`
  - `index.html` (form leve + validação JS)
  - `styles.css` (design mobile-first, foco conversão)
- `/backend`
  - `index.js` (Express + validações + SQLite + n8n + WhatsApp)
  - `db.js` (inicializa tabela `leads`)
  - `package.json`
  - `.env.example`

## Requisitos usados

- Node.js 16+
- npm
- SQLite (biblioteca `better-sqlite3`, não precisa instalar DB externo)

## Funcionalidade completa

1. Formulário com: nome, CPF, data de nascimento, WhatsApp, email, tempo de trabalho, função/profissão
2. Validações: campos obrigatórios, CPF real, email, telefone formatação simples
3. Backend: `POST /lead`, valida, salva em SQLite e envia para n8n via webhook
4. Integração n8n: JSON com `origem: "instagram_story"`
5. Exemplo de automação WhatsApp via provider (WAHA/Meta)
6. Resposta JSON com sucesso/erro e payloads
7. Copy para Instagram Stories, CTA e sugestões de melhoria

## Instalação e execução

### Backend

1. Abra terminal em `/backend`
2. Copie `.env.example` para `.env` e preencha:
   - `PORT` (ex: 3000)
   - `N8N_WEBHOOK_URL` (ex: `https://seu-n8n/webhook/lead-capture`)
   - `WHATSAPP_PROVIDER_URL` (ex: `https://api.seu-provedor.com/messages`)
   - `WHATSAPP_PROVIDER_TOKEN` (token do provedor)
3. Instale dependências:
   - `npm install`
4. Inicie servidor:
   - `npm run start`
5. A API roda em: `http://localhost:3000`
6. Teste healthcheck:
   - `GET http://localhost:3000/health`

### Frontend

1. Abra `frontend/index.html` direto no navegador (ideal) ou via servidor estático:
   - `cd frontend && python -m http.server 8000` (opcional)
2. Aponte o `fetch` para o backend local (`http://localhost:3000/lead`)
3. Preencha e envie o formulário

### Expor ao Instagram

1. Use ngrok ou similar:
   - `ngrok http 3000` (ou porta que você usar)
2. Use URL https do ngrok para o n8n e/ou link no Story

## API `/lead`

- Método: POST
- Corpo JSON:
  - `nome` (string)
  - `cpf` (string)
  - `data_nascimento` (YYYY-MM-DD)
  - `whatsapp` (string)
  - `email` (string)
  - `tempo_trabalho` (string)
  - `funcao_profissao` (string)

### Exemplo de payload para n8n

```json
{
  "nome": "Ana Silva",
  "cpf": "12345678909",
  "data_nascimento": "1990-05-15",
  "whatsapp": "5511999999999",
  "email": "ana@exemplo.com",
  "tempo_trabalho": "8 anos",
  "funcao_profissao": "Técnica em Eletricidade",
  "origem": "instagram_story"
}
```

## Exemplo automação WhatsApp (payload de saída)

```json
{
  "provider": "waha/meta-api",
  "to": "5511999999999",
  "text": "Olá Ana Silva, recebemos seu cadastro e em breve entraremos em contato. Obrigado por confiar no nosso trabalho!",
  "template": {
    "namespace": "default",
    "name": "lead_recebido",
    "language": "pt_BR",
    "components": [{ "type": "body", "parameters": [{ "type": "text", "text": "Ana Silva" }] }]
  }
}
```

> Observação: esse envio está como exemplo e precisa de URL/token de API real para funcionar.

## Copy de alta conversão para Instagram Story (versão pronta)

- Título curto (até 12s): "Oportunidade única para profissionais já!" 
- Texto: "🔥 Vagas exclusivas abertas AGORA. Cadastre-se em 30s e receba proposta direta no WhatsApp. Vagas limitadas para quem chegar primeiro." 
- CTA do botão: "Quero minha vaga agora"

### Sugestões de melhoria de conversão

- usar prova social: "+500 profissionais aprovados".
- adicionar senso de urgência: "últimas 12 vagas".
- usar lead magnet (e-book gratuito ou consultoria 10m).
- teste A/B com variações de título e texto (Story 1x e 2x).
- usar rastreamento UTM + parâmetros no link.

## Dicas de performance

- Frontend sem frameworks, minificado por simples execução no navegador.
- Imagens externas otimizadas (WebP + LCP baixo).
- respostas backend rápidas, e OACK de payload reduzido.

## Verificação rápida

1. Submeta lead via UI.
2. Confirme registro em `backend/leads.db` (SQLite Browser) na tabela `leads`.
3. Verifique log de webhook n8n via n8n UI.
4. Verifique que retorno tem `whatsappPayload` e texto personalizado.

---

Pronto: sistema completo, leve e pronto para teste em produção leve. Aproveite! 

