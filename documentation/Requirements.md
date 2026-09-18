# ===============================Requisitos da Aplicação JOby=====================================

# 1. Requisitos Funcionais (RF):

# 1.1 - Módulo de Usuário e Autenticação:
    RF001. Deve permitir o cadastro, login e gerenciamento de conta do usuário            |       -- (Alta Importância)
    RF002. Deve permitir a gestão de Perfil (identificador, apelido e foto)               |       -- (Alta Importância)
    RF003. Deve registrar o último acesso para controle de inatividade                    |       -- (Média Importância)
    RF004. Deve permitir a reativação de contas inativadas por falta de uso               |       -- (Média Importância)

# 1.2 - Módulo de Organizações e Colaboradores:
    RF005. Deve permitir a criação e gerenciamento de Organizações (nome, foto, desc)     |       -- (Alta Importância)
    RF006. Deve permitir a gestão de Convites para organizações (pendente/aceito/recusado)|       -- (Alta Importância)
    RF007. Deve permitir a gestão de membros e permissões (leitura, escrita, gerenciar)   |       -- (Alta Importância)
    RF008. Deve permitir a criação e gestão de Subgrupos/Setores na organização           |       -- (Alta Importância)
    RF009. Deve permitir associar membros a um ou mais subgrupos                          |       -- (Alta Importância)

# 1.3 - Módulo de Tarefas, Notas e Categorias:
    RF010. Deve permitir o gerenciamento de Tarefas (privadas e organizacionais)          |       -- (Alta Importância)
    RF011. Deve permitir a atribuição de tarefas a um ou mais usuários                    |       -- (Alta Importância)
    RF012. Deve permitir o gerenciamento de Notas/Anotações com suporte a lembretes       |       -- (Alta Importância)
    RF013. Deve permitir a criação de Seções/Categorias coloridas (privadas e da org)     |       -- (Alta Importância)
    RF014. Deve permitir a vinculação (link) entre Notas e Tarefas                        |       -- (Média Importância)

# 1.4 - Módulo de Comunicação e Produtividade:
    RF015. Deve disponibilizar Mural de Avisos para organizações e subgrupos              |       -- (Alta Importância)
    RF016. Deve permitir a gestão do Armazenamento em Nuvem (upload e controle)           |       -- (Alta Importância)
    RF017. Deve disponibilizar Chat em Grupo por Organização com suporte a anexos         |       -- (Média Importância)
    RF018. Deve disponibilizar Chat Privado (1 para 1) entre usuários                     |       -- (Média Importância)
    RF019. Deve notificar usuários sobre tarefas, convites, mensagens e alertas           |       -- (Média Importância)
    RF020. Deve emitir relatórios de atividades e desempenho de tarefas                   |       -- (Média Importância)


# 2. Requisitos Não Funcionais (RNF):

    RNF001. Interface Responsiva -> Funcional em Desktop, Notebook, Tablets e Smartphones |       -- (Alta Importância)
    RNF002. Segurança e LGPD -> Criptografia de senhas e proteção de dados pessoais       |       -- (Alta Importância)
    RNF003. Controle de Acesso -> Autorização baseada em permissões por middleware        |       -- (Alta Importância)
    RNF004. Desempenho e Carga -> Suportar pelo menos 100 acessos simultâneos             |       -- (Média Importância)
    RNF005. Integridade de Dados -> Tratamento de chaves estrangeiras e relacionamentos   |       -- (Alta Importância)


# 3. Regras de Negócio (RN):

    RN001. Um usuário pode utilizar o sistema em modo Privado (pessoal) ou Organizacional |       -- (Escopo de Uso)
    RN002. Tarefas e notas pessoais só são visíveis pelo próprio criador                  |       -- (Privacidade)
    RN003. O criador da organização possui controle total sobre membros e permissões      |       -- (Hierarquia)
    RN004. O nome do subgrupo deve ser único dentro da mesma organização                  |       -- (Unicidade)
    RN005. O nome da Seção/Categoria deve ser único dentro do mesmo escopo                |       -- (Unicidade)
    RN006. O nome do Chat em Grupo deve ser único por organização                         |       -- (Unicidade)
    RN007. Só pode existir 1 canal de Chat Privado ativo entre a mesma dupla de usuários  |       -- (Unicidade)
    RN008. Tarefas com restrição de quantidade limitam a quantidade de realizantes        |       -- (Capacidade)
    RN009. Contas inativas há 12 meses são alertadas e inativadas após prazo de 3 dias    |       -- (Inatividade)


# 4. Entidades do Sistema:

    1. usuarios                 | -- Cadastro central de usuários e credenciais
    2. organizacao              | -- Organizações criadas pelos usuários
    3. subgrupo_organizacao     | -- Setores/subgrupos pertencentes às organizações
    4. usuario_organizacao      | -- Vínculo de membros e permissões com a organização
    5. subgrupo_usuario         | -- Vínculo de membros aos subgrupos/setores
    6. secao                    | -- Categorias para organização de itens (pessoais ou org)
    7. notas                    | -- Anotações do usuário (com suporte a lembretes e anexos)
    8. tarefas                  | -- Atividades e tarefas a serem executadas
    9. usuario_tarefa           | -- Atribuição de realizantes para tarefas
    10. link_nota_tarefa        | -- Relacionamento de vinculo entre nota e tarefa
    11. mural                   | -- Posts de aviso informativos
    12. arquivo_nuvem           | -- Armazenamento de arquivos na nuvem
    13. chat_grupo              | -- Canais de conversa em grupo da organização
    14. mensagem_grupo          | -- Mensagens enviadas nos chats de grupo
    15. usuario_chat_grupo      | -- Participantes e papéis nos chats de grupo
    16. chat_privado            | -- Canais de conversa direta 1 para 1
    17. mensagem_privado        | -- Mensagens enviadas em chat privado
    18. perfil                  | -- Detalhes públicos do perfil do usuário
    19. notificacao             | -- Alertas e notificações do sistema
    20. convite_organizacao     | -- Solicitações de entrada em organizações
