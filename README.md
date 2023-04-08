# Trabalho efetivo discente - Banco de dados

> Status: Concluído

## QUESTÃO

Um consultório médico deseja um sistema de informação para controlar o atendimento aos pacientes feitos pelos médicos.

No consultório médico existem funcionários encarregados da limpeza, funcionários responsáveis pelo atendimento aos pacientes e médicos, que por sua vez possui especialização em uma ou mais áreas. Existem várias especialidades médicas (clínica geral, cardiologia, urologia, dermatologia, etc). Cada médico possui ao menos uma especialidade e uma especialidade possui ao menos um médico especializado.

Para os funcionários é importante armazenar o nome, rg, endereço residencial e telefone. Os funcionários que fazem atendimentos aos pacientes devem possuir curso superior em enfermagem, sendo necessário armazenar o ano de conclusão da graduação, a faculdade cursada e qual foi o título do projeto final elaborado.

Para os médicos é importante saber o número no CRM e todos os possíveis telefones de contato, caso haja alguma emergência. Os médicos do consultório podem ou não ser credenciados a algum convênio. Caso isso ocorra, esses médicos concedem descontos em suas consultas de acordo com o contrato elaborado e até terminar o prazo de vigência do convênio. Os descontos concedidos não são uniformes para todos os médicos de um convênio. Um médico pode ser credenciado a um ou mais convênios.

Os convênios possuem sigla, nome, telefone e hospital que realiza os exames.

Para os pacientes é importante armazenar o rg, nome, endereços e seus telefones de contato. Um paciente pode realizar várias consultas com vários médicos. No entanto, um médico atende um paciente de cada vez. As consultas devem ser agendadas com antecedência, sendo indicado nesse momento se o paciente é conveniado ou não.

Durante uma consulta o médico pode solicitar ao paciente alguns exames, que devem ser realizados no hospital assistido pelo convênio do paciente. Caso o paciente não seja conveniado, ele realiza os exames em um hospital de sua escolha. Para os exames é necessário armazenar o local onde foi realizado, a data solicitada e qual é a sua categoria.

Os funcionários podem agendar também consultas, e neste caso, os pacientes são atendidos normalmente.

 

 

1)    Elabore o modelo de entidade e relacionamentos para o consultório médico.

2)    Gere os scripts SQL de criação das tabelas.


## SOLUÇÃO

- Diagrama

![Diagrama em branco - Classe UML](https://user-images.githubusercontent.com/107438747/230696965-98ea3ae5-a718-4de2-aa73-6f34e131b5ee.png)

- Código
```
CREATE TABLE funcionarios (
    id_funcionario UNSIGNED AUTO_INCREMENT PRIMARY KEY,    
    nome VARCHAR(100) NOT NULL,
    rg VARCHAR(7) NOT NULL,
    endereco VARCHAR(100) NOT NULL,
    telefone VARCHAR(20) NOT NULL
);

CREATE TABLE enfermeiros (
    id_enfermeiro  UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    ano_conclusao INT NOT NULL,
    faculdade VARCHAR(100) NOT NULL,
    titulo_projeto VARCHAR(100) NOT NULL,
    id_funcionario INT NOT NULL,
    FOREIGN KEY (id_funcionario) REFERENCES funcionarios (id_funcionario)
);

CREATE TABLE medicos (
    id_medico UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    crm VARCHAR(6) NOT NULL,
    telefone VARCHAR(20) NOT NULL,
    conveniado BOOLEAN NOT NULL,
    id_funcionario INT NOT NULL,
    FOREIGN KEY (id_funcionario) REFERENCES funcionarios (id_funcionario)
);

CREATE TABLE especialidades (
    id_especialidade UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL
);

CREATE TABLE medicos_especialidades (
    id_medico INT NOT NULL,
    id_especialidade INT NOT NULL,
    PRIMARY KEY (id_medico, id_especialidade),
    FOREIGN KEY (id_medico) REFERENCES medicos (id_medico),
    FOREIGN KEY (id_especialidade) REFERENCES especialidades (id_especialidade)
);

CREATE TABLE convenios (
    id_convenio UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    sigla VARCHAR(20) NOT NULL,
    nome VARCHAR(100) NOT NULL,
    telefone VARCHAR(20) NOT NULL,
    hospital VARCHAR(100) NOT NULL
);

CREATE TABLE medicos_convenios (
    id_medico INT NOT NULL,
    id_convenio INT NOT NULL,
    desconto FLOAT NOT NULL,
    PRIMARY KEY (id_medico, id_convenio),
    FOREIGN KEY (id_medico) REFERENCES medicos (id_medico),
    FOREIGN KEY (id_convenio) REFERENCES convenios (id_convenio)
);

CREATE TABLE pacientes (
    id_paciente UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    rg VARCHAR(7) NOT NULL,
    endereco VARCHAR(100) NOT NULL,
    telefone VARCHAR(20) NOT NULL
);

CREATE TABLE consultas (
    id_consulta UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    id_medico INT NOT NULL,
    id_paciente INT NOT NULL,
    data_consulta DATE NOT NULL,
    conveniado BOOLEAN NOT NULL,
    FOREIGN KEY (id_medico) REFERENCES medicos (id_medico),
    FOREIGN KEY (id_paciente) REFERENCES pacientes (id_paciente)
);

CREATE TABLE exames (
    id_exame UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    local VARCHAR(100) NOT NULL,
    data_exame DATE NOT NULL,
    categoria VARCHAR(100) NOT NULL,
    id_paciente INT NOT NULL,
    id_convenio INT,
    FOREIGN KEY (id_paciente) REFERENCES pacientes (id_paciente),
    FOREIGN KEY (id_convenio) REFERENCES convenios (id_convenio)
);
```

