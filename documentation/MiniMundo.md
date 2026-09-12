# MiniMundo:
    O Joby é uma plataforma onde os usuários podem se cadastrar e usar para auxiliar no gerenciamento de suas tarefas, permitindo o aumento de produtividade de seus usuários e organizações. 
    O desenvolvimento desta aplicação será desenvolvida em módulos, definidos pela sua importância para o funcionamento do sistema, sendo o primeiro módulo para funcionalidades como:
    --Cadastro do usuário e gerenciamento de conta/perfil;
    --Criação e gerenciamento de tarefas;
    --criação e gerenciamento de organizações;
    --criação e gerenciamento de notas;
    --Criar posts de aviso em modo organização;
    --criação e gerenciamento de categorias;
    --criação e gerenciamento de subgrupo/setores;
    --Armazenamento em nuvem.

    O segundo módulo vai trabalhar com questões de experiência de usuário:
    --cahat interno de organizção;
    --relatórios de tarefas;
    --notificações de eventos e tarefas;
    --linkar tarefas e notas;


    O usuário poderá criar sua conta, para isso será necessário alguns dados do próprio, tais como:
    --nome completo;
    --email;
    --telefone;

    O usuário tem um perfil, constituido de:
    --nome completo;
    --apelido;
    --descricao;
    --foto;


    Após criar sua conta, o usuário poderá acessar a plataforma sempre que quiser, onde estará disponível a criar suas anotações, suas tarefas, suas organizações, seu gerenciamento na nuvem, chat, relatórios e notificações.

    Também é possivel criar categorias, que servem como uma forma de você filtrar tarefas e anotações através destas categorias, EX:
        É criada uma categoria de "autentificação", onde todas as tarefas e anotações relacionadas aquela categoria ficarão dentro daquele bloco específico, ideal para as pessoas que são responsáveis por setores específicos, que neste caso seria o pessoal do backend e segurança;

    Os subgrupos são basicamente setores de uma organização, igualmente a RH, administrativo, contabilidade, entre outros da vida real. 
        Aqui a organização pode atribuir um funcionário a atuar em 1 ou mais setores. Isto atribui ao usuário uma melhor distribuição de tarefas pelo sistema, onde tarefas destinadas diretamente ao subgrupo/setor daquele funcionário serão as tarefas que aparecerão exclusivamente para eles ou com ênfase (aparecerão no topo com marcação especial) em relação as demais.

    As anotações devem ser constituidas de:
        --titulo;
        --texto;
        --categorias;
        --data de criacao;
        --data de modificacao;

    As tarefas são constituidas de: 
        --titulo;
        --descricao;
        --categorias;
   #     --subgrupo/setor (se feita por uma organização);
   #     --realizante (quais usuários estão realizando, se feito em modo organização);
        --status: (à realizar, realizada, em execução);
        --data de criacao;
        --data de modificação;

    As organizações são constituidas de:

        --criador;
        --nome;
        --descricao;
        --foto;
        --membros;
        --data de criacao;
        --data de modificacao;
        --data de exclusao;

    
    Todas as tarefas e anotações feitas pelo usuário de forma privativa(fora das organizações), só deverão ser vistas pelo próprio. Já as anotações e Tarefas feitas em uma organização, ficará a mostra para os todos. E as organizações podem acessar os relatórios das atuações dos usuários lá dentro (suas ações em notas, quantas tarefas já realizou, quais tarefas realizou, quais tarefas está realizando), além de relatórios gerais sobre todas as tarefas, podendo ser filtradas por atributos como Data, Título, categoria, subgrupo/setor, etc.
    As organizações são criadas por um usuário, que realiza a solicitação de convite a outros usuários, ao aceitarem já participam da própria, la dentro a organização pode criar tarefas e deixá-las livres para quem quiser, ou simplesmente delegar diretamente as tarefas a usuários específicos (que são notificados, e a tarefa aparece em sua lista de afazeres), além de destinar subgrupos/setores aos colaboradores. Uma tarefa pode ser feita por uma ou mais pessoas, desde de eestejam dentro dos limites impostos pelo criador da tarefa (podendo ser x pessoas quaisquer, ou x pessoas específicas). organizações também possuem armazenamento em nuvem privada. Com direito a chat livre (aberto a todos os participantes). 
    É possível conectar uma nota a uma tarefa, de modo que o usuário possa ter acesso a anotação que o ajudou na realização de uma tarefa específica. 
    Se o usuário se mantiver mais de 12 meses sem logar, ele receberá uma notificação via email alertanto da exclusão de suas criações (tarefas, notas e armazenamento em nuvem) dentro da aplicação para a liberação de espaço e a inativação da conta. A pessoa terá 3 dias para logar e reativar a conta, caso contrário, todas suas criações serão apagadas para liberar espaço no armazenamento. 
    Após a inativação da conta, será possível ativá-la novamente através da nossa página de reativação disponível pela aplicação.