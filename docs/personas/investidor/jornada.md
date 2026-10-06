# Jornada: Investidor / Gestor

**Jornada:** J-INV-01 — Consultar métricas de utilização

**Persona:** [Investidor / Gestor](persona.md)

**Story:** [Acompanhar utilização e interesse dos usuários](stories.md)

## Objetivo e escopo

**Objetivo principal:** analisar utilização e interesse dos usuários por meio dos indicadores disponíveis.

**Objetivos secundários:** comparar o volume de acessos, a quantidade de usuários, os clubes mais consultados e a frequência das consultas.

**Informações consultadas:** os quatro indicadores listados em RF12.

**Ações e entradas:** acessar a área de métricas e solicitar a consulta. Período, filtros e seleção de dimensões não estão definidos.

**Resultados esperados:** indicadores autorizados, interpretáveis e acompanhados de definições suficientes para análise.

**Restrições:** RN06 determina acesso apenas a usuários autorizados; os perfis autorizados e a associação do Investidor/Gestor a esses perfis não estão definidos.

## Etapas da jornada

### Etapa INV-01 — Acessar a área de indicadores

- **Objetivo da etapa:** iniciar a consulta de engajamento.
- **Ação do usuário:** acessar a área de indicadores da aplicação.
- **Resposta do front-end:** apresentar a área ou encaminhar a solicitação de acesso, sem expor métricas antes da verificação de autorização.
- **Processamento esperado no back-end:** identificar a sessão/usuário apresentada pela interação e verificar se há acesso permitido à área.
- **Dados envolvidos:** identidade e contexto de acesso, caso existam; política de autorização aplicável.
- **Resposta retornada ao front-end:** acesso permitido ou negado, ou necessidade de autenticação conforme a política definida.
- **Resultado percebido:** usuário autorizado prossegue; usuário sem autorização recebe uma resposta clara.
- **Erros ou alternativas:** o método de autenticação, os perfis autorizados e a resposta a uma sessão ausente/expirada são pontos em aberto.

### Etapa INV-02 — Solicitar as métricas

- **Objetivo da etapa:** solicitar dados para análise.
- **Ação do usuário:** pedir os indicadores de utilização. Selecionar período ou filtros só será possível se o projeto os definir.
- **Resposta do front-end:** indicar processamento e comunicar os critérios selecionados; não inventar um período padrão ou filtro não aprovado.
- **Processamento esperado no back-end:** validar autorização novamente para a operação e determinar o conjunto de dados segundo os critérios acordados.
- **Dados envolvidos:** autorização, eventos/dados de utilização e parâmetros de apuração que vierem a ser definidos.
- **Resposta retornada ao front-end:** confirmação de processamento ou erro de autorização/validação.
- **Resultado percebido:** o usuário sabe quais métricas e qual recorte está solicitando.
- **Erros ou alternativas:** parâmetros inválidos, recorte não definido ou falta de autorização devem ser distinguidos.

### Etapa INV-03 — Apurar acessos, usuários, clubes e frequência

- **Objetivo da etapa:** obter indicadores comparáveis para análise.
- **Ação do usuário:** aguardar o retorno da solicitação.
- **Resposta do front-end:** manter estado de processamento e não apresentar valores parciais como definitivos.
- **Processamento esperado no back-end:** apurar número de acessos, quantidade de usuários, clubes mais consultados e frequência de consultas a partir dos dados disponíveis e das definições acordadas.
- **Dados envolvidos:** registros de uso, identificadores de consulta/clube e definições de acesso, usuário, frequência e período. A coleta e a definição operacional não estão cobertas de forma suficiente nos RF atuais.
- **Resposta retornada ao front-end:** métricas, período/critério aplicado e estado de completude, quando definidos.
- **Resultado percebido:** o usuário recebe indicadores que pode interpretar dentro de um contexto conhecido.
- **Erros ou alternativas:** dados incompletos ou indisponíveis devem ser sinalizados; não se deve substituir valor desconhecido por zero.

### Etapa INV-04 — Analisar os indicadores

- **Objetivo da etapa:** compreender o uso da aplicação e o interesse pelos clubes.
- **Ação do usuário:** comparar os indicadores recebidos.
- **Resposta do front-end:** apresentar os quatro indicadores de maneira legível e associá-los ao recorte e às definições retornadas.
- **Processamento esperado no back-end:** retornar dados consistentes com a solicitação, sem alterar sua interpretação na apresentação.
- **Dados envolvidos:** valores agregados, definições e recorte de apuração, se estabelecidos.
- **Resposta retornada ao front-end:** conteúdo autorizado pronto para consulta.
- **Resultado percebido:** o Investidor/Gestor consegue examinar volume de uso e interesse relativo pelos clubes.
- **Erros ou alternativas:** se não houver ocorrências, indicar ausência de dados; falha de apuração deve ser diferente de resultado vazio.

### Etapa INV-05 — Tratar acesso negado ou métrica indisponível

- **Objetivo da etapa:** evitar exposição indevida e interpretações erradas.
- **Ação do usuário:** tentar acessar sem permissão ou consultar quando os dados não estão disponíveis.
- **Resposta do front-end:** informar acesso negado, ausência de dados ou indisponibilidade com estados distintos e sem exibir métricas protegidas.
- **Processamento esperado no back-end:** negar a operação protegida ou comunicar indisponibilidade/incompletude sem retornar dados não autorizados.
- **Dados envolvidos:** identidade, permissões, solicitação e estado da fonte de métricas.
- **Resposta retornada ao front-end:** resultado de autorização ou estado da consulta, sem conteúdo protegido quando o acesso for negado.
- **Resultado percebido:** o usuário entende por que não recebeu os indicadores.
- **Erros ou alternativas:** canal para solicitar acesso e política de nova tentativa não estão definidos.