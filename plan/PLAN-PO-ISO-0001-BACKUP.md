# Plano: Procedimento Operacional de Backup — ISO 27001:2022 Controle 8.13

## Contexto

O controle **ISO 27001:2022 8.13 — Backup das informações** exige que:
> Cópias de backup de informações, software e sistemas sejam mantidas e testadas regularmente de acordo com a política específica por tema acordada sobre backup.

Este plano descreve como construir o conjunto documental que implementa o controle 8.13, **separando claramente as quatro camadas da pirâmide documental da ISO 27001** e produzindo o documento principal `PO-ISO-0001-BACKUP.md` mais as Instruções de Trabalho (IT) e Registros (REG) vinculados.

---

## Princípio orientador: separação das camadas documentais

O erro mais comum em procedimentos de backup é misturar, num único documento, decisões de política, processo de gestão, execução técnica e evidências. Isso torna o documento pesado, difícil de manter (qualquer mudança de comando obriga a re-aprovar o procedimento inteiro) e confuso em auditoria. Este plano evita isso desde a origem:

| Camada | Pergunta que responde | Onde fica | Estabilidade |
|--------|----------------------|-----------|--------------|
| **Política** (tema-específica, exigida pelo 8.13) | *O que* a organização decide (tiers, frequência, retenção, criptografia) | **Seção** dentro do `PO` | Muda raramente (decisão de gestão) |
| **Procedimento Operacional (PO)** | *Como gerir* o ciclo de backup/restauração (papéis, monitoramento, falhas, escalonamento, revisão) | `PO-ISO-0001-BACKUP.md` | Estável |
| **Instrução de Trabalho (IT)** | *Como executar* a tarefa técnica (comandos, scripts, passo-a-passo) | `IT-ISO-0001-{TECNOLOGIA}.md` | Muda com versões/ferramentas |
| **Registro (REG)** | *Qual a evidência* produzida (inventário, logs, relatórios, listas) | `REG-ISO-0001-{TIPO}.md` | Preenchido a cada execução |

> **Regra prática:** se é uma *decisão* → Política (seção do PO). Se é *gestão do processo* → PO. Se tem *comando ou passo técnico* → IT. Se é *algo a preencher/assinar/listar* → Registro.

### Convenção de nomenclatura

Formato: **`<tipo>-<departamento>-<número>-<nome>`**

| Campo | Significado |
|-------|-------------|
| `<tipo>` | Tipo do documento: `PO`, `IT`, `REG` |
| `<departamento>` | Área responsável (ex.: `ISO`) |
| `<número>` | **Sequência própria de cada tipo** — independente; **não** é o mesmo número do PO |
| `<nome>` | Tema/identificação do documento |

| Tipo | Exemplo |
|------|---------|
| Procedimento Operacional | `PO-ISO-0001-BACKUP.md` |
| Instrução de Trabalho | `IT-ISO-0001-POSTGRESQL.md` |
| Registro/template | `REG-ISO-0001-INVENTARIO.md` |

> **Importante:** cada tipo tem sua própria contagem (o `0001` da IT não tem relação com o `0001` do PO). A ligação entre IT/REG e seu PO é feita por **referência cruzada explícita** dentro dos documentos (seções "Referências"/"Documentos relacionados"), nunca pelo número.

---

## Etapa 0 — Levantamento do estado atual (AS-IS) **[fazer primeiro]**

> ### ⚠️ Princípio anti-viés
> Nesta etapa a IA **conduz o levantamento com perguntas abertas e neutras** e apenas **registra** as respostas. **Não** propõe frequências, tiers, retenção ou ferramentas "ideais" — isso induziria a resposta e mascararia a realidade da empresa. Valores de referência e boas práticas entram **somente na Etapa 1 (GAP)**, sempre marcados como *recomendação*, nunca como *estado atual*.
>
> Formato sugerido: a IA faz uma pergunta aberta por vez (ou em blocos curtos), sem listar opções pré-definidas, e transcreve a resposta literal para o `REG-ISO-0001-INVENTARIO` e para uma ata de levantamento.

Roteiro de perguntas abertas (sem sugerir respostas):

**A. Inventário e topologia**
- [ ] Quais bancos de dados e sistemas existem? Onde rodam (cloud, on-prem, gerenciado)?
- [ ] Quais ambientes existem (produção, homologação, dev)? Quem é o dono de cada base?

**B. Como o backup é feito hoje**
- [ ] Existe backup hoje? De quais bases/sistemas? De quais não existe?
- [ ] Como o backup é disparado e com qual ferramenta? Quem executa e quem acompanha?
- [ ] Com que frequência ocorre? Quem definiu essa frequência e por quê?

**C. Armazenamento e proteção**
- [ ] Onde o backup é armazenado? Existe cópia em local remoto/separado do principal?
- [ ] O backup é criptografado (em trânsito e/ou em repouso)? Quem detém as chaves?

**D. Retenção**
- [ ] Por quanto tempo os backups são guardados? Quem definiu esse prazo? Há exigência legal/contratual conhecida?

**E. Restauração**
- [ ] Já foi necessário restaurar dados de verdade? O que aconteceu, quanto tempo levou, deu certo?
- [ ] O passo a passo de restauração está documentado em algum lugar hoje?

**F. Teste de restauração**
- [ ] Já se testou restaurar um backup (fora de uma emergência real)? Com que frequência? Há evidência registrada?

**G. Monitoramento e falhas**
- [ ] Como se descobre que um backup falhou? Quem é avisado? O que se faz quando falha?

**H. Responsabilidades**
- [ ] Quem responde por backup hoje (executar, monitorar, aprovar)? Está formalizado?

**I. Requisitos de negócio**
- [ ] Existe RPO (perda máxima tolerável) e RTO (tempo máximo de recuperação) definidos? Por quem?

**Saída da Etapa 0:** retrato fiel do AS-IS (preenche o `REG-ISO-0001-INVENTARIO` e uma ata de levantamento). Nenhuma recomendação ainda.

---

## Etapa 1 — Análise de lacunas (GAP: AS-IS × 8.13)

Só agora a IA compara o estado atual com os requisitos do controle 8.13 (itens a–g + monitoramento de falhas + backup em nuvem + retenção/expurgo) e marca cada ponto:

- [ ] Para cada requisito do 8.13: **atende / atende parcialmente / não atende**, com evidência do AS-IS.
- [ ] Listar lacunas e, para cada uma, uma **recomendação explicitamente marcada como tal** (não como fato).
- [ ] Priorizar lacunas por risco.

**Saída:** tabela de GAP que fundamenta as decisões de política da Etapa 2. As recomendações ficam visíveis e separadas do que a empresa já faz.

---

## Etapa 2 — Decidir a Política (será a Seção 6 do PO)

A partir do AS-IS + GAP, a empresa **decide** (a IA não decide por ela):
- [ ] Classificação de criticidade / tiers das bases
- [ ] Frequência de backup por tier
- [ ] Retenção por tier (on-site / off-site / cloud) e regra de expurgo
- [ ] Criptografia (trânsito/repouso) e gestão de chaves
- [ ] RPO/RTO por tier (validados pela área de negócio)

**Saída:** decisões registradas — viram a Seção 6 do PO.

---

## Estrutura do documento principal — `PO-ISO-0001-BACKUP.md` (simplificada)

Enxuto: governança e processo, **sem comandos técnicos** (esses vão para as ITs) e **sem evidências** (essas vão para os REGs).

```
PO-ISO-0001-BACKUP.md
├── 1. Objetivo
├── 2. Escopo
├── 3. Referências (normativas + documentos relacionados: ITs e REGs)
├── 4. Definições e Terminologia (RPO, RTO, full/incremental/diferencial…)
├── 5. Responsabilidades (RACI)
├── 6. Política de Backup            ← decisões da Etapa 2
│   ├── 6.1 Classificação / tiers de criticidade
│   ├── 6.2 Frequência por tier
│   ├── 6.3 Retenção, armazenamento remoto e expurgo
│   └── 6.4 Criptografia e RPO/RTO
├── 7. Gestão do ciclo de backup e restauração   ← o "como gerir"
│   ├── 7.1 Execução e agendamento (remete às ITs por tecnologia)
│   ├── 7.2 Monitoramento e verificação de integridade
│   ├── 7.3 Tratamento de falhas e escalonamento (SLA, fluxo Eng→DBA→TI→CISO)
│   └── 7.4 Governança dos testes de restauração (periodicidade, quem aprova — remete à IT e ao REG de teste)
├── 8. Registros e evidências (lista os REGs, retenção e onde ficam — cláusula 7.5)
└── 9. Revisão e melhoria contínua (anual ou pós-incidente; aprovação do resp. de SI)
```

De 13 seções com scripts embutidos para **9 seções de governança**. Toda execução técnica saiu para as ITs; toda evidência saiu para os REGs.

---

## Estrutura sugerida das Instruções de Trabalho (IT) — uma por tecnologia

Um arquivo por tecnologia, cobrindo backup + restauração + teste daquele banco. Conjunto inicial (ajustar ao que o AS-IS revelar):

```
IT-ISO-0001-POSTGRESQL.md
IT-ISO-0002-MYSQL.md
IT-ISO-0003-MONGODB.md
IT-ISO-0004-REDIS.md
```

**Template comum de cada IT:**

```
IT-ISO-{NNNN}-{TECNOLOGIA}.md
├── 1. Objetivo e escopo (tecnologia, versões cobertas)
├── 2. Pré-requisitos (acessos, ferramentas, variáveis de ambiente, permissões)
├── 3. Procedimento de Backup
│   ├── 3.1 Comando/ferramenta nativa (pg_dump, mysqldump, mongodump, BGSAVE…)
│   ├── 3.2 Compressão e verificação de integridade (checksum)
│   └── 3.3 Upload para o storage e versionamento
├── 4. Procedimento de Restauração
│   ├── 4.1 Pré-condições (parar serviço, espaço, permissões)
│   ├── 4.2 Passo a passo numerado
│   ├── 4.3 Validação pós-restauração (queries de sanidade, contagens)
│   └── 4.4 Rollback em caso de falha
├── 5. Procedimento de Teste de Restauração
│   ├── 5.1 Provisionar ambiente isolado (docker-compose / sandbox)
│   ├── 5.2 Executar restauração e medir tempo (vs. RTO)
│   └── 5.3 Critérios de aprovação / falha
├── 6. Erros comuns e troubleshooting
└── 7. Registros gerados (quais REGs esta IT alimenta)
```

A IT é o lugar dos comandos, scripts e checklists técnicos — pode ser revisada sem reabrir o PO.

---

## Estrutura sugerida dos Registros (REG)

Evidências e listas exigidas para rastreabilidade do 8.13 e da cláusula 7.5. Cada REG é um **template a ser preenchido** (planilha/tabela ou ferramenta de GRC).

| Registro | Conteúdo (colunas) | Alimentado por | Atende ao 8.13 |
|----------|--------------------|----------------|----------------|
| `REG-ISO-0001-INVENTARIO` | Base, tecnologia, ambiente, dono, tier, RPO/RTO, frequência, retenção, destino, criptografado? | Etapa 0 + manutenção contínua | Lista das bases que **precisam** de backup |
| `REG-ISO-0002-EXECUCAO` | Data/hora, base, tipo (full/incr.), tamanho, duração, checksum, status, operador | Execução das ITs (item 3) | Registros precisos de cópias (8.13.a) |
| `REG-ISO-0003-TESTE-RESTAURACAO` | Data, backup testado (data+hash), ambiente, executor, tempo vs. RTO, resultado, desvios, assinatura/aprovação | IT item 5 | Evidência de teste regular (8.13.e) |
| `REG-ISO-0004-PLANO-TESTES` | Calendário de testes por tier + lista dos testes **realizados** vs. planejados | Governança do PO (7.4) | Comprova periodicidade dos testes |
| `REG-ISO-0005-RESTAURACOES` | Data, base, solicitante, motivo (incidente/erro/perda/emergência), backup usado (data+hash), executor, RTO real vs. alvo, resultado, validação pós-restauração, observações | Execução das ITs (item 4) | Evidência de restaurações reais (≠ testes) e aderência ao RTO |
| `REG-ISO-0006-INCIDENTES` | Data, base, falha detectada, causa, ação corretiva, status, responsável | PO 7.3 | Resolução de falhas de backup (8.13) |

> Os registros ficam claramente separados:
> - **lista de bancos que precisam de backup** → `REG-ISO-0001-INVENTARIO`
> - **lista de testes de restauração realizados** → `REG-ISO-0004-PLANO-TESTES`
> - **evidências dos testes** → `REG-ISO-0003-TESTE-RESTAURACAO`
> - **lista de restaurações solicitadas/emergenciais (restores reais)** → `REG-ISO-0005-RESTAURACOES`
>
> Atenção à distinção: `TESTE-RESTAURACAO` é restauração de validação (em ambiente isolado, planejada); `RESTAURACOES` é restauração **real** disparada por solicitação ou emergência (incidente, perda, erro). São evidências de naturezas diferentes.

---

## Etapas de criação dos documentos (após Etapas 0–2)

### Etapa 3 — Redigir o PO (governança)
- [ ] Seções 1–5 (objetivo, escopo, referências, definições, RACI)
- [ ] Seção 6 = decisões da Etapa 2
- [ ] Seção 7 = processo de gestão (execução/agendamento, monitoramento, falhas/escalonamento, governança dos testes) — **sem comandos**, remetendo às ITs
- [ ] Seções 8–9 (registros e revisão)

### Etapa 4 — Criar os templates de Registro (REG)
- [ ] Criar os 6 REGs como templates vazios com cabeçalhos definidos
- [ ] Preencher `REG-ISO-0001-INVENTARIO` com o resultado da Etapa 0

### Etapa 5 — Redigir as ITs por tecnologia
- [ ] Uma IT por tecnologia identificada no AS-IS, seguindo o template comum
- [ ] Validar tecnicamente os comandos no ambiente real (responsabilidade humana)

### Etapa 6 — Amarrar referências cruzadas
- [ ] PO §3 e §7 referenciam as ITs; PO §8 referencia os REGs; cada IT §7 referencia os REGs que alimenta
- [ ] Atualizar o `README.md` (estrutura do repositório, tabela de arquivos e convenção de nomenclatura) para refletir IT e REG

### Etapa 7 — Revisão e aprovação
- [ ] Revisão técnica + aderência ao AS-IS
- [ ] Aprovação formal pelo responsável de Segurança da Informação

---

## Decisões já tomadas

| # | Decisão | Efeito |
|---|---------|--------|
| 1 | Política como **seção do PO** (não documento separado) | Mantém o conjunto enxuto; Seção 6 do PO |
| 2 | **Uma IT por tecnologia** (backup+restauração+teste juntos) | Define os arquivos `IT-ISO-0001-{TECNOLOGIA}` |

## Decisões que emergem do AS-IS (não pré-definir)

| # | Questão | Resolvida em |
|---|---------|--------------|
| 1 | Quais tecnologias SQL/NoSQL existem? | Etapa 0 → define quantas ITs |
| 2 | Storage de destino e se há cópia remota | Etapa 0 |
| 3 | Existe ambiente de teste/sandbox? | Etapa 0 → viabilidade do item 5 das ITs |
| 4 | Orquestração de backup existente (cron, K8s CronJob, AWS Backup) | Etapa 0 → conteúdo das ITs |
| 5 | RPO/RTO definidos pelo negócio? | Etapa 0/2 |
| 6 | Tiers, frequência e retenção | Etapa 2 (decisão da empresa, pós-GAP) |

---

## Ordem de execução

```
Etapa 0 (AS-IS, sem viés) → Etapa 1 (GAP) → Etapa 2 (decisões de política)
   → Etapa 3 (PO) + Etapa 4 (REGs)  → Etapa 5 (ITs) → Etapa 6 (referências + README) → Etapa 7 (aprovação)
```
