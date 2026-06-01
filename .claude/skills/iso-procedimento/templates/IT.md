# IT-<DEPTO>-<NNNN>-<TECNOLOGIA> — Instrução de Trabalho

> Template. Aqui ficam comandos, scripts e checklists técnicos. Use placeholders genéricos
> (`<base>`, `<ambiente>`, `<bucket>`); nenhum dado real de organização.

## 1. Objetivo
Propósito da IT e resultado esperado.

## 2. Abrangência
Tecnologia/versões cobertas e o **público-alvo** (quem executa).

## 3. Responsabilidades
Cargos/áreas que executam a IT (sucinto).

## 4. Instrução de trabalho
- 4.1 Pré-requisitos (acessos, ferramentas, variáveis de ambiente, permissões)
- 4.2 Configuração da automação (referência): onde está definida (console/IaC), agendamento,
  retenção; como verificar que rodou e está íntegro. *(Não documentar execução manual quando
  o processo for automático.)*
- 4.3 Recuperação/Restauração (mesmos passos para teste E emergência)
  - 4.3.1 Pré-condições
  - 4.3.2 Passo a passo numerado
  - 4.3.3 Validação pós-execução
  - 4.3.4 Rollback em caso de falha
- 4.4 Teste (ambiente isolado; executa 4.3; mede RTO; critérios de aprovação/falha)
- 4.5 Erros comuns e troubleshooting

## 5. Matriz de registro
| Identificação do registro | Local de armazenamento | Tempo de retenção |
|---------------------------|------------------------|-------------------|
| `REG-<DEPTO>-<NNNN>-<TIPO>` | | |

> "N/A" se a IT não gerar registros.
