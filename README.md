# Lazoos.me - E-commerce Intelligence & Automation

<p align="center">
  <img src="https://img.shields.io/badge/Status-Em%20Produ%C3%A7%C3%A3o-green" alt="Status">
  <img src="https://img.shields.io/badge/Stack-Django%20%7C%20React%20%7C%20SQL%20Server-blue" alt="Stack">
</p>

## 🔗 Sobre o Projeto
O **Lazoos.me** é uma plataforma de e-commerce completa desenvolvida para automatizar processos de venda e otimizar a comunicação com o cliente. Diferente de soluções prontas, este projeto foi construído do zero para suportar integrações complexas de pagamento e fluxos de dados personalizados.

> **Nota:** Por questões de propriedade intelectual, o código-fonte deste projeto é mantido em um repositório privado. Esta documentação visa detalhar as decisões técnicas e a arquitetura do sistema.

---

## 🛠️ Tecnologias e Ferramentas
* **Frontend:** React (Interface responsiva e dinâmica).
* **Backend:** Python / Django (Processamento de regras de negócio e APIs).
* **Banco de Dados:** SQL Server (Modelagem relacional e integridade de dados).
* **Pagamentos:** Integração com APIs do **Mercado Pago** e **Stripe**.
* **Comunicação:** SMTP para e-mails transacionais automatizados.

---

## 🏗️ Arquitetura e Fluxo de Integração
O sistema utiliza uma arquitetura baseada em eventos para garantir que o status do pedido seja atualizado em tempo real via Webhooks.

```mermaid
sequenceDiagram
    participant U as Usuário
    participant F as Frontend (React)
    participant B as Backend (Django)
    participant DB as SQL Server
    participant MP as API Mercado Pago
    participant E as Serviço de E-mail

    U->>F: Finaliza Compra
    F->>B: Requisição de Checkout
    B->>MP: Criar Preferência de Pagamento
    MP-->>B: Retorna URL de Pagamento
    B-->>F: Envia URL ao Usuário
    U->>MP: Realiza Pagamento
    MP-->>B: Notificação Webhook (Pagamento Aprovado)
    B->>DB: Atualiza Status do Pedido
    B->>E: Dispara E-mail de Confirmação (Automático)
    E-->>U: Recebe Confirmação de Compra
