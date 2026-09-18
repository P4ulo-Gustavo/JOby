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
    2. id_usuario -> foreign key (usuarios);                               |        --Chave estrangeira que representa o usuário que criou a organização
    3. nome -> varchar(100);                                               |        --Campo que representa o nome da organização
    4. descricao ->varchar(1024)->nullable();                              |        --Campo que representa a descrição da organização
    5. foto_organizacao - varchar(1024)->nullable();                       |        --Caminho do arquivo que representa a foto da organização
    6. ativo -> boolean->default(true);                                    |        --Campo que representa a atividade da organização
    7. criado_em -> datetime;                                              |        --Campo que representa a data de criação da conta
    8. atualizado_em -> datetime;                                          |        --Campo que representa a data de atualização da conta

# 1.3 - subgrupo_organizacao:

    1. id_subgrupo -> int primary key;                                     |        --Chave primaria que representa a relação subgrupo & organização
    2. id_organizacao -> int foreign key (organizacao);                    |        --chave secundária que introduz a organização do subgrupo
    3. nome -> varchar(50)->unique();                                      |        --Nome do subgrupo (unico dentro da organização)
    4. descricao -> varchar(1024)->nullable();                             |        --Descrição do subgrupo
    5. criado_em -> datetime;                                              |        --Data de criação daquele subgrupo
    6. atualizado_em -> datetime;                                          |        --Data de atualização nas informações do subgrupo

    unique(id_organizacao, nome);                                          |        --A organização só pode ter um subgrupo com o respectivo nome

# 1.4 - usuario_organizacao:

    1. id_usuario_organizacao -> int primary key;                             |        --Chave primaria que representa a relação usuario & organização
    2. id_usuario -> int foreign key (usuario);                               |        --chave secundária que introduz o usuário
    3. id_organizacao -> int foreign key (organizacao);                       |        --chave secundária que introduz a organização
    4. ativo -> boolean->default(true);                                       |        --Campo que representa a atividade do usuário
    5. leitura -> boolean->default(true);                                     |        --Campo que representa se o usuário tem permissão de leitura
    6. escrita -> boolean->default(true);                                     |        --Campo que representa se o usuário tem permissão de escrita
    7. gerenciar -> boolean->default(true);                                   |        --Campo que representa se o usuário tem permissão de gerenciar
    8. criado_em -> datetime;                                                 |        --Data de criação daquele usuário na organização
    9. atualizado_em -> datetime;                                             |        --Data de atualização nas informações do usuário na organização
    
    unique(id_usuario, id_organizacao);                                       |        --um usuário só pode estar presente em uma organização uma única vez

# 1.5 - subgrupo_usuario:

    1. id_subgrupo_usuario -> int primary key;                                |        --Chave primária que representa a relação subgrupo & usuário
    2. id_subgrupo -> int foreign key (subgrupo_organizacao);                 |        --Chave secundária que representa o subgrupo
    3. id_usuario -> int foreign key (usuarios);                              |        --chave secundária que representa o usuário
    4. ativo -> boolean -> default(true);                                     |        --Campo que representa a atividade do usuário no subgrupo
    5. criado_em -> datetime;                                                 |        --Data de criação daquele usuário no subgrupo
    6. atualizado_em -> datetime;                                             |        --Data de atualização nas informações do usuário no subgrupo
    
    unique(id_subgrupo, id_usuario);                                          |        --um usuário só pode estar presente em um subgrupo uma única vez

# 1.6 - secao: 
    1. id_secao - primary key;                                                |        --chave primária que representa a seção
    2. id_organizacao - foreign key (organizacao) -> nullable();              |        --chave que representa a organização em que a seção foi feita
    3. nome - varchar(100);                                                   |        --nome da seção
    4. cor - varchar(7)->default("#006f1bff");                              |        --cor da seção
    5. ativo -> boolean -> default(true);                                     |        --Campo que representa a atividade da seção
    6. criado_em - datetime;                                                  |        --Data de criação da seção
    7. atualizado_em - datetime;                                              |        --Data de atualização no âmbito da seção

    unique(id_organizacao, nome);                                             |        --A organização só pode ter uma seção com o respectivo nome
    
# 1.7 - notas:
    1. id_nota - int primary key;                                             |        --chave primária que representa as notas de um usuário
    2. id_usuario - int foreign key (usuario);                                |        --chave que representa o usuário que criou a nota   
    3. id_organizacao - int foreign key (organizacao) -> nullable();          |        --chave que representa a organização em que a nota foi feita (pode não ser feita em nenhuma)
    4. id_secao - int foreign key (secao) -> nullable();                      |        --chave que representa a seção da nota (pode não ser categorizada)
    5. id_subgrupo - int foreign key (subgrupo_organizacao) -> nullable();    |        --chave que representa o subgrupo em que a nota foi feita (pode não ser feito em nenhum)
    6. titulo - varchar(100);                                                 |        --titulo da nota
    7. texto - varchar(4096) -> nullable();                                   |        --texto da nota
    8. anexo - varchar(1024) -> nullable()                                    |        --Representa link de anexo para a nota
    9. ativo -> boolean -> default(true);                                     |        --representa se a nota está ativa
    10. restricao_subgrupo -> boolean -> default(false);                      |        --representa se a nota é restrita ao subgrupo
    11. criado_em - datetime;                                                 |        --Data de criação da nota
    12. lembrete_em - datetime -> nullable();                                 |        --Data de lembrete da nota
    13. atualizado_em - datetime;                                             |        --Data de atualização no âmbito da nota

# 1.8 - tarefas:

    1. id_tarefa - int primary key;                                           |        --chave primária que representa as tarefas de um usuário
    2. id_usuario - int foreign key (usuario);                                |        --chave que representa o usuário que criou a tarefa
    3. id_organizacao - int foreign key (organizacao) -> nullable();          |        --chave que representa a organização em que a tarefa foi feita (pode não ser feita em nenhuma)
    4. id_secao - int foreign key (secao) -> nullable();                      |        --chave que representa a seção da tarefa (pode não ser categorizada)
    5. id_subgrupo - int foreign key (subgrupo_organizacao) -> nullable();    |        --chave que representa o subgrupo em que a tarefa foi feita (pode não ser feito em nenhum)
    6. titulo - varchar(100);                                                 |        --titulo da tarefa
    7. descricao - varchar(2048)->nullable();                                 |        --descrição da tarefa
    8. status - enum('pendente', 'em progresso', 'concluida');                |        --status da tarefa
    9. restricao_subgrupo - boolean->default(false);                          |        --representa se a tarefa é restrita ao subgrupo
    10. restricao_quantidade - int(2)->default(1);                            |        --representa a quantidade de usuários que podem realizar a tarefa
    11. criado_em - datetime;                                                 |        --Data de criação da tarefa
    12. fim_prazo - date;                                                     |        --Data de fim da tarefa
    13. atualizado_em - datetime;                                             |        --Data de atualização no âmbito da tarefa

# 1.9 - usuario_tarefa:

    1. id_usuario_tarefa - primary key;                                       |        --chave primária que representa a relação usuario & tarefa
    2. id_usuario - foreign key (usuario);                                    |        --chave que representa o usuário na tarefa   
    3. id_tarefa - foreign key (tarefa);                                      |        --chave que representa a tarefa em que o usuario esta presente
    4. ativo - boolean->default(true);                                        |        --representa se a relação está ativa
    5. criado_em - datetime;                                                  |        --Data de criação da relação
    6. atualizado_em - datetime;                                              |        --Data de atualização no âmbito da relação


# 1.10 - link_nota_tarefa:

    1. id_nota_tarefa - primary key;                                          |       --chave primária que representa a relação nota & tarefa
    2. id_nota - foreign key (notas);                                         |       --chave que representa a nota
    3. id_tarefa - foreign key (tarefas);                                     |       --chave que representa a tarefa


# 1.11 - mural:
    1. id_mural - primary key;                                                |       --chave primária que representa os murais de um usuário
    2. id_usuario - foreign key (usuario);                                    |       --chave que representa o usuário que criou o mural   
    3. titulo - varchar(100);                                                 |       --titulo do mural
    4. texto - varchar(4096);                                                 |       --texto do mural
    5. id_organizacao - foreign key (organizacao) -> nullable();              |       --chave que representa a organização em que o mural foi feito (pode não ser feito em nenhuma)
    6. restricao_subgrupo - boolean->default(false);                          |       --representa se o mural é restrito ao subgrupo
    7. id_secao - foreign key (secao) -> nullable();                          |       --chave que representa a seção do mural (pode não ser categorizado)
    8. id_subgrupo - foreign key (subgrupo_organizacao) -> nullable();        |       --chave que representa o subgrupo em que o mural foi feito (pode não ser feito em nenhum)
    9. criado_em - datetime;                                                  |       --Data de criação do mural
    10. atualizado_em - datetime;                                             |       --Data de atualização no âmbito do mural

# 1.12 - arquivo_nuvem:
    1. id_arquivo - int primary key;                                          |       --chave primária que representa os arquivos de um usuário
    2. id_usuario - foreign key (usuario);                                    |       --chave que representa o usuário que criou o arquivo   
    3. titulo - varchar(100);                                                 |       --titulo do arquivo
    4. anexo - varchar(1024);                                                 |       --caminho do arquivo
    5. id_organizacao - foreign key (organizacao) -> nullable();              |       --chave que representa a organização em que o arquivo foi feito (pode não ser feito em nenhuma)
    6. restricao_subgrupo - boolean->default(false);                          |       --representa se o arquivo é restrito ao subgrupo
    7. id_secao - foreign key (secao) -> nullable();                          |       --chave que representa a seção do arquivo (pode não ser categorizado)
    8. id_subgrupo - foreign key (subgrupo_organizacao) -> nullable();        |       --chave que representa o subgrupo em que o arquivo foi feito (pode não ser feito em nenhum)
    9. criado_em - datetime;                                                  |       --Data de criação do arquivo

# 1.13 - chat_grupo:
    1. id_chat_grupo - int primary key;                                       |       --chave primária que representa os chats de um usuário
    2. id_usuario - foreign key (usuario);                                    |       --chave que representa o usuário que criou o chat   
    3. nome_chat - varchar(100);                                              |       --nome do chat
    4. descricao - varchar(2048);                                             |       --texto do chat
    5. id_organizacao - foreign key (organizacao);                            |       --chave que representa a organização em que o chat foi feito
    6. restricao_subgrupo - boolean->default(false);                          |       --representa se o chat é restrito ao subgrupo
    7. id_subgrupo - foreign key (subgrupo_organizacao) -> nullable();        |       --chave que representa o subgrupo em que o chat foi feito (pode não ser feito em nenhum)
    8. criado_em - datetime;                                                  |       --Data de criação do chat
    9. atualizado_em - datetime;                                              |       --Data de atualização no âmbito do chat

    unique(id_organizacao, nome_chat);                                        |       --O nome do chat deve ser único por organização
    

# 1.14 - mensagem_grupo:
    1. id_mensagem_grupo - int primary key;                                   |       --chave primária que representa as mensagens de um usuário
    2. id_chat_grupo - foreign key (chat_grupo);                              |       --chave que representa o chat em que a mensagem foi enviada
    3. id_usuario - foreign key (usuario);                                    |       --chave que representa o usuário que enviou a mensagem
    4. mensagem - text;                                                       |       --mensagem enviada
    5. anexo - varchar(255) -> nullable();                                    |       --anexo da mensagem
    6. criado_em - datetime;                                                  |       --Data de criação da mensagem
    7. atualizado_em - datetime;                                              |       --Data de atualização no âmbito da mensagem

# 1.15 usuario_chat_grupo:

    1. id_usuario_grupo - int primary key;                                     |       -- Relacionamento de usuario com chat em grupo
    2. id_chat_grupo - foreign key(chat_grupo);                                |       -- Grupo em que o usuário esta
    3. id_usuario - foreign key(usuario);                                      |       -- Usuario que está no grupo
    4. ativo - boolean->default(true);                                         |       -- Define se o usuário está ativo no grupo (não é permitido excluir) 
    5. cargo_usuario - enum('usuario', 'admin');                               |       -- define as permissões do usuário no chat
    6. criado_em - datetime();                                                 |       -- Data em que o usuário foi incluído no chat em grupo
    7. atualizado_em - datetime();                                             |       -- Data em que o usuário foi atualizado do chat

    unique(id_chat_grupo, id_usuario);                                         |       -- O usuário só pode fazer parte deste grupo 1 vez

# 1.16 - chat_privado:
    1. id_chat_privado - primary key;                                          |       --chave primária que representa a relação usuário & chat
    2. id_usuario_1 - foreign key(usuarios);                                   |       --usuario que esta no chat
    3. id_usuario_2 - foreign key(usuarios);                                   |       --usuário que também participa do chat
    4. criado_em - datetime();                                                 |       --data de criação do chat
    
    unique(id_usuario_1, id_usuario_2);                                          |       -- Só pode existir um chat privado entre estes dois indivíduos

# 1.17 - mensagem_privado:
    1. id_mensagem_privado - primary key;                                      |       --chave primária que representa as mensagens de um usuário
    2. id_chat_privado - foreign key(chat_privado);                            |       --chave que representa o chat em que a mensagem foi enviada
    3. id_usuario - foreign key(usuario);                                      |       --chave que representa o usuário que enviou a mensagem
    4. mensagem - text;                                                        |       --mensagem enviada
    5. anexo - varchar(1024) -> nullable();                                    |       --anexo da mensagem
    6. criado_em - datetime;                                                   |       --Data de criação da mensagem

# 1.18 - Perfil:

    id_perfil - int primary key;                                               |       --chave primaria que representa o perfil
    id_usuario - int foreign key (usuarios);                                   |       --chave que representa o usuário
    identificador - varchar(255) -> unique();                                  |       --identificador do usuário (#será gerado aleatoriamente pelo sistema)
    apelido - varchar(100) -> unique();                                        |       --apelido do usuário
    imagem_perfil - varchar(255);                                              |       --imagem do perfil
    criado_em - datetime;                                                      |       --Data de criação do perfil
    atualizado_em - datetime;                                                  |       --Data de atualização nas informações do perfil

    unique(id_usuario, identificador);                                         |       -- O usuário só pode ter um identificador por perfil

# 1.19 - notificação:
    1. id_notificacao - int primary key;                                       |       --chave primaria que representa a notificação
    2. id_usuario - int foreign key (usuarios);                                |       --chave que representa o usuário que recebeu a notificação
    3. titulo - varchar(100);                                                  |       --titulo da notificação
    4. mensagem - text;                                                        |       --mensagem da notificação
    5. tipo - enum('usuario', 'organizacao', 'subgrupo', 'tarefa', 'nota');    |       --tipo de notificação
    6. status - enum('lida', 'nao_lida');                                      |       --status da notificação
    7. criado_em - datetime;                                                   |       --Data de criação da notificação

# 1.20 - convite_organizacao:
    1. id_convite_usuario - int primary key;                                   |       --chave primaria que representa o convite
    2. id_organizacao - int foreign key (organizacao);                         |       --chave que representa a organização
    3. id_usuario - int foreign key (usuario);                                 |       --chave que representa o usuário
    4. status - enum('pendente', 'aceito', 'recusado');                        |       --status do convite
    5. criado_em - datetime;                                                   |       --Data de criação do convite
    












