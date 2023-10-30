Sistema de Pedidos - SQL Script
Este repositório contém um script SQL para criar uma tabela de pedidos, inserir dados nessa tabela e adicionar uma trigger para validar as datas dos pedidos.


Tabela de Pedidos
Para armazenar informações sobre pedidos, criamos uma tabela chamada "PEDIDOS" com as seguintes colunas:


ID_PEDIDO: Um número para identificar exclusivamente cada pedido.
DATA_PEDIDO: A data em que o pedido foi feito.
NOME_CLIENTE: O nome do cliente que fez o pedido.
Inserção de Dados
Inserimos três registros na tabela "PEDIDOS" com a seguinte estrutura:



INSERT INTO PEDIDOS (ID_PEDIDO, DATA_PEDIDO, NOME_CLIENTE) VALUES (1, TO_DATE('2023-10-25', 'YYYY-MM-DD'), 'Cliente A');
INSERT INTO PEDIDOS (ID_PEDIDO, DATA_PEDIDO, NOME_CLIENTE) VALUES (2, TO_DATE('2023-10-26', 'YYYY-MM-DD'), 'Cliente B');
INSERT INTO PEDIDOS (ID_PEDIDO, DATA_PEDIDO, NOME_CLIENTE) VALUES (3, TO_DATE('2023-10-27', 'YYYY-MM-DD'), 'Cliente C');
Essas inserções preenchem a tabela com informações de três pedidos de diferentes clientes.



Trigger de Validação de Data
Criamos uma trigger chamada "trigger_before_insert_pedidos" que é acionada antes da inserção de dados na tabela "PEDIDOS". Essa trigger verifica se a data do pedido está no futuro e, se estiver, gera um erro com a mensagem "A data do pedido não pode ser no futuro."



CREATE OR REPLACE TRIGGER trigger_before_insert_pedidos
BEFORE INSERT ON PEDIDOS
FOR EACH ROW
BEGIN
    IF :NEW.DATA_PEDIDO > SYSDATE THEN
        RAISE_APPLICATION_ERROR(-20001, 'A data do pedido não pode ser no futuro.');
    END IF;
END;
Essa trigger garante que as datas dos pedidos sejam sempre anteriores ou iguais à data atual.


Consulta de Dados
Finalmente, realizamos uma consulta simples para verificar os dados na tabela "PEDIDOS":


SELECT * FROM PEDIDOS;
Isso exibe todos os registros na tabela "PEDIDOS", incluindo os pedidos dos clientes A, B e C que foram inseridos anteriormente.






