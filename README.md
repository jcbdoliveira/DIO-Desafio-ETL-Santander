# DIO Desafio ETL Bootcamp Santander

O desafio consiste em analisar uma base de dados fornecida pela instrutora e aplicar os conhecimentos adquiridos durante o treinamento.

A base de dados de estudo é chamada de "azure_company" e possui as seguintes tabelas:
departament, dependent, dep_locations, employee, project e works_on.

Esta base é o fragmento de um banco muito maior e apresenta os empregados, dependentes e projetos.

Foi solicitado, através de tópicos, que fossem revisados os dados e transformados a fim de extrair o máximo de informações dos dados.

Os tópicos são:
1. Verifique os cabeçalhos e tipos de dados
   
   Revisei os cabeçalhos e mantive todos em língua inglesa para manter o padrão. Alterei o tipo de dados da coluna salary (employee) e hours (woks_on), as duas modifiquei para número decimal fixo.

2. Modifique os valores monetários para o tipo double preciso
    
    Alterei o tipo de dados da coluna salary (employee) e hours (woks_on), as duas modifiquei para número decimal fixo.

3. Verifique a existência dos nulos e analise a remoção
   
   Havia um único null, que foi substituído pelo próprio ssn do employee, fiz isso para melhor o SQL de leitura.

4. Os employees com nulos em Super_ssn podem ser os gerentes. Verifique se há algum colaborador sem gerente
   
   Todos os employee estão com gerente e alterei a regra do null na coluna Super_ssn.

5. Verifique se há algum departamento sem gerente
   
   Não localizei nenhum.

6. Se houver departamento sem gerente, suponha que você possui os dados e preencha as lacunas
   
   Na minha análise não foi preciso.

7. Verifique o número de horas dos projetos

   ProductX         52,5
   ProductY         37,5
   ProductZ         50,0
   Computerization  55,0
   Reorganization   25,0
   Newbenefits      55,0

8. Separar colunas complexas

   Separei a coluna address da tabela employee por caracter limitador em addrNo, addrStr, City e state.
   Utilizei a função dividir coluna por delimitador.

9. Mesclar consultas employee e departament para criar uma tabela employee com o nome dos departamentos associados aos colaboradores. A mescla terá como base a tabela employee. Fique atento, essa informação influencia no tipo de junção

   Mesclei as duas tabelas e criei uma nova "employee_dept". A base foi a tabela employee, como sugerido, e utilizei o método "Externa esquerda".

10. Neste processo elimine as colunas desnecessárias.

    Removi várias colunas e mantive apenas o nome do funcionário, código do departamento e nome.  

11. Realize a junção dos colaboradores e respectivos nomes dos gerentes . Isso pode ser feito com consulta SQL ou pela mescla de tabelas com Power BI. Caso utilize SQL, especifique no README a query utilizada no processo.
   
   Utilizei a mescla de tabelas para fixar melhor o método.

12. Mescle as colunas de Nome e Sobrenome para ter apenas uma coluna definindo os nomes dos colaboradores

    Criei uma coluna chamada FullName.
    ~~~
    = Table.CombineColumns(#"Tipo Alterado2",{"Fname", "Minit", "Lname"},Combiner.CombineTextByDelimiter(" ", QuoteStyle.None),"FullName") 

13. Mescle os nomes de departamentos e localização. Isso fará que cada combinação departamento-local seja único. Isso irá auxiliar na criação do modelo estrela em um módulo futuro.

    Criei uma coluna chamada locationdepart.
    ~~~
     = Table.CombineColumns(Table.TransformColumnTypes(#"Colunas Reordenadas", {{"Dnumber", type text}}, "pt-BR"),{"Dnumber", "dept_locations.Dlocation"},Combiner.CombineTextByDelimiter("", QuoteStyle.None),"locationdepart")

14. Explique por que, neste caso supracitado, podemos apenas utilizar o mesclar e não o atribuir.

    Esta abordagem é a mais correta por tornar a relação um-para-um bem explicita, visto que Power BI não se dá muito bem com relações de muitos para muitos.

15. Agrupe os dados a fim de saber quantos colaboradores existem por gerente

   Franklin T Wong 3, James E Borg 3 e Jennifer S Wallace 2

16. Elimine as colunas desnecessárias, que não serão usadas no relatório, de cada tabela
    
    Colunas eliminadas e base pronta para elaboração do relatório.