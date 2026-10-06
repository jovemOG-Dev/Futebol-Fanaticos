# Jornada: Torcedor

**Jornada:** J-TOR-01 — Consultar competição e desempenho de clube

**Persona:** [Torcedor](persona.md)

**Story:** [Acompanhar o campeonato e o desempenho de um clube](stories.md)

## Objetivo e escopo

**Objetivo principal:** acompanhar a classificação, os resultados e o desempenho de um ou mais clubes durante o Campeonato Brasileiro Série A.

**Objetivos secundários:** consultar informações de um clube, comparar seus indicadores da competição e acompanhar sua evolução.

**Informações consultadas:** posição, pontos, jogos, vitórias, empates, derrotas, gols marcados, gols sofridos, saldo de gols, informações/estatísticas do clube e resultados de partidas realizadas.

**Ações e entradas:** escolher uma área de consulta e selecionar um clube; não há necessidade de entrada de dados pessoais definida para essa jornada.

**Resultados esperados:** dados claros, consistentes, atualizados e acessíveis em diferentes dispositivos.

**Restrições:** não há requisito de autenticação para as consultas do Torcedor. A ausência dessa exigência não define, por si só, que toda consulta será pública; esse aspecto permanece em aberto.

## Etapas da jornada

### Etapa TOR-01 — Entrar e escolher o caminho de consulta

- **Objetivo da etapa:** chegar às informações da competição necessárias ao acompanhamento.
- **Ação do usuário:** acessar a aplicação e escolher consultar classificação, clube, resultados ou desempenho.
- **Resposta do front-end:** apresentar os caminhos de consulta e sinalizar carregamento, sem exigir dados que não façam parte da jornada definida.
- **Processamento esperado no back-end:** disponibilizar as informações de navegação e, quando solicitada uma consulta, encaminhá-la ao conjunto de dados correspondente. O requisito não define autenticação do Torcedor.
- **Dados envolvidos:** seleção da área e, nas etapas seguintes, identificação do clube ou consulta solicitada.
- **Resposta retornada ao front-end:** conteúdo inicial ou confirmação de que a consulta escolhida está sendo processada.
- **Resultado percebido:** o Torcedor reconhece como chegar à informação desejada.
- **Erros ou alternativas:** indisponibilidade inicial deve ser comunicada. A forma de entrada, a navegação inicial e a necessidade de autenticação são definições em aberto.

### Etapa TOR-02 — Consultar a classificação

- **Objetivo da etapa:** identificar a posição dos clubes e os indicadores da tabela.
- **Ação do usuário:** solicitar a classificação.
- **Resposta do front-end:** indicar carregamento e, ao receber os dados, apresentar posição, clube, pontos, jogos, vitórias, empates, derrotas, gols marcados, gols sofridos e saldo de gols.
- **Processamento esperado no back-end:** consultar os dados de clubes e resultados, calcular ou obter os indicadores atualizados e ordenar conforme RN05.
- **Dados envolvidos:** clubes participantes, resultados válidos, estatísticas, pontuação e critérios oficiais de classificação.
- **Resposta retornada ao front-end:** classificação ordenada, indicadores por clube e informação de estado da consulta.
- **Resultado percebido:** o Torcedor consegue localizar a situação dos clubes no campeonato.
- **Erros ou alternativas:** informar classificação indisponível ou ainda sem dados; não apresentar uma ordenação como oficial se os dados necessários estiverem inconsistentes. A frequência de atualização percebida não está definida.

### Etapa TOR-03 — Consultar um clube e suas informações

- **Objetivo da etapa:** aprofundar a consulta sobre um clube participante.
- **Ação do usuário:** selecionar um clube a partir da classificação ou de outro caminho de navegação disponível.
- **Resposta do front-end:** identificar o clube selecionado, apresentar suas informações e oferecer acesso à consulta de desempenho relacionada.
- **Processamento esperado no back-end:** localizar o clube e retornar suas informações e estatísticas disponíveis, distinguindo os dados descritivos das estatísticas cobertas por RF04.
- **Dados envolvidos:** identificação do clube, informações cadastradas, resultados e estatísticas relacionadas.
- **Resposta retornada ao front-end:** informações do clube e indicação dos dados disponíveis.
- **Resultado percebido:** o Torcedor encontra o clube de interesse e consegue seguir para os detalhes de desempenho.
- **Erros ou alternativas:** clube inexistente, inativo ou sem dados deve ser distinguido de falha de consulta. O conjunto de informações cadastrais do clube não está especificado.

### Etapa TOR-04 — Consultar resultados de partidas realizadas

- **Objetivo da etapa:** verificar resultados registrados no campeonato.
- **Ação do usuário:** solicitar os resultados, partindo da navegação geral ou da consulta de um clube.
- **Resposta do front-end:** apresentar os resultados retornados e manter um caminho de navegação para a classificação ou o clube consultado.
- **Processamento esperado no back-end:** consultar partidas realizadas com resultado válido e retornar os dados registrados.
- **Dados envolvidos:** identificação da partida, clubes participantes, data/horário cadastrados e resultado válido, quando disponíveis.
- **Resposta retornada ao front-end:** conjunto de resultados e estado da consulta. Filtros por clube, período ou rodada não são definidos nesta análise.
- **Resultado percebido:** o Torcedor verifica os resultados disponíveis sem perder o contexto da competição.
- **Erros ou alternativas:** lista vazia deve ser diferenciada de indisponibilidade. Um resultado inconsistente não deve ser apresentado como definitivo.

### Etapa TOR-05 — Acompanhar estatísticas e evolução do clube

- **Objetivo da etapa:** entender o desempenho do clube durante a competição, não apenas consultar um dado isolado.
- **Ação do usuário:** solicitar o desempenho do clube selecionado.
- **Resposta do front-end:** apresentar vitórias, empates, derrotas e saldo de gols; apresentar a evolução do desempenho na medida em que os dados históricos definidos estiverem disponíveis.
- **Processamento esperado no back-end:** consolidar os resultados válidos do clube e retornar os indicadores de desempenho; para evolução, fornecer os dados históricos necessários, sem pressupor formato visual.
- **Dados envolvidos:** clube, partidas e resultados válidos, gols marcados/sofridos, saldo, vitórias, empates e derrotas.
- **Resposta retornada ao front-end:** estatísticas consolidadas e, se definida e disponível, a sequência histórica correspondente.
- **Resultado percebido:** o Torcedor entende o desempenho do clube e sua evolução no campeonato.
- **Erros ou alternativas:** sem partidas registradas, informar que ainda não há dados; inconsistência nos resultados deve ser comunicada sem produzir estatística enganosa. Granularidade e apresentação da evolução são pontos em aberto.

### Etapa TOR-06 — Navegar, retornar ou tratar consulta incompleta

- **Objetivo da etapa:** permitir a continuidade entre classificação, clube, resultados e desempenho.
- **Ação do usuário:** retornar à tabela, abrir outra informação relacionada ou repetir uma consulta após uma falha.
- **Resposta do front-end:** preservar o contexto conhecido quando possível e distinguir sucesso, ausência de dados, indisponibilidade e inconsistência.
- **Processamento esperado no back-end:** atender à nova consulta usando o estado válido dos dados; não mascarar ausência de informação como sucesso.
- **Dados envolvidos:** clube selecionado, consulta anterior e dados atualizados da competição.
- **Resposta retornada ao front-end:** conteúdo atualizado ou estado específico da consulta.
- **Resultado percebido:** o Torcedor consegue concluir a busca sem interpretar uma falha como dado esportivo.
- **Erros ou alternativas:** mensagens e eventual tentativa posterior precisam ser definidas; não se presume persistência de preferências ou seleção entre sessões.