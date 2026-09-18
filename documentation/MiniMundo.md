# ===============================Representação da Documentação do MiniMundo=====================================

# 1. Visão Geral:
    O JOby é uma plataforma web voltada para o gerenciamento de tarefas, anotações, organizações, comunicação e arquivos em nuvem. 
    Ele visa auxiliar no aumento da produtividade tanto no uso individual (privativo) quanto no uso corporativo/em grupo (organizações).
    O desenvolvimento é estruturado em módulos funcionais que contemplam desde a gestão pessoal de atividades até o gerenciamento avançado de equipes e colaboração.

# 2. Módulos da Aplicação:

# 2.1 - Módulo 1 (Funcionalidades Principais & Gestão):
    -- Cadastro e Autenticação de Usuário (gestão de conta, senha e controle de último login);
    -- Gestão de Perfil do Usuário (identificador único, apelido e foto de perfil);
    -- Gestão e Organização de Tarefas (privadas e organizacionais);
    -- Gestão e Criação de Notas/Anotações (com suporte a lembretes e anexos);
    -- Criação e Gerenciamento de Organizações (com fotos, membros e convites);
    -- Gestão de Subgrupos e Setores de Organização (RH, Financeiro, TI, etc.);
    -- Gestão de Seções/Categorias com cores personalizadas (uso privado ou em organização);
    -- Mural de Avisos e Informativos para organizações e subgrupos;
    -- Gestão de Armazenamento em Nuvem Privada e Organizacional;
    -- Gestão de Colaboradores e Níveis de Permissão (leitura, escrita e gerenciamento).

# 2.2 - Módulo 2 (Experiência do Usuário & Comunicação):
    -- Chat Interno em Grupo por Organização (canais de comunicação);
    -- Chat Privado Direto entre Usuários (mensagens 1 para 1);
    -- Notificações de Eventos, Tarefas, Lembretes, Convites e Avisos do Sistema;
    -- Vinculação (Link) entre Notas e Tarefas para rápido acesso a conteúdos de apoio;
    -- Emissão de Relatórios de Produtividade e Execução de Tarefas;
    -- Monitoramento de Inatividade e Processo Automático de Inativação/Reativação de Conta.

# 3. Detalhamento do Funcionamento por Entidade:

# 3.1 - Usuários e Perfis:
    -- O usuário realiza seu cadastro fornecendo nome completo, e-mail, telefone e senha.
    -- Cada usuário possui um Perfil associado contendo um identificador único (#código gerado pelo sistema), apelido único e foto de perfil.
    -- O sistema mantém registro de atividade via campo de último login para controle de inatividade.

# 3.2 - Organizações, Convites e Permissões:
    -- Usuários podem criar organizações definindo nome, descrição e foto da organização.
    -- A entrada de novos membros ocorre mediante o envio de Convites (com status pendente, aceito ou recusado).
    -- Cada membro na organização possui um conjunto de permissões (leitura, escrita, gerenciar).
    -- A organização possui Armazenamento em Nuvem compartilhado e Mural de Avisos exclusivo.

# 3.3 - Subgrupos / Setores:
    -- Organizações podem ser divididas em Subgrupos (setores como RH, TI, Administração).
    -- Os colaboradores são associados a um ou mais subgrupos.
    -- Tarefas, notas e murais podem ser marcados com restrição de subgrupo, garantindo visualização direcionada ou priorizada aos membros daquele setor.

# 3.4 - Seções (Categorias):
    -- As Seções servem como categorias visuais para organizar tarefas, notas, murais e arquivos.
    -- Cada seção possui um nome e uma cor identificadora.
    -- Podem ser criadas para uso Pessoal (fora de organizações) ou para uso em Organizações específicas.

# 3.5 - Notas e Anotações:
    -- Constituídas de título, texto, anexo, categoria (seção) e data de lembrete.
    -- Podem ser feitas em modo privativo ou associadas a uma organização/subgrupo.

# 3.6 - Tarefas e Atribuições:
    -- Constituídas de título, descrição, status (pendente, em progresso, concluída), prazo final, seção e limite de realizantes.
    -- Podem ser atribuídas a 1 ou mais usuários (relação usuário-tarefa).
    -- Podem ser criadas no modo privado ou organizacional.

# 3.7 - Vinculação Nota & Tarefa:
    -- Permite conectar diretamente uma Nota a uma Tarefa, possibilitando consultar anotações explicativas no momento de executar um trabalho.

# 3.8 - Mural de Avisos:
    -- Permite a publicação de posts de avisos em modo organização ou restritos a um subgrupo específico.

# 3.9 - Armazenamento em Nuvem:
    -- Permite o envio e gerenciamento de arquivos (título, anexo/caminho, seção e restrição de subgrupo).

# 3.10 - Comunicação (Chat em Grupo e Chat Privado):
    -- Chat em Grupo: canais abertos por organização, com permissões de administrador/usuário e suporte ao envio de anexos.
    -- Chat Privado: conversas diretas entre 2 usuários dentro da plataforma com suporte a mensagens de texto e anexos.

# 3.11 - Notificações:
    -- Sistema de alertas para notificar usuários sobre novas tarefas atribuídas, lembretes de notas, convites de organização e mensagens.

# 3.12 - Controle de Inatividade e Reativação:
    -- Caso o usuário fique 12 meses sem realizar login (verificado pelo último login), o sistema envia uma notificação via e-mail informando sobre a futura inativação da conta e remoção dos dados para liberação de espaço.
    -- O usuário terá 3 dias após a notificação para acessar a plataforma e reativar sua conta através da página de reativação; caso contrário, os dados privativos serão inativados/removidos.