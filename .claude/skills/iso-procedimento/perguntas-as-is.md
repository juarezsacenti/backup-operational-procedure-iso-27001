# Banco de perguntas — Levantamento AS-IS (anti-viés)

> Regra de ouro: **pergunte e registre**. Não ofereça opções nem valores "ideais" antes de
> capturar a realidade. Uma pergunta aberta por vez (ou em blocos curtos). Transcreva a
> resposta literal. Conduza por setor quando houver mais de um responsável.

## A. Inventário e topologia
- Quais bancos de dados e sistemas existem? Onde rodam (cloud, on-prem, gerenciado)?
- Quais ambientes existem (produção, homologação, dev)? Quem é o dono de cada base?

## B. Como o processo é feito hoje
- Existe o controle hoje? Sobre o quê? De quais ativos não existe?
- Como é disparado e com qual ferramenta? Quem executa e quem acompanha?
- Com que frequência ocorre? Quem definiu e por quê?

## C. Armazenamento e proteção
- Onde o resultado é armazenado? Existe cópia remota/separada do principal?
- É criptografado (em trânsito e/ou em repouso)? Quem detém as chaves?

## D. Retenção
- Por quanto tempo se guarda? Quem definiu o prazo? Há exigência legal/contratual conhecida?

## E. Recuperação
- Já foi necessário recuperar de verdade? O que aconteceu, quanto tempo levou, deu certo?
- O passo a passo está documentado hoje em algum lugar?

## F. Teste
- Já se testou a recuperação fora de uma emergência real? Com que frequência? Há evidência?

## G. Monitoramento e falhas
- Como se descobre que houve falha? Quem é avisado? O que se faz?

## H. Responsabilidades e divisão por setor
- Quem responde por isto hoje (executar, monitorar, aprovar)? Está formalizado?
- Quais setores participam? Conduza os blocos B–G separadamente com cada setor.
- Cada setor cobre quais ativos/tecnologias?

## I. Requisitos de negócio
- Existem RPO/RTO (ou equivalentes do controle) definidos? Por quem?
