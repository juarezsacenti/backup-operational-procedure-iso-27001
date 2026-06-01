# Procedimentos Operacionais — ISO 27001

Repositório de procedimentos operacionais criados para atender aos controles da norma **ISO/IEC 27001:2022**, com foco em rastreabilidade, conformidade e continuidade operacional.

---

## Sobre este repositório

Trabalhei **cinco anos aplicando melhoria contínua a processos de backup e restauração** — definindo políticas, padronizando a execução e amadurecendo os testes de recuperação. Este repositório é a minha forma de **registrar e compartilhar esse conhecimento de maneira genérica e reaproveitável**, desacoplado de qualquer organização.

**Por que usar IA para especificar a ISO?** Escrever bons procedimentos exige fluência na norma, profundidade técnica e consistência — algo caro e demorado de produzir à mão. A IA acelera o rascunho estruturado enquanto eu mantenho o papel de especialista: valido o conteúdo técnico, ajusto à realidade do controle e aprovo. O resultado é o conhecimento que acumulei na prática, formalizado no vocabulário da ISO 27001, em uma fração do tempo (ver [IA como parceira](#ia-como-parceira-na-criação-de-procedimentos-controlados-e-auditáveis)).

> ### ⚠️ Aviso de confidencialidade
> Todo o conteúdo deste repositório é **genérico e ilustrativo**. **Não há — e não deve haver — nenhuma informação sigilosa de qualquer organização**: sem nomes reais de sistemas, hosts, IPs, credenciais, topologia de rede, dados de negócio ou configurações reais. Tecnologias, *tiers*, comandos e exemplos são didáticos. O objetivo é documentar o **método**, não a infraestrutura de ninguém.

---

## Por que procedimentos operacionais para controles ISO 27001?

A ISO 27001 define *o que* deve ser feito — os controles estabelecem requisitos e orientações. Os **procedimentos operacionais** transformam esses requisitos em *como* fazer: passos concretos, responsáveis definidos, critérios de sucesso e evidências auditáveis.

Sem procedimentos documentados:
- Controles existem apenas no papel e não são executados de forma consistente
- Auditorias internas e externas não encontram evidência de conformidade
- A organização depende do conhecimento tácito de indivíduos, criando risco de continuidade
- Falhas se repetem porque não há processo formal de aprendizado e melhoria

Com procedimentos operacionais bem definidos:
- A execução dos controles é **repetível e verificável**, independentemente de quem executa
- Cada ação deixa **rastro auditável** (logs, registros, relatórios) exigido pela norma
- O time de segurança consegue medir, monitorar e melhorar continuamente a postura de conformidade
- Em caso de incidente, a resposta é orientada por processo, reduzindo tempo e erro humano

---

## IA como parceira na criação de procedimentos controlados e auditáveis

Procedimentos operacionais de segurança têm um problema clássico: são caros de escrever bem. Exigem conhecimento técnico profundo, fluência na norma, consistência entre seções e tempo — um recurso escasso em times de segurança. O resultado prático é que muitas organizações têm procedimentos desatualizados, incompletos ou que nunca saíram do papel.

O uso de IA assistida por humanos, combinado com um fluxo de trabalho baseado em planos versionados, muda essa equação sem abrir mão do controle e da auditabilidade exigidos pela ISO 27001.

### Como funciona o fluxo neste repositório

```
Controle ISO (o quê)
        │
        ▼
  PLAN (como construir)   ← IA + humano definem escopo, etapas e decisões pendentes
        │
        ▼
Decisões confirmadas      ← humano valida tecnologias, RPO/RTO, ambientes
        │
        ▼
  PO (procedimento)       ← IA redige; humano revisa, ajusta e aprova
        │
        ▼
Git / versionamento       ← histórico auditável de cada mudança, por quem e quando
```

Cada etapa produz um artefato rastreável. O plano documenta as decisões *antes* da execução — tornando o processo auditável desde a origem, não apenas o resultado final.

### Vantagens concretas

**Velocidade sem perda de qualidade**
A IA conhece a estrutura da norma, padrões de procedimento e ferramentas técnicas (pg_dump, mongodump, políticas de retenção). O que levaria dias de redação pode ser produzido em horas, com a qualidade técnica revisada pelo especialista humano em vez de escrita do zero por ele.

**Decisões explícitas e documentadas**
O plano (`plan/`) força a externalização das decisões antes de redigir o procedimento: quais tecnologias, quais ambientes, qual o RPO/RTO. Isso evita procedimentos escritos com premissas implícitas que se tornam inconsistências descobertas apenas em auditoria.

**Rastreabilidade de ponta a ponta**
O repositório git registra *o quê* mudou, *quando* e *por quem*. Combinado com o plano que registra *por quê* cada decisão foi tomada, a organização tem uma cadeia de evidências que atende diretamente ao requisito de controle de documentos da ISO 27001 (cláusula 7.5).

**Revisão humana como controle de qualidade, não gargalo**
Com a IA gerando o rascunho estruturado, o especialista humano foca em validar o conteúdo técnico e a aderência à realidade operacional — em vez de gastar energia na estrutura e na redação. O humano permanece como aprovador final e responsável pela conformidade.

**Consistência entre procedimentos**
À medida que o repositório cresce com novos controles, a IA mantém consistência de estrutura, nomenclatura e nível de detalhe entre os procedimentos — algo difícil de sustentar manualmente em times distribuídos ao longo do tempo.

**Atualização contínua facilitada**
Quando uma tecnologia muda (nova versão do banco, mudança de storage) ou a norma é revisada, o ciclo plano → procedimento pode ser reexecutado incrementalmente, com diff claro do que mudou e registro no histórico git.

### O que a IA não substitui

- A **validação técnica** dos scripts e procedimentos no ambiente real da organização
- A **aprovação formal** pelo responsável de Segurança da Informação
- O **julgamento de risco** sobre o que é crítico para o negócio (RPO/RTO, tier de criticidade)
- A **execução e os testes** — o procedimento só tem valor se for praticado e evidenciado

---

## Estrutura do repositório

```
.
├── README.md                          # Este arquivo
├── LICENSE.txt                        # Licença CC BY 4.0
├── ISO-27001-8-13.md                  # Texto oficial do controle 8.13 (PT-BR)
├── .claude/skills/                    # Skills (método executável — ver "Passos futuros")
│   ├── iso-procedimento/              # Pipeline: AS-IS → GAP → PO/IT/REG
│   ├── restauracao-postgresql/        # Execução assistida de restauração — PostgreSQL
│   ├── restauracao-mongodb/           # Execução assistida de restauração — MongoDB
│   └── restauracao-storage-bucket/    # Execução assistida de restauração — Storage Bucket
├── plan/
│   └── PLAN-PO-ISO-0001-BACKUP.md     # Plano de criação do conjunto documental
│
│   # Documentos a serem produzidos a partir do plano (pirâmide documental):
├── PO-ISO-0001-BACKUP.md              # Procedimento Operacional (governança do ciclo)
├── IT-ISO-0001-POSTGRESQL.md          # Instrução de Trabalho: backup/restauração/teste — PostgreSQL
├── IT-ISO-0002-MONGODB.md             # Instrução de Trabalho: backup/restauração/teste — MongoDB
├── IT-ISO-0003-STORAGE-BUCKET.md      # Instrução de Trabalho: backup/restauração/teste — Storage Bucket
├── REG-ISO-0001-INVENTARIO.md         # Registro: inventário de bases que requerem backup
├── REG-ISO-0002-EXECUCAO.md           # Registro: log de execução de backups
├── REG-ISO-0003-TESTE-RESTAURACAO.md  # Registro: evidência dos testes de restauração
├── REG-ISO-0004-PLANO-TESTES.md       # Registro: plano e lista de testes realizados
├── REG-ISO-0005-RESTAURACOES.md       # Registro: restaurações reais (solicitadas/emergenciais)
└── REG-ISO-0006-INCIDENTES.md         # Registro: incidentes/falhas de backup
```

> As tecnologias listadas nas ITs são ilustrativas — o conjunto real é definido pelo levantamento AS-IS descrito no plano.

### Descrição dos arquivos

A pirâmide documental da ISO 27001 separa quatro camadas — **Política** (decisão), **Procedimento** (gestão), **Instrução de Trabalho** (execução técnica) e **Registro** (evidência). Aqui a Política é uma seção do PO; as demais camadas são documentos próprios.

| Arquivo | Tipo | Descrição |
|---------|------|-----------|
| `ISO-27001-8-13.md` | Referência normativa | Texto do controle 8.13 da ISO/IEC 27001:2022 — *Information Backup*. Âncora normativa de todos os documentos. |
| `plan/PLAN-PO-ISO-0001-BACKUP.md` | Plano de trabalho | Roteiro de criação do conjunto documental: levantamento AS-IS, análise de lacunas, estrutura dos documentos e convenções. |
| `PO-ISO-0001-BACKUP.md` | Procedimento Operacional | *Como gerir* o ciclo de backup/restauração: política (seção), responsabilidades, monitoramento, tratamento de falhas, governança dos testes e revisão. Sem comandos técnicos. |
| `IT-ISO-{NNNN}-{TECNOLOGIA}.md` | Instrução de Trabalho | *Como executar* a tarefa técnica por tecnologia (uma IT por banco): comandos de backup, restauração e teste, validação e troubleshooting. |
| `REG-ISO-{NNNN}-{TIPO}.md` | Registro / evidência | Templates a preencher: inventário de bases, log de execução, evidência de testes, plano/lista de testes, restaurações reais e incidentes. Sustentam a rastreabilidade (cláusula 7.5). |

---

## Convenção de nomenclatura

Formato: **`<tipo>-<departamento>-<número>-<nome>`**

| Campo | Significado |
|-------|-------------|
| `<tipo>` | `PO` (Procedimento Operacional), `IT` (Instrução de Trabalho) ou `REG` (Registro) |
| `<departamento>` | Área responsável — ex.: `ISO` |
| `<número>` | Sequência **própria de cada tipo**, independente (o `0001` de uma IT não tem relação com o `0001` do PO) |
| `<nome>` | Tema ou identificação do documento |

| Prefixo | Significado |
|---------|-------------|
| `ISO-27001-{seção}` | Texto de referência de um controle da norma |
| `plan/PLAN-{documento}` | Plano de criação de um documento |
| `PO-ISO-{nº}-{tema}` | Procedimento Operacional vinculado a um controle ISO 27001 |
| `IT-ISO-{nº}-{tecnologia}` | Instrução de Trabalho (execução técnica) |
| `REG-ISO-{nº}-{tipo}` | Registro / template de evidência |

> A ligação entre IT/REG e seu PO é feita por **referência cruzada explícita** dentro dos documentos, nunca pelo número.

---

## Controle coberto neste repositório

### 8.13 — Backup das informações

> Cópias de backup de informações, software e sistemas devem ser mantidas e testadas regularmente de acordo com a política específica por tema acordada sobre backup.

**Propósito:** Permitir a recuperação da perda de dados ou sistemas.

O procedimento `PO-ISO-0001-BACKUP.md` implementa este controle cobrindo:
- Política de backup (frequência, retenção, criptografia, armazenamento remoto)
- Procedimentos por tecnologia (em ITs): PostgreSQL, MongoDB e Storage Bucket
- Procedimentos de restauração com critérios de validação (RPO/RTO)
- Testes periódicos de restauração com registro de evidências auditáveis
- Monitoramento, alertas e gestão de falhas

---

## Como usar este repositório

1. Consulte `ISO-27001-8-13.md` para entender o requisito normativo de origem
2. Execute os procedimentos de `PO-ISO-0001-BACKUP.md` conforme a periodicidade definida
3. Registre evidências de execução (logs, relatórios de teste) em ferramenta de GRC ou pasta de evidências vinculada
4. Revise os procedimentos anualmente ou após qualquer incidente relevante de backup

---

## Referências

- ISO/IEC 27001:2022 — Information security, cybersecurity and privacy protection
- ISO/IEC 27002:2022 — Information security controls (guidance for 8.13)
- ISO/IEC 27040 — Storage security (referenciada no controle 8.13)

---

## Passos futuros

Este repositório evolui em duas frentes: os **documentos** (PO/IT/REG por controle) e o
**método** (os skills que os produzem e executam).

### Documentos
- Produzir, a partir do `plan/`, o `PO-ISO-0001-BACKUP` e as ITs/REGs correspondentes.
- Cobrir novos controles da ISO 27001, cada um com seu próprio `plan/PLAN-PO-ISO-{nº}-{tema}`.

### Skills (`.claude/skills/`)
O método deixou de ser apenas prosa e passou a ser **executável e versionado**:

| Skill | Papel |
|-------|-------|
| `iso-procedimento` | Pipeline completo: AS-IS (anti-viés) → GAP → decisões → PO/IT/REG, nas convenções do repo. **Gera um `plan/` por controle** (não substitui o plano). |
| `restauracao-postgresql` | Execução assistida da restauração PostgreSQL (teste e emergência), com registro de evidência. |
| `restauracao-mongodb` | Execução assistida da restauração MongoDB. |
| `restauracao-storage-bucket` | Execução assistida da restauração de object storage. |

### Melhoria contínua dos skills
Os skills são tratados como artefatos vivos, sob o mesmo rigor dos procedimentos:
- **Aprende-se com o uso:** após cada execução, registra-se o que faltou ou atritou
  (pergunta que não cobriu um caso, passo ausente) e ajustam-se templates, banco de
  perguntas e guardrails.
- **Versionado no git:** cada mudança de skill é commitada com o aprendizado que a motivou,
  preservando a rastreabilidade.
- **Acompanha a norma e a tecnologia:** revisões da ISO ou novas tecnologias entram de forma
  incremental, mantendo a coerência entre skill, `plan/` de referência e documentos.
- **Humano no comando:** os skills aceleram e padronizam o rascunho/execução; validação
  técnica, julgamento de risco e aprovação formal permanecem do especialista.

---

## Licença

Este repositório é licenciado sob a **[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)** — ver o arquivo [`LICENSE.txt`](LICENSE.txt).

Você pode compartilhar e adaptar o conteúdo, inclusive para fins comerciais, desde que **dê o devido crédito**. Sugestão de atribuição:

> Baseado em "Procedimentos Operacionais — ISO 27001" de Juarez Sacenti, licenciado sob CC BY 4.0.