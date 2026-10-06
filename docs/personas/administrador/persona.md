# Persona: Administrador

## Identificação

- **Nome/personagem:** Não definido nos requisitos; persona representativa, sem nome próprio.
- **Perfil:** Usuário responsável pela operação e manutenção das informações da aplicação.
- **Fonte:** Requisitos da Aplicação, seção 2.3.

## Objetivos

- Manter os clubes participantes cadastrados e atualizados.
- Cadastrar partidas e registrar ou atualizar seus resultados.
- Atualizar as informações do campeonato e a classificação.
- Gerenciar usuários e níveis de acesso.
- Consultar indicadores administrativos, respeitando as permissões aplicáveis.

## Necessidades

- Cadastrar e editar clubes, além de removê-los ou desativá-los respeitando a integridade dos dados.
- Cadastrar partidas com clubes participantes, data, horário e demais informações necessárias.
- Registrar e atualizar resultados.
- Atualizar estatísticas e classificação após o registro de resultados.
- Consultar e gerenciar usuários e seus níveis de acesso.
- Ter autenticação e autorização para proteger as funcionalidades administrativas.

## Motivações

As motivações abaixo são derivadas da responsabilidade e das necessidades descritas no requisito: manter as informações da competição atualizadas de forma controlada e preservar a operação consistente da aplicação.

## Dores e problemas

O requisito não registra dores como declarações diretas da persona. Como pontos de atenção inferidos das responsabilidades e regras de negócio:

- Atualizações inconsistentes de resultados podem comprometer estatísticas e classificação.
- Remover um clube sem respeitar vínculos existentes pode comprometer a integridade dos dados.
- Permissões administrativas mal aplicadas podem permitir alterações por usuários não autorizados.
- O processo de classificação depende dos critérios oficiais, que não estão detalhados no documento de requisitos.

## Expectativas em relação à aplicação

- Permitir operações administrativas apenas a usuários com permissão administrativa.
- Manter consistentes os dados de clubes, partidas, resultados e classificação.
- Refletir os resultados nas estatísticas e na classificação dos clubes envolvidos.
- Impedir mais de um resultado válido simultaneamente para uma partida finalizada.
- Respeitar os critérios oficiais de classificação do Campeonato Brasileiro Série A.
- Disponibilizar funcionalidades em computadores, tablets e dispositivos móveis conforme o requisito de responsividade.

## Contexto de utilização

Usa a aplicação para operar e manter os dados do campeonato e gerenciar usuários e permissões. As operações de cadastro, alteração e remoção são restritas a usuários com permissão administrativa. O requisito não especifica frequência de uso, local de acesso ou fluxo operacional detalhado.

## Story relacionada

- [Administrar dados da competição e acessos](stories.md)