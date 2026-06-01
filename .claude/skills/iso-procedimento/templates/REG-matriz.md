# Registros e Matriz de Registro

> Template. Cada registro é preenchido a cada execução (planilha/tabela ou ferramenta de GRC).
> Conteúdo genérico; nenhum dado real de organização.

## Matriz de registro (vai para a Seção 6 do PO)

| Identificação do registro | Local de armazenamento | Tempo de retenção |
|---------------------------|------------------------|-------------------|
| `REG-<DEPTO>-<NNNN>-INVENTARIO` | | |
| `REG-<DEPTO>-<NNNN>-EXECUCAO` | | |
| `REG-<DEPTO>-<NNNN>-TESTE-RESTAURACAO` | | |
| `REG-<DEPTO>-<NNNN>-PLANO-TESTES` | | |
| `REG-<DEPTO>-<NNNN>-RESTAURACOES` | | |
| `REG-<DEPTO>-<NNNN>-INCIDENTES` | | |

> **Retenção dos registros ≠ retenção dos backups/ativos.** A retenção de cada registro é
> própria, ditada por conformidade/auditoria (p.ex. ≥ 1 ciclo de auditoria), e não segue a
> retenção operacional definida na Política.
>
> Se o processo não gerar registros, manter a seção e preencher com "N/A".

## Colunas sugeridas por registro (templates a preencher)

- **INVENTARIO** — ativo, tecnologia, ambiente, dono, tier, RPO/RTO, frequência, retenção, destino, criptografado?
- **EXECUCAO** — data/hora, ativo, tipo, tamanho, duração, checksum, status (fonte: automação)
- **TESTE-RESTAURACAO** — data, item testado (data+hash), ambiente, executor, tempo vs. RTO, resultado, desvios, aprovação
- **PLANO-TESTES** — calendário por tier + lista dos testes realizados vs. planejados
- **RESTAURACOES** — data, ativo, solicitante, motivo, item usado (data+hash), executor, RTO real vs. alvo, resultado, validação, observações
- **INCIDENTES** — data, ativo, falha, causa, ação corretiva, status, responsável
