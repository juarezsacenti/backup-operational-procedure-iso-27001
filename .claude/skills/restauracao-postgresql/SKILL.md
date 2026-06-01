---
name: restauracao-postgresql
description: Conduz a execução assistida de uma restauração PostgreSQL — teste em ambiente isolado OU restauração emergencial — seguindo a IT de restauração PostgreSQL (§4.3/§4.4) e registrando a evidência no REG correspondente. Use ao testar ou executar a restauração de um backup PostgreSQL.
---

# Skill: Restauração assistida — PostgreSQL

Guia a execução passo a passo de uma restauração PostgreSQL, conforme a
`IT-...-POSTGRESQL` (§4.3 Restauração e §4.4 Teste). Os mesmos passos servem para **teste**
(ambiente isolado) e para **emergência** (produção, sob governança do PO §5).

## Guardrails (ler antes de qualquer comando)

1. **Confirme o alvo em voz alta.** Pergunte e confirme: é **teste** (sandbox isolado) ou
   **emergência** (produção)? Qual instância/host de destino? Restauração NUNCA deve
   sobrescrever a origem sem confirmação explícita.
2. **Prefira restaurar para uma instância nova/limpa.** Evite restaurar por cima de dados
   vivos; restaure para um destino isolado e só então promova, se aplicável.
3. **Nada destrutivo sem confirmação.** `DROP`/`--clean`/recriação de role só após o humano
   confirmar o alvo. Mostre o comando e peça OK antes de executar.
4. **Confidencialidade.** Não registre credenciais nem dados de negócio. Use placeholders.
5. **Autorização.** Restauração emergencial em produção exige a aprovação prevista no PO §5.

## Passos

### 1. Pré-condições (IT §4.3.1)
- Confirmar acessos/permissões e a ferramenta (`pg_restore`/`psql`, versão compatível).
- Verificar espaço em disco no destino.
- Localizar o backup a restaurar: data e **checksum/hash** (validar integridade antes).

### 2. Restauração (IT §4.3.2)
- Para dump custom/diretório: `pg_restore` para a base de destino `<base>` em `<host>`.
- Para dump SQL puro: `psql` aplicando o arquivo.
- Capturar logs da operação (sem segredos).

### 3. Validação pós-restauração (IT §4.3.3)
- Queries de sanidade e contagem de registros das tabelas-chave.
- Conferir versões/extensões/sequences quando relevante.

### 4. Rollback se falhar (IT §4.3.4)
- Descartar o destino restaurado; preservar a origem intacta; registrar a falha.

### 5. Se for TESTE (IT §4.4)
- Provisionar ambiente isolado (ex.: container/sandbox).
- Medir o tempo total vs. **RTO** definido na Política.
- Aplicar os critérios de aprovação/falha.

### 6. Registrar a evidência
- **Teste** → `REG-...-TESTE-RESTAURACAO` (data, item testado+hash, ambiente, executor,
  tempo vs. RTO, resultado, desvios, aprovação).
- **Emergência** → `REG-...-RESTAURACOES` (data, base, solicitante, motivo, item usado+hash,
  RTO real vs. alvo, resultado, validação, observações).

## Melhoria contínua
Após cada uso, anote no git o que faltou (passo ausente, validação que não pegou um caso) e
ajuste este skill e a IT correspondente.
