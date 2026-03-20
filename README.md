# 🎯 Lead Capture System

Sistema moderno e responsivo para captura de leads em 7 etapas, ideal para campanhas de crédito pessoal, financiamentos ou consultorias. Interface premium com tema alternável (claro/escuro) e integração automática com WhatsApp.

---

## ✨ O que o projeto faz

- ✅ **Fluxo de 7 etapas** otimizado para conversão  
- ✅ **Captura completa** de dados: nome, WhatsApp, CPF, email, data de nascimento, vínculo (CLT/PJ) e tempo de trabalho  
- ✅ **Validações inteligentes** em cada campo (máscara de entrada, formato, obrigatoriedade)  
- ✅ **Envio incremental** de dados à API (`etapa a etapa`, não apenas ao final)  
- ✅ **Tema claro/escuro** com persistência em localStorage  
- ✅ **CTA WhatsApp nativo** após conclusão + botão flutuante  
- ✅ **Zero dependências** – roda direto no navegador  
- ✅ **Pronto para Vercel, Netlify, GitHub Pages**

---

## 📁 Estrutura

```
lead-capture-system/
├── index.html          # UI + CSS + JavaScript (tudo integrado)
├── config.js           # Configurações de ambiente
└── README.md           # Este arquivo
```

---

## 🚀 Como começar (5 minutos)

### Opção 1: Abrir direto no navegador
```bash
# No Windows, macOS ou Linux, apenas abra:
file:///seu-caminho/index.html
```

### Opção 2: Servidor local (recomendado)
```bash
# Se tiver Python 3 instalado:
python -m http.server 8000

# Abra: http://localhost:8000
```

### Opção 3: Deploy rápido
- **Vercel**: Suba a pasta como projeto estático
- **Netlify**: Drag-and-drop dos arquivos
- **GitHub Pages**: Commit em `gh-pages` branch

---

## ⚙️ Configuração (config.js)

Edite o arquivo `config.js` com seus dados:

```javascript
window.APP_CONFIG = {
  API_URL: 'https://seu-backend.com/api/leads',  // Endpoint que receberá os dados
  WHATSAPP_NUMBER: '5551999999999'                // Número com código de país (sem +)
};
```

**O que fazer:**
- **API_URL**: Aponte para seu backend (Node.js, Django, Vercel Function, etc.)  
  *ou* use um webhook (n8n, Zapier, Make, etc.)
- **WHATSAPP_NUMBER**: Seu número de WhatsApp Business (com 55 para Brasil)

---

## 📋 As 7 Etapas

| Etapa | Campo | Validação |
|-------|-------|-----------|
| 1 | Nome | Mínimo 3 caracteres |
| 2 | WhatsApp | Formato brasileiro (11 98765-4321) |
| 3 | CPF | Máscara 000.000.000-00 |
| 4 | Email | Validação de email |
| 5 | Data de Nascimento | Formato DD/MM/YYYY |
| 6 | Vínculo Profissional | CLT / PJ |
| 7 | Tempo de Trabalho | Pré-selecionado (3-6 meses, 6-12, etc.) |

Cada etapa envia um **POST JSON** para sua API.

---

## 📡 API esperada

### Método
```
POST https://seu-backend.com/api/leads
Content-Type: application/json
```

### Payload exemplo (etapa final 7)
```json
{
  "sessionId": "550e8400-e29b-41d4-a716-446655440000",
  "nome": "João Silva",
  "whatsapp": "11 98765-4321",
  "cpf": "123.456.789-00",
  "email": "joao@example.com",
  "dataNascimento": "15/03/1990",
  "emprego": "CLT",
  "tempoTrabalho": "6 a 12 meses",
  "etapa_atual": "etapa_7_tempo",
  "timestamp": "2026-03-19T14:30:00Z"
}
```

### Respostas esperadas
- **200 OK**: Lead salvo com sucesso
- **4xx / 5xx**: Erro (será logado no DevTools, formulário permite retry)

---

## 🎨 Personalização

### Textos e headlines
Abra `index.html` e procure por seções comentadas:
```html
<!-- CUSTOMIZE: Altere textos, benefícios, prova social aqui -->
<h1>Seu título aqui</h1>
<p>Sua proposta de valor</p>
```

### Cores e tema
As cores estão em variáveis CSS no `<style>` de `index.html`:
```css
:root {
  --gold: #C9A84C;      /* Ajuste a cor dourada */
  --bg-page: #0D0D0D;   /* Fundo tema escuro */
  /* ... mais variáveis */
}
```

### Número de WhatsApp
Altere em `config.js`:
```javascript
WHATSAPP_NUMBER: '5585987654321'  // Novo número
```

---

## 🧪 Testes

### 1. Teste local
```bash
# Terminal
python -m http.server 8000

# Navegador
http://localhost:8000
```

### 2. Preencha o formulário até o final
- Complete todas as 7 etapas
- Você deve ver sucessivamente "Etapa X enviada"
- Na etapa 7, será exibida tela de sucesso

### 3. Abra DevTools e verifique requisições
- Clique **F12** ou **Right-click → Inspect**
- Vá à aba **Network**
- Preencha o formulário e veja os POSTs sendo enviados

### 4. Teste o botão WhatsApp
- Após sucesso, click no botão deve abrir WhatsApp
- Verifique se o número está correto em `config.js`

### Debug de erros
- Verifique **Console** no DevTools para logs
- Se POST falhar, veja a resposta no Network
- A API precisa responder **200 OK** (ou será considerado erro)

---

## 🔗 Integrações prontas

### n8n / Zapier / Make
Configure `API_URL` como seu webhook. Exemplo:
```javascript
API_URL: 'https://hook.n8n.cloud/webhook/lead-capture'
```

### Seu backend próprio
Node.js / Express:
```javascript
app.post('/api/leads', (req, res) => {
  const data = req.body;
  // Salve no banco, envie email, etc.
  res.json({ success: true });
});
```

Python / Flask:
```python
@app.route('/api/leads', methods=['POST'])
def capture_lead():
    data = request.json
    # Salve no banco
    return {'success': True}
```

---

## 💡 Dicas

- **Sessão**: Um `sessionId` único é gerado por navegador (localStorage)
- **Tema**: Usuário pode alternar claro/escuro; é salvo localmente
- **Offline**: Funciona offline (dados não saem do navegador até envio)
- **Retry**: Se a API falhar, o botão de "Próxima etapa" permanece habilitado
- **CORS**: Sua API deve aceitar requests de `Access-Control-Allow-Origin: *` ou configurar CORS corretamente

---

## 📦 Deploy em 2 minutos

### Vercel
```bash
npm install -g vercel
vercel
```

### Netlify
```bash
npm install -g netlify-cli
netlify deploy
```

### GitHub Pages
```bash
git add .
git commit -m "Deploy lead-capture"
git push origin gh-pages
```

---

## 📝 Notas

- ✅ **Zero build**: Projeto funciona direto (HTML + CSS + JS)
- ✅ **Mobile-first**: Responsivo em celular, tablet e desktop
- ✅ **Privacy**: Dados são enviados direto para seu backend (não passam aqui)
- ✅ **Performance**: Rápido, sem frameworks pesados
- ❌ **Sem dependências NPM**: HTML puro

---

## 🐛 Suporte

Dúvidas ou melhorias? Verifique:
1. O `config.js` está correto?
2. Sua API responde com `200 OK` e `Content-Type: application/json`?
3. CORS está ativado na API?
4. O número de WhatsApp tem o formato correto (55 + DDD + número)?

**Boa captura! 🚀**
