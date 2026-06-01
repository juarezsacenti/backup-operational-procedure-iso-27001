---
name: iso-procedimento
description: Cria ou revisa o conjunto documental (Procedimento Operacional, Instruções de Trabalho e Registros) que implementa um controle da ISO/IEC 27001:2022, seguindo um fluxo anti-viés (levantamento AS-IS → análise de GAP → decisões → redação) e as convenções deste repositório. Use ao documentar/operacionalizar um controle ISO 27001 (ex.: 8.13 Backup) ou ao revisar um procedimento existente.
---

# Skill: Procedimento ISO 27001 (PO + IT + REG)

Conduz, de ponta a ponta, a criação do conjunto documental que implementa um controle
da ISO/IEC 27001:2022, separando as quatro camadas da pirâmide documental e gerando os
artefatos já no padrão deste repositório.

Este skill é a versão executável do método descrito em `plan/PLAN-PO-ISO-0001-BACKUP.md`
— consulte aquele plano como exemplo de referência concreta (controle 8.13).

## Relação com os planos (`plan/`)

Este skill **não substitui** o plan — gera um. São papéis distintos:

- **Skill** = o *método* reutilizável (permanente, sob melhoria contínua).
- **Plan** (`plan/PLAN-PO-ISO-{nº}-{tema}.md`) = a *instância por controle*, que registra o
  AS-IS, o GAP e as decisões daquele controle (o "porquê", rastreável para auditoria).
- **PO/IT/REG** = os *entregáveis* finais (o "o quê").

A cada rodada para um novo controle, **gere um novo plan**: as Etapas 0–2 abaixo *produzem*
o `plan/PLAN-PO-ISO-{nº}-{tema}.md`; as Etapas 3–5 produzem o PO/IT/REG a partir dele.
Não pule o plan — ele é a cadeia de evidências que separa o raciocínio (plan) do resultado
limpo (documentos).

## Princípios inegociáveis

1. **Anti-viés no levantamento.** No AS-IS, faça apenas perguntas abertas e **registre** as
   respostas. NÃO sugira frequências, tiers, retenção ou ferramentas "ideais" antes de
   capturar a realidade. Recomendações só entram na análise de GAP, sempre rotuladas como
   *recomendação* — nunca como *estado atual*. (Banco de perguntas em `perguntas-as-is.md`.)
2. **Pirâmide documental.** Decisão → Política (seção do PO); gestão do processo → PO;
   execução técnica → IT; evidência → Registro. Não misture as camadas. (Ver `convencoes.md`.)
3. **Confidencialidade.** NUNCA inclua dado real de organização (nomes de sistemas, hosts,
   IPs, credenciais, topologia, dados de negócio, configurações reais). Tudo é genérico e
   ilustrativo. Use placeholders (`<base>`, `<ambiente>`, `<bucket>`).
4. **Humano é o aprovador.** O skill produz rascunhos estruturados; validação técnica,
   julgamento de risco e aprovação formal são do especialista humano.

## Fluxo

### Etapa 0 — Levantamento AS-IS (sem viés)
Conduza o roteiro de `perguntas-as-is.md`, por setor quando houver mais de um responsável.
Saída: retrato fiel do estado atual (preenche o registro de inventário). Sem recomendações.

### Etapa 1 — Análise de GAP
Compare o AS-IS com o texto do controle (cada requisito: atende / parcial / não atende, com
evidência). Para cada lacuna, uma recomendação **marcada como tal**. Priorize por risco.

### Etapa 2 — Decisões (Política)
A organização decide (o skill não decide): classificação/tiers, frequência, retenção,
criptografia, RPO/RTO. Vira a seção Política do PO.

### Etapa 3 — Redigir o PO
Use `templates/PO.md`. Estrutura padrão: 1. Objetivo · 2. Abrangência · 3. Responsabilidades
· 4. Política · 5. Procedimento · 6. Matriz de registro. **Sem comandos técnicos** (vão para
as ITs). Quando houver mais de um setor responsável, crie uma subseção por setor em §5.

### Etapa 4 — Criar os Registros (REG)
Crie os templates vazios e a Matriz de registro (`templates/REG-matriz.md`): identificação,
local de armazenamento, tempo de retenção. Retenção dos registros é própria (conformidade),
≠ retenção dos backups. Use "N/A" se o processo não gerar registros.

### Etapa 5 — Redigir as IT
Uma IT por tecnologia (`templates/IT.md`). Estrutura padrão: 1. Objetivo · 2. Abrangência
· 3. Responsabilidades · 4. Instrução de trabalho · 5. Matriz de registro. Documente a
configuração de automações como referência; não crie instruções de execução manual quando
o processo for automático.

### Etapa 6 — Referências cruzadas
PO §5 cita as ITs inline; PO §6 e cada IT §5 (Matriz) citam os REGs. Aplique a convenção de
nomenclatura `<tipo>-<departamento>-<número>-<nome>` (número próprio por tipo).

### Etapa 7 — Versionar
Crie uma branch (não commite direto na main). Mensagem de commit documentando os **prompts**
que originaram as mudanças (convenção deste repositório). Abra o PR pelo link do GitHub após
`git push` (não use `gh`).

## Convenções
Consulte `convencoes.md` para nomenclatura, pirâmide documental e regras de confidencialidade.

## Melhoria contínua deste skill
Este skill é, ele próprio, um artefato sob melhoria contínua:
- Após cada uso, registre o que faltou ou atritou (perguntas que não cobriram um caso, seção
  que ficou ambígua) e ajuste os templates/perguntas.
- Versione as mudanças no git com mensagem explicando o aprendizado.
- Quando a norma for revisada ou surgir um novo tipo de tecnologia, atualize os templates e
  o banco de perguntas de forma incremental.
- Mantenha a coerência entre este skill e o `plan/PLAN-...` de referência.
