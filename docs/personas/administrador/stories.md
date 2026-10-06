# Story: Administrar dados da competição e acessos

**Persona:** Administrador
**Status:** Draft
**Prioridade, estimativa e ID:** A definir no planejamento do backlog

## História do usuário

Como administrador responsável pela operação da aplicação, quero gerenciar clubes, partidas, resultados, usuários e permissões, para manter as informações do campeonato atualizadas e controlar o acesso às funcionalidades administrativas.

## Objetivo

Permitir a manutenção controlada dos dados da competição e dos níveis de acesso, preservando a integridade dos dados e atualizando a classificação quando resultados forem registrados.

## Critérios de aceite

```gherkin
Cenário: Gerenciar clubes
  Dado que o usuário tenha permissão administrativa
  Quando cadastrar ou editar um clube
  Então o sistema salva as informações do clube

Cenário: Remover ou desativar clube
  Dado que o usuário tenha permissão administrativa
  Quando solicitar a remoção ou desativação de um clube
  Então o sistema respeita as regras de integridade dos dados

Cenário: Cadastrar uma partida
  Dado que o usuário tenha permissão administrativa
  Quando cadastrar uma partida com os clubes participantes, data e horário
  Então o sistema registra a partida

Cenário: Registrar ou atualizar resultado
  Dado que o usuário tenha permissão administrativa
  Quando registrar ou atualizar o resultado de uma partida
  Então o sistema mantém um único resultado válido para uma partida finalizada
  E atualiza as estatísticas dos clubes envolvidos
  E atualiza a classificação conforme a pontuação e os critérios oficiais

Cenário: Gerenciar usuários e níveis de acesso
  Dado que o usuário tenha permissão administrativa
  Quando consultar ou gerenciar usuários
  Então o sistema permite administrar seus níveis de acesso

Cenário: Restringir operações administrativas
  Dado que o usuário não tenha permissão administrativa
  Quando tentar cadastrar, alterar ou remover informações da competição
  Então o sistema não permite a operação
```

## Requisitos relacionados

- RF05 — Cadastrar clube; RF06 — Editar clube; RF07 — Remover clube.
- RF08 — Cadastrar partida; RF09 — Registrar resultado; RF10 — Atualizar classificação.
- RF11 — Gerenciar usuários; RF12 — Consultar métricas de utilização.
- RN01 — Pontuação; RN02 — Atualização da classificação; RN03 — Integridade dos resultados; RN04 — Controle administrativo; RN05 — Critérios de classificação; RN06 — Acesso às métricas.
- RNF03 — Segurança; RNF06 — Integridade dos dados.

## Dependências e pontos em aberto

- As permissões administrativas precisam ser verificadas em todas as operações de cadastro, alteração e remoção (RN04, RNF03).
- Os critérios oficiais de classificação e as regras de integridade relacionadas à remoção de clubes precisam ser definidos ou aplicados antes das operações correspondentes (RF07, RN05).
- RF12 permite métricas apenas a usuários autorizados; o requisito não detalha quais indicadores compõem a visão administrativa nem quais níveis de acesso podem consultá-los.

## Riscos e mitigação

| Risco | Mitigação |
|---|---|
| Uma atualização de resultado pode deixar estatísticas e classificação inconsistentes. | Tratar a atualização do resultado, estatísticas e classificação de forma consistente e validar a regra RN02. |
| Remover um clube com partidas associadas pode comprometer a integridade histórica. | Aplicar as regras de integridade antes de remover ou desativar o clube, conforme RF07. |
| Permissões aplicadas de forma incompleta podem permitir alterações indevidas. | Validar autorização nas operações administrativas, conforme RN04 e RNF03. |

## Definition of Done

- [ ] Todos os critérios de aceite foram atendidos.
- [ ] Operações administrativas são restritas a usuários com permissão administrativa.
- [ ] Registro e atualização de resultados preservam a integridade e atualizam a classificação.
- [ ] Regras de pontuação, resultado único válido e ordenação oficial são respeitadas.
- [ ] Testes cobrem operações permitidas, negadas e integridade dos dados.

## Histórico

| Data | Alteração |
|---|---|
| 2026-10-05 | Criação do draft com base nos requisitos da aplicação. |