# Descrição do sistema Veterinario
Sistema para clinica veterinaria

nome= Carinho de Pets

Exercício 1:

2: Uma clínica veterinária atende apenas os animais: gatos e cachorros.

3: Os clientes devem fazer um cadastro de si e dos animais.

4: Os clientes devem informar as condições nas quais os animais chegam.

5: Os clientes devem informar o tipo de ração que o animal come.

6: O cliente deve informar hábitos do animal.

7: Para cada animal é possível que mais de um veterinário o atenda.

8: Os animais podem chegar e serem atendidos de acordo com uma agenda do dia.

9: Cada animal atendido receberá uma ficha e um prontuário.

10: Outros dono podem querer marcar horários de atendimento futuro.

11: O atendimento gera uma receita para o animal.

12: Quando um cliente chega na clínica veterinária ele é atendido por um atendente.

13: O atendente deve verificar se existe agenda disponível com um veterinário.

14: O atendente deve colocar o cliente e seu animal na fila de espera, se for o caso.

15: O atendente deve levar o cliente e o animal até o veterinário.

16: O veterinário deve realizar uma entrevista com o dono do animal.

17: O resultado da entrevista deve ir para um formulário.

18: O veterinário deverá examinar o animal e anotar em prontuário(ficha) suas observações.

19: tera que realizar cada tipo de exame do animal.

20: cada animal terá que ter o seu documento próprio, para fazer uma ficha de atendimento

21: cada dono do animal também terá que ter o seu próprio documento.

22: o veterinario tera que conhecer qual é o caso de doença do animal.

23: após ter conhecido o tipo de doença no animal, terá que passar o medicamento.


# diagrama do banco de dados


-- Criação do Banco de DadosCREATE DATABASE carinho_de_pets;
USE carinho_de_pets;

-- Tabela para ClientesCREATETABLE clientes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOTNULL,
    telefone VARCHAR(20),
    endereco TEXT
);

-- Tabela para AnimaisCREATETABLE animais (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOTNULL,
    especie ENUM('Cachorro', 'Gato') NOTNULL,
    idade INT,
    raca VARCHAR(50),
    racao_preferida VARCHAR(50),
    habitos TEXT,
    cliente_id INT,
    FOREIGN KEY (cliente_id) REFERENCES clientes(id)
);

-- Tabela para VeterináriosCREATETABLE veterinarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOTNULL,
    especialidade VARCHAR(100)
);

-- Tabela para AtendimentosCREATETABLE atendimentos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    data DATETIME NOTNULL,
    animal_id INT,
    veterinario_id INT,
    cliente_id INT,
    estado_atendimento ENUM('Agendado', 'Em Atendimento', 'Finalizado') DEFAULT'Agendado',
    FOREIGN KEY (animal_id) REFERENCES animais(id),
    FOREIGN KEY (veterinario_id) REFERENCES veterinarios(id),
    FOREIGN KEY (cliente_id) REFERENCES clientes(id)
);

-- Tabela para ProntuáriosCREATETABLE prontuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    atendimento_id INT,
    observacoes TEXT,
    receita TEXT,
    FOREIGN KEY (atendimento_id) REFERENCES atendimentos(id)
);

-- Tabela para ExamesCREATETABLE exames (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100),
    descricao TEXT
);

-- Tabela para Resultados de ExamesCREATETABLE resultados_exames (
    id INT AUTO_INCREMENT PRIMARY KEY,
    exame_id INT,
    atendimento_id INT,
    resultado TEXT,
    FOREIGN KEY (exame_id) REFERENCES exames(id),
    FOREIGN KEY (atendimento_id) REFERENCES atendimentos(id)
);

-- Tabela para Documentos dos AnimaisCREATETABLE documentos_animais (
    id INT AUTO_INCREMENT PRIMARY KEY,
    animal_id INT,
    tipo_documento VARCHAR(50),
    caminho_documento VARCHAR(255),
    FOREIGN KEY (animal_id) REFERENCES animais(id)
);

-- Tabela para Documentos dos ClientesCREATETABLE documentos_clientes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    cliente_id INT,
    tipo_documento VARCHAR(50),
    caminho_documento VARCHAR(255),
    FOREIGN KEY (cliente_id) REFERENCES clientes(id)
);

-- Tabela para Fichas de AtendimentoCREATETABLE fichas_atendimento (
    id INT AUTO_INCREMENT PRIMARY KEY,
    atendimento_id INT,
    documento TEXT,
    FOREIGN KEY (atendimento_id) REFERENCES atendimentos(id)
);

-- Tabela para MedicamentosCREATETABLE medicamentos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100),
    descricao TEXT
);

-- Tabela para Prescrições de MedicamentosCREATETABLE prescricoes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    atendimento_id INT,
    medicamento_id INT,
    dosagem VARCHAR(50),
    FOREIGN KEY (atendimento_id) REFERENCES atendimentos(id),
    FOREIGN KEY (medicamento_id) REFERENCES medicamentos(id)
);


# diagrama do caso de uso 



# principais telas do sistema



# arquitetura do sistema