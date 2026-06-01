---
name: restauracao-storage-bucket
description: Conduz a execução assistida de uma restauração de Storage Bucket (object storage, ex.: S3/GCS) — teste em destino isolado OU restauração emergencial — seguindo a IT de restauração Storage Bucket (§4.3/§4.4) e registrando a evidência no REG correspondente. Use ao testar ou executar a restauração de objetos de um bucket.
---

# Skill: Restauração assistida — Storage Bucket

Guia a recuperação de objetos de um bucket de object storage (S3/GCS/equivalente), conforme
a `IT-...-STORAGE-BUCKET` (§4.3 Restauração e §4.4 Teste). Serve para **teste** (destino
isolado) e **emergência** (produção, sob governança do PO §5).

## Guardrails (ler antes de qualquer comando)

1. **Confirme o alvo em voz alta.** É **teste** (bucket/prefixo isolado) ou **emergência**
   (bucket de produção)? Qual bucket/prefixo de destino? Nunca sobrescreva o bucket de origem
   sem confirmação explícita.
2. **Prefira restaurar para um bucket/prefixo novo.** Restaure para `<bucket-destino>` e só
   promova depois, se aplicável. Cuidado com `--delete` em sync (remove no destino o que não
   existe na origem) — só após confirmação.
3. **Versionamento.** Se o bucket tem versionamento/lock de objeto, prefira restaurar a versão
   correta do objeto a sobrescrever — evita perda irreversível.
4. **Nada destrutivo sem confirmação.** Mostre o comando e peça OK antes de executar.
5. **Confidencialidade.** Não registre credenciais/keys nem conteúdo dos objetos.
6. **Autorização.** Restauração emergencial em produção exige aprovação prevista no PO §5.

## Passos

### 1. Pré-condições (IT §4.3.1)
- Confirmar credenciais/permissões (somente o necessário) e a CLI (`aws s3`/`gsutil`).
- Identificar a fonte da cópia: snapshot/versão/réplica, com data e **hash** quando houver.

### 2. Restauração (IT §4.3.2)
- Restaurar versão de objeto (versionamento) **ou** copiar/sincronizar de `<bucket-origem>`
  para `<bucket-destino>`/`<prefixo>` (ex.: `aws s3 sync` / `gsutil rsync`, sem `--delete`
  por padrão).
- Capturar logs (sem segredos).

### 3. Validação pós-restauração (IT §4.3.3)
- Conferir contagem/listagem de objetos, tamanhos e checksums (ETag/CRC) vs. esperado.
- Amostragem de objetos-chave.

### 4. Rollback se falhar (IT §4.3.4)
- Descartar o destino restaurado; preservar origem; registrar a falha.

### 5. Se for TESTE (IT §4.4)
- Usar bucket/prefixo isolado; medir tempo vs. **RTO**; aplicar critérios de aprovação/falha.

### 6. Registrar a evidência
- **Teste** → `REG-...-TESTE-RESTAURACAO`.
- **Emergência** → `REG-...-RESTAURACOES`.

## Melhoria contínua
Após cada uso, anote no git o que faltou e ajuste este skill e a IT correspondente.
