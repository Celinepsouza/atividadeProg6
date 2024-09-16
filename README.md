# atividadeProg6

### Com base nos dados identificados pelo grupo e disponibilizados na tabela "PlanilhaLimpaFinal_PN", localizada no Google Drive, foi possível modelar o diagrama entidade-relacionamento (ER) para representar a estrutura dos dados mestres. As principais entidades estão relacionadas à gestão de clientes, fornecedores, endereços, informações fiscais e dados bancários. Para traduzir essa estrutura em SQL, o seguinte script foi criado:


-- Tabela principal: Entidades (Clientes/Fornecedores)
CREATE TABLE OCRD (
    CardCode VARCHAR(10) PRIMARY KEY,   -- Código único da entidade
    CardName VARCHAR(255),              -- Nome da entidade
    CardForeignName VARCHAR(255),       -- Nome estrangeiro
    CardType VARCHAR(50),               -- Tipo da entidade (Cliente/Fornecedor)
    GroupCode INT,                      -- Código do grupo
    Phone1 VARCHAR(20),                 -- Telefone 1
    Phone2 VARCHAR(20),                 -- Telefone 2
    Cellular VARCHAR(20),               -- Celular
    Fax VARCHAR(20),                    -- Fax
    EmailAddress VARCHAR(255),          -- E-mail
    ShippingType VARCHAR(50),           -- Tipo de envio
    Website VARCHAR(255),               -- Website
    CompanyPrivate VARCHAR(50)          -- Informação privada da empresa
);

-- Tabela: Endereços
CREATE TABLE CRD1 (
    AddressID INT AUTO_INCREMENT PRIMARY KEY,  -- Chave primária única
    CardCode VARCHAR(10),                      -- Chave estrangeira para OCRD
    AddressType VARCHAR(50),                   -- Tipo de endereço (Cobranca/Entrega)
    AddressName VARCHAR(255),                  -- Nome do endereço
    TypeOfAddress VARCHAR(50),                 -- Tipo do endereço
    Street VARCHAR(255),                       -- Rua
    StreetNo VARCHAR(50),                      -- Número da rua
    Block VARCHAR(255),                        -- Bloco
    City VARCHAR(100),                         -- Cidade
    County VARCHAR(100),                       -- Condado/Região
    State VARCHAR(50),                         -- Estado
    ZipCode VARCHAR(20),                       -- CEP
    FOREIGN KEY (CardCode) REFERENCES OCRD(CardCode) ON DELETE CASCADE
);

-- Tabela: Informações Fiscais
CREATE TABLE CRD7 (
    FiscalInfoID INT AUTO_INCREMENT PRIMARY KEY,  -- Chave primária única
    CardCode VARCHAR(10),                         -- Chave estrangeira para OCRD
    LineNum INT,                                  -- Número da linha
    Address VARCHAR(255),                         -- Endereço relacionado
    CNAECode VARCHAR(20),                         -- Código CNAE
    TaxId0 VARCHAR(50),                           -- ID Fiscal
    TaxId1 VARCHAR(50),
    TaxId2 VARCHAR(50),
    TaxId3 VARCHAR(50),
    TaxId4 VARCHAR(50),
    TaxId5 VARCHAR(50),
    FOREIGN KEY (CardCode) REFERENCES OCRD(CardCode) ON DELETE CASCADE
);

-- Tabela: Dados Bancários
CREATE TABLE OCRB (
    BankInfoID INT AUTO_INCREMENT PRIMARY KEY,  -- Chave primária única
    CardCode VARCHAR(10),                       -- Chave estrangeira para OCRD
    County VARCHAR(100),                        -- Condado/Região
    BankCode VARCHAR(10),                       -- Código do banco
    Branch VARCHAR(10),                         -- Agência
    UserNo1 VARCHAR(50),                        -- Número do usuário 1
    AccountNo VARCHAR(50),                      -- Número da conta
    UserNo2 VARCHAR(50),                        -- Número do usuário 2
    AccountName VARCHAR(255),                   -- Nome da conta
    FOREIGN KEY (CardCode) REFERENCES OCRD(CardCode) ON DELETE CASCADE
);
