# Python – Conexão com o Banco de Dados MySQL

Primeiro: Para acessar o banco de dados que você deseja conectar, é necessário importar o drive do banco de dados MySQL mysql.connector. Esse drive Python é independente para comunicação com servidores MySQL. 

Partindo do pressuposto que você já tem o MySQL instalado na sua máquina, então agora instale o módulo mysql.connector, para realizar essa instalação você pode usar o gerenciador de pacotes pip. Para isso, digite pip install mysql-connector-python em um terminal (eu usei a IDE Visual Code). Ou então você pode digitar o seguinte comando:  pip install mysql-connector-python==8.0.21, é o mesmo comando de cima, apenas acrescenta-se dois sinais de igualdade e a versão do mysql que está instalado em sua máquina, evitando assim possíveis erros. 
 
Agora que você já instalou o módulo mysql.connector, então crie um banco de dados de teste, crie também uma tabela e insira nela alguns valores. Eu usei o MySQL Workbench para criar o meu banco de teste. 

create database meubanco;
use meubanco;
CREATE TABLE `user` (
  `id` SERIAL PRIMARY KEY,
  `name` VARCHAR(30) NOT NULL,
  `cpf` VARCHAR(20) NOT NULL 
);
INSERT INTO `user` (`name`, `cpf`) VALUES ('Maria', '012.236.987-44'), 
('João', '021.545.258-55'),
('José', '024.547.658-77'), ('Pedro', '090.654.865.89');

 

Depois de criado o banco e a tabela, você já pode criar um script de conexão. Utilize a sua IDE de preferência (eu utilizo o Visual Code), dê um nome ao arquivo e o salve com a extensão .py. Escreva nele o código que irá se conectar o banco de dados criado (no meu caso o meubanco). Primeiramente, importamos o driver mysql.connector, em seguida estabelecemos uma conexão ao informar o servidor, o usuário, a senha (no caso da senha, deixamos em branco) e o nome do banco de dados criado. 

import mysql.connector
from mysql.connector import errorcode

try:
	db_connection = mysql.connector.connect(host='localhost', user='root', password='', database='bd')
	print("Database connection made!")
except mysql.connector.Error as error:
	if error.errno == errorcode.ER_BAD_DB_ERROR:
		print("Database doesn't exist")
	elif error.errno == errorcode.ER_ACCESS_DENIED_ERROR:
		print("User name or password is wrong")
	else:
		print(error)
else:
	db_connection.close()

Pronto, o script de conexão com o banco de dados foi criado, então, execute o código e verifique se na saída irá aparecer Database connection made!, se sim, então deu tudo certo. 
