# Weni Agent — n8n Workflow

Automação n8n (arquivado, não está mais em uso) que implementa um agente de IA de atendimento via WhatsApp/webhook para uma loja com integração VTEX, com as seguintes capacidades:

- Recebe mensagens via webhook e mantém sessão/histórico de conversa (Postgres)
- Busca produtos, adiciona itens ao carrinho e finaliza/cancela pedidos via sub-workflows e integração VTEX
- Calcula a loja física mais próxima do cliente por distância (fórmula de Haversine)
- Verifica horário de funcionamento e disponibilidade de entrega no mesmo dia
- Consulta status de entrega em um sistema externo

## Stack

- n8n + `@n8n/n8n-nodes-langchain` (AI Agent)
- LLM: Groq (`openai/gpt-oss-20b`) como modelo principal, Gemini como alternativa
- Memória de conversa: PostgreSQL
- E-commerce: VTEX Checkout API

## Status

Projeto descontinuado — publicado como referência/portfólio.

## Observações

Este export foi sanitizado antes da publicação: credenciais, tokens, URLs específicas de loja/API e dados de negócio (lista de lojas, coordenadas) foram substituídos por placeholders (`SUBSTITUA_PELO_...`). Para reutilizar, é necessário:

1. Recriar as credenciais no n8n (VTEX, Postgres, Groq, Gemini) e apontar os nós para elas
2. Substituir a URL da API de entrega e o token em `HTTP Request`
3. Substituir a URL da loja VTEX no nó `Carrinho`
4. Preencher a lista real de lojas (nome/lat/lon) no nó `Code Tool`
5. Recriar os sub-workflows referenciados (`Sub - Verificar Entrega`, `Sub - Buscar Produtos`, `Sub - Finalizar Pedido`, `Sub - Cancelar Pedido`) e atualizar os IDs
