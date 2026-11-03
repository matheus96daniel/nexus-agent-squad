---
name: exemplo-monitor-canal
description: Varre um canal do Slack em busca de eventos novos e publica um resumo curto. Use quando o gatilho agendado disparar ou quando pedirem "varre o canal".
---

# Monitor de canal (modelo)

## Gatilho
- Cron: a cada 30 min, dias úteis, 08h–20h.
- Manual: "varre o canal".

## Entrada
- Canal de origem: `<CANAL_ORIGEM>`
- Estado: `state/cursor.json` com `ultimo_evento_processado`.

## Passos
1. Ler o cursor. Se estiver no futuro ou for mais antigo que o último registrado, **parar e avisar o dono** (regressão).
2. Buscar mensagens depois do cursor.
3. Descartar o que o filtro rejeita (bot errado, duplicata, fora de horário).
4. Classificar cada evento e agrupar por tipo.
5. Se não há nada novo, **não postar nada**.
6. Publicar o resumo no destino de negócio. Falhas de infra vão por DM ao dono.
7. Atualizar o cursor **depois** da publicação bem-sucedida.

## Saída
Assinatura da skill, no máximo 5 linhas, números só se existirem nos dados.

## Limites (guardrails)
- Teto de `<N>` mensagens por execução; acima disso, não enviar e avisar o dono.
- Nunca contatar pessoas da lista de não contato.
- Nunca imprimir tokens ou dados pessoais.
- Erro 401: parar e avisar, sem repetir em loop.
