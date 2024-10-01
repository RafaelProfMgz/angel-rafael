# Angel Rafael Souza da Silva

Repositório para engenhario de software modelagem de dados.

- [Angel Rafael / Souza \_AXO](#Angel_axo)
- [1. Introdução](#1-introdução)
- [2. Problema e descrição do negócio.](#2-problema-e-descrição-do-negócio)
- [3. Visão geral do sistema](#3-visão-geral-do-sistema)
- [4. Diagrama ER](#4-diagrama-er)
- [5. Diagrama de classe](#5-diagrama-de-classe)
- [6. Casos de uso](#6-casos-de-uso)
  - [6.1 Histórias de usuário](#61-histórias-de-usuário)
- [7. Diagrama de componentes](#7-diagrama-de-componentes)
- [8. Diagrama de implantação](#8-diagrama-de-implantação)
- [9. Protótipo de telas](#9-protótipo-de-telas)
- [10. Diagrama de navegação de telas.](#10-diagrama-de-navegação-de-telas)
- [11. Pilha tecnológica](#11-pilha-tecnológica)
- [12. Requisitos de sistema](#12-requisitos-de-sistema)
- [13. Considerações sobre segurança](#13-considerações-sobre-segurança)
- [14. Manutenção e instalação](#14-manutenção-e-instalação)
- [15. Glossário](#15-glossário)
- [16. Script SQL](#16-script-sql)

# 1. Introdução

O projeto a seguir apresenta um sistema desenvolvido para um petshop. A empresa é considerada micro e iniciou as atividades recentemente. Ao possuir serviços exclusivos, os sistemas presentes no mercado não se enquadra, desta forma, os propietários decidiram desenvolver uma solução própria. Esta solução é detalhada a seguir.

# 2. Problema e descrição do negócio.

Descrição do cenário onde o sistema deverá funcionar.

1. Marcar animais com RFID.
2. Realizar procedimento de vacinação de banho e tosa.
3. Uma clínica veterinária atende apenas os animais: gatos e cachorros.
4. Os clientes devem fazer um cadastro de si e dos animais.
5. Os clientes devem informar as condições nas quais os animais chegam.
6. Os clientes devem informar o tipo de ração que o animal come.
7. O cliente deve informar hábitos do animal.
8. Para cada animal é possível que mais de um veterinário o atenda.
9. Os animais podem chegar e serem atendidos de acordo com uma agenda do dia.
10. Cada animal atendido receberá uma ficha e um prontuário.
11. Outros dono podem querer marcar horários de atendimento futuro.
12. O atendimento gera uma receita para o animal.
13. Quando um cliente chega na clínica veterinária ele é atendido por um atendente.
14. O atendente deve verificar se existe agenda disponível com um veterinário.
15. O atendente deve colocar o cliente e seu animal na fila de espera, se for o caso.
16. O atendente deve levar o cliente e o animal até o veterinário.
17. O veterinário deve realizar uma entrevista com o dono do animal.
18. O resultado da entrevista deve ir para um formulário.
19. O veterinário deverá examinar o animal e anotar em prontuário(ficha) suas observações.
20. Dependendo da situação do animal este receberá uma receita.
21. A Petshop vende rações para os animais de raças: felinas, canídeas, aves, roedores.
22. A Petshop fornece atendimento para creche de animais, onde deve ser informado horário e custo.
23. A Petshop vende roupas e acessórios para animais.
24. A Petshop vende produtos para banho para os animais.
25. A Petshop vende roupas para animais.
26. A Petshop fica localizada no centro.
27. A Petshop deve cuidar do animal ate o dono buscar.
28. A Petshop assumi responsabilidade pelos animais dentro do seu estabelecimento.
29. O animal ficara em local adequado até o retorno do responsável.
30. O valor total.

# 3. Visão geral do sistema

O sistema proposto para a clínica veterinária e petshop foi desenvolvido para otimizar o atendimento aos clientes, organizar os procedimentos de cuidado com os animais, e facilitar a gestão de produtos e serviços oferecidos. O fluxo de operações vai desde o cadastro de clientes e animais até o agendamento de consultas e procedimentos como vacinação, banho e tosa. Além disso, o sistema possibilita o controle de vendas de produtos, como rações, acessórios, e serviços de creche.

O sistema também lida com a administração da agenda de veterinários, permitindo que o atendente organize o fluxo de atendimento e atribua o animal ao profissional disponível. Ele gerencia prontuários, receitas e outras informações relacionadas ao histórico de saúde dos animais, garantindo que os dados sejam armazenados de forma segura e acessível. Os prontuários são criados a partir dos exames realizados pelos veterinários e as observações registradas durante o atendimento.

Além disso, o petshop é integrado ao sistema para gerenciar a venda de produtos para os animais e a prestação de serviços complementares, como creche e cuidados temporários. O sistema fornece funcionalidades para que os clientes reservem horários futuros e acompanhem a situação do atendimento de seus animais, seja durante consultas ou em serviços como banho e tosa.

A funcionalidade de RFID garante a identificação precisa dos animais, melhorando a gestão de cadastro e facilitando a recuperação de informações durante os atendimentos. Dessa forma, o sistema oferece uma solução completa, integrando a gestão clínica com as operações comerciais do petshop, visando eficiência e melhoria na experiência dos clientes e no cuidado com os animais.

# 4. Diagrama ER

```mermaid
erDiagram
    CLIENTE {
        int id_cliente
        string nome
        string telefone
        string email
    }

    ANIMAL {
        int id_animal
        string nome
        string especie
        string raca
        date data_nascimento
        string RFID
        string condicao_chegada
        string tipo_racao
        string habitos
    }

    VETERINARIO {
        int id_veterinario
        string nome
        string especialidade
    }

    ATENDENTE {
        int id_atendente
        string nome
    }

    AGENDA {
        int id_agenda
        date data
        time hora
        bool disponivel
    }

    ATENDIMENTO {
        int id_atendimento
        date data_atendimento
        string tipo
        string descricao
        float valor_total
    }

    PRONTUARIO {
        int id_prontuario
        string observacoes
        string receita
    }

    PRODUTO {
        int id_produto
        string nome
        string tipo
        float preco
    }

    CRECHE {
        int id_creche
        date horario
        float custo
    }

    CLIENTE_ANIMAL {
        int id_cliente
        int id_animal
    }

    CLIENTE_ANIMAL ||--o{ CLIENTE : "pertence"
    CLIENTE_ANIMAL ||--o{ ANIMAL : "tem"

    ANIMAL ||--o{ VETERINARIO : "atendido_por"
    VETERINARIO ||--o{ AGENDA : "disponivel_em"
    ATENDIMENTO ||--o{ ANIMAL : "realizado_em"
    ATENDIMENTO ||--o{ VETERINARIO : "feito_por"
    ATENDIMENTO ||--o{ AGENDA : "agendado_para"
    ATENDIMENTO ||--|{ PRONTUARIO : "gera"

    CLIENTE ||--o{ ATENDENTE : "atendido_por"
    ATENDENTE ||--o{ AGENDA : "organiza"
    PRODUTO ||--o{ CLIENTE : "comprado_por"
    CLIENTE ||--o{ CRECHE : "utiliza"

    CRECHE ||--o{ ANIMAL : "recebe_cuidado"
    PRODUTO ||--o{ ANIMAL : "utilizado_por"
    CLIENTE ||--o{ AGENDA : "faz_reserva"
```

# 5. Diagrama de classe

```mermaid
classDiagram
    class Cliente {
        +int id_cliente
        +string nome
        +string telefone
        +string email
        +void cadastrarAnimal()
        +void informarCondicoesChegada()
        +void informarTipoRacao()
        +void informarHabitos()
    }

    class Animal {
        +int id_animal
        +string nome
        +string especie
        +string raca
        +date data_nascimento
        +string RFID
        +string condicao_chegada
        +string tipo_racao
        +string habitos
        +void receberFicha()
        +void receberProntuario()
    }

    class Veterinario {
        +int id_veterinario
        +string nome
        +string especialidade
        +void realizarEntrevista()
        +void examinarAnimal()
        +void gerarReceita()
    }

    class Atendente {
        +int id_atendente
        +string nome
        +void verificarAgendaDisponivel()
        +void colocarNaFilaEspera()
        +void encaminharParaVeterinario()
    }

    class Agenda {
        +int id_agenda
        +date data
        +time hora
        +bool disponivel
    }

    class Atendimento {
        +int id_atendimento
        +date data_atendimento
        +string tipo
        +string descricao
        +float valor_total
        +void gerarReceita()
    }

    class Prontuario {
        +int id_prontuario
        +string observacoes
        +string receita
        +void preencherObservacoes()
        +void emitirReceita()
    }

    class Produto {
        +int id_produto
        +string nome
        +string tipo
        +float preco
    }

    class Venda {
        +int id_venda
        +date data_venda
        +int quantidade
        +float valor_total
    }

    class Creche {
        +int id_creche
        +time horario
        +float custo
    }

    Cliente "1" -- "n" Animal : possui >
    Cliente "1" -- "n" Venda : realiza >
    Animal "1" -- "n" Atendimento : é atendido em >
    Veterinario "1" -- "n" Atendimento : realiza >
    Veterinario "1" -- "n" Animal : atende >
    Atendente "1" -- "n" Atendimento : gerencia >
    Atendimento "1" -- "1" Prontuario : gera >
    Agenda "1" -- "n" Atendimento : organiza >
    Animal "1" -- "n" Creche : permanece >
    Cliente "1" -- "n" Creche : utiliza >
    Produto "1" -- "n" Venda : é vendido em >
```

# 6. Casos de uso

```mermaid
graph TD;
    subgraph Sistema Veterinário
        Cliente --> |Faz cadastro| CadastroCliente
        Cliente --> |Informa condições do animal| CondicoesAnimal
        Cliente --> |Informa tipo de ração| TipoRacao
        Cliente --> |Informa hábitos do animal| HabitosAnimal
        Cliente --> |Marca horário para atendimento| MarcarHorario
        Cliente --> |Chega na clínica| ChegadaClinica
        Cliente --> |Realiza pagamento| RealizarPagamento
        Atendente --> |Verifica agenda disponível| VerificarAgenda
        Atendente --> |Coloca na fila de espera| FilaEspera
        Atendente --> |Leva ao veterinário| LevarVeterinario
        Veterinario --> |Realiza entrevista com dono| EntrevistaDono
        Veterinario --> |Examina animal| ExaminarAnimal
        Veterinario --> |Registra observações no prontuário| Prontuario
        Veterinario --> |Emite receita| ReceitaAnimal
        Veterinario --> |Preenche ficha do animal| FichaAnimal
        Veterinario --> |Consulta histórico do animal| HistoricoAnimal
        Veterinario --> |Consulta condição de saúde| CondicaoSaude
        Veterinario --> |Consulta hábitos do animal| HabitosVeterinario
        Petshop --> |Vende rações| VenderRacao
        Petshop --> |Vende roupas e acessórios| VenderRoupasAcessorios
        Petshop --> |Vende produtos para banho| VenderProdutosBanho
        Petshop --> |Fornece atendimento para creche| AtendimentoCreche
        Petshop --> |Cuidar do animal| CuidarAnimal
        Petshop --> |Assume responsabilidade| ResponsabilidadePetshop
        Cliente --> |Informa horário e custo da creche| HorarioCustoCreche
        Cliente --> |Deixa o animal para cuidados| DeixarAnimalCuidados
        Cliente --> |Consulta disponibilidade de produtos| ConsultarProdutos
        Cliente --> |Marca atendimento futuro| MarcarAtendimentoFuturo
        Cliente --> |Recebe notificação de retorno| NotificacaoRetorno
        Cliente --> |Avalia o atendimento| AvaliarAtendimento
        Atendente --> |Gerencia agendamentos| GerenciarAgendamentos
        Veterinario --> |Avalia prontuário| AvaliarProntuario
        Cliente --> |Recebe receita| ReceberReceita
    end
```

# 6.1 Casos de uso

@startuml
actor Cliente
actor Atendente
actor Veterinario
actor Petshop

usecase "Cadastrar Cliente" as UC1
usecase "Cadastrar Animal" as UC2
usecase "Informar Condições de Chegada" as UC3
usecase "Informar Tipo de Ração" as UC4
usecase "Informar Hábitos" as UC5
usecase "Marcar Animal com RFID" as UC6
usecase "Atendimento Veterinário" as UC7
usecase "Realizar Procedimento de Banho e Tosa" as UC8
usecase "Realizar Entrevista com Dono" as UC9
usecase "Examinar Animal" as UC10
usecase "Gerar Prontuário" as UC11
usecase "Gerar Receita" as UC12
usecase "Verificar Agenda Disponível" as UC13
usecase "Colocar Cliente na Fila de Espera" as UC14
usecase "Levar Animal para o Veterinário" as UC15
usecase "Vender Rações" as UC16
usecase "Vender Roupas e Acessórios" as UC17
usecase "Vender Produtos para Banho" as UC18
usecase "Cuidar do Animal até Busca" as UC19
usecase "Oferecer Serviço de Creche" as UC20

Cliente --> UC1
Cliente --> UC2
Cliente --> UC3
Cliente --> UC4
Cliente --> UC5
Cliente --> UC8
Cliente --> UC9

Atendente --> UC13
Atendente --> UC14
Atendente --> UC15

Veterinario --> UC9
Veterinario --> UC10
Veterinario --> UC11
Veterinario --> UC12

Petshop --> UC6
Petshop --> UC16
Petshop --> UC17
Petshop --> UC18
Petshop --> UC19
Petshop --> UC20

UC9 --> UC11
UC10 --> UC12
@enduml

# 6.2 Histórias de usuário

1. Cadastro de Clientes e Animais
   Como um cliente,
   Eu quero realizar o cadastro dos meus dados pessoais e dos meus animais,
   Para que a clínica veterinária possa ter minhas informações e as dos meus pets registradas.

2. Informar Condições e Hábitos do Animal
   Como um cliente,
   Eu quero informar as condições de saúde e os hábitos alimentares e comportamentais dos meus animais,
   Para que o veterinário e a clínica possam prestar o atendimento adequado.

3. Agendar Atendimento Veterinário
   Como um cliente,
   Eu quero agendar o atendimento de meus animais com um veterinário,
   Para garantir que eles recebam os cuidados necessários no horário adequado.

4. Atendimento por Múltiplos Veterinários
   Como um cliente,
   Eu quero que meus animais possam ser atendidos por mais de um veterinário,
   Para que cada profissional cuide de diferentes necessidades do meu pet, se necessário.

5. Receber Ficha e Prontuário do Animal
   Como um veterinário,
   Eu quero criar uma ficha e um prontuário para cada animal atendido,
   Para registrar o histórico de saúde e cuidados realizados no animal.

6. Fila de Espera para Atendimento Veterinário
   Como um atendente,
   Eu quero verificar a disponibilidade de agenda com os veterinários e, caso necessário,
   Colocar o cliente e seu animal na fila de espera,
   Para garantir que todos os animais sejam atendidos de maneira organizada.

7. Realizar Entrevista Inicial com o Dono
   Como um veterinário,
   Eu quero realizar uma entrevista inicial com o dono do animal,
   Para entender o motivo da consulta e coletar informações essenciais para o atendimento.

8. Anotar Observações no Prontuário
   Como um veterinário,
   Eu quero anotar no prontuário todas as observações e resultados do exame do animal,
   Para registrar o estado de saúde e possíveis tratamentos.

9. Gerar Receita para Tratamento
   Como um veterinário,
   Eu quero emitir uma receita de medicamentos ou tratamentos para o animal,
   Para que o dono possa seguir com o tratamento adequado.

10. Serviço de Creche para Animais
    Como um cliente,
    Eu quero deixar meu animal na creche da petshop,
    Para que ele seja cuidado enquanto estou ausente, com horário de entrada e custo informados.

11. Vender Rações e Produtos para Animais
    Como um cliente,
    Eu quero comprar ração, roupas e acessórios para meu animal,
    Para que ele tenha alimentação e conforto adequados.

12. Cuidar dos Animais na Petshop
    Como um cliente,
    Eu quero que a petshop cuide do meu animal até que eu o busque,
    Para que ele fique seguro e confortável no estabelecimento.

13. Garantir Local Adequado para Animais na Petshop
    Como o proprietário da petshop,
    Eu quero garantir que todos os animais fiquem em locais adequados até o retorno de seus donos,
    Para oferecer um ambiente seguro e confortável.

14. Vender Produtos de Higiene para Animais
    Como um cliente,
    Eu quero comprar produtos de higiene, como shampoos e acessórios para banho,
    Para manter a limpeza e a saúde do meu animal.

15. Valor Total dos Serviços e Produtos
    Como um cliente,
    Eu quero ser informado do valor total dos serviços e produtos adquiridos,
    Para que eu saiba o custo completo ao final da visita.

16. Responsabilidade pelos Animais no Estabelecimento+
    Como o proprietário da petshop,
    Eu quero assumir a responsabilidade pelos animais enquanto estiverem em meu estabelecimento,
    Para garantir que os donos confiem na segurança e cuidado que oferecemos.

17. Atendimento por Agendamento ou Ordem de Chegada
    Como um cliente,
    Eu quero que meu animal seja atendido na clínica veterinária conforme o agendamento ou pela ordem de chegada,
    Para que ele receba os cuidados no momento certo.

18. Marcar Atendimentos Futuros
    Como um cliente,
    Eu quero agendar atendimentos veterinários para datas futuras,
    Para garantir que meu animal receba acompanhamento contínuo e planejado.

19. Atendimento ao Chegar na Clínica
    Como um cliente,
    Eu quero ser atendido por um atendente assim que chego na clínica veterinária,
    Para que meu animal seja prontamente direcionado ao veterinário.

20. Verificar Agenda de Veterinários Disponíveis
    Como um atendente,
    Eu quero verificar a agenda dos veterinários disponíveis,
    Para agendar ou organizar o atendimento dos animais de acordo com a disponibilidade.

21. Levar Cliente e Animal ao Veterinário
    Como um atendente,
    Eu quero levar o cliente e seu animal até o veterinário responsável,
    Para que o atendimento aconteça de forma organizada e sem atrasos.

22. Realizar Marcação de Animais com RFID
    Como um veterinário,
    Eu quero marcar os animais com RFID,
    Para facilitar a identificação e rastreamento de cada pet atendido.

23. Realizar Procedimentos de Banho e Tosa
    Como um cliente,
    Eu quero que a clínica veterinária ou petshop realize o serviço de banho e tosa no meu animal,
    Para garantir que ele esteja sempre limpo e bem cuidado.

24. Vender Rações Específicas para Cada Tipo de Animal
    Como um cliente,
    Eu quero que a petshop tenha rações específicas para cada tipo de animal (felinos, canídeos, aves, roedores),
    Para que eu possa adquirir o alimento mais adequado ao meu pet.

25. Disponibilizar Receitas no Sistema
    Como um cliente,
    Eu quero que as receitas veterinárias estejam disponíveis no sistema da clínica,
    Para poder acessar a qualquer momento o tratamento prescrito para meu animal.

26. Entregar Animais Após Banho, Tosa ou Creche
    Como um cliente,
    Eu quero buscar meu animal após a realização dos serviços de banho, tosa ou creche,
    Para que ele esteja pronto para ir para casa no horário combinado.

27. Cadastro de Produtos e Serviços
    Como um atendente da petshop,
    Eu quero cadastrar produtos como ração, roupas, acessórios e serviços como creche, banho e tosa,
    Para oferecer uma variedade de opções aos clientes da loja.

28. Emitir Relatórios de Atendimentos e Vendas
    Como o proprietário da petshop,
    Eu quero gerar relatórios sobre os atendimentos realizados e os produtos vendidos,
    Para ter controle sobre o faturamento e a eficiência dos serviços prestados.

29. Cálculo do Custo Total dos Serviços
    Como um cliente,
    Eu quero que o sistema me mostre o custo total dos serviços prestados (creche, banho, tosa, consulta veterinária),
    Para que eu saiba quanto precisarei pagar no final.

30. Garantir a Segurança dos Animais na Creche
    Como o proprietário da petshop,
    Eu quero garantir a segurança dos animais que ficam na creche,
    Para que os donos sintam confiança em deixar seus pets no local durante o dia.

# 7. Diagrama de componentes

# 8. Diagrama de implantação

# 9. Protótipo de telas

# 10. Diagrama de navegação de telas.

# 11. Pilha tecnológica

# 12. Requisitos de sistema

# 13. Considerações sobre segurança

# 14. Manutenção e instalação

# 15. Glossário

# 16. Script SQL

# 16.1. Comando Create table

```sql
CREATE TABLE Cliente (
    id_cliente INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    telefone VARCHAR(20),
    email VARCHAR(100)
);

CREATE TABLE Animal (
    id_animal INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    especie ENUM('gato', 'cachorro') NOT NULL,
    raca VARCHAR(100),
    data_nascimento DATE,
    RFID VARCHAR(50) NOT NULL,
    condicao_chegada TEXT,
    tipo_racao VARCHAR(100),
    habitos TEXT,
    id_cliente INT,
    FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente) ON DELETE CASCADE
);


CREATE TABLE Veterinario (
    id_veterinario INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    especialidade VARCHAR(100)
);


CREATE TABLE Atendente (
    id_atendente INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL
);


CREATE TABLE Agenda (
    id_agenda INT AUTO_INCREMENT PRIMARY KEY,
    data DATE NOT NULL,
    hora TIME NOT NULL,
    disponivel BOOLEAN DEFAULT TRUE,
    id_veterinario INT,
    FOREIGN KEY (id_veterinario) REFERENCES Veterinario(id_veterinario) ON DELETE SET NULL
);


CREATE TABLE Atendimento (
    id_atendimento INT AUTO_INCREMENT PRIMARY KEY,
    data_atendimento DATE NOT NULL,
    tipo VARCHAR(100),
    descricao TEXT,
    valor_total DECIMAL(10, 2),
    id_animal INT,
    id_veterinario INT,
    id_agenda INT,
    FOREIGN KEY (id_animal) REFERENCES Animal(id_animal) ON DELETE CASCADE,
    FOREIGN KEY (id_veterinario) REFERENCES Veterinario(id_veterinario) ON DELETE SET NULL,
    FOREIGN KEY (id_agenda) REFERENCES Agenda(id_agenda) ON DELETE SET NULL
);


CREATE TABLE Prontuario (
    id_prontuario INT AUTO_INCREMENT PRIMARY KEY,
    observacoes TEXT,
    receita TEXT,
    id_animal INT,
    id_atendimento INT,
    FOREIGN KEY (id_animal) REFERENCES Animal(id_animal) ON DELETE CASCADE,
    FOREIGN KEY (id_atendimento) REFERENCES Atendimento(id_atendimento) ON DELETE CASCADE
);


CREATE TABLE Produto (
    id_produto INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    tipo ENUM('racao', 'acessorio', 'roupa', 'banho') NOT NULL,
    preco DECIMAL(10, 2)
);


CREATE TABLE Venda (
    id_venda INT AUTO_INCREMENT PRIMARY KEY,
    data_venda DATE NOT NULL,
    id_cliente INT,
    id_produto INT,
    quantidade INT,
    valor_total DECIMAL(10, 2),
    FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente) ON DELETE CASCADE,
    FOREIGN KEY (id_produto) REFERENCES Produto(id_produto) ON DELETE CASCADE
);

CREATE TABLE Creche (
    id_creche INT AUTO_INCREMENT PRIMARY KEY,
    horario TIME NOT NULL,
    custo DECIMAL(10, 2) NOT NULL,
    id_animal INT,
    FOREIGN KEY (id_animal) REFERENCES Animal(id_animal) ON DELETE CASCADE
);


CREATE TABLE Fila_Espera (
    id_fila INT AUTO_INCREMENT PRIMARY KEY,
    id_animal INT,
    id_agenda INT,
    status ENUM('aguardando', 'em_atendimento', 'finalizado') DEFAULT 'aguardando',
    FOREIGN KEY (id_animal) REFERENCES Animal(id_animal) ON DELETE CASCADE,
    FOREIGN KEY (id_agenda) REFERENCES Agenda(id_agenda) ON DELETE CASCADE
);
```

# 16.2. Comando INSERT gerando dados ficticios

```sql
INSERT INTO Cliente (nome, telefone, email) VALUES
('João Silva', '123456789', 'joao.silva@email.com'),
('Maria Oliveira', '987654321', 'maria.oliveira@email.com'),
('Ana Souza', '555123456', 'ana.souza@email.com'),
('Pedro Lima', '999888777', 'pedro.lima@email.com');


INSERT INTO Animal (nome, especie, raca, data_nascimento, RFID, condicao_chegada, tipo_racao, habitos, id_cliente) VALUES
('Rex', 'cachorro', 'Pastor Alemão', '2018-06-12', 'RFID123456', 'Animal limpo e saudável', 'Royal Canin', 'Corre todos os dias no parque', 1),
('Luna', 'gato', 'Persa', '2020-04-25', 'RFID654321', 'Animal com sinais de estresse', 'Whiskas', 'Dorminhoca e caseira', 2),
('Bob', 'cachorro', 'Bulldog', '2019-11-05', 'RFID987654', 'Animal com tosse leve', 'Pedigree', 'Brincalhão e sociável', 3),
('Mia', 'gato', 'Siamês', '2021-02-18', 'RFID112233', 'Animal com perda de pelos', 'Golden', 'Adora subir em árvores', 4);


INSERT INTO Veterinario (nome, especialidade) VALUES
('Dr. Carlos Almeida', 'Clínico Geral'),
('Dra. Beatriz Mendes', 'Dermatologia Animal'),
('Dr. Felipe Santos', 'Ortopedia Animal');

INSERT INTO Atendente (nome) VALUES
('Fernanda Souza'),
('Ricardo Lopes'),
('Carla Ferreira');


INSERT INTO Agenda (data, hora, disponivel, id_veterinario) VALUES
('2024-09-20', '10:00:00', TRUE, 1),
('2024-09-20', '11:00:00', TRUE, 2),
('2024-09-21', '09:00:00', TRUE, 3),
('2024-09-21', '10:30:00', TRUE, 1);


INSERT INTO Atendimento (data_atendimento, tipo, descricao, valor_total, id_animal, id_veterinario, id_agenda) VALUES
('2024-09-20', 'Consulta', 'Consulta geral e exame clínico', 200.00, 1, 1, 1),
('2024-09-20', 'Consulta', 'Consulta dermatológica', 250.00, 2, 2, 2),
('2024-09-21', 'Exame Ortopédico', 'Exame ortopédico completo', 300.00, 3, 3, 3);


INSERT INTO Prontuario (observacoes, receita, id_animal, id_atendimento) VALUES
('Animal saudável, sem anomalias visíveis.', 'Manter dieta habitual', 1, 1),
('Animal com dermatite leve, recomendar shampoo específico.', 'Shampoo dermatológico 2x por semana', 2, 2),
('Animal com problema articular, indicar acompanhamento', 'Suplemento de articulação 1x por dia', 3, 3);


INSERT INTO Produto (nome, tipo, preco) VALUES
('Ração Royal Canin', 'racao', 120.00),
('Coleira de Couro', 'acessorio', 40.00),
('Camiseta para cães', 'roupa', 30.00),
('Shampoo para Cães', 'banho', 25.00);


INSERT INTO Venda (data_venda, id_cliente, id_produto, quantidade, valor_total) VALUES
('2024-09-18', 1, 1, 1, 120.00),
('2024-09-18', 2, 2, 1, 40.00),
('2024-09-19', 3, 3, 2, 60.00),
('2024-09-19', 4, 4, 1, 25.00);


INSERT INTO Creche (horario, custo, id_animal) VALUES
('08:00:00', 150.00, 1),
('09:00:00', 150.00, 2),
('10:00:00', 150.00, 3),
('11:00:00', 150.00, 4);


INSERT INTO Fila_Espera (id_animal, id_agenda, status) VALUES
(1, 1, 'aguardando'),
(2, 2, 'aguardando'),
(3, 3, 'em_atendimento');
```
