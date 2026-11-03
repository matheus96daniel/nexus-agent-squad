# Guardrails

Regras que valem para todos os módulos. Foram escritas depois de incidentes reais, por isso são específicas.

## Gerais
- Nunca postar senha, token, documento pessoal ou dado sensível em canal ou log.
- Nenhum módulo fala com cliente final. A squad é interna e B2B.
- Nenhuma migração destrutiva sem confirmação humana.
- Nenhum módulo apaga arquivo nem altera código de outro módulo sem aprovação.
- Planilhas mantidas por outra pessoa são somente leitura.
- Análise preditiva com menos de 30 dias de dados é rotulada "amostra insuficiente".
- Relatórios semanais só dentro da janela definida.

## Padrões reutilizáveis

| Padrão | Exemplo |
|---|---|
| **Janela de silêncio** | Só disparar mensagens em dias úteis, de manhã a noite |
| **Teto por execução** | Mais de N mensagens numa rodada: não envia nada e avisa o dono |
| **Lista de não contato** | Pessoas e grupos que nunca recebem mensagem automática |
| **Parar em 401** | Erro de autenticação: não repetir em loop, avisar o dono |
| **Não inventar números** | Dado ausente significa campo omitido, nunca estimado |
| **Canal único de relatório** | Todo relatório vai a um canal; canais legados são proibidos |
| **Infra ≠ negócio** | Falha de agente por DM ao dono; assunto de negócio no canal |
| **Na dúvida, escale** | Categoria incerta é tratada como operacional |
| **Vitória silenciosa** | Silêncio é a saída padrão |

## Por que explícito

Um agente autônomo erra por excesso de iniciativa, não por falta. Cada regra acima corta uma classe de erro
(spam, vazamento, loop, alucinação de número) e pode ser testada em revisão de código.
