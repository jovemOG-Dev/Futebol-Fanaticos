# Requisitos da Aplicação — Campeonato Brasileiro Série A (Futebol-Fanaticos)

## 1. Objetivo do Negócio

Desenvolver uma aplicação web para acompanhamento do **Campeonato Brasileiro de Futebol — Série A**, permitindo que torcedores acompanhem o desempenho dos clubes e que administradores gerenciem as informações da competição.

A aplicação será inicialmente dimensionada para aproximadamente **100 usuários simultâneos**.

---

## 2. Personas

### 2.1 Torcedor

Usuário interessado em acompanhar o desempenho de um ou mais clubes durante o campeonato.

**Necessidades:**

* Acompanhar a posição do time na tabela.
* Consultar resultados das partidas.
* Acompanhar vitórias, empates e derrotas.
* Consultar gols marcados, sofridos e saldo de gols.
* Acompanhar a evolução do clube durante a competição.

### 2.2 Investidor / Gestor

Usuário interessado em indicadores de utilização e engajamento da aplicação.

**Necessidades:**

* Acompanhar a quantidade de acessos.
* Identificar os clubes mais consultados.
* Analisar o interesse dos usuários pelos diferentes clubes.
* Visualizar indicadores gerais de utilização da plataforma.

### 2.3 Administrador

Usuário responsável pela operação e manutenção das informações da aplicação.

**Necessidades:**

* Gerenciar clubes.
* Gerenciar partidas e resultados.
* Atualizar informações do campeonato.
* Gerenciar usuários e permissões.
* Consultar indicadores administrativos.

---

## 3. Objetivos de Negócio

* Disponibilizar uma plataforma centralizada para acompanhamento do Campeonato Brasileiro Série A.
* Facilitar o acesso dos torcedores às principais informações da competição.
* Permitir o acompanhamento do desempenho dos clubes.
* Disponibilizar indicadores de utilização para análise de engajamento.
* Garantir que os dados da competição possam ser administrados e atualizados de forma controlada.
* Suportar inicialmente aproximadamente 100 usuários simultâneos.

---

# 4. Requisitos Funcionais

### RF01 — Consultar classificação

O sistema deve permitir que o torcedor consulte a classificação atualizada do campeonato, apresentando:

* Posição;
* Clube;
* Pontos;
* Jogos;
* Vitórias;
* Empates;
* Derrotas;
* Gols marcados;
* Gols sofridos;
* Saldo de gols.

### RF02 — Consultar clube

O sistema deve permitir consultar informações e estatísticas de um clube participante do campeonato.

### RF03 — Consultar resultados

O sistema deve permitir consultar os resultados das partidas realizadas.

### RF04 — Acompanhar desempenho

O sistema deve apresentar o desempenho de um clube ao longo da competição, incluindo vitórias, empates, derrotas e saldo de gols.

### RF05 — Cadastrar clube

O administrador deve poder cadastrar novos clubes participantes.

### RF06 — Editar clube

O administrador deve poder alterar as informações cadastradas de um clube.

### RF07 — Remover clube

O administrador deve poder remover ou desativar um clube cadastrado, respeitando as regras de integridade dos dados.

### RF08 — Cadastrar partida

O administrador deve poder cadastrar partidas, informando os clubes participantes, data, horário e demais informações necessárias.

### RF09 — Registrar resultado

O administrador deve poder registrar ou atualizar o resultado de uma partida.

### RF10 — Atualizar classificação

O sistema deve atualizar os dados de classificação dos clubes após o registro de um resultado.

### RF11 — Gerenciar usuários

O administrador deve poder consultar e gerenciar os usuários da aplicação, incluindo seus níveis de acesso.

### RF12 — Consultar métricas de utilização

O sistema deve permitir que usuários autorizados consultem métricas de utilização, como:

* Número de acessos;
* Quantidade de usuários;
* Clubes mais consultados;
* Frequência de consultas.

---

# 5. Regras de Negócio

### RN01 — Pontuação

Uma vitória deve atribuir **3 pontos**, um empate **1 ponto** e uma derrota **0 pontos** ao clube.

### RN02 — Atualização da classificação

O registro de um resultado deve refletir nos dados estatísticos e na classificação dos clubes envolvidos.

### RN03 — Integridade dos resultados

Uma partida finalizada não deve possuir mais de um resultado válido simultaneamente.

### RN04 — Controle administrativo

Somente usuários com permissão administrativa poderão cadastrar, alterar ou remover informações da competição.

### RN05 — Critérios de classificação

A ordenação dos clubes deve respeitar os critérios oficiais definidos para o Campeonato Brasileiro Série A.

### RN06 — Acesso às métricas

As métricas de utilização devem estar disponíveis somente para usuários autorizados.

---

# 6. Requisitos Não Funcionais

### RNF01 — Capacidade

A aplicação deve suportar aproximadamente **100 usuários simultâneos** em sua capacidade inicial.

### RNF02 — Disponibilidade

A aplicação deve permanecer disponível durante os períodos de maior utilização da competição.

### RNF03 — Segurança

O sistema deve controlar o acesso às funcionalidades administrativas por meio de autenticação e autorização.

### RNF04 — Usabilidade

As principais informações do campeonato devem ser apresentadas de forma clara e intuitiva, permitindo que o torcedor encontre rapidamente a tabela, os clubes e os resultados.

### RNF05 — Responsividade

A aplicação deve ser acessível em computadores, tablets e dispositivos móveis.

### RNF06 — Integridade dos dados

As informações de clubes, partidas, resultados e classificação devem permanecer consistentes após operações de cadastro e atualização.

### RNF07 — Desempenho

As consultas mais utilizadas, como classificação, resultados e informações dos clubes, devem apresentar tempo de resposta adequado mesmo durante períodos de maior acesso.

---

## 7. Resumo da Separação

| Categoria                   | Pergunta que responde               | Exemplo                                                    |
| --------------------------- | ----------------------------------- | ---------------------------------------------------------- |
| **Objetivo de negócio**     | Por quê?                            | Disponibilizar uma plataforma para acompanhar o campeonato |
| **Persona**                 | Para quem?                          | Torcedor, investidor/gestor e administrador                |
| **Requisito funcional**     | O que o sistema faz?                | Consultar a classificação                                  |
| **Regra de negócio**        | Quais regras devem ser respeitadas? | Vitória = 3 pontos                                         |
| **Requisito não funcional** | Como o sistema deve funcionar?      | Suportar 100 usuários simultâneos                          |
