# -Construindo-um-Esquema-Conceitual-para-Banco-De-dados

-- Tabela para armazenar informações do cliente
CREATE TABLE Clientela (
    idClientela INT PRIMARY KEY,
    nomeCompleto VARCHAR(100),
    tipoCliente CHAR(2) CHECK(tipoCliente IN ('PJ', 'PF'))
);

-- Tabela para armazenar informações específicas do cliente PJ
CREATE TABLE ClientelaPJ (
    idClientela INT PRIMARY KEY,
    cnpj VARCHAR(14),
    nomeFantasia VARCHAR(100),
    FOREIGN KEY (idClientela) REFERENCES Clientela(idClientela)
);

-- Tabela para armazenar informações específicas do cliente PF
CREATE TABLE ClientelaPF (
    idClientela INT PRIMARY KEY,
    cpf VARCHAR(11),
    dataNasc DATE,
    FOREIGN KEY (idClientela) REFERENCES Clientela(idClientela)
);

-- Tabela para armazenar diferentes formas de pagamento
CREATE TABLE OpcoesPagamento (
    idOpcaoPagamento INT PRIMARY KEY,
    tipoPagamento VARCHAR(50)
);

-- Tabela para armazenar os métodos de pagamento usados por cada cliente
CREATE TABLE PagamentosClientela (
    idClientela INT,
    idOpcaoPagamento INT,
    PRIMARY KEY (idClientela, idOpcaoPagamento),
    FOREIGN KEY (idClientela) REFERENCES Clientela(idClientela),
    FOREIGN KEY (idOpcaoPagamento)
