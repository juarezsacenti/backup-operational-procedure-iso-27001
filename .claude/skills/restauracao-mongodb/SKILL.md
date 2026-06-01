---
name: restauracao-mongodb
description: Conduz a execução assistida de uma restauração MongoDB — teste em ambiente isolado OU restauração emergencial — seguindo a IT de restauração MongoDB (§4.3/§4.4) e registrando a evidência no REG correspondente. Use ao testar ou executar a restauração de um backup MongoDB.
---

# Skill: Restauração assistida — MongoDB

Guia a execução passo a passo de uma restauração MongoDB, conforme a `IT-...-MONGODB`
(§4.3 Restauração e §4.4 Teste). Os mesmos passos servem para **teste** (ambiente isolado) e
para **emergência** (produção, sob governança do PO §5).

## Guardrails (ler antes de qualquer comando)

1. **Confirme o alvo em voz alta.** É **teste** (sandbox) ou **emergência** (produção)? Qual
   cluster/host e banco de destino? Nunca sobrescreva a origem sem confirmação explícita.
2. **Prefira restaurar para um cluster/banco novo.** Cuidado redobrado com `--drop`, que
   apaga coleções no destino antes de restaurar — só após confirmação do humano.
3. **Nada destrutivo sem confirmação.** Mostre o comando e peça OK antes de executar.
4. **Confidencialidade.** Não registre credenciais (connection strings) nem dados de negócio.
5. **Autorização.** Restauração emergencial em produção exige aprovação prevista no PO §5.

## Passos

### 1. Pré-condições (IT §4.3.1)
- Confirmar acessos/roles e a ferramenta (`mongorestore`, versão compatível).
- Verificar espaço no destino.
- Localizar o dump (data + **checksum/hash**) e validar integridade.

### 2. Restauração (IT §4.3.2)
- `mongorestore` para o destino `<host>`/`<base>` (atenção a `--nsInclude`/`--drop`).
- Capturar logs (sem segredos).

### 3. Validação pós-restauração (IT §4.3.3)
- Contagem de documentos das coleções-chave; checagem de índices.
- Consultas de sanidade.

### 4. Rollback se falhar (IT §4.3.4)
- Descartar o destino restaurado; preservar a origem; registrar a falha.

### 5. Se for TESTE (IT §4.4)
- Provisionar ambiente isolado; medir tempo vs. **RTO**; aplicar critérios de aprovação/falha.

### 6. Registrar a evidência
- **Teste** → `REG-...-TESTE-RESTAURACAO`.
- **Emergência** → `REG-...-RESTAURACOES`.

## Melhoria contínua
Após cada uso, anote no git o que faltou e ajuste este skill e a IT correspondente.
