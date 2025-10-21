# 🧪 Indie Comments - Guia de Testes e Configuração

## 📋 Status Atual do Projeto

✅ **Backend:** NocodeBackEnd configurado com instância `41300_indie_comments_v2`
✅ **Usuário de Teste:** Criado (ID: 1) - `renato.mugrabi@gmail.com` / `12345678`
✅ **Arquivos:** Todos os componentes criados e integrados
✅ **Segurança:** MVP funcional (comparação direta de senha)

## 🚀 Configuração e Testes Imediatos

### **1. Verificar Servidores Locais**

```bash
# Terminal 1: Dashboard Administrativo
cd painel && python -m http.server 8000
# Acesse: http://localhost:8000

# Terminal 2: Arquivos do Widget
cd widget && python -m http.server 8001

# Terminal 3: Landing Page + Widget Demo
python -m http.server 3000
# Acesse: http://localhost:3000
```

### **2. Credenciais de Teste**

- **Email:** `renato.mugrabi@gmail.com`
- **Senha:** `12345678`
- **Usuário ID:** 1
- **Plano:** free

### **3. Teste do Dashboard**

1. Acesse `http://localhost:8000`
2. Faça login com as credenciais acima
3. Deve aparecer: "Olá, Renato!"
4. Clique em "Adicionar Novo Site"
5. Preencha:
   - URL: `http://localhost:3000`
   - Nome: `Landing Page Demo`
6. Clique "Gerar Código"
7. Copie o código embed gerado

### **4. Teste do Widget na Landing Page**

1. Acesse `http://localhost:3000`
2. Role até a seção "Teste o Widget de Comentários"
3. O widget deve carregar automaticamente
4. Preencha o formulário de comentário:
   - Nome: `Test User`
   - Email: `test@example.com`
   - Mensagem: `Este é um teste do widget!`
5. Clique "Enviar Comentário"
6. Deve aparecer: "✅ Comentário enviado para aprovação!"

### **5. Teste de Moderação**

1. Volte ao dashboard (`http://localhost:8000`)
2. Deve aparecer uma seção de comentários pendentes (se implementada)
3. Ou verifique via API:
```bash
curl "https://openapi.nocodebackend.com/read/comments?Instance=41300_indie_comments_v2&visible=false"
```

## 🔧 APIs para Testes Diretos

### **Criar Site de Teste**
```bash
curl -X POST "https://openapi.nocodebackend.com/create/sites?Instance=41300_indie_comments_v2" \
  -H "Content-Type: application/json" \
  -d '{
    "user_id": 1,
    "site_url": "http://localhost:3000",
    "site_name": "Landing Page Demo",
    "api_key": "demo-key-123"
  }'
```

### **Verificar Comentários Pendentes**
```bash
curl "https://openapi.nocodebackend.com/read/comments?Instance=41300_indie_comments_v2&visible=false"
```

### **Aprovar Comentário (substitua {ID} pelo ID real)**
```bash
curl -X PUT "https://openapi.nocodebackend.com/update/comments/{ID}?Instance=41300_indie_comments_v2" \
  -H "Content-Type: application/json" \
  -d '{"visible": true}'
```

## 📁 Estrutura de Arquivos

```
indie_comments_v03/
├── index.html              # Landing page com demo do widget
├── TESTING.md             # Este arquivo
├── README.md              # Documentação completa
├── painel/                # Dashboard administrativo
│   ├── index.html
│   ├── css/style.css
│   └── js/
│       ├── api.js         # API client (login ajustado para MVP)
│       └── app.js
├── widget/
│   └── indie_comments.js  # Widget principal
└── [arquivos de documentação]
```

## 🔒 Notas de Segurança (MVP)

- **Login:** Comparação direta de senha (temporário)
- **Comentários:** Vão para moderação (`visible=false`)
- **IP:** Coletado via ipify.org
- **Cache:** Sites em cache por 5 minutos

Para produção, implementar:
- bcrypt no backend
- JWT tokens
- Rate limiting mais robusto

## 🎯 Próximos Passos Após Testes

### **Fase 1: Testes Locais ✅**
- [x] Servidores rodando
- [x] Login funcionando
- [x] Widget carregando
- [x] Comentários sendo enviados

### **Fase 2: Deploy**
- [ ] Hospedar landing page (Netlify/Vercel)
- [ ] Hospedar dashboard (Netlify/Vercel)
- [ ] Hospedar widget JS (CDN)
- [ ] Atualizar URLs nos arquivos

### **Fase 3: Produção**
- [ ] Configurar Buy Me a Coffee
- [ ] Implementar autenticação segura
- [ ] Adicionar analytics
- [ ] Testes com usuários reais

## 🐛 Troubleshooting

### **Widget não carrega**
```javascript
// Verificar no console do navegador
console.log('Widget script loaded');

// Se erro 404:
# Verificar se widget/indie_comments.js existe
ls -la widget/
```

### **Login falha**
```javascript
// Verificar credenciais
// Email: renato.mugrabi@gmail.com
// Senha: 12345678 (comparação direta)
```

### **Comentários não aparecem**
```bash
# Verificar se thread foi criado
curl "https://openapi.nocodebackend.com/read/threads?Instance=41300_indie_comments_v2"

# Verificar comentários
curl "https://openapi.nocodebackend.com/read/comments?Instance=41300_indie_comments_v2"
```

## 📞 Suporte

Para dúvidas:
1. Verifique os logs do console do navegador (F12)
2. Teste as APIs diretamente com cURL
3. Verifique se os servidores locais estão rodando
4. Consulte o README.md para detalhes técnicos

---

**Status:** ✅ Pronto para testes locais
**Última atualização:** 21/10/2025