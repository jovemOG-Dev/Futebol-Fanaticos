# Jornadas das Personas e Reavaliação dos Requisitos Funcionais

**Base de análise:** `docs/Requisitos da Aplicação — Futebol-Fanaticos.md` e os arquivos de persona e story em `docs/personas/`.

**Data:** 2026-10-06

**Escopo:** comportamento, responsabilidades, fluxos, dados e regras. Nenhuma tecnologia ou arquitetura é definida neste documento.

## Convenções da análise

- **Existente:** informação expressa nas personas, stories, requisitos ou regras atuais.
- **Inferência:** comportamento necessário para completar uma jornada, mas não especificado diretamente.
- **Proposta:** requisito sugerido para fechar uma lacuna; depende de validação do projeto e não deve ser tratado como decisão aprovada.
- Os requisitos não funcionais (RNF) e as regras de negócio (RN) continuam sendo restrições de apoio. Não são convertidos em requisitos funcionais apenas por serem citados nas jornadas.

## 1. Resumo da análise

As jornadas confirmam que os RF01–RF04 atendem ao objetivo do Torcedor, mas precisam esclarecer a separação entre informação cadastral do clube, estatísticas acumuladas e evolução ao longo do campeonato. RF05–RF09 dão suporte à manutenção da competição pelo Administrador. O RF10 é uma consequência necessária do RF09, não uma ação independente, e deve ser consolidado com ele. O RF11 contém duas capacidades distintas: consultar usuários e gerenciar usuários/níveis de acesso. O RF12 cobre a consulta de métricas, mas não define como os dados necessários são registrados ou calculados.

As jornadas também expõem comportamentos transversais que não aparecem como RF explícitos: autenticar usuários de áreas restritas, verificar autorização em cada operação protegida e retornar estados compreensíveis para acesso negado, ausência/indisponibilidade de dados, validação e conflito de integridade. As propostas correspondentes estão marcadas como **Novo — proposta**, sujeitas à validação do responsável pelo produto.

O fluxo de maior consequência cruzada é: **registrar/alterar resultado → manter um único resultado válido → atualizar estatísticas → recalcular classificação → disponibilizar o estado atualizado às consultas do Torcedor**. Pontuação, integridade, ordenação oficial e consistência continuam vinculadas às RN01–RN06 e RNF aplicáveis.

## 2. Jornada do Torcedor

J-TOR-01 detalha a consulta do Torcedor desde a entrada até a navegação entre classificação, clube, resultados e desempenho, incluindo dados indisponíveis ou inconsistentes. O documento preserva as etapas TOR-01 a TOR-06 para rastreabilidade.

**Jornada completa:** [docs/personas/torcedor/jornada.md](personas/torcedor/jornada.md)

## 3. Jornada do Investidor / Gestor

J-INV-01 detalha a entrada na área de indicadores, verificação de autorização, solicitação e apuração de métricas, análise e tratamento de acesso negado ou dados indisponíveis. As etapas INV-01 a INV-05 permanecem rastreáveis.

**Jornada completa:** [docs/personas/investidor/jornada.md](personas/investidor/jornada.md)

## 4. Jornada do Administrador

J-ADM-01 detalha autenticação e autorização, manutenção de clubes e partidas, propagação de resultados para estatísticas/classificação, gerenciamento de usuários e consulta de métricas quando autorizada. As etapas ADM-01 a ADM-07 permanecem rastreáveis.

**Jornada completa:** [docs/personas/administrador/jornada.md](personas/administrador/jornada.md)

## 5. Responsabilidades do Front-end

- Apresentar classificação, informações de clube, resultados, estatísticas e métricas retornadas pelo sistema.
- Disponibilizar ações coerentes com as jornadas: consultar, navegar, selecionar clube, submeter dados administrativos e solicitar métricas.
- Coletar as entradas previstas para clubes, partidas, resultados, usuários e níveis de acesso, após definição dos campos e operações.
- Apresentar estados distinguíveis de carregamento, sucesso, lista vazia/ausência de dados, dados indisponíveis, validação, conflito de integridade, autenticação necessária e acesso negado.
- Não exibir dados de métricas quando o acesso for negado nem apresentar informação parcial/inconsistente como definitiva.
- Preservar o contexto de navegação entre classificação, clube, resultados e desempenho, dentro da interação atual.
- Refletir a confirmação do back-end; não indicar uma alteração como concluída antes do retorno de sucesso.
- Atender aos requisitos de clareza e responsividade RNF04–RNF05. Não são definidos aqui estrutura visual, telas ou componentes.

## 6. Responsabilidades do Back-end

- Consultar e retornar clubes, partidas, resultados, classificação, estatísticas e métricas necessários a cada jornada.
- Processar cadastro, edição e remoção/desativação de clubes; cadastro de partidas; registro/atualização de resultados; e operações aprovadas sobre usuários/permissões.
- Aplicar RN01 (pontuação), RN02 (reflexo do resultado), RN03 (resultado válido único), RN04 (controle administrativo), RN05 (ordenação) e RN06 (acesso às métricas).
- Validar referências e integridade entre clubes, partidas, resultados, estatísticas e classificação.
- Verificar identidade e permissão antes de operações restritas, conforme política que o projeto definir.
- Apurar e retornar as métricas solicitadas conforme definições e recortes aprovados; registrar os dados de utilização necessários somente após validar a proposta de RF13.
- Retornar ao front-end resultado e estado da operação suficientes para distinguir sucesso, ausência de dados, indisponibilidade, validação, conflito e falta de autorização.
- Manter consistentes os dados após cadastro e atualização conforme RNF06 e atender aos requisitos de capacidade, disponibilidade e desempenho RNF01–RNF02 e RNF07.

## 7. Fluxos compartilhados entre as jornadas

### Dados esportivos e consultas

**Cadastro/atualização administrativa → persistência válida → consulta pelo Torcedor.** O front-end administrativo envia entradas e apresenta o resultado da operação; o back-end valida e mantém os dados; o front-end do Torcedor solicita e apresenta apenas o estado retornado.

### Resultado e classificação

**Registrar resultado → validar autorização e integridade → atualizar estatísticas → aplicar pontuação e ordenação → confirmar operação → disponibilizar novo estado às consultas.** RF09 revisado concentra o processamento que hoje aparece dividido entre RF09 e RF10. O fluxo deve evitar que resultado, estatísticas e classificação sejam apresentados em estados incompatíveis.

### Métricas e autorização

**Registrar dados de utilização (proposta) → verificar autorização → apurar indicadores → apresentar recorte e definições.** O Torcedor e o Administrador podem gerar consultas que interessem às métricas, mas a coleta, os perfis autorizados e o escopo dos dados precisam ser aprovados. A apresentação deve diferenciar falta de autorização de ausência de dados.

### Respostas e estados de erro

Em todas as jornadas, o back-end retorna um estado interpretável da operação; o front-end comunica o estado sem converter falha em ausência de dados, nem ausência de dados em valor zero. A lista de estados é uma proposta funcional transversal descrita em RF16.

## 8. Reavaliação dos requisitos funcionais existentes

| RF atual | Jornada/etapa atendida | Avaliação | Classificação | Destino na lista revisada |
|---|---|---|---|---|
| RF01 — Consultar classificação | J-TOR-01, TOR-02; J-ADM-01, ADM-05 como origem dos dados | Capacidade real e necessária. Os campos estão listados; atualização e ordenação dependem de RN02/RN05. Definir o estado a apresentar se dados estiverem ausentes/inconsistentes. | **Refinar** | RF01 |
| RF02 — Consultar clube | J-TOR-01, TOR-03 | Capacidade real, mas “informações e estatísticas” não delimita dados descritivos versus estatísticas de desempenho. Convém explicitar referência a RF04 para reduzir sobreposição. | **Refinar** | RF02 |
| RF03 — Consultar resultados | J-TOR-01, TOR-04 | Capacidade real. “Resultados das partidas realizadas” não define quais dados de partida são apresentados nem como ausência de resultados é distinguida de falha. Filtros não são exigidos pela fonte. | **Refinar** | RF03 |
| RF04 — Acompanhar desempenho | J-TOR-01, TOR-05; J-ADM-01, ADM-05 como origem dos dados | Necessidade real da persona/story. Os indicadores mínimos aparecem, mas “ao longo da competição” exige esclarecer como a evolução histórica será representada e com qual granularidade. | **Refinar** | RF04 |
| RF05 — Cadastrar clube | J-ADM-01, ADM-03 | Capacidade real e suficientemente identificável. Campos, validações e resposta de sucesso/erro dependem de definição dos dados do clube. | **Manter** | RF05 |
| RF06 — Editar clube | J-ADM-01, ADM-03 | Capacidade real e independente do cadastro inicial. Requer política de validação e preservação de integridade, sem detalhamento atual dos campos. | **Manter** | RF06 |
| RF07 — Remover clube | J-ADM-01, ADM-03 | Capacidade real, mas “remover ou desativar” representa comportamentos diferentes e as relações com partidas/resultados não estão definidas. | **Refinar** | RF07 |
| RF08 — Cadastrar partida | J-ADM-01, ADM-04 | Capacidade real. Clubes, data e horário são citados; “demais informações necessárias” é aberto e validações/conflitos não estão definidos. | **Refinar** | RF08 |
| RF09 — Registrar resultado | J-ADM-01, ADM-05 | Capacidade real. Precisa declarar seus efeitos obrigatórios em estatísticas e classificação, atualmente espalhados entre RF09/RF10 e RN02. | **Unificar** com RF10 | RF09 revisado |
| RF10 — Atualizar classificação | J-ADM-01, ADM-05; J-TOR-01, TOR-02 | Não é uma ação administrativa independente; é consequência do registro/atualização de resultado. Separado, pode permitir estados divergentes ou duplicar o fluxo. | **Unificar** com RF09 | RF09 revisado |
| RF11 — Gerenciar usuários | J-ADM-01, ADM-06 e ADM-01/02 | Capacidade real, mas reúne consulta, gerenciamento de contas e níveis de acesso. As operações incluídas não estão enumeradas. | **Dividir** | RF10 e RF11 revisados |
| RF12 — Consultar métricas | J-INV-01, INV-01–05; J-ADM-01, ADM-07 quando autorizado | Capacidade real e necessária. Lista os indicadores e requer autorização, mas não define período, fórmulas, fonte dos dados nem perfis autorizados. | **Refinar** | RF12; coleta proposta em RF13 |

Nenhum RF existente foi classificado como **Remover**: cada um está ligado a uma necessidade explícita. RF02 e RF04 têm potencial de sobreposição, mas não são redundantes se RF02 tratar informações do clube e RF04 tratar desempenho esportivo ao longo do campeonato.

## 9. Requisitos funcionais revisados

Os RF01–RF12 abaixo preservam e refinam capacidades existentes. RF13–RF16 são **propostas novas** derivadas das lacunas das jornadas; dependem de validação antes de serem consideradas requisitos aprovados.

| ID | Requisito | Descrição | Persona relacionada | Jornada relacionada | Status e observações/dependências |
|---|---|---|---|---|---|
| RF01 | Consultar classificação | O sistema deve retornar a classificação do campeonato com posição, clube, pontos, jogos, vitórias, empates, derrotas, gols marcados, gols sofridos e saldo de gols, ordenada conforme RN05 e baseada nos resultados válidos registrados. | Torcedor; dados mantidos pelo Administrador | J-TOR-01: TOR-02; J-ADM-01: ADM-05 | **Refinar** RF01 atual. Depende de RN01, RN02, RN05 e tratamento de dados indisponíveis/inconsistentes. |
| RF02 | Consultar informações de clube | O sistema deve permitir consultar informações cadastradas de um clube participante e indicar as estatísticas esportivas disponíveis por meio de RF04, sem duplicar sua definição. | Torcedor | J-TOR-01: TOR-03 | **Refinar** RF02 atual. Os campos informativos do clube ainda precisam ser definidos. |
| RF03 | Consultar resultados de partidas | O sistema deve permitir consultar resultados registrados de partidas realizadas, distinguindo resultado disponível, ausência de resultado e falha de consulta. | Torcedor | J-TOR-01: TOR-04 | **Refinar** RF03 atual. Filtros e campos exibidos não estão especificados e não são assumidos. |
| RF04 | Consultar desempenho e evolução de clube | O sistema deve apresentar, por clube, vitórias, empates, derrotas e saldo de gols e permitir acompanhar a evolução desses dados durante a competição conforme o histórico registrado. | Torcedor | J-TOR-01: TOR-03, TOR-05; J-ADM-01: ADM-05 | **Refinar** RF04 atual. Granularidade e forma de representar a evolução permanecem em aberto; gols marcados/sofridos são dados da classificação e devem ter apresentação coerente. |
| RF05 | Cadastrar clube | O sistema deve permitir que usuário com permissão administrativa cadastre um clube participante, validando os dados requeridos definidos para o cadastro. | Administrador | J-ADM-01: ADM-02, ADM-03 | **Manter** RF05 atual. Campos e validações precisam ser especificados; autorização é aplicada conforme RF15. |
| RF06 | Editar clube | O sistema deve permitir que usuário com permissão administrativa altere informações cadastradas de um clube, preservando a integridade dos dados relacionados. | Administrador | J-ADM-01: ADM-02, ADM-03 | **Manter** RF06 atual. Campos e validações precisam ser especificados; autorização é aplicada conforme RF15. |
| RF07 | Remover ou desativar clube | O sistema deve permitir que usuário com permissão administrativa solicite remoção ou desativação de clube e deve preservar a integridade das partidas, resultados e histórico associados conforme política definida. | Administrador | J-ADM-01: ADM-02, ADM-03 | **Refinar** RF07 atual. Remoção física, desativação e tratamento de vínculos são decisões em aberto; autorização é aplicada conforme RF15. |
| RF08 | Cadastrar partida | O sistema deve permitir que usuário com permissão administrativa cadastre partida informando clubes participantes, data, horário e demais campos que forem definidos, retornando validações ou conflitos. | Administrador | J-ADM-01: ADM-02, ADM-04 | **Refinar** RF08 atual. Campos complementares e regras de conflito precisam ser definidos; autorização é aplicada conforme RF15. |
| RF09 | Registrar resultado e atualizar dados da competição | O sistema deve permitir que usuário com permissão administrativa registre ou atualize o resultado de uma partida e, como consequência, mantenha um único resultado válido para partida finalizada, atualize estatísticas dos clubes envolvidos e atualize a classificação conforme RN01, RN02 e RN05. | Administrador; Torcedor como consumidor do estado atualizado | J-ADM-01: ADM-02, ADM-05; J-TOR-01: TOR-02, TOR-04, TOR-05 | **Unificar** RF09 e RF10 atuais. Depende de RN01–RN03, RN05, RNF06 e definição do tratamento de correções/conflitos. |
| RF10 | Consultar usuários | O sistema deve permitir que usuário com permissão adequada consulte os usuários e os níveis de acesso que esteja autorizado a visualizar. | Administrador | J-ADM-01: ADM-02, ADM-06 | **Dividir** RF11 atual. Escopo dos dados visíveis e permissões de consulta precisam ser definidos; não presume exposição de dados pessoais específicos. |
| RF11 | Gerenciar usuários e níveis de acesso | O sistema deve permitir que usuário com permissão administrativa execute as operações aprovadas de gerenciamento de usuários e de seus níveis de acesso. | Administrador | J-ADM-01: ADM-02, ADM-06 | **Dividir** RF11 atual. Operações incluídas e matriz de níveis/permissões são pontos em aberto; autorização é aplicada conforme RF15. |
| RF12 | Consultar métricas de utilização | O sistema deve permitir a usuários autorizados consultar número de acessos, quantidade de usuários, clubes mais consultados e frequência de consultas, informando o recorte e as definições aprovados para a apuração. | Investidor/Gestor; Administrador somente se autorizado | J-INV-01: INV-01–05; J-ADM-01: ADM-07 | **Refinar** RF12 atual. Depende de RN06, RF13 (proposta), RF15 e definições de período/indicadores. |
| RF13 | Registrar dados necessários às métricas | **Proposta:** o sistema deve registrar os eventos de utilização estritamente necessários para apurar as métricas aprovadas em RF12, incluindo consultas a clubes quando usadas para identificar os mais consultados. | Sistema; benefício para Investidor/Gestor | J-INV-01: INV-02–04; J-TOR-01: TOR-03 | **Novo — proposta/inferência necessária.** RF12 depende de dados de origem, mas a coleta não está explicitada. Eventos, escopo e tratamento precisam de validação; não define dados pessoais ou retenção. |
| RF14 | Autenticar usuário em áreas restritas | **Proposta:** o sistema deve verificar a identidade do usuário antes de permitir acesso a funcionalidades que exijam autenticação. | Administrador; usuários de métricas, se a política exigir | J-ADM-01: ADM-01; J-INV-01: INV-01 | **Novo — proposta.** Derivado de RNF03 e das jornadas de acesso restrito. Método, dados solicitados, sessão e regras de recuperação não são definidos. |
| RF15 | Verificar autorização por operação | **Proposta:** o sistema deve verificar se o usuário autenticado possui permissão para cada operação administrativa ou consulta de métrica protegida e negar a operação quando não possuir. | Administrador; Investidor/Gestor; outros usuários autorizados | J-ADM-01: ADM-02, ADM-03–07; J-INV-01: INV-01–02, INV-05 | **Novo — proposta de operacionalização** de RN04, RN06 e RNF03. Não cria novos perfis; a matriz de permissões deve ser definida. |
| RF16 | Comunicar o estado de consultas e operações | **Proposta:** o sistema deve retornar um estado distinguível de sucesso, ausência de dados, indisponibilidade, validação, conflito de integridade, autenticação necessária ou acesso negado, permitindo ao front-end informar o resultado sem apresentar dados incorretos como válidos. | Todas | J-TOR-01: TOR-02–06; J-INV-01: INV-01–05; J-ADM-01: ADM-01–07 | **Novo — proposta transversal.** Estados e mensagens são necessários para completar os fluxos de erro solicitados; vocabulário e comportamento de recuperação precisam ser definidos. |

## 10. Matriz de rastreabilidade

| Persona | Objetivo | Jornada | Etapa | Requisito funcional relacionado | Cobertura/observação |
|---|---|---|---|---|---|
| Torcedor | Chegar às informações do campeonato | J-TOR-01 | TOR-01 | RF01–RF04, RF16 | Navegação inicial não tem RF dedicado; comportamento de entrada é ponto de definição. |
| Torcedor | Consultar posição e situação dos clubes | J-TOR-01 | TOR-02 | RF01, RF09, RF16 | Coberto; depende dos resultados válidos e RN01/RN02/RN05. |
| Torcedor | Consultar informações de um clube | J-TOR-01 | TOR-03 | RF02, RF13, RF16 | RF02 cobre consulta; registrar consulta para métrica de clubes mais acessados depende da aprovação de RF13. |
| Torcedor | Consultar resultados de partidas | J-TOR-01 | TOR-04 | RF03, RF09, RF16 | Coberto; filtros não são requisito existente. |
| Torcedor | Acompanhar estatísticas e evolução | J-TOR-01 | TOR-05 | RF04, RF09, RF16 | Parcial até definir histórico e granularidade da evolução. |
| Torcedor | Navegar entre informações e entender falhas | J-TOR-01 | TOR-06 | RF01–RF04, RF16 | RF16 é proposta; navegação/contexto não tem comportamento formal detalhado. |
| Investidor/Gestor | Acessar indicadores com permissão | J-INV-01 | INV-01 | RF12, RF14, RF15, RF16 | RF12/RN06 cobrem autorização em princípio; identidade e perfis não estão definidos. |
| Investidor/Gestor | Solicitar métricas e recorte | J-INV-01 | INV-02 | RF12, RF13, RF15, RF16 | Solicitação coberta; parâmetros e período são pontos em aberto. |
| Investidor/Gestor | Obter métricas de uso e interesse | J-INV-01 | INV-03 | RF12, RF13, RF16 | RF12 lista métricas; RF13 é proposta para origem dos dados. |
| Investidor/Gestor | Analisar indicadores | J-INV-01 | INV-04 | RF12, RF16 | Cobertura parcial até definir significado, período e apresentação dos indicadores. |
| Investidor/Gestor | Entender negativa ou indisponibilidade | J-INV-01 | INV-05 | RF15, RF16 | RN06 determina restrição; resposta funcional detalhada é proposta em RF16. |
| Administrador | Autenticar-se para área restrita | J-ADM-01 | ADM-01 | RF14, RF16 | Não existe RF atual; RF14 é proposta baseada em RNF03 e jornada solicitada. |
| Administrador | Ter operação autorizada | J-ADM-01 | ADM-02 | RF15, RF16 | RN04/RN06 existem como regras; RF15 operacionaliza verificação. |
| Administrador | Manter clubes | J-ADM-01 | ADM-03 | RF05, RF06, RF07, RF15, RF16 | Capacidades cobertas; campos, remoção/desativação e vínculos estão incompletos. |
| Administrador | Cadastrar partidas | J-ADM-01 | ADM-04 | RF08, RF15, RF16 | Capacidade coberta; campos adicionais e conflitos precisam de definição. |
| Administrador | Registrar resultado e atualizar competição | J-ADM-01 | ADM-05 | RF09, RF15, RF16 | Coberto após unificar RF09/RF10; correção e comportamento em falha parcial em aberto. |
| Torcedor | Receber efeitos de novo resultado | J-TOR-01 | TOR-02, TOR-04, TOR-05 após ADM-05 | RF01, RF03, RF04, RF09, RF16 | Rastreia o efeito cruzado do fluxo administrativo nas consultas. |
| Administrador | Consultar usuários | J-ADM-01 | ADM-06 | RF10, RF15, RF16 | Coberto após divisão de RF11; dados visíveis dependem de definição. |
| Administrador | Gerenciar usuários e permissões | J-ADM-01 | ADM-06 | RF11, RF15, RF16 | Capacidade explícita, mas operações e matriz de acesso não estão detalhadas. |
| Administrador | Consultar métricas se autorizado | J-ADM-01 | ADM-07 | RF12, RF13, RF15, RF16 | Necessidade existe na persona; elegibilidade do Administrador não está decidida. |

Todos os requisitos revisados RF01–RF16 estão associados a uma etapa e a uma necessidade ou regra de acesso identificável. RF13–RF16 são propostas funcionais transversais ou derivadas, não capacidades aprovadas pela fonte original.

## 11. Lacunas funcionais

### Lacunas funcionais

1. **Origem das métricas:** RF12 solicita agregados, mas não há capacidade explícita para registrar os eventos necessários para calcular acessos, clubes mais consultados e frequência. RF13 propõe cobrir essa lacuna; aprovação e escopo da coleta são necessários.
2. **Autenticação funcional:** RNF03 exige autenticação e autorização para área administrativa, mas nenhum RF descreve a verificação da identidade. RF14 é uma proposta a validar.
3. **Autorização por operação:** RN04 e RN06 estabelecem restrições, mas não descrevem o comportamento que verifica e nega cada operação protegida. RF15 operacionaliza essas regras, sem decidir quais perfis recebem permissões.
4. **Estados de resposta e erro:** as jornadas precisam distinguir consulta vazia, falha/indisponibilidade, validação, conflito, autenticação e autorização. Não há RF transversal para isso; RF16 é proposta a validar.
5. **Evolução histórica do desempenho:** RF04 e a persona pedem acompanhamento ao longo da competição, mas a fonte não determina como histórico ou progresso é consultado nem a granularidade dos dados.

### Lacunas de definição

- Campos obrigatórios e conjunto de informações descritivas de clube.
- Política de remoção física versus desativação, preservação de partidas e resultados históricos.
- Campos adicionais de partida e regras para partidas conflitantes ou referências inválidas.
- O que constitui resultado válido, quais validações numéricas existem e como uma correção afeta estatísticas já calculadas.
- Procedimento e consistência esperada ao atualizar resultado, estatísticas e classificação.
- Critérios oficiais completos de desempate e dados requeridos para aplicá-los.
- Granularidade e forma de consulta da evolução do clube; representação visual não foi decidida.
- Operações incluídas em “gerenciar usuários”, dados que podem ser consultados e níveis de acesso disponíveis.
- Quem pode consultar métricas, incluindo se Investidor/Gestor e Administrador têm autorização.
- Definição de acesso, usuário, consulta, clube mais consultado e frequência; período de apuração e tratamento de duplicidades.
- Tratamento funcional de lista vazia, falha, indisponibilidade, conflito e nova tentativa.
- Necessidade de autenticação para consultas do Torcedor e demais áreas não administrativas.

## 12. Pontos em aberto

1. **Validar propostas RF13–RF16:** confirmar se a coleta de utilização, autenticação, verificação explícita de autorização e estados de resposta devem integrar o escopo funcional.
2. **Definir perfis e permissões:** indicar quem administra clubes/partidas/resultados/usuários, quem consulta métricas e se Investidor/Gestor constitui um perfil próprio.
3. **Definir autenticação:** especificar quais áreas exigem autenticação e o comportamento esperado para acesso sem identidade válida. Nenhum método técnico é proposto aqui.
4. **Definir métricas:** estabelecer período, fórmula, unidade e origem de cada indicador antes de disponibilizá-lo para análise.
5. **Definir coleta de utilização:** decidir quais eventos são necessários para RF12, incluindo se consultas a clubes serão contadas e com que regra.
6. **Definir classificação oficial:** registrar critérios de ordenação e dados necessários para desempates segundo RN05.
7. **Definir histórico de desempenho:** determinar que informação representa a evolução do clube e com qual frequência/granularidade será consultável.
8. **Definir política de integridade histórica:** esclarecer remoção/desativação de clubes e correção de resultados já refletidos nas estatísticas/classificação.
9. **Definir operações de usuários:** delimitar o que “gerenciar” permite além de consultar e alterar níveis de acesso.
10. **Definir respostas funcionais de erro:** aprovar estados que o sistema comunica e ações permitidas depois de cada estado, sem especificar formato técnico.

## 13. Conclusão

Os RF existentes cobrem as capacidades centrais das três personas, mas ainda não formam sozinhos fluxos ponta a ponta completamente verificáveis. A revisão preserva os requisitos legítimos, refina descrições vagas, consolida o recálculo da classificação ao registro do resultado e separa consulta de usuários do gerenciamento de acessos. As jornadas também tornam visíveis dependências entre administração, integridade esportiva, consulta pública e métricas.

RF13–RF16 são propostas para lacunas derivadas da análise, não decisões definitivas. Antes de implementação, o projeto deve validar essas propostas e resolver os pontos em aberto, em especial autorização, definição das métricas, atualização consistente de resultados e critérios oficiais de classificação.