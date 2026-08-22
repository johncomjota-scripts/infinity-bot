# 🚀 Guia de Integração: Webhooks do Mercado Pago (Checkout Pro)

Este documento resume o funcionamento e a configuração das notificações automáticas (**Webhooks**) para processamento de pagamentos via Mercado Pago, conforme a [documentação oficial](https://www.mercadopago.com.br/developers/pt/docs/checkout-pro/payment-notifications).

---

## 📌 O que são Webhooks?
Os Webhooks são métodos que permitem aos servidores do Mercado Pago enviar informações em tempo real quando ocorre um evento específico (como a aprovação de um pagamento). 
* **Vantagem:** O seu sistema não precisa realizar consultas contínuas (polling), otimizando a comunicação e reduzindo a carga nos servidores através de solicitações HTTP POST.

---

## ⚙️ Como Configurar (Passo a Passo)

1. **Acesse o Painel:** Vá até o seu Painel de Desenvolvedor do Mercado Pago e selecione a sua aplicação integrada ao Checkout Pro.
2. **Configurar Webhooks:** No menu lateral esquerdo, clique em **Webhooks** > **Configurar notificações**.
3. **Adicionar URL:** Insira a sua URL HTTPS de produção (ou o link público do seu túnel de testes, como o Ngrok).
4. **Selecionar Eventos:** Marque a opção **Pagamentos** (`payment`) para receber os avisos de criação e atualização de pagamentos.
5. **Salvar:** Clique em **Salvar configuração**. Isso gerará uma chave de assinatura secreta exclusiva.

---

## 🔒 Segurança e Validação de Origem
Para garantir que as requisições recebidas pelo seu servidor são legítimas e vindas diretamente do Mercado Pago, é importante validar o cabeçalho **`x-signature`** enviado nas solicitações:

* O SDK oficial do Mercado Pago oferece utilitários de validação baseados em HMAC (como o `WebhookSignatureValidator`) para autenticar cada notificação.
