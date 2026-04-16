# Luís Henrique Ávila — Currículo Online

[![Website](https://img.shields.io/badge/Website-Online-blue?style=flat-square)](https://seu-dominio.com)  
[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Deployed-green?style=flat-square)](https://github.com/seu-usuario/lead-capture-system)  
[![Cloudflare](https://img.shields.io/badge/Cloudflare-Hosted-orange?style=flat-square)](https://seu-dominio.com)

Currículo interativo e responsivo de Luís Henrique Ávila, profissional com experiência em suporte técnico, automação e análise de dados. Desenvolvido com HTML, CSS e JavaScript puro, otimizado para impressão em PDF e visualização web.

---

## 🚀 Sobre Mim

Profissional com mais de 5 anos de experiência em Suporte Técnico, dashboards e automação. Especialista em Python, Node.js, SQL e integração com Google Sheets. Foco em soluções que entregam resultados mensuráveis e reduzem retrabalho.

**Especialidades:**
- Suporte Técnico e Manutenção de Computadores
- Desenvolvimento de Dashboards e KPIs
- Automação de Processos e Integração de Sistemas
- Análise de Dados e Relatórios

---

## 💼 Experiência Profissional

### Phoenix Connect (2025 – 2026)
- Manutenção de computadores
- Suporte técnico aos usuários
- Criação de painéis de desempenho

### JH Prestadora de Serviços LTDA (2024 – 2025)
- Manutenção de computadores
- Suporte técnico aos usuários
- Criação de painéis de desempenho

### ASS Prestação de Serviços de Apoio ADMIN (2022 – 2024)
- Manutenção de computadores
- Suporte técnico aos usuários
- Criação de painéis de desempenho

### Grupo Panvel Distribuidora de Medicamentos (2015 – 2021)
- Rotinas logísticas completas: recebimento, separação, controle de estoques e auditoria

### Hospital Militar de Área de Porto Alegre (Exército Brasileiro) (2013 – 2014)
- Condução e cuidado de viaturas
- Suporte às operações logísticas

### Secretaria Estadual da Saúde (2012 – 2013)
- Estágio em rotinas administrativas e acompanhamento de processos internos

---

## 🛠️ Habilidades Técnicas

- **Linguagens:** Python, Node.js, SQL, HTML, CSS, JavaScript
- **Banco de Dados:** SQLite, Google Sheets API
- **Automação:** Bots, Integração de Sistemas
- **Relatórios:** Dashboards, KPIs
- **Suporte:** Manutenção Técnica, Assistência a Usuários
- **Outros:** Modelagem de Dados, Consultas SQL

---

## 🎓 Formação

- **Análise e Desenvolvimento de Sistemas** — ULBRA (Cursando)

---

## 📞 Contato

- **Email:** lhavila@outlook.com.br
- **Telefone:** (51) 99611-0749
- **Localização:** Guaíba, RS

---

## 🌐 Visualizar Currículo

Acesse o currículo online: [https://seu-dominio.com](https://seu-dominio.com)

### Como Visualizar Localmente
1. Clone o repositório:
   ```bash
   git clone https://github.com/seu-usuario/lead-capture-system.git
   cd lead-capture-system
   ```

2. Abra o `index.html` no navegador ou use um servidor local:
   ```bash
   python -m http.server 8000
   # Acesse: http://localhost:8000
   ```

### Gerar PDF
No navegador, clique em "Gerar PDF" para imprimir ou salvar como PDF.

---

## 🏆 Destaques

- **Bot de Relatórios:** Integração via WhatsApp com Google Sheets e SQLite para geração automática de KPIs e redução de tempo em análises.
- **Responsivo:** Design adaptável para desktop e mobile.
- **Impressão Otimizada:** Estilos específicos para geração de PDF profissional.

---

## 📄 Licença

Este projeto é pessoal e não possui licença específica. Sinta-se à vontade para usar como referência.

---

*Desenvolvido com ❤️ por Luís Henrique Ávila*

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
