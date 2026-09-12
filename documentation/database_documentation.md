# ===============================Representação da estrutura do banco de dados=====================================

# 1. Tabelas:

# 1.1 - usuarios:

    id_usuario - primary key;                                                   --chave primária do usuário
    nome_completo - varchar(100);                                               --Nome completo do usuário
    email - varchar(100) -> unique();                                           --Email do usuário, único pois será utilizado para autenticação e ações na aplicação
    telefone - varchar(11) -> unique();                                         --Telefone do usuário
    senha - varchar(255);                                                       --senha do usuário hasheada em aragon2i (para maior segurança)
    ativo - boolean->default(true);                                             --representar a atividade do usuário dentro da aplicação
    remember_me - boolean->default(false);                                      --representa a opção de manter o usuário logado no sistema pelo navegador
    create_at - datetime;                                                       --Representa a data de criação da conta
    update_at - datetime;

# 1.2 - organizacao:

    id_organizacao - primary key;                                               --chave primária da organização
    nome_organizacao - varchar(100);                                            --Nome da organização
    criador_organizacao - foreign key(id_usuario);                              --Criador da organização, referenciado por um usuário
    descricao - varchar(255);                                                   --Descrição curta da organização (para aparecer no perfil)
    create_at - datetime;                                                       --Data de criação da organização
    update_at - datetime;                                                       --Data de atualização no âmbito da organização (descrição, nome, recrutamento, suspensão, etc)
    excluse_at - datetime;                                                      --Data de exclusão, para caso a organização seja deletada

# 1.3 - subgrupo_organizacao:

    id_subgrupo_organizacao - primary key;                                      --Chave primaria que representa a relação subgrupo & organização
    id_organizacao - foreign key;                                               --chave secundária que introduz a organização do subgrupo
    nome - varchar(50)->unique();                                               --Nome do subgrupo (unico dentro da organização)
    descricao - varchar(255);                                                   --Descrição do subgrupo
    creat_at - datetime                                                         --Data de criação daquele subgrupo
    update_at - datetime                                                        --data de atualização nas informações do subgrupo
    excluse_at - datetime                                                       --Data em que aquele subgrupo foi excluído da organização

    unique(id_organizacao, nome);                                               --um subgrupo só pode ter um nome por organização
    

# 1.3 - usuario_organizacao:

    id_usuario_organização - primary key;                                        --chave primária que representa a relação usuario & organização
    id_usuario - foreign key (usuarios);                                         --chave que representa o usuário na organização   
    id_organizacao - foreign key (organizacao)                                   --chave que representa a organização em que o usuarios esta presente
    ler - boolean->default(true);                                                --representa se o usuário pode ler notificações, posts, tarefas, etc ...
    escrever - boolean->default(false);                                          --representa se o usuário pode escrever no mural, tarefas, notas, etc ...
    gerenciar - boolean->default(false);                                         --representa se o usuário pode gerenciar a organização (con exceção de exclusão)
    subgrupo - foreign key(subgrupo_organizacao) -> nullable();                  --chave que representa a que subgrupo aquele usuario pertence (pode não pertencer a nenhum)
    create_at - datetime;                                                        --data em que aquele usuario entrou na organização
    update_at - datetime;                                                        --Data em que aquele usuário teve alguma modificação no subgrupo
    excluse_at - datetime;                                                       --Data em que aquele usuário foi excluido da organização

    unique(id_usuario, subgrupo, id_organizacao);                                 --um usuário só pode estar presente em um subgrupo uma única vez por organização
    

# 1.4 - notas:
    id_notas - primary key;                                                       --chave primária que representa as notas de um usuário
    id_usuario - foreign key (usuario);                                           --chave que representa o usuário que criou a nota   
    titulo - varchar(100);                                                        --titulo da nota
    texto - text;                                                                 --texto da nota
    organizacao - foreign key (organizacao) -> nullable();                        --chave que representa a organização em que a nota foi feita (pode não ser feita em nenhuma)
    restricao_subgrupo - boolean                                                  --representa se a nota é restrita ao subgrupo
    categoria - foreign key (categorias) -> nullable();                           --chave que representa a categoria da nota (pode não ser categorizada)
    subgrupo - foreign key (subgrupo_organizacao) -> nullable();                  --chave que representa o subgrupo em que a nota foi feita (pode não ser feito em nenhum)
    create_at - datetime;                                                         --Data de criação da nota
    update_at - datetime;                                                         --Data de atualização no âmbito da nota
    excluse_at - datetime;                                                        --Data de exclusão, para caso a organização seja deletada

# 1.5 - tarefas:

    id_tarefa - primary key;                                                      --chave primária que representa as tarefas de um usuário
    id_usuario - foreign key (usuario);                                           --chave que representa o usuário que criou a tarefa   
    titulo - varchar(100);                                                        --titulo da tarefa
    descricao - varchar(255);                                                     --descrição da tarefa
    status - enum('pendente', 'em progresso', 'concluida');                       --status da tarefa
    organizacao - foreign key (organizacao) -> nullable();                        --chave que representa a organização em que a tarefa foi feita (pode não ser feita em nenhuma)
    subgrupo - foreign key (subgrupo_organizacao) -> nullable();                  --chave que representa o subgrupo em que a tarefa foi feita (pode não ser feito em nenhum)
    categoria - foreign key (categorias) -> nullable();                           --chave que representa a categoria da tarefa (pode não ser categorizada)
    restricao_subgrupo - boolean                                                  --representa se a tarefa é restrita ao subgrupo
    restricao_quantidade - int(2);                                                --representa a quantidade de usuários que podem realizar a tarefa
    inicio_prazo - datetime;                                                      --data de inicio da tarefa
    fim_prazo - datetime;                                                         --data de fim da tarefa
    create_at - datetime;                                                         --Data de criação da tarefa
    update_at - datetime;                                                         --Data de atualização no âmbito da tarefa
    excluse_at - datetime;                                                        --Data de exclusão, para caso a organização seja deletada

# 1.6 - usuario_tarefa:

    id_usuario_tarefa - primary key;                                              --chave primária que representa a relação usuario & tarefa
    id_usuario - foreign key (usuario);                                           --chave que representa o usuário na tarefa   
    id_tarefa - foreign key (tarefa);                                             --chave que representa a tarefa em que o usuario esta presente
    create_at - datetime;                                                         --Data de criação da relação
    update_at - datetime;                                                         --Data de atualização no âmbito da relação
    excluse_at - datetime;                                                        --Data de exclusão, para caso a relação seja deletada

# 1.7 - mural:
    id_mural - primary key;                                                       --chave primária que representa os murais de um usuário
    id_usuario - foreign key (usuario);                                           --chave que representa o usuário que criou o mural   
    titulo - varchar(100);                                                        --titulo do mural
    texto - text;                                                                 --texto do mural
    organizacao - foreign key (organizacao) -> nullable();                        --chave que representa a organização em que o mural foi feito (pode não ser feito em nenhuma)
    restricao_subgrupo - boolean                                                  --representa se o mural é restrito ao subgrupo
    categoria - foreign key (categorias) -> nullable();                           --chave que representa a categoria do mural (pode não ser categorizado)
    subgrupo - foreign key (subgrupo_organizacao) -> nullable();                  --chave que representa o subgrupo em que o mural foi feito (pode não ser feito em nenhum)
    create_at - datetime;                                                         --Data de criação do mural
    update_at - datetime;                                                         --Data de atualização no âmbito do mural
    excluse_at - datetime;                                                        --Data de exclusão, para caso a organização seja deletada

# 1.8 - chats:
    id_chat - primary key;                                                        --chave primária que representa os chats de um usuário
    id_usuario - foreign key (usuario);                                           --chave que representa o usuário que criou o chat   
    titulo - varchar(100);                                                        --titulo do chat
    texto - text;                                                                 --texto do chat
    organizacao - foreign key (organizacao) -> nullable();                        --chave que representa a organização em que o chat foi feito (pode não ser feito em nenhuma)
    restricao_subgrupo - boolean                                                  --representa se o chat é restrito ao subgrupo
    subgrupo - foreign key (subgrupo_organizacao) -> nullable();                  --chave que representa o subgrupo em que o chat foi feito (pode não ser feito em nenhum)
    create_at - datetime;                                                         --Data de criação do chat
    update_at - datetime;                                                         --Data de atualização no âmbito do chat
    excluse_at - datetime;                                                        --Data de exclusão, para caso a organização seja deletada
    
# 1.9 - mensagem:
    id_mensagem - primary key;                                                    --chave primária que representa as mensagens de um usuário
    id_chat - foreign key (chat);                                                 --chave que representa o chat em que a mensagem foi enviada
    id_usuario - foreign key (usuario);                                           --chave que representa o usuário que enviou a mensagem
    mensagem - text;                                                              --mensagem enviada
    anexo - varchar(255) -> nullable();                                           --anexo da mensagem
    create_at - datetime;                                                         --Data de criação da mensagem
    update_at - datetime;                                                         --Data de atualização no âmbito da mensagem
    excluse_at - datetime;                                                        --Data de exclusão, para caso a mensagem seja deletada
    
# 1.10 - arquivo_nuvem:
    id_arquivo - primary key;                                                     --chave primária que representa os arquivos de um usuário
    id_usuario - foreign key (usuario);                                           --chave que representa o usuário que criou o arquivo   
    titulo - varchar(100);                                                        --titulo do arquivo
    texto - text;                                                                 --texto do arquivo
    organizacao - foreign key (organizacao) -> nullable();                        --chave que representa a organização em que o arquivo foi feito (pode não ser feito em nenhuma)
    restricao_subgrupo - boolean                                                  --representa se o arquivo é restrito ao subgrupo
    categoria - foreign key (categorias) -> nullable();                           --chave que representa a categoria do arquivo (pode não ser categorizado)
    subgrupo - foreign key (subgrupo_organizacao) -> nullable();                  --chave que representa o subgrupo em que o arquivo foi feito (pode não ser feito em nenhum)
    create_at - datetime;                                                         --Data de criação do arquivo
    update_at - datetime;                                                         --Data de atualização no âmbito do arquivo
    excluse_at - datetime;                                                        --Data de exclusão, para caso a organização seja deletada
    
# 1.11 - link_nota_tarefa:

    id_nota_tarefa - primary key;                                                 --chave primária que representa a relação nota & tarefa
    id_nota - foreign key (notas);                                                --chave que representa a nota
    id_tarefa - foreign key (tarefas);                                            --chave que representa a tarefa
    id_usuario - foreign key (usuario);                                           --chave que representa o usuário que criou o link
    id_organizacao - foreign key (organizacao) -> nullable();                     --chave que representa a organização em que o link foi feito (pode não ser feito em nenhuma)
    id_subgrupo - foreign key (subgrupo_organizacao) -> nullable();               --chave que representa o subgrupo em que o link foi feito (pode não ser feito em nenhum)
    id_categoria - foreign key (categorias) -> nullable();                        --chave que representa a categoria do link (pode não ser categorizado)
    create_at - datetime;                                                         --Data de criação da relação
    update_at - datetime;                                                         --Data de atualização no âmbito da relação
    excluse_at - datetime;                                                        --Data de exclusão, para caso a relação seja deletada

# 1.12 - Categoria: 
    id_categoria - primary key;                                                   --chave primária que representa a categoria
    id_organizacao - foreign key (organizacao);                                 --chave que representa a organização em que a categoria foi feita
    nome - varchar(100);                                                          --nome da categoria
    cor - varchar(7);                                                             --cor da categoria
    create_at - datetime;                                                         --Data de criação da categoria
    update_at - datetime;                                                         --Data de atualização no âmbito da categoria
    excluse_at - datetime;                                                        --Data de exclusão, para caso a categoria seja deletada


# 2. Relacionamento:

# 2.1 Usuario: 

    1. Usuario -- (1:N) --> Notas
    2. Usuario -- (1:N) --> Tarefas
    3. Usuario -- (1:N) --> Usuario_organizacao
    4. Usuario -- (1:N) --> Subgrupo
    5. Usuario -- (1:N) --> Tarefa_realizante
    6. Usuario -- (1:N) --> Link_nota_tarefa

# 2.2 - Organização:

    1. Organização --(1:N)--> Categoria
    2. Organização --(1:N)--> Subgrupo
    3. Organização --(1:N)--> Usuario_organizacao
    4. Organização --(1:N)--> Tarefa
    5. Organização --(1:N)--> Nota
    6. Organização --(1:N)--> Chat
    7. Organização --(1:N)--> Arquivo_nuvem
    8. Organização --(1:N)--> Link_nota_tarefa

# 2.3 - Categoria:

    1. Categoria --(1:N)--> Tarefa
    2. Categoria --(1:N)--> Nota
    3. Categoria --(1:N)--> Arquivo_nuvem
    4. Categoria --(1:N)--> Link_nota_tarefa

# 2.4 - 








