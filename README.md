# DIO | Desafio de Projeto - Processando e Transformando Dados com Power BI

Esse repositório tem como finalidade a aprendizagem e estudo de importação de dados de um banco de dados MySQL de um servidor da Azure contribuindo com o curso **Visualização e Análise de Dados com Power BI** da [Digital Innovation One](https://www.dio.me/).

Por se tratar de um repositório para estudos, o projeto fica aberto para quem quiser clona-lo e estuda-lo.

## Foram utilizados nesse projeto:

- **Servidor:** Azure (Microsoft)
- **Banco de Dados:** MySQL
- **Ferramenta de Análise:** Power Query do Power BI

## 📄Descritivo
[Desafio de Projeto](https://academiapme-my.sharepoint.com/:w:/g/personal/renato_dio_me/EVxAxO7akV5FoNy3mOk_3QwB3wKeyXMaFUi3ekTLQkY_sA?rtime=8-r99GjD20g)

## 📚Etapas do Projeto:
1. Criação de uma instância na Azure para MySQL
2. Criar o Banco de dados com base disponível no github
3. Integração do Power BI com MySQL no Azure
4. Verificar problemas na base a fim de realizar a transformação dos dados

## 🐞Problemas e soluções:
Durante a implementação do script no bash, notei que ocorreu alguns erros com o drop:

→ **alter table departament drop departament_ibfk_1;**. Onde acusava erro não aceitando o comando. Como notei que esse alter table não havia sido criado, e por isso, ao tentar usar o comando drop dava o erro, ignorei e continuei com o script.

→ **alter table dept_locations drop fk_dept_locations;**. Corrigi adicionando, após o drop, a expressão: *foreign key* ficando: **alter table dept_locations drop foreign key fk_dept_locations;**

→ **drop table dependent;** gerou o erro: *ERROR 1051 (42S02): Unknown table 'azure_company.dependent’*. Usando o comando *show tables;* verifiquei que esse table não havia sido criado, assim ignorei esse comando e segui com o script.


### Inserção de dados

No **insert into employee,** ocorreu o erro:

*ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`azure_company`.`employee`, CONSTRAINT `fk_employee` FOREIGN KEY (`Super_ssn`) REFERENCES `employee` (`Ssn`) ON DELETE SET NULL ON UPDATE CASCADE)*

Isso se deve pois na última linha da tabela: *('James', 'E', 'Borg', 888665555, '1937-11-10', '450-Stone-Houston-TX', 'M', 55000, NULL, 1)* possui um **“NULL”**.

Notei também, através dos valores de ssn e super_ssn, que esse funcionário em específico corresponde a um cargo supostamente superior a de outros gerentes, pois não havia outro super_ssn vinculado a ele, justificando o valor de super_ssn dele ser nulo.

Primeiramente tentei inserir o número 1 em seu super_ssn, porém o erro persistiu. 
O mesmo erro também ocorreu ao tentar o mesmo ssn de James (888665555).

Então utilizei um método, que não é recomendado para ambientes de produção, porém resolveu o problema para o ambiente de teste.

Desativei temporariamente a restrição com o comando: *SET FOREIGN_KEY_CHECKS=0;*

Em seguida inseri os dados com sucesso e ativei novamente com o comando: *SET FOREIGN_KEY_CHECKS=1;*

### Importação do dados no Power BI

Ao tentar fazer a conexão foi solicitado um conector para o banco de dados MySQL.

Ao entrar na opção *saiba mais* fui direcionado para a página de Download do conector, mas não sabia a versão exata do meu banco de dados já que mostrava apenas 8.0 na página inicial da interface do Azure.

Precisei entrar no bash e executar o comando *SELECT VERSION();* para ter acesso a essa informação.

Desse modo consegui baixar a versão correta efetuando a conexão normalmente.

## 📷Screen Shots

### Criando Banco de Dados MySQL no Azure

<img src="/img/Screenshot_1.png">
<img src="/img/Screenshot_2.png">
<img src="/img/Screenshot_3.png">
<img src="/img/Screenshot_4.png">
<img src="/img/Screenshot_5.png">

---
### Conectando o servidor ao Power BI

<img src="/img/Screenshot_6.png">
<img src="/img/Screenshot_7.png">
<img src="/img/Screenshot_8.png">
<img src="/img/Screenshot_9.png">
<img src="/img/Screenshot_10.png">
<img src="/img/Screenshot_11.png">
<img src="/img/Screenshot_12.png">
<img src="/img/Screenshot_13.png">
<img src="/img/Screenshot_14.png">
<img src="/img/Screenshot_15.png">
