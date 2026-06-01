# Convenções

## Pirâmide documental (separe sempre)

| Camada | Pergunta | Onde |
|--------|----------|------|
| Política | *O que* a organização decide | Seção do PO |
| Procedimento (PO) | *Como gerir* o processo | `PO-...` |
| Instrução de Trabalho (IT) | *Como executar* a tarefa técnica | `IT-...` |
| Registro (REG) | *Qual a evidência* | `REG-...` |

Regra prática: decisão → Política · gestão → PO · comando/passo → IT · algo a
preencher/assinar/listar → Registro.

## Nomenclatura

Formato: `<tipo>-<departamento>-<número>-<nome>`

- `<tipo>`: `PO`, `IT` ou `REG`
- `<departamento>`: área responsável (ex.: `ISO`)
- `<número>`: sequência **própria de cada tipo** (independente; o nº da IT não é o do PO)
- `<nome>`: tema/identificação

A ligação entre IT/REG e seu PO é por **referência cruzada explícita** nos documentos,
nunca pelo número.

## Confidencialidade (obrigatório)

NUNCA inclua dado real de organização. Proibido: nomes reais de sistemas/hosts, IPs,
credenciais, segredos, topologia de rede, dados de negócio, configurações reais.
Use placeholders genéricos: `<base>`, `<ambiente>`, `<bucket>`, `<host>`, `<usuario>`.
O objetivo é documentar o **método**, não a infraestrutura de ninguém.
