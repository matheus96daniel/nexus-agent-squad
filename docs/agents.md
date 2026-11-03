# Os agentes

Cada agente virou um conjunto de skills do Nexus. Abaixo, o papel e as decisões de design de cada um.

## Tommy — cancelamentos e recusas
- Lê um canal alimentado por um bot e classifica cada cancelamento (empresa, espaço, motivo).
- **Estado durável:** guarda o último evento processado para não repetir e detectar buracos.
- Entrega relatório semanal e recortes sob demanda (por empresa, cidade, motivo, período).
- **Decisão:** parou de mandar mensagens a pessoas; reporta só a um dono e a um canal.

## Slackira — integrações
- Detecta erros reincidentes (mesmo espaço três vezes ou mais) e bypass em massa.
- Monta rascunho de e-mail ao espaço quando uma integração está desativada.
- Acompanha o funil de novos parceiros que preenchem um formulário.

## WobaCoins — créditos promocionais
- Varre tickets de um pipeline, localiza o usuário e prepara o comando de liberação.
- **Guardrails:** token nunca impresso; 401 não é repetido em loop; campo ausente fica nulo, nunca inventado.
- Gera relatório de impacto: créditos liberados e tempo operacional poupado.

## R Contact — descoberta de contato
- Recebe uma pergunta ("qual o contato da unidade X?") e responde com o e-mail, as evidências e, se houver dúvida, candidatos.
- Fica quieto quando não há pergunta pendente.

## Bookius — reservas de sala
- Varre a fila de pendentes, agrupa por espaço, pergunta ao espaço no WhatsApp Web e aprova ou recusa conforme a resposta.
- Trata primeiro as reservas de hoje e relê a fila ao fim de cada bloco.
- **LGPD:** nunca passa telefone nem documento do cliente final ao espaço.
- Tem lista de espaços que só humanos contatam.

## Monitorius — observabilidade
- Health check de todos os módulos, digest diário, relatório semanal e alerta crítico fora de cadência.
- Mantém um painel web com indicadores semanais.
- Princípio: **vitória silenciosa**.
