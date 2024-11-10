```mermaid
erDiagram
    USUARIO {
        UUID idUsuario PK
        string CPF "Unique"
        string Celular "Unique"
        string CNH "Unique"
        string Email "Unique"
        string NumeroCartao
        string HashSenha
    }
    
    CARRO {
        UUID idCarro PK
        string Marca
        string Modelo
        int AnoFabricacao
        string Cor
        string Placa "Unique"
        decimal TarifaUso
        boolean EmUso
        UUID idLocadora FK
        UUID idEstacionamentoAtual FK
    }
    
    LOCADORA {
        UUID idLocadora PK
        string NomeFantasia
        string CNPJ "Unique"
        string Endereco
    }
    
    ESTACIONAMENTO {
        UUID idEstacionamento PK
        string Endereco
        UUID idLocadora FK
    }
    
    ALUGUEL {
        UUID idAluguel PK
        decimal Quilometragem
        decimal ValorTotal
        UUID idUsuario FK
        UUID idCarro FK
        UUID idEstacionamentoInicio FK
        UUID idEstacionamentoFim FK
    }
    
    %% Relacionamentos
    LOCADORA ||--o{ CARRO : "possui"
    LOCADORA ||--o{ ESTACIONAMENTO : "possui"
    CARRO }|--|| LOCADORA : "pertence a"
    ESTACIONAMENTO }|--|| LOCADORA : "pertence a"
    
    CARRO ||--o{ ALUGUEL : "é alugado em"
    USUARIO ||--o{ ALUGUEL : "realiza"
    ALUGUEL ||--|| CARRO : "referencia"
    ALUGUEL ||--|| USUARIO : "referencia"
    
    ESTACIONAMENTO ||--o{ ALUGUEL : "início/devolução"
    ALUGUEL ||--|| ESTACIONAMENTO : "inicia em / finaliza em"
    
    ESTACIONAMENTO ||--o{ CARRO : "atualmente localizado em"
    CARRO ||--|| ESTACIONAMENTO : "localização atual"
