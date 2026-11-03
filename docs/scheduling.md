# Agendamento: local × nuvem

| Precisa de... | Roda em |
|---|---|
| Só conectores (Slack, HubSpot, Drive, Gmail) | **Nuvem**: roda com o app fechado |
| Navegador logado ou arquivos e variáveis locais | **Local**: só roda com o app aberto |

## Exemplos de cadência

| Rotina | Cadência | Onde |
|---|---|---|
| Ronda de reservas pendentes | a cada 10–15 min, horário comercial | Local (navegador logado) |
| Monitor de cancelamentos | a cada 30 min, horário comercial | Local |
| Monitores de integração | de hora em hora, em minutos escalonados | Nuvem |
| Digest matinal | dia útil, início da manhã | Nuvem |
| Relatório semanal | segunda-feira, manhã | Nuvem |
| Sincronização do painel | de hora em hora | Local |

## Lições

- **Escalone os minutos** das rotinas de nuvem para não colidirem.
- **Duas rotinas para o mesmo evento duplicam a ação.** Mantenha um único dono por evento.
- **Antes de declarar "agente parado"**, confira os dois agendadores.
- **Tarefas pausadas não são apagadas**; viram documentação do que já foi tentado.
- **Segredo não vai no prompt da rotina.** Use variável de ambiente.
