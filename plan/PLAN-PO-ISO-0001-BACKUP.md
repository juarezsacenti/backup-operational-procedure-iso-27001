# Plano: Procedimento Operacional de Backup — ISO 27001:2022 Controle 8.13

## Contexto

O controle **ISO 27001:2022 8.13 — Information Backup** exige que:
> Cópias de backup de informações, software e sistemas sejam mantidas e testadas regularmente conforme a política de backup definida.

Este plano descreve as etapas para criar o documento **PO-ISO-0001-BACKUP.md**, cobrindo backup, restauração e testes de restauração para ferramentas SQL e NoSQL.

---

## Estrutura do Documento Final

```
PO-ISO-0001-BACKUP.md
├── 1. Objetivo
├── 2. Escopo
├── 3. Referências Normativas
├── 4. Definições e Terminologia
├── 5. Responsabilidades (RACI)
├── 6. Política de Backup
│   ├── 6.1 Classificação dos dados e criticidade
│   ├── 6.2 Tipos de backup (full, incremental, diferencial)
│   ├── 6.3 Frequência e janelas de backup
│   └── 6.4 Retenção e armazenamento (on-site / off-site / cloud)
├── 7. Procedimentos de Backup por Tecnologia
│   ├── 7.1 SQL — PostgreSQL
│   ├── 7.2 SQL — MySQL / MariaDB
│   ├── 7.3 SQL — SQL Server (se aplicável)
│   ├── 7.4 NoSQL — MongoDB
│   ├── 7.5 NoSQL — Redis
│   └── 7.6 NoSQL — Elasticsearch / OpenSearch (se aplicável)
├── 8. Procedimentos de Restauração por Tecnologia
│   ├── 8.1 PostgreSQL
│   ├── 8.2 MySQL / MariaDB
│   ├── 8.3 MongoDB
│   └── 8.4 Redis
├── 9. Procedimentos de Teste de Restauração
│   ├── 9.1 Escopo e periodicidade dos testes
│   ├── 9.2 Ambiente de teste (isolado / sandbox)
│   ├── 9.3 Checklist de execução do teste
│   ├── 9.4 Critérios de aprovação / falha
│   └── 9.5 Registro e evidência dos testes
├── 10. Monitoramento e Alertas
│   ├── 10.1 Indicadores de sucesso / falha de backup
│   └── 10.2 Fluxo de escalonamento em caso de falha
├── 11. Gestão de Incidentes de Backup
├── 12. Registros e Evidências (rastreabilidade ISO 27001)
└── 13. Revisão e Melhoria Contínua
```

---

## Etapas de Criação

### Etapa 1 — Definir escopo de tecnologias
- [ ] Levantar quais SGBDs SQL são usados (PostgreSQL, MySQL, SQL Server…)
- [ ] Levantar quais bancos NoSQL são usados (MongoDB, Redis, Elasticsearch…)
- [ ] Identificar ambientes: produção, staging, dev
- [ ] Identificar onde os backups são armazenados hoje (S3, GCS, local, NFS…)

### Etapa 2 — Política de Backup (Seção 6)
- [ ] Definir classificação de criticidade por base (ex.: Tier 1 = produção, Tier 2 = staging)
- [ ] Definir frequência por tier:
  - Tier 1: full diário + incremental a cada 6h
  - Tier 2: full semanal + incremental diário
- [ ] Definir retenção por tier:
  - Tier 1: 30 dias on-site, 1 ano off-site
  - Tier 2: 7 dias on-site
- [ ] Definir criptografia em trânsito e em repouso para todos os backups

### Etapa 3 — Procedimentos de Backup SQL (Seção 7.1–7.3)
Para cada SGBD:
- [ ] Comando / ferramenta nativa (pg_dump, mysqldump, pg_basebackup…)
- [ ] Script de automação (exemplo funcional com variáveis de ambiente)
- [ ] Compressão e verificação de integridade (checksum)
- [ ] Upload para storage (ex.: `aws s3 cp`, `gsutil cp`)
- [ ] Log de execução e notificação (sucesso / erro)

### Etapa 4 — Procedimentos de Backup NoSQL (Seção 7.4–7.6)
Para cada banco NoSQL:
- [ ] Ferramenta nativa (mongodump, redis-cli BGSAVE / RDB, Elasticsearch Snapshot API…)
- [ ] Script de automação com checklist de pré-condições
- [ ] Verificação de consistência pós-backup
- [ ] Upload e versionamento no storage

### Etapa 5 — Procedimentos de Restauração (Seção 8)
Para cada tecnologia:
- [ ] Pré-condições (parar serviço, verificar espaço, permissões)
- [ ] Passo a passo numerado de restauração
- [ ] Validação pós-restauração (queries de sanidade, contagem de registros)
- [ ] Estimativa de RTO (Recovery Time Objective) por tecnologia
- [ ] Rollback se restauração falhar

### Etapa 6 — Procedimentos de Teste de Restauração (Seção 9)
- [ ] Definir periodicidade mínima: trimestral para Tier 1, semestral para Tier 2
- [ ] Descrever ambiente de teste isolado (docker-compose / sandbox cloud)
- [ ] Criar checklist de teste padronizado:
  1. Identificar backup a ser testado (data, hash)
  2. Provisionar ambiente isolado
  3. Executar restauração conforme Seção 8
  4. Validar integridade dos dados (queries, contagens)
  5. Medir tempo total (vs. RTO definido)
  6. Documentar resultado e assinar evidência
- [ ] Template de relatório de teste (quem, quando, resultado, desvios)

### Etapa 7 — Monitoramento, Alertas e Incidentes (Seções 10–11)
- [ ] Definir métricas: taxa de sucesso de backup, tamanho, duração, idade do último backup
- [ ] Definir canal de alerta (e-mail, Slack, PagerDuty…)
- [ ] SLA de resposta para falha de backup (ex.: 2h para Tier 1)
- [ ] Fluxo de escalonamento: Engenheiro → DBA → Gerente de TI → CISO

### Etapa 8 — Registros e Evidências (Seção 12)
- [ ] Log de execução retido por no mínimo 1 ano
- [ ] Relatórios de teste de restauração como evidência de conformidade ISO 27001
- [ ] Registro de mudanças no procedimento (controle de versão do documento)

### Etapa 9 — Revisão (Seção 13)
- [ ] Revisão anual obrigatória ou após incidente de backup
- [ ] Aprovação pelo responsável de Segurança da Informação

---

## Decisões a Confirmar

| # | Questão | Impacto |
|---|---------|---------|
| 1 | Quais SGBDs SQL estão em uso (PostgreSQL, MySQL, SQL Server)? | Define seções 7.1–7.3 e 8.1–8.3 |
| 2 | Quais bancos NoSQL estão em uso (MongoDB, Redis, Elasticsearch)? | Define seções 7.4–7.6 e 8.4 |
| 3 | Qual o storage de destino dos backups (S3, GCS, Azure Blob, on-prem)? | Impacta scripts de upload e política de retenção |
| 4 | Existe ambiente de teste/sandbox disponível para testes de restauração? | Define viabilidade da Seção 9 |
| 5 | Qual ferramenta de orquestração de backups existe (cron, Kubernetes CronJob, AWS Backup)? | Impacta scripts de automação |
| 6 | RPO e RTO definidos pela área de negócio? | Base para frequência e critérios de teste |

---

## Ordem de Execução

```
Etapa 1 → Etapa 2 → Etapas 3+4 (paralelo) → Etapa 5 → Etapa 6 → Etapas 7+8 (paralelo) → Etapa 9
```

Estimativa total: **4–6 horas** de redação colaborativa, dependendo das tecnologias confirmadas.