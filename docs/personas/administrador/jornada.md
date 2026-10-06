# Jornada: Administrador

**Jornada:** J-ADM-01 — Manter competição e controlar acessos

**Persona:** [Administrador](persona.md)

**Story:** [Administrar dados da competição e acessos](stories.md)

## Objetivo e escopo

**Objetivo principal:** manter informações da competição e acessos de forma controlada e íntegra.

**Objetivos secundários:** consultar indicadores administrativos quando autorizado e assegurar que as consultas do Torcedor reflitam os dados válidos.

**Informações consultadas:** clubes, partidas, resultados, usuários, níveis de acesso e, se autorizado, métricas.

**Ações e entradas:** autenticar-se; cadastrar, editar ou remover/desativar clube; cadastrar partidas; registrar/atualizar resultados; consultar/gerenciar usuários e níveis de acesso; consultar métricas quando autorizado.

**Resultados esperados:** confirmação ou recusa clara, dados persistidos de forma consistente e classificação/estatísticas atualizadas após resultados.

**Restrições:** RN04 restringe operações de competição a usuários com permissão administrativa; RN06 restringe métricas a usuários autorizados; RN01–RN03 e RN05 governam resultados e classificação.

## Etapas da jornada

### Etapa ADM-01 — Autenticar e iniciar uma operação restrita

- **Objetivo da etapa:** estabelecer a identidade necessária para administrar a aplicação.
- **Ação do usuário:** apresentar os dados de autenticação que o projeto vier a definir e solicitar acesso à área administrativa.
- **Resposta do front-end:** solicitar os dados definidos, indicar processamento e apresentar o resultado sem revelar detalhes protegidos.
- **Processamento esperado no back-end:** verificar a identidade e estabelecer ou recusar o contexto autenticado.
- **Dados envolvidos:** dados de autenticação e estado da identidade. Os campos e o fluxo não estão especificados.
- **Resposta retornada ao front-end:** autenticação aceita ou recusada.
- **Resultado percebido:** o Administrador sabe se pode prosseguir.
- **Erros ou alternativas:** credenciais inválidas, identidade indisponível ou sessão expirada são cenários a especificar. Autenticação é requisito funcional proposto a partir de RNF03, ainda sujeito à validação.

### Etapa ADM-02 — Validar permissão para cada operação

- **Objetivo da etapa:** impedir operações administrativas ou consulta de métricas sem autorização.
- **Ação do usuário:** escolher uma operação de manutenção ou solicitar métricas.
- **Resposta do front-end:** oferecer ações compatíveis com o estado conhecido e, ao receber uma negativa, informar acesso negado sem simular sucesso.
- **Processamento esperado no back-end:** conferir identidade e permissão para a operação solicitada, aplicando RN04 ou RN06 conforme o caso.
- **Dados envolvidos:** identidade autenticada, permissão, recurso e ação solicitados.
- **Resposta retornada ao front-end:** autorização ou negativa para a operação.
- **Resultado percebido:** somente operações permitidas podem prosseguir.
- **Erros ou alternativas:** permissão ausente, revogada ou identidade não autenticada deve resultar em recusa; a matriz de perfis e permissões permanece em aberto.

### Etapa ADM-03 — Cadastrar, editar ou remover/desativar clubes

- **Objetivo da etapa:** manter os clubes participantes e suas informações.
- **Ação do usuário:** cadastrar ou editar dados do clube, ou solicitar sua remoção/desativação.
- **Resposta do front-end:** apresentar os campos que forem definidos, permitir confirmar a operação e informar o resultado.
- **Processamento esperado no back-end:** validar a autorização, processar a alteração solicitada e preservar as relações e a integridade dos dados conforme RF07 e RNF06.
- **Dados envolvidos:** informações do clube e referências a partidas/resultados relacionados, se existentes.
- **Resposta retornada ao front-end:** confirmação com estado atualizado ou recusa com motivo compreensível.
- **Resultado percebido:** o Administrador sabe se o clube foi mantido, alterado ou removido/desativado.
- **Erros ou alternativas:** conflito com dados relacionados, informação inválida, clube inexistente ou falta de permissão. Campos cadastrais, política de remoção e tratamento de histórico são pontos em aberto.

### Etapa ADM-04 — Cadastrar uma partida

- **Objetivo da etapa:** registrar uma partida da competição.
- **Ação do usuário:** informar clubes participantes, data, horário e demais dados necessários definidos pelo projeto.
- **Resposta do front-end:** coletar os dados definidos e apresentar erros de validação sem descartar entradas válidas.
- **Processamento esperado no back-end:** verificar autorização, validar as referências e os dados recebidos segundo regras aprovadas e registrar a partida.
- **Dados envolvidos:** clubes participantes, data, horário e outros campos ainda não especificados.
- **Resposta retornada ao front-end:** partida registrada ou conjunto de erros/conflitos detectados.
- **Resultado percebido:** o Administrador confirma o cadastro ou entende o que impede a operação.
- **Erros ou alternativas:** clube inexistente/inativo, dados incompletos ou conflito de integridade; critérios de validação e regras de conflito não estão detalhados.

### Etapa ADM-05 — Registrar ou atualizar um resultado e propagar seus efeitos

- **Objetivo da etapa:** registrar um resultado válido e refletir seus efeitos na competição.
- **Ação do usuário:** selecionar a partida e informar ou atualizar seu resultado.
- **Resposta do front-end:** solicitar os dados definidos, confirmar o alvo da operação e apresentar sucesso ou conflito.
- **Processamento esperado no back-end:**
  1. verificar a autorização administrativa;
  2. validar partida e resultado;
  3. garantir um único resultado válido para partida finalizada (RN03);
  4. registrar ou atualizar o resultado;
  5. atualizar estatísticas dos clubes envolvidos (RN02);
  6. recalcular pontuação conforme RN01 e classificação conforme RN05;
  7. manter consistentes resultado, estatísticas e classificação (RNF06).
- **Dados envolvidos:** partida, clubes participantes, resultado, resultados anteriores, estatísticas derivadas e classificação.
- **Resposta retornada ao front-end:** confirmação do estado final válido, estatísticas/classificação resultantes ou erro de validação/conflito. A consulta do Torcedor deve passar a receber o estado atualizado após a conclusão da operação.
- **Resultado percebido:** o Administrador confirma a atualização e o Torcedor pode consultar a classificação e o desempenho derivados do resultado.
- **Erros ou alternativas:** partida inexistente, resultado inválido conforme regras a definir, conflito com resultado válido, falha parcial ou dados inconsistentes. O comportamento de correção/reversão e a garantia de atualização conjunta precisam ser definidos.

### Etapa ADM-06 — Consultar e gerenciar usuários e níveis de acesso

- **Objetivo da etapa:** administrar usuários e seus níveis de acesso.
- **Ação do usuário:** consultar usuários e solicitar as operações de gerenciamento/permissão definidas.
- **Resposta do front-end:** apresentar os usuários e níveis que o Administrador esteja autorizado a consultar e permitir as ações aprovadas.
- **Processamento esperado no back-end:** validar a autorização administrativa, consultar usuários e processar alterações permitidas nos níveis de acesso.
- **Dados envolvidos:** usuário, nível/permissão atual e alteração solicitada.
- **Resposta retornada ao front-end:** dados autorizados ou confirmação/recusa da alteração.
- **Resultado percebido:** o Administrador consegue revisar e manter os níveis de acesso permitidos.
- **Erros ou alternativas:** usuário inexistente, conflito de permissão ou operação não autorizada. RF11 não especifica quais operações de gerenciamento de usuários estão incluídas.

### Etapa ADM-07 — Consultar métricas administrativas, se autorizado

- **Objetivo da etapa:** consultar indicadores de utilização quando o perfil do Administrador estiver autorizado.
- **Ação do usuário:** solicitar métricas administrativas.
- **Resposta do front-end:** apresentar os indicadores apenas após autorização e informar ausência/indisponibilidade de dados.
- **Processamento esperado no back-end:** verificar RN06, apurar RF12 segundo as definições aprovadas e retornar somente dados autorizados.
- **Dados envolvidos:** identidade, permissões e métricas de uso.
- **Resposta retornada ao front-end:** indicadores autorizados ou acesso negado/estado de indisponibilidade.
- **Resultado percebido:** o Administrador consulta os indicadores permitidos, sem presumir que toda permissão administrativa inclui métricas.
- **Erros ou alternativas:** perfis autorizados, indicadores administrativos e política de apresentação precisam ser definidos.