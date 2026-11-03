# Nexus — a squad de agentes de IA para operação

Um agente unificado (**Nexus**) que reúne seis agentes de operação como *skills* de um único cérebro.
Ele monitora canais do Slack, filas de tickets no HubSpot, e-mails e um backoffice web, e age
dentro de regras explícitas (guardrails) e com poucos humanos no circuito.

> Este repositório é uma versão **sanitizada** do projeto real: não há credenciais, IDs internos,
> dados de clientes nem nomes de pessoas. Serve para mostrar a arquitetura e as decisões de design.

## O que o Nexus faz

| Módulo (ex-agente) | Função | Fonte de eventos |
|---|---|---|
| **Tommy** | Acompanha cancelamentos e recusas de reservas de sala | Canal do Slack alimentado por um bot |
| **Slackira** | Monitora erros de integração com um sistema de agenda e convida novos parceiros | Slack, Gmail, formulários |
| **WobaCoins** | Libera créditos promocionais a partir de tickets | Pipeline do HubSpot |
| **R Contact** | Descobre o contato certo de uma unidade a partir do Gmail | Perguntas em um canal |
| **Bookius** | Aprova ou recusa reservas pendentes conversando com o espaço no WhatsApp Web | Backoffice, WhatsApp Web, HubSpot |
| **Monitorius** | Observa os outros módulos, gera digest e relatório semanal e alimenta um painel | Todos os demais |

## Princípios de design

1. **Um agente, muitas skills.** Cada skill é um arquivo `SKILL.md` com gatilho, passos, saída e limites.
2. **Guardrails como código de primeira classe.** Regras do tipo "nunca contatar X" ou "teto de 15 envios por execução" ficam num documento único e valem para todos os módulos. Veja [docs/guardrails.md](docs/guardrails.md).
3. **Silêncio é a saída padrão.** O agente só fala quando algo muda a decisão de alguém.
4. **Alertas de infra e de negócio têm destinos diferentes.** Falha de agente vai por DM ao dono; assunto de negócio vai ao canal da operação.
5. **Estado durável fora do agente.** O loop não guarda memória própria; o cursor de leitura e os logs ficam em arquivos versionáveis.
6. **Local ou nuvem conforme a dependência.** Só conectores: nuvem. Precisa de navegador logado ou arquivos locais: local. Veja [docs/scheduling.md](docs/scheduling.md).

## Documentação

- [Arquitetura](docs/architecture.md)
- [Do Nexus ao super-agent e ao agente mãe](docs/super-agent-design.md)
- [Guardrails](docs/guardrails.md)
- [Agendamento: local × nuvem](docs/scheduling.md)
- [Os agentes](docs/agents.md)
- [Modelo de skill](examples/skill-template/SKILL.md)

## Estrutura

```
nexus-agent-squad/
├── docs/                 arquitetura, guardrails, agendamento, agentes
├── examples/
│   ├── skill-template/   modelo de SKILL.md
│   └── credentials.example.json
├── .env.example
└── .gitignore
```

## Como rodar

O projeto original roda dentro do Claude Code, com conectores (Slack, HubSpot, Gmail, Drive) e tarefas
agendadas. Para reproduzir:

1. Copie `.env.example` para `.env` e preencha com as suas chaves. **Nunca** faça commit do `.env`.
2. Crie uma pasta `skills/` e uma skill a partir do [modelo](examples/skill-template/SKILL.md).
3. Registre a rotina no agendador escolhido (local ou nuvem).

## Status

Projeto em uso interno. Notas de design e protótipo, não um produto empacotado.

## Autor

Matheus Ferreira.
