# ===============================Representação da estrutura do banco de dados=====================================

# 1. Tabelas:

# 1.1 - usuarios:

    1. id_usuario -> int primary key;                                      |       -- Chave primária que representa o usuário
    2. nome_completo -> varchar(100);                                      |       -- Campo que representa o nome completo do usuário
    3. email -> varchar(100) -> unique();                                  |       -- Campo que representa o email do usuário
    4. telefone -> varchar(11) -> unique();                                |       -- Campo que representa o telefone do usuário
    5. senha -> varchar(255);                                              |       -- Campo que representa a senha do usuário
    6. ativo -> boolean->default(true);                                    |       -- Campo que representa a atividade do usuário
    7. remember_me -> boolean->default(false);                             |       -- Campo que representa a opção de manter o usuário logado no sistema
    8. criado_em -> datetime;                                              |       -- Campo que representa a data de criação da conta
    9. atualizado_em -> datetime;                                          |       -- Campo que representa a data de atualização da conta
    10. ultimo_login -> datetime;                                          |       -- Campo que representa a data do ultimo login


# 1.2 - organizacao:

    1. id_organizacao -> int primary key;                                  |        --Chave primária que representa a organização
    2. id_usuario -> int foreign key (usuarios);                           |        --Chave estrangeira que representa o usuário que criou a organização
    3. nome -> varchar(100);                                               |        --Campo que representa o nome da organização
    4. descricao -> varchar(1024)->nullable();                             |        --Campo que representa a descrição da organização
    5. foto_organizacao -> varchar(1024)->nullable();                      |        --Caminho do arquivo que representa a foto da organização
    6. ativo -> boolean->default(true);                                    |        --Campo que representa a atividade da organização
    7. criado_em -> datetime;                                              |        --Campo que representa a data de criação da conta
    8. atualizado_em -> datetime;                                          |        --Campo que representa a data de atualização da conta

# 1.3 - subgrupo_organizacao:

    1. id_subgrupo -> int primary key;                                     |        --Chave primaria que representa a relação subgrupo & organização
    2. id_organizacao -> int foreign key (organizacao);                    |        --chave secundária que introduz a organização do subgrupo
    3. nome -> varchar(50);                                                |        --Nome do subgrupo
    4. descricao -> varchar(1024)->nullable();                             |        --Descrição do subgrupo
    5. criado_em -> datetime;                                              |        --Data de criação daquele subgrupo
    6. atualizado_em -> datetime;                                          |        --Data de atualização nas informações do subgrupo

    unique(id_organizacao, nome);                                          |        --A organização só pode ter um subgrupo com o respectivo nome

# 1.4 - usuario_organizacao:

    1. id_usuario_organizacao -> int primary key;                          |        --Chave primaria que representa a relação usuario & organização
    2. id_usuario -> int foreign key (usuarios);                           |        --chave secundária que introduz o usuário
    3. id_organizacao -> int foreign key (organizacao);                    |        --chave secundária que introduz a organização
    4. ativo -> boolean->default(true);                                    |        --Campo que representa a atividade do usuário
    5. leitura -> boolean->default(true);                                  |        --Campo que representa se o usuário tem permissão de leitura
    6. escrita -> boolean->default(true);                                  |        --Campo que representa se o usuário tem permissão de escrita
    7. gerenciar -> boolean->default(true);                                |        --Campo que representa se o usuário tem permissão de gerenciar
    8. criado_em -> datetime;                                              |        --Data de criação daquele usuário na organização
    9. atualizado_em -> datetime;                                          |        --Data de atualização nas informações do usuário na organização
    
    unique(id_usuario, id_organizacao);                                    |        --um usuário só pode estar presente em uma organização uma única vez

# 1.5 - subgrupo_usuario:

    1. id_subgrupo_usuario -> int primary key;                             |        --Chave primária que representa a relação subgrupo & usuário
    2. id_subgrupo -> int foreign key (subgrupo_organizacao);              |        --Chave secundária que representa o subgrupo
    3. id_usuario -> int foreign key (usuarios);                           |        --chave secundária que representa o usuário
    4. ativo -> boolean->default(true);                                    |        --Campo que representa a atividade do usuário no subgrupo
    5. criado_em -> datetime;                                              |        --Data de criação daquele usuário no subgrupo
    6. atualizado_em -> datetime;                                          |        --Data de atualização nas informações do usuário no subgrupo
    
    unique(id_subgrupo, id_usuario);                                       |        --um usuário só pode estar presente em um subgrupo uma única vez

# 1.6 - secao: 
    1. id_secao -> int primary key;                                        |        --chave primária que representa a seção
    2. id_organizacao -> int foreign key (organizacao) -> nullable();       |        --chave que representa a organização em que a seção foi feita
    3. id_usuario -> int foreign key (usuarios);                           |        --chave que representa o usuário que criou a seção
    4. nome -> varchar(100);                                               |        --nome da seção
    5. cor -> varchar(9)->default("#006f1bff");                            |        --cor da seção
    6. ativo -> boolean->default(true);                                    |        --Campo que representa a atividade da seção
    7. criado_em -> datetime;                                              |        --Data de criação da seção
    8. atualizado_em -> datetime;                                          |        --Data de atualização no âmbito da seção

    unique(id_organizacao, nome);                                          |        --A organização só pode ter uma seção com o respectivo nome
    unique(id_usuario, nome);                                              |        --O usuário só pode ter uma seção privada com o respectivo nome (quando id_organizacao for nulo)
    
# 1.7 - notas:
    1. id_nota -> int primary key;                                         |        --chave primária que representa as notas de um usuário
    2. id_usuario -> int foreign key (usuarios);                           |        --chave que representa o usuário que criou a nota   
    3. id_organizacao -> int foreign key (organizacao) -> nullable();      |        --chave que representa a organização em que a nota foi feita (pode não ser feita em nenhuma)
    4. id_secao -> int foreign key (secao) -> nullable();                  |        --chave que representa a seção da nota (pode não ser categorizada)
    5. id_subgrupo -> int foreign key (subgrupo_organizacao) -> nullable();|        --chave que representa o subgrupo em que a nota foi feita (pode não ser feito em nenhum)
    6. titulo -> varchar(100);                                             |        --titulo da nota
    7. texto -> varchar(4096)->nullable();                                 |        --texto da nota
    8. anexo -> varchar(1024)->nullable();                                 |        --Representa link de anexo para a nota
    9. ativo -> boolean->default(true);                                    |        --representa se a nota está ativa
    10. restricao_subgrupo -> boolean->default(false);                     |        --representa se a nota é restrita ao subgrupo
    11. criado_em -> datetime;                                             |        --Data de criação da nota
    12. lembrete_em -> datetime->nullable();                               |        --Data de lembrete da nota
    13. atualizado_em -> datetime;                                         |        --Data de atualização no âmbito da nota

# 1.8 - tarefas:

    1. id_tarefa -> int primary key;                                       |        --chave primária que representa as tarefas de um usuário
    2. id_usuario -> int foreign key (usuarios);                           |        --chave que representa o usuário que criou a tarefa
    3. id_organizacao -> int foreign key (organizacao) -> nullable();      |        --chave que representa a organização em que a tarefa foi feita (pode não ser feita em nenhuma)
    4. id_secao -> int foreign key (secao) -> nullable();                  |        --chave que representa a seção da tarefa (pode não ser categorizada)
    5. id_subgrupo -> int foreign key (subgrupo_organizacao) -> nullable();|        --chave que representa o subgrupo em que a tarefa foi feita (pode não ser feito em nenhum)
    6. titulo -> varchar(100);                                             |        --titulo da tarefa
    7. descricao -> varchar(2048)->nullable();                             |        --descrição da tarefa
    8. status -> enum('pendente', 'em progresso', 'concluida');            |        --status da tarefa
    9. restricao_subgrupo -> boolean->default(false);                      |        --representa se a tarefa é restrita ao subgrupo
    10. restricao_quantidade -> int(2)->default(1);                        |        --representa a quantidade de usuários que podem realizar a tarefa
    11. criado_em -> datetime;                                             |        --Data de criação da tarefa
    12. fim_prazo -> date;                                                 |        --Data de fim da tarefa
    13. atualizado_em -> datetime;                                         |        --Data de atualização no âmbito da tarefa

# 1.9 - usuario_tarefa:

    1. id_usuario_tarefa -> int primary key;                               |        --chave primária que representa a relação usuario & tarefa
    2. id_usuario -> int foreign key (usuarios);                           |        --chave que representa o usuário na tarefa   
    3. id_tarefa -> int foreign key (tarefas);                             |        --chave que representa a tarefa em que o usuario esta presente
    4. ativo -> boolean->default(true);                                    |        --representa se a relação está ativa
    5. criado_em -> datetime;                                              |        --Data de criação da relação
    6. atualizado_em -> datetime;                                          |        --Data de atualização no âmbito da relação

    unique(id_usuario, id_tarefa);                                         |        --Só pode existir uma relação entre o usuário e a tarefa


# 1.10 - link_nota_tarefa:

    1. id_nota_tarefa -> int primary key;                                      |       --chave primária que representa a relação nota & tarefa
    2. id_nota -> int foreign key (notas);                                     |       --chave que representa a nota
    3. id_tarefa -> int foreign key (tarefas);                                 |       --chave que representa a tarefa

    unique(id_nota, id_tarefa);                                                |       --Só pode existir uma relação entre a nota e a tarefa


# 1.11 - mural:
    1. id_mural -> int primary key;                                            |       --chave primária que representa os murais de um usuário
    2. id_usuario -> int foreign key (usuarios);                               |       --chave que representa o usuário que criou o mural   
    3. titulo -> varchar(100);                                                 |       --titulo do mural
    4. texto -> varchar(4096);                                                 |       --texto do mural
    5. id_organizacao -> int foreign key (organizacao) -> nullable();          |       --chave que representa a organização em que o mural foi feito (pode não ser feito em nenhuma)
    6. restricao_subgrupo -> boolean->default(false);                          |       --representa se o mural é restrito ao subgrupo
    7. id_secao -> int foreign key (secao) -> nullable();                      |       --chave que representa a seção do mural (pode não ser categorizado)
    8. id_subgrupo -> int foreign key (subgrupo_organizacao) -> nullable();    |       --chave que representa o subgrupo em que o mural foi feito (pode não ser feito em nenhum)
    9. criado_em -> datetime;                                                  |       --Data de criação do mural
    10. atualizado_em -> datetime;                                             |       --Data de atualização no âmbito do mural

# 1.12 - arquivo_nuvem:
    1. id_arquivo -> int primary key;                                          |       --chave primária que representa os arquivos de um usuário
    2. id_usuario -> int foreign key (usuarios);                               |       --chave que representa o usuário que criou o arquivo   
    3. titulo -> varchar(100);                                                 |       --titulo do arquivo
    4. anexo -> varchar(1024);                                                 |       --caminho do arquivo
    5. id_organizacao -> int foreign key (organizacao) -> nullable();          |       --chave que representa a organização em que o arquivo foi feito (pode não ser feito em nenhuma)
    6. restricao_subgrupo -> boolean->default(false);                          |       --representa se o arquivo é restrito ao subgrupo
    7. id_secao -> int foreign key (secao) -> nullable();                      |       --chave que representa a seção do arquivo (pode não ser categorizado)
    8. id_subgrupo -> int foreign key (subgrupo_organizacao) -> nullable();    |       --chave que representa o subgrupo em que o arquivo foi feito (pode não ser feito em nenhum)
    9. criado_em -> datetime;                                                  |       --Data de criação do arquivo
    10. atualizado_em -> datetime;                                             |       --Data de atualização no âmbito do arquivo

# 1.13 - chat_grupo:
    1. id_chat_grupo -> int primary key;                                       |       --chave primária que representa os chats de um usuário
    2. id_usuario -> int foreign key (usuarios);                               |       --chave que representa o usuário que criou o chat   
    3. nome_chat -> varchar(100);                                              |       --nome do chat
    4. descricao -> varchar(2048)->nullable();                                 |       --texto do chat
    5. id_organizacao -> int foreign key (organizacao);                        |       --chave que representa a organização em que o chat foi feito
    6. restricao_subgrupo -> boolean->default(false);                          |       --representa se o chat é restrito ao subgrupo
    7. id_subgrupo -> int foreign key (subgrupo_organizacao) -> nullable();    |       --chave que representa o subgrupo em que o chat foi feito (pode não ser feito em nenhum)
    8. criado_em -> datetime;                                                  |       --Data de criação do chat
    9. atualizado_em -> datetime;                                              |       --Data de atualização no âmbito do chat

    unique(id_organizacao, nome_chat);                                        |       --O nome do chat deve ser único por organização
    

# 1.14 - mensagem_grupo:
    1. id_mensagem_grupo -> int primary key;                                   |       --chave primária que representa as mensagens de um usuário
    2. id_chat_grupo -> int foreign key (chat_grupo);                          |       --chave que representa o chat em que a mensagem foi enviada
    3. id_usuario -> int foreign key (usuarios);                               |       --chave que representa o usuário que enviou a mensagem
    4. mensagem -> text;                                                       |       --mensagem enviada
    5. anexo -> varchar(255)->nullable();                                      |       --anexo da mensagem
    6. criado_em -> datetime;                                                  |       --Data de criação da mensagem
    7. atualizado_em -> datetime;                                              |       --Data de atualização no âmbito da mensagem

# 1.15 usuario_chat_grupo:

    1. id_usuario_grupo -> int primary key;                                    |       -- Relacionamento de usuario com chat em grupo
    2. id_chat_grupo -> int foreign key (chat_grupo);                          |       -- Grupo em que o usuário esta
    3. id_usuario -> int foreign key (usuarios);                               |       -- Usuario que está no grupo
    4. ativo -> boolean->default(true);                                        |       -- Define se o usuário está ativo no grupo (não é permitido excluir) 
    5. cargo_usuario -> enum('usuario', 'admin');                              |       -- define as permissões do usuário no chat
    6. criado_em -> datetime;                                                  |       -- Data em que o usuário foi incluído no chat em grupo
    7. atualizado_em -> datetime;                                              |       -- Data em que o usuário foi atualizado do chat

    unique(id_chat_grupo, id_usuario);                                         |       -- O usuário só pode fazer parte deste grupo 1 vez

# 1.16 - chat_privado:
    1. id_chat_privado -> int primary key;                                     |       --chave primária que representa a relação usuário & chat
    2. id_usuario_1 -> int foreign key (usuarios);                             |       --usuario que esta no chat
    3. id_usuario_2 -> int foreign key (usuarios);                             |       --usuário que também participa do chat
    4. criado_em -> datetime;                                                  |       --data de criação do chat
    
    unique(id_usuario_1, id_usuario_2); check(id_usuario_1 < id_usuario_2);    |       -- Só pode existir um chat privado entre estes dois indivíduos (ordenado)

# 1.17 - mensagem_privado:
    1. id_mensagem_privado -> int primary key;                                 |       --chave primária que representa as mensagens de um usuário
    2. id_chat_privado -> int foreign key (chat_privado);                      |       --chave que representa o chat em que a mensagem foi enviada
    3. id_usuario -> int foreign key (usuarios);                               |       --chave que representa o usuário que enviou a mensagem
    4. mensagem -> text;                                                       |       --mensagem enviada
    5. anexo -> varchar(1024)->nullable();                                     |       --anexo da mensagem
    6. criado_em -> datetime;                                                  |       --Data de criação da mensagem

# 1.18 - Perfil:

    1. id_perfil -> int primary key;                                           |       --chave primaria que representa o perfil
    2. id_usuario -> int foreign key (usuarios)->unique();                     |       --chave que representa o usuário
    3. identificador -> varchar(255)->unique();                                |       --identificador do usuário (#será gerado aleatoriamente pelo sistema)
    4. apelido -> varchar(100)->unique();                                      |       --apelido do usuário
    5. imagem_perfil -> varchar(255)->nullable();                              |       --imagem do perfil
    6. criado_em -> datetime;                                                  |       --Data de criação do perfil
    7. atualizado_em -> datetime;                                              |       --Data de atualização nas informações do perfil


# 1.19 - notificação:
    1. id_notificacao -> int primary key;                                      |       --chave primaria que representa a notificação
    2. id_usuario -> int foreign key (usuarios);                               |       --chave que representa o usuário que recebeu a notificação
    3. titulo -> varchar(100);                                                 |       --titulo da notificação
    4. mensagem -> text;                                                       |       --mensagem da notificação
    5. tipo -> enum('usuario', 'organizacao', 'subgrupo', 'tarefa', 'nota', 'convite', 'mensagem', 'mural'); | --tipo de notificação
    6. id_referencia -> int->nullable();                                       |       --ID do item referenciado (ex: id_tarefa, id_convite)
    7. status -> enum('lida', 'nao_lida')->default('nao_lida');                |       --status da notificação
    8. criado_em -> datetime;                                                  |       --Data de criação da notificação

# 1.20 - convite_organizacao:
    1. id_convite_organizacao -> int primary key;                              |       --chave primaria que representa o convite
    2. id_organizacao -> int foreign key (organizacao);                        |       --chave que representa a organização
    3. id_usuario -> int foreign key (usuarios);                               |       --chave que representa o usuário
    4. status -> enum('pendente', 'aceito', 'recusado')->default('pendente');   |       --status do convite
    5. criado_em -> datetime;                                                  |       --Data de criação do convite
    6. atualizado_em -> datetime->nullable();                                  |       --Data de resposta/atualização do convite
    
    unique(id_organizacao, id_usuario, status);                                |       --Evita envio repetido de convites no mesmo status

# 2. Relacionamentos

# 2.1 - usuarios:
   1. usuarios --(1,n)--> organizacao                  | Um usuário pode criar uma ou muitas organizações (criador)
   2. usuarios --(1,n)--> usuario_organizacao          | Um usuário pode estar em uma ou mais organizações (membro)
   3. usuarios --(1,n)--> subgrupo_usuario             | Um usuário pode estar associado a um ou mais subgrupos
   4. usuarios --(1,n)--> secao                        | Um usuário pode criar uma ou muitas seções
   5. usuarios --(1,n)--> notas                        | Um usuário pode criar uma ou muitas notas
   6. usuarios --(1,n)--> tarefas                      | Um usuário pode criar uma ou muitas tarefas
   7. usuarios --(1,n)--> usuario_tarefa               | Um usuário pode estar atribuído a uma ou muitas tarefas
   8. usuarios --(1,n)--> mural                        | Um usuário pode criar uma ou muitas publicações no mural
   9. usuarios --(1,n)--> arquivo_nuvem                | Um usuário pode fazer upload de um ou muitos arquivos em nuvem
   10. usuarios --(1,n)--> chat_grupo                  | Um usuário pode criar um ou muitos chats em grupo
   11. usuarios --(1,n)--> mensagem_grupo              | Um usuário pode enviar uma ou muitas mensagens em chats de grupo
   12. usuarios --(1,n)--> usuario_chat_grupo          | Um usuário pode participar de um ou muitos chats em grupo
   13. usuarios --(1,n)--> chat_privado                | Um usuário pode participar de um ou muitos chats privados (como usuario_1 ou usuario_2)
   14. usuarios --(1,n)--> mensagem_privado            | Um usuário pode enviar uma ou muitas mensagens em chats privados
   15. usuarios --(1,1)--> perfil                      | Um usuário possui um único perfil
   16. usuarios --(1,n)--> notificacao                 | Um usuário pode receber uma ou muitas notificações
   17. usuarios --(1,n)--> convite_organizacao         | Um usuário pode receber um ou muitos convites de organizações

# 2.2 - organizacao:
   1. organizacao --(n,1)--> usuarios                  | Uma organização pertence a um usuário (criador)
   2. organizacao --(1,n)--> subgrupo_organizacao      | Uma organização pode conter um ou muitos subgrupos
   3. organizacao --(1,n)--> usuario_organizacao       | Uma organização pode ter um ou muitos membros vinculados
   4. organizacao --(1,n)--> secao                     | Uma organização pode ter uma ou muitas seções
   5. organizacao --(1,n)--> notas                     | Uma organização pode conter uma ou muitas notas vinculadas
   6. organizacao --(1,n)--> tarefas                   | Uma organização pode conter uma ou muitas tarefas vinculadas
   7. organizacao --(1,n)--> mural                     | Uma organização pode conter uma ou muitas publicações no mural
   8. organizacao --(1,n)--> arquivo_nuvem             | Uma organização pode conter um ou muitos arquivos em nuvem vinculados
   9. organizacao --(1,n)--> chat_grupo                | Uma organização pode ter um ou muitos chats em grupo
   10. organizacao --(1,n)--> convite_organizacao      | Uma organização pode emitir um ou muitos convites para usuários

# 2.3 - subgrupo_organizacao:
   1. subgrupo_organizacao --(n,1)--> organizacao      | Um subgrupo pertence a uma única organização
   2. subgrupo_organizacao --(1,n)--> subgrupo_usuario | Um subgrupo pode conter um ou muitos usuários vinculados
   3. subgrupo_organizacao --(1,n)--> notas            | Um subgrupo pode conter uma ou muitas notas vinculadas
   4. subgrupo_organizacao --(1,n)--> tarefas          | Um subgrupo pode conter uma ou muitas tarefas vinculadas
   5. subgrupo_organizacao --(1,n)--> mural            | Um subgrupo pode conter uma ou muitas publicações no mural
   6. subgrupo_organizacao --(1,n)--> arquivo_nuvem    | Um subgrupo pode conter um ou muitos arquivos em nuvem vinculados
   7. subgrupo_organizacao --(1,n)--> chat_grupo       | Um subgrupo pode ter um ou muitos chats em grupo vinculados

# 2.4 - usuario_organizacao:
   1. usuario_organizacao --(n,1)--> usuarios          | Cada vínculo pertence a um usuário
   2. usuario_organizacao --(n,1)--> organizacao       | Cada vínculo pertence a uma organização

# 2.5 - subgrupo_usuario:
   1. subgrupo_usuario --(n,1)--> subgrupo_organizacao | Cada vínculo pertence a um subgrupo
   2. subgrupo_usuario --(n,1)--> usuarios             | Cada vínculo pertence a um usuário

# 2.6 - secao:
   1. secao --(n,1)--> organizacao                     | Uma seção pode pertencer a uma organização (opcional / nullable)
   2. secao --(n,1)--> usuarios                        | Uma seção pertence ao usuário que a criou
   3. secao --(1,n)--> notas                           | Uma seção pode conter uma ou muitas notas categorizadas
   4. secao --(1,n)--> tarefas                         | Uma seção pode conter uma ou muitas tarefas categorizadas
   5. secao --(1,n)--> mural                           | Uma seção pode conter uma ou muitas publicações no mural categorizadas
   6. secao --(1,n)--> arquivo_nuvem                   | Uma seção pode conter um ou muitos arquivos categorizados

# 2.7 - notas:
   1. notas --(n,1)--> usuarios                        | Uma nota pertence ao usuário que a criou
   2. notas --(n,1)--> organizacao                     | Uma nota pode pertencer a uma organização (opcional / nullable)
   3. notas --(n,1)--> secao                           | Uma nota pode pertencer a uma seção (opcional / nullable)
   4. notas --(n,1)--> subgrupo_organizacao            | Uma nota pode pertencer a um subgrupo (opcional / nullable)
   5. notas --(1,n)--> link_nota_tarefa                | Uma nota pode estar vinculada a uma ou muitas tarefas através da tabela associativa

# 2.8 - tarefas:
   1. tarefas --(n,1)--> usuarios                      | Uma tarefa pertence ao usuário que a criou
   2. tarefas --(n,1)--> organizacao                   | Uma tarefa pode pertencer a uma organização (opcional / nullable)
   3. tarefas --(n,1)--> secao                         | Uma tarefa pode pertencer a uma seção (opcional / nullable)
   4. tarefas --(n,1)--> subgrupo_organizacao          | Uma tarefa pode pertencer a um subgrupo (opcional / nullable)
   5. tarefas --(1,n)--> usuario_tarefa                | Uma tarefa pode ter um ou muitos usuários atribuídos a ela
   6. tarefas --(1,n)--> link_nota_tarefa              | Uma tarefa pode estar vinculada a uma ou muitas notas através da tabela associativa

# 2.9 - usuario_tarefa:
   1. usuario_tarefa --(n,1)--> usuarios               | Cada atribuição pertence a um usuário
   2. usuario_tarefa --(n,1)--> tarefas                | Cada atribuição pertence a uma tarefa

# 2.10 - link_nota_tarefa:
   1. link_nota_tarefa --(n,1)--> notas                | Cada vínculo pertence a uma nota
   2. link_nota_tarefa --(n,1)--> tarefas              | Cada vínculo pertence a uma tarefa

# 2.11 - mural:
   1. mural --(n,1)--> usuarios                        | Uma publicação no mural pertence ao usuário que a criou
   2. mural --(n,1)--> organizacao                     | Uma publicação no mural pode pertencer a uma organização (opcional / nullable)
   3. mural --(n,1)--> secao                           | Uma publicação no mural pode pertencer a uma seção (opcional / nullable)
   4. mural --(n,1)--> subgrupo_organizacao            | Uma publicação no mural pode pertencer a um subgrupo (opcional / nullable)

# 2.12 - arquivo_nuvem:
   1. arquivo_nuvem --(n,1)--> usuarios                | Um arquivo em nuvem pertence ao usuário que fez o upload
   2. arquivo_nuvem --(n,1)--> organizacao             | Um arquivo em nuvem pode pertencer a uma organização (opcional / nullable)
   3. arquivo_nuvem --(n,1)--> secao                   | Um arquivo em nuvem pode pertencer a uma seção (opcional / nullable)
   4. arquivo_nuvem --(n,1)--> subgrupo_organizacao    | Um arquivo em nuvem pode pertencer a um subgrupo (opcional / nullable)

# 2.13 - chat_grupo:
   1. chat_grupo --(n,1)--> usuarios                   | Um chat em grupo pertence ao usuário que o criou
   2. chat_grupo --(n,1)--> organizacao                | Um chat em grupo pertence a uma organização
   3. chat_grupo --(n,1)--> subgrupo_organizacao       | Um chat em grupo pode pertencer a um subgrupo (opcional / nullable)
   4. chat_grupo --(1,n)--> mensagem_grupo             | Um chat em grupo pode conter uma ou muitas mensagens
   5. chat_grupo --(1,n)--> usuario_chat_grupo         | Um chat em grupo pode ter um ou muitos membros participantes

# 2.14 - mensagem_grupo:
   1. mensagem_grupo --(n,1)--> chat_grupo             | Uma mensagem de grupo pertence a um único chat em grupo
   2. mensagem_grupo --(n,1)--> usuarios               | Uma mensagem de grupo pertence ao usuário que a enviou

# 2.15 - usuario_chat_grupo:
   1. usuario_chat_grupo --(n,1)--> chat_grupo         | Cada vínculo pertence a um chat em grupo
   2. usuario_chat_grupo --(n,1)--> usuarios           | Cada vínculo pertence a um usuário participante

# 2.16 - chat_privado:
   1. chat_privado --(n,1)--> usuarios (id_usuario_1)  | Um chat privado referencia o primeiro usuário participante
   2. chat_privado --(n,1)--> usuarios (id_usuario_2)  | Um chat privado referencia o segundo usuário participante
   3. chat_privado --(1,n)--> mensagem_privado         | Um chat privado pode conter uma ou muitas mensagens

# 2.17 - mensagem_privado:
   1. mensagem_privado --(n,1)--> chat_privado         | Uma mensagem privada pertence a um único chat privado
   2. mensagem_privado --(n,1)--> usuarios             | Uma mensagem privada pertence ao usuário que a enviou

# 2.18 - perfil:
   1. perfil --(1,1)--> usuarios                       | Um perfil pertence exclusivamente a um único usuário

# 2.19 - notificacao:
   1. notificacao --(n,1)--> usuarios                  | Uma notificação pertence ao usuário destinatário

# 2.20 - convite_organizacao:
   1. convite_organizacao --(n,1)--> organizacao       | Um convite pertence à organização que o enviou
   2. convite_organizacao --(n,1)--> usuarios          | Um convite pertence ao usuário convidado


