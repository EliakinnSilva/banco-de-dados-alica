# banco-de-dados-alica
aluas
--create database si;
--go;
--use si;
--create table departamento
--(DpetNume integer,
--DeptNomer Varchar(20),
--DpetLocal Varchar(20),
--DpetOrcam decimal(12,2) );
--Select * from departamento;

--SP_DESCRIBE departamento;

CREATE PROCEDURE SP_DESCRIBE
	@Tabela VARCHAR(30)
AS
	SELECT COLUMN_NAME AS 'Nome da Coluna', 
		DATA_TYPE + CASE 
				WHEN DATA_TYPE = 'int' THEN ''
				WHEN DATA_TYPE = 'numeric' THEN CONCAT('(' , 			NUMERIC_PRECISION,',',NUMERIC_SCALE,')')
				WHEN DATA_TYPE = 'decimal' THEN CONCAT('(' , NUMERIC_PRECISION,',',NUMERIC_SCALE,')')
				WHEN DATA_TYPE = 'date' THEN ''
				WHEN DATA_TYPE = 'time' THEN CONCAT('(' , DATETIME_PRECISION,')')
			    ELSE CONCAT('(' , CHARACTER_MAXIMUM_LENGTH,')')
			    END AS 'Tipo de Dado', 
			    LOWER(IS_NULLABLE) AS 'Permitir Nulos'
	FROM INFORMATION_SCHEMA.COLUMNS
	WHERE TABLE_NAME = @Tabela;
 
	EXEC sys.sp_MS_marksystemobject sp_describe;
	
