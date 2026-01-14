# 🚨 Workflow n8n - Monitor de Preço do Bitcoin

## 📋 Descrição
Este workflow monitora o preço do Bitcoin e envia alertas por email e WhatsApp quando o preço se aproxima do valor mínimo dos últimos 3 anos (dentro de 10% do mínimo).

## 🔧 Componentes do Workflow

### 1. **Schedule Trigger**
- Executa a cada 6 horas
- Você pode ajustar para 1, 3, 12 ou 24 horas conforme preferir

### 2. **Get 3 Year Bitcoin History**
- Busca dados históricos de 3 anos (1095 dias) da API CoinGecko
- API gratuita, sem necessidade de chave
- Retorna preços diários em USD

### 3. **Analyze Price Data**
- Calcula o preço mínimo dos últimos 3 anos
- Calcula o preço médio do período
- Define threshold de alerta (10% acima do mínimo)
- Determina se deve enviar alerta

### 4. **IF Near Minimum?**
- Verifica se o preço está próximo do mínimo
- Se SIM: envia notificações
- Se NÃO: workflow termina

### 5. **Send Email Alert**
- Envia email formatado em HTML
- Inclui tabela com todos os dados relevantes

### 6. **Send WhatsApp Alert**
- Envia mensagem via CallMeBot API
- Formato texto simples otimizado para WhatsApp

## 🚀 Como Configurar

### Passo 1: Importar o Workflow
1. Abra o n8n
2. Clique em "Import from File"
3. Selecione o arquivo `bitcoin_monitor_workflow.json`

### Passo 2: Configurar Email (Gmail)

#### Opção A - Usar Gmail SMTP:
1. No nó "Send Email Alert", configure:
   - **Host:** smtp.gmail.com
   - **Port:** 587
   - **From Email:** seu-email@gmail.com
   - **To Email:** email-destino@gmail.com
   - **Username:** seu-email@gmail.com
   - **Password:** Senha de app do Gmail

#### Como criar senha de app Gmail:
1. Acesse: https://myaccount.google.com/security
2. Ative a verificação em 2 etapas
3. Vá em "Senhas de app"
4. Selecione "Email" e "Outro dispositivo"
5. Copie a senha de 16 dígitos gerada
6. Use esta senha no n8n

#### Opção B - Usar outro provedor de email:
Configure o nó SMTP com as credenciais do seu provedor.

### Passo 3: Configurar WhatsApp (CallMeBot)

1. **Ativar o CallMeBot no seu WhatsApp:**
   - Adicione o número +34 644 34 76 64 aos seus contatos
   - Envie a mensagem: `I allow callmebot to send me messages`
   - Você receberá sua API Key

2. **No nó "Send WhatsApp Alert", configure:**
   - **phone:** Seu número com código do país (ex: +5511999999999)
   - **apikey:** A chave que você recebeu do CallMeBot

### Passo 4: Ajustar Parâmetros (Opcional)

No nó "Analyze Price Data", você pode modificar:

```javascript
// Linha 15 - Alterar threshold de alerta
const threshold = minPrice * 1.10; // 1.10 = 10% acima do mínimo

// Opções:
// 1.05 = alerta quando 5% acima do mínimo (mais sensível)
// 1.15 = alerta quando 15% acima do mínimo (menos sensível)
// 1.20 = alerta quando 20% acima do mínimo
```

### Passo 5: Testar o Workflow

1. Clique em "Execute Workflow" para testar
2. Verifique se recebeu as notificações
3. Se funcionou, ative o workflow (toggle no topo)

## 📊 Dados Fornecidos

O alerta inclui:
- ✅ Preço atual do Bitcoin
- ✅ Preço mínimo dos últimos 3 anos
- ✅ Preço médio dos últimos 3 anos
- ✅ Porcentagem acima do mínimo
- ✅ Data e hora do alerta

## 🔄 Frequência de Execução

Configurado para rodar a cada **6 horas**. Você pode ajustar:

No nó "Schedule Trigger":
- **A cada 1 hora:** `hoursInterval: 1`
- **A cada 3 horas:** `hoursInterval: 3`
- **A cada 12 horas:** `hoursInterval: 12`
- **Uma vez por dia:** `hoursInterval: 24`

## ⚠️ Observações Importantes

1. **API CoinGecko:** Gratuita mas tem limite de requisições. Para 6 em 6 horas está dentro do limite.

2. **CallMeBot WhatsApp:** 
   - Gratuito
   - Requer ativação prévia
   - Mensagens podem demorar alguns minutos

3. **Threshold de 10%:** É configurável. Ajuste conforme sua estratégia de investimento.

4. **Dados históricos:** 3 anos (1095 dias) é um período robusto para análise de mínimos.

## 🛠️ Troubleshooting

### Email não chega:
- Verifique a senha de app do Gmail
- Confirme que a verificação em 2 etapas está ativa
- Verifique a pasta de spam

### WhatsApp não funciona:
- Confirme que enviou a mensagem de ativação corretamente
- Verifique se o número está no formato correto (+55...)
- Aguarde alguns minutos, pode haver delay

### Workflow não executa:
- Certifique-se de que o workflow está ATIVO (toggle verde)
- Verifique os logs de execução no n8n
- Teste manualmente primeiro

## 💡 Melhorias Sugeridas

Você pode expandir este workflow:
- Adicionar alertas para múltiplas criptomoedas
- Incluir análise de RSI ou MACD
- Enviar para Telegram ao invés de WhatsApp
- Salvar histórico em banco de dados
- Criar gráficos com os dados

## 📝 Licença

Workflow de uso livre. Modifique conforme suas necessidades!
