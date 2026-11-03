# Do Nexus ao super-agent e ao agente mãe

Inspirado no desenho "Super-agent" (DeepSeek Harness, *Exploring Super-agent Design*, nov/2026): um agente
sempre ativo que recebe eventos de vários canais e divide o trabalho em tarefas paralelas.

## Mapa conceitual

| Super-agent | Nexus hoje | Próximo passo |
|---|---|---|
| Filtro (regras + LLM) | Janelas de horário, cursores de estado, canais permitidos | Filtro explícito com classificação "agir / ignorar" |
| Router que nunca executa | O Nexus escolhe a skill e assina a saída | Separar o roteador dos executores |
| Workers com contexto próprio | Skills rodando em sessões separadas | Um worker por tarefa, com estado persistido |
| Prompt pequeno, links para o resto | IDs e ponteiros para arquivos de contexto | Cada item carrega os IDs dos itens relacionados |
| Jobs longos não travam o chat | Rotinas agendadas em segundo plano | Resultado volta como nova mensagem |
| Watchdog separado | Monitorius | Torná-lo independente do loop principal |

## Ligação com um agente mãe

O Nexus é o **agente de setor**. Para plugá-lo a um agente mãe da empresa, a fronteira é um contrato simples:

```
mãe  →  Nexus : { tarefa, prioridade, contexto_ids[], prazo }
Nexus →  mãe  : { status, resumo, artefatos[], pendências[] }
```

Regras da fronteira:

1. **A mãe delega objetivos, não passos.** O Nexus decide qual skill usar.
2. **Guardrails do setor são soberanos.** A mãe não pode pedir algo que o Nexus proíbe; ela recebe uma recusa com motivo.
3. **Alertas de infra sobem à mãe, não aos canais de negócio.**
4. **Mínimo de dados.** Só IDs e resumos cruzam a fronteira. Dados pessoais ficam no setor.
5. **Um dono por tarefa.** Follow-ups da mesma conversa voltam ao mesmo worker.

## Questões em aberto

- Memória de longo prazo compartilhada entre setor e mãe.
- Quando dividir o roteador por volume.
- Segurança: um agente comprometido não deve alcançar as máquinas de outros setores.
