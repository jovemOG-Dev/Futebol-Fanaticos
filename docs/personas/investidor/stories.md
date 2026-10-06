# Story: Acompanhar utilização e interesse dos usuários

**Persona:** Investidor / Gestor
**Status:** Draft
**Prioridade, estimativa e ID:** A definir no planejamento do backlog

## História do usuário

Como investidor ou gestor interessado no engajamento da aplicação, quero consultar indicadores de utilização e interesse pelos clubes, para analisar o uso da plataforma.

## Objetivo

Disponibilizar a usuários autorizados métricas gerais de utilização, incluindo acessos, quantidade de usuários, clubes mais consultados e frequência das consultas.

## Critérios de aceite

```gherkin
Cenário: Consultar métricas de utilização com autorização
  Dado que o usuário esteja autorizado a consultar métricas
  Quando acessar os indicadores de utilização
  Então o sistema apresenta o número de acessos
  E apresenta a quantidade de usuários
  E apresenta os clubes mais consultados
  E apresenta a frequência de consultas

Cenário: Impedir acesso não autorizado às métricas
  Dado que o usuário não esteja autorizado a consultar métricas
  Quando tentar acessar esses indicadores
  Então o sistema não disponibiliza as métricas para esse usuário
```

## Requisitos relacionados

- RF12 — Consultar métricas de utilização.
- RN06 — Acesso às métricas.
- RNF03 — Segurança.

## Dependências e pontos em aberto

- A consulta depende de uma política de autorização definida para os usuários que podem acessar métricas (RN06). O requisito não determina quais níveis de acesso incluem o investidor/gestor.
- O requisito não especifica período de apuração, filtros, forma de apresentação ou definição operacional de acesso, usuário e frequência; esses detalhes precisam ser definidos antes da implementação.

## Riscos e mitigação

| Risco | Mitigação |
|---|---|
| Uma política de autorização indefinida pode expor métricas a usuários não autorizados ou impedir o acesso esperado pelo investidor/gestor. | Definir os níveis de acesso e aplicar o controle de autorização antes de liberar a consulta. |
| Métricas sem definições comuns podem ser interpretadas de maneiras diferentes. | Validar com os responsáveis o significado e o período de apuração de cada indicador antes de implementá-los. |

## Definition of Done

- [ ] Todos os indicadores listados em RF12 estão disponíveis para usuários autorizados.
- [ ] Usuários sem autorização não conseguem consultar as métricas.
- [ ] Testes cobrem autorização e apresentação dos indicadores definidos.
- [ ] Definições de indicadores e níveis de acesso foram documentadas.

## Histórico

| Data | Alteração |
|---|---|
| 2026-10-05 | Criação do draft com base nos requisitos da aplicação. |