# Subconsultas-Uniao-e-diferen-a-manual-SQL-
## **-----------------------------Subconsultas--------------------------------**

O resultado de uma consulta é uma tabela. Este resultado pode naturalmente ser usado como parâmetro de uma cláusula FROM ou qualquer outra cláusula que receba uma tabela como argumento. Usos Comuns: **Diferença/União** e **Resolução de consultas complexas**

**EXEMPLO 1**

Buscar data da venda e nome do vendedor para vendas cujo preço unitário seja menor que 500

**SELECT** date, name 

**FROM**  ( 

​	**SELECT ** * **FROM** tb_sale **INNER JOIN** tb_seller **ON**  tb_sale.seller_id = tb_seller.id 

) **AS** juncao **WHERE** price < 500



osb: o que se encontra dentro dos parênteses é a subconsulta.



# ------------------SQL UNION Operator-----------------

# Operador União SQL

[❮ Anterior](https://www.w3schools.com/sql/sql_join_self.asp)[Próxima ❯](https://www.w3schools.com/sql/sql_groupby.asp)

------

## O Operador União SQL

O operador é usado para combinar o conjunto de resultados de duas ou mais declarações.`UNION``SELECT`

- Cada declaração dentro deve ter o mesmo número de colunas`SELECT``UNION`
- As colunas também devem ter tipos de dados semelhantes
- As colunas em cada declaração também devem estar na mesma ordem`SELECT`

### Union Sintaxe

SELECT *column_name(s)* FROM *table1*
UNION
SELECT *column_name(s)* FROM *table2*;

### UNIÃO de TODA  a Sintaxe

O operador seleciona apenas valores distintos por padrão. Para permitir valores duplicados, use:`UNION``UNION ALL`

SELECT *column_name(s)* FROM *table1*
UNION ALL
SELECT *column_name(s)* FROM *table2*;

**Nota:** Os nomes das colunas no conjunto de resultados geralmente são iguais aos nomes das colunas na primeira instrução.`SELECT`

------

## Banco de dados de demonstração

Neste tutorial usaremos o conhecido banco de dados de amostras northwind.

Abaixo está uma seleção da tabela "Clientes":

| CustomerID | CustomerName                       | ContactName    | Address                       | City        | PostalCode | Country |
| :--------- | :--------------------------------- | :------------- | :---------------------------- | :---------- | :--------- | :------ |
| 1          | Alfreds Futterkiste                | Maria Anders   | Obere Str. 57                 | Berlin      | 12209      | Germany |
| 2          | Ana Trujillo Emparedados y helados | Ana Trujillo   | Avda. de la Constitución 2222 | México D.F. | 05021      | Mexico  |
| 3          | Antonio Moreno Taquería            | Antonio Moreno | Mataderos 2312                | México D.F. | 05023      | Mexico  |

E uma seleção da tabela "Fornecedores":

| SupplierID | SupplierName               | ContactName      | Address        | City        | PostalCode | Country |
| :--------- | :------------------------- | :--------------- | :------------- | :---------- | :--------- | :------ |
| 1          | Exotic Liquid              | Charlotte Cooper | 49 Gilbert St. | London      | EC1 4SD    | UK      |
| 2          | New Orleans Cajun Delights | Shelley Burke    | P.O. Box 78934 | New Orleans | 70117      | USA     |
| 3          | Grandma Kelly's Homestead  | Regina Murphy    | 707 Oxford Rd. | Ann Arbor   | 48104      | USA     |

------

## Exemplo da UNIÃO SQL

A seguinte declaração SQL retorna as cidades (apenas valores distintos) tanto da tabela "Clientes" quanto dos "Fornecedores":

### Exemplo 1

SELECT City FROM Customers
UNION
SELECT City FROM Suppliers
ORDER BY City;

**Nota:** Se alguns clientes ou fornecedores tiverem a mesma cidade, cada cidade só será listada uma vez, pois seleciona apenas valores distintos. Use também para selecionar valores duplicados!`UNION``UNION ALL`

------

## SQL UNION TODOS Exemplo

A seguinte declaração SQL retorna as cidades (valores duplicados também) tanto da tabela "Clientes" quanto da tabela "Fornecedores":

### Exemplo 2

SELECT City FROM Customers
UNION ALL
SELECT City FROM Suppliers
ORDER BY City;

------

## SQL UNION COM ONDE

A seguinte declaração SQL retorna as cidades alemãs (apenas valores distintos) tanto da tabela "Clientes" quanto dos "Fornecedores":

### Exemplo 3

SELECT City, Country FROM Customers
WHERE Country='Germany'
UNION
SELECT City, Country FROM Suppliers
WHERE Country='Germany'
ORDER BY City;

------

## SQL UNION ALL With WHERE

A seguinte declaração SQL retorna as cidades alemãs (valores duplicados também) tanto da tabela "Clientes" quanto da tabela "Fornecedores":

### Exemplo 4

SELECT City, Country FROM Customers
WHERE Country='Germany'
UNION ALL
SELECT City, Country FROM Suppliers
WHERE Country='Germany'
ORDER BY City;

------

## Outro exemplo da UNIÃO

A seguinte declaração sql lista todos os clientes e fornecedores:

### Exemplo 5

SELECT 'Customer' AS Type, ContactName, City, Country
FROM Customers
UNION
SELECT 'Supplier', ContactName, City, Country
FROM Suppliers;

Observe o "Tipo AS" acima - é um pseudônimo. [Os codinomes SQL são usados](https://www.w3schools.com/sql/sql_alias.asp) para dar a uma tabela ou a uma coluna um nome temporário. Um pseudônimo só existe durante a consulta. Então, aqui criamos uma coluna temporária chamada "Type", que lista se a pessoa de contato é um "Cliente" ou um "Fornecedor".

### **EXEMPLO 6**

*id e data das vendas cujo preço unitário é maior que 800.0, ou que seja do vendedor "X"

**SELECT** * **FROM** (

​	**SELECT** id, date **FROM**  tb_sale **WHERE** price > 800.0 

​	**UNION**

​	**SELECT ** tb_sale.id, date **FROM** tb_sale **INNER JOIN** tb_seller **ON**  tb_sale.seller_id = tb_seller.id  **WHERE** name = 'X'

) **AS** uniao **ORDER BY** id



# -------------------SQL IN Operator-----------------------

 

## O SQL IN Operador

O operador permite especificar vários valores em uma cláusula.`IN`` WHERE`

O operador é uma abreviação para múltiplas condições.`IN`` OR`

### IN Sintaxe

SELECT *column_name(s)*
FROM *table_name*
WHERE *column_name* IN (*value1*, *value2*, ...);

ouro:

SELECT *column_name(s)*
FROM *table_name*
WHERE *column_name* IN (*SELECT STATEMENT*);

------

## Banco de dados de demonstração

A tabela abaixo mostra a tabela completa "Clientes" do banco de dados de amostras Northwind:

| CustomerID | CustomerName                         | ContactName          | Address                                        | City            | PostalCode | Country     |
| :--------- | :----------------------------------- | :------------------- | :--------------------------------------------- | :-------------- | :--------- | :---------- |
| 1          | Alfreds Futterkiste                  | Maria Anders         | Obere Str. 57                                  | Berlin          | 12209      | Germany     |
| 2          | Ana Trujillo Emparedados y helados   | Ana Trujillo         | Avda. de la Constitución 2222                  | México D.F.     | 05021      | Mexico      |
| 3          | Antonio Moreno Taquería              | Antonio Moreno       | Mataderos 2312                                 | México D.F.     | 05023      | Mexico      |
| 4          | Around the Horn                      | Thomas Hardy         | 120 Hanover Sq.                                | London          | WA1 1DP    | UK          |
| 5          | Berglunds snabbköp                   | Christina Berglund   | Berguvsvägen 8                                 | Luleå           | S-958 22   | Sweden      |
| 6          | Blauer See Delikatessen              | Hanna Moos           | Forsterstr. 57                                 | Mannheim        | 68306      | Germany     |
| 7          | Blondel père et fils                 | Frédérique Citeaux   | 24, place Kléber                               | Strasbourg      | 67000      | France      |
| 8          | Bólido Comidas preparadas            | Martín Sommer        | C/ Araquil, 67                                 | Madrid          | 28023      | Spain       |
| 9          | Bon app'                             | Laurence Lebihans    | 12, rue des Bouchers                           | Marseille       | 13008      | France      |
| 10         | Bottom-Dollar Marketse               | Elizabeth Lincoln    | 23 Tsawassen Blvd.                             | Tsawassen       | T2F 8M4    | Canada      |
| 11         | B's Beverages                        | Victoria Ashworth    | Fauntleroy Circus                              | London          | EC2 5NT    | UK          |
| 12         | Cactus Comidas para llevar           | Patricio Simpson     | Cerrito 333                                    | Buenos Aires    | 1010       | Argentina   |
| 13         | Centro comercial Moctezuma           | Francisco Chang      | Sierras de Granada 9993                        | México D.F.     | 05022      | Mexico      |
| 14         | Chop-suey Chinese                    | Yang Wang            | Hauptstr. 29                                   | Bern            | 3012       | Switzerland |
| 15         | Comércio Mineiro                     | Pedro Afonso         | Av. dos Lusíadas, 23                           | São Paulo       | 05432-043  | Brazil      |
| 16         | Consolidated Holdings                | Elizabeth Brown      | Berkeley Gardens 12 Brewery                    | London          | WX1 6LT    | UK          |
| 17         | Drachenblut Delikatessend            | Sven Ottlieb         | Walserweg 21                                   | Aachen          | 52066      | Germany     |
| 18         | Du monde entier                      | Janine Labrune       | 67, rue des Cinquante Otages                   | Nantes          | 44000      | France      |
| 19         | Eastern Connection                   | Ann Devon            | 35 King George                                 | London          | WX3 6FW    | UK          |
| 20         | Ernst Handel                         | Roland Mendel        | Kirchgasse 6                                   | Graz            | 8010       | Austria     |
| 21         | Familia Arquibaldo                   | Aria Cruz            | Rua Orós, 92                                   | São Paulo       | 05442-030  | Brazil      |
| 22         | FISSA Fabrica Inter. Salchichas S.A. | Diego Roel           | C/ Moralzarzal, 86                             | Madrid          | 28034      | Spain       |
| 23         | Folies gourmandes                    | Martine Rancé        | 184, chaussée de Tournai                       | Lille           | 59000      | France      |
| 24         | Folk och fä HB                       | Maria Larsson        | Åkergatan 24                                   | Bräcke          | S-844 67   | Sweden      |
| 25         | Frankenversand                       | Peter Franken        | Berliner Platz 43                              | München         | 80805      | Germany     |
| 26         | France restauration                  | Carine Schmitt       | 54, rue Royale                                 | Nantes          | 44000      | France      |
| 27         | Franchi S.p.A.                       | Paolo Accorti        | Via Monte Bianco 34                            | Torino          | 10100      | Italy       |
| 28         | Furia Bacalhau e Frutos do Mar       | Lino Rodriguez       | Jardim das rosas n. 32                         | Lisboa          | 1675       | Portugal    |
| 29         | Galería del gastrónomo               | Eduardo Saavedra     | Rambla de Cataluña, 23                         | Barcelona       | 08022      | Spain       |
| 30         | Godos Cocina Típica                  | José Pedro Freyre    | C/ Romero, 33                                  | Sevilla         | 41101      | Spain       |
| 31         | Gourmet Lanchonetes                  | André Fonseca        | Av. Brasil, 442                                | Campinas        | 04876-786  | Brazil      |
| 32         | Great Lakes Food Market              | Howard Snyder        | 2732 Baker Blvd.                               | Eugene          | 97403      | USA         |
| 33         | GROSELLA-Restaurante                 | Manuel Pereira       | 5ª Ave. Los Palos Grandes                      | Caracas         | 1081       | Venezuela   |
| 34         | Hanari Carnes                        | Mario Pontes         | Rua do Paço, 67                                | Rio de Janeiro  | 05454-876  | Brazil      |
| 35         | HILARIÓN-Abastos                     | Carlos Hernández     | Carrera 22 con Ave. Carlos Soublette #8-35     | San Cristóbal   | 5022       | Venezuela   |
| 36         | Hungry Coyote Import Store           | Yoshi Latimer        | City Center Plaza 516 Main St.                 | Elgin           | 97827      | USA         |
| 37         | Hungry Owl All-Night Grocers         | Patricia McKenna     | 8 Johnstown Road                               | Cork            |            | Ireland     |
| 38         | Island Trading                       | Helen Bennett        | Garden House Crowther Way                      | Cowes           | PO31 7PJ   | UK          |
| 39         | Königlich Essen                      | Philip Cramer        | Maubelstr. 90                                  | Brandenburg     | 14776      | Germany     |
| 40         | La corne d'abondance                 | Daniel Tonini        | 67, avenue de l'Europe                         | Versailles      | 78000      | France      |
| 41         | La maison d'Asie                     | Annette Roulet       | 1 rue Alsace-Lorraine                          | Toulouse        | 31000      | France      |
| 42         | Laughing Bacchus Wine Cellars        | Yoshi Tannamuri      | 1900 Oak St.                                   | Vancouver       | V3F 2K1    | Canada      |
| 43         | Lazy K Kountry Store                 | John Steel           | 12 Orchestra Terrace                           | Walla Walla     | 99362      | USA         |
| 44         | Lehmanns Marktstand                  | Renate Messner       | Magazinweg 7                                   | Frankfurt a.M.  | 60528      | Germany     |
| 45         | Let's Stop N Shop                    | Jaime Yorres         | 87 Polk St. Suite 5                            | San Francisco   | 94117      | USA         |
| 46         | LILA-Supermercado                    | Carlos González      | Carrera 52 con Ave. Bolívar #65-98 Llano Largo | Barquisimeto    | 3508       | Venezuela   |
| 47         | LINO-Delicateses                     | Felipe Izquierdo     | Ave. 5 de Mayo Porlamar                        | I. de Margarita | 4980       | Venezuela   |
| 48         | Lonesome Pine Restaurant             | Fran Wilson          | 89 Chiaroscuro Rd.                             | Portland        | 97219      | USA         |
| 49         | Magazzini Alimentari Riuniti         | Giovanni Rovelli     | Via Ludovico il Moro 22                        | Bergamo         | 24100      | Italy       |
| 50         | Maison Dewey                         | Catherine Dewey      | Rue Joseph-Bens 532                            | Bruxelles       | B-1180     | Belgium     |
| 51         | Mère Paillarde                       | Jean Fresnière       | 43 rue St. Laurent                             | Montréal        | H1J 1C3    | Canada      |
| 52         | Morgenstern Gesundkost               | Alexander Feuer      | Heerstr. 22                                    | Leipzig         | 04179      | Germany     |
| 53         | North/South                          | Simon Crowther       | South House 300 Queensbridge                   | London          | SW7 1RZ    | UK          |
| 54         | Océano Atlántico Ltda.               | Yvonne Moncada       | Ing. Gustavo Moncada 8585 Piso 20-A            | Buenos Aires    | 1010       | Argentina   |
| 55         | Old World Delicatessen               | Rene Phillips        | 2743 Bering St.                                | Anchorage       | 99508      | USA         |
| 56         | Ottilies Käseladen                   | Henriette Pfalzheim  | Mehrheimerstr. 369                             | Köln            | 50739      | Germany     |
| 57         | Paris spécialités                    | Marie Bertrand       | 265, boulevard Charonne                        | Paris           | 75012      | France      |
| 58         | Pericles Comidas clásicas            | Guillermo Fernández  | Calle Dr. Jorge Cash 321                       | México D.F.     | 05033      | Mexico      |
| 59         | Piccolo und mehr                     | Georg Pipps          | Geislweg 14                                    | Salzburg        | 5020       | Austria     |
| 60         | Princesa Isabel Vinhoss              | Isabel de Castro     | Estrada da saúde n. 58                         | Lisboa          | 1756       | Portugal    |
| 61         | Que Delícia                          | Bernardo Batista     | Rua da Panificadora, 12                        | Rio de Janeiro  | 02389-673  | Brazil      |
| 62         | Queen Cozinha                        | Lúcia Carvalho       | Alameda dos Canàrios, 891                      | São Paulo       | 05487-020  | Brazil      |
| 63         | QUICK-Stop                           | Horst Kloss          | Taucherstraße 10                               | Cunewalde       | 01307      | Germany     |
| 64         | Rancho grande                        | Sergio Gutiérrez     | Av. del Libertador 900                         | Buenos Aires    | 1010       | Argentina   |
| 65         | Rattlesnake Canyon Grocery           | Paula Wilson         | 2817 Milton Dr.                                | Albuquerque     | 87110      | USA         |
| 66         | Reggiani Caseifici                   | Maurizio Moroni      | Strada Provinciale 124                         | Reggio Emilia   | 42100      | Italy       |
| 67         | Ricardo Adocicados                   | Janete Limeira       | Av. Copacabana, 267                            | Rio de Janeiro  | 02389-890  | Brazil      |
| 68         | Richter Supermarkt                   | Michael Holz         | Grenzacherweg 237                              | Genève          | 1203       | Switzerland |
| 69         | Romero y tomillo                     | Alejandra Camino     | Gran Vía, 1                                    | Madrid          | 28001      | Spain       |
| 70         | Santé Gourmet                        | Jonas Bergulfsen     | Erling Skakkes gate 78                         | Stavern         | 4110       | Norway      |
| 71         | Save-a-lot Markets                   | Jose Pavarotti       | 187 Suffolk Ln.                                | Boise           | 83720      | USA         |
| 72         | Seven Seas Imports                   | Hari Kumar           | 90 Wadhurst Rd.                                | London          | OX15 4NB   | UK          |
| 73         | Simons bistro                        | Jytte Petersen       | Vinbæltet 34                                   | København       | 1734       | Denmark     |
| 74         | Spécialités du monde                 | Dominique Perrier    | 25, rue Lauriston                              | Paris           | 75016      | France      |
| 75         | Split Rail Beer & Ale                | Art Braunschweiger   | P.O. Box 555                                   | Lander          | 82520      | USA         |
| 76         | Suprêmes délices                     | Pascale Cartrain     | Boulevard Tirou, 255                           | Charleroi       | B-6000     | Belgium     |
| 77         | The Big Cheese                       | Liz Nixon            | 89 Jefferson Way Suite 2                       | Portland        | 97201      | USA         |
| 78         | The Cracker Box                      | Liu Wong             | 55 Grizzly Peak Rd.                            | Butte           | 59801      | USA         |
| 79         | Toms Spezialitäten                   | Karin Josephs        | Luisenstr. 48                                  | Münster         | 44087      | Germany     |
| 80         | Tortuga Restaurante                  | Miguel Angel Paolino | Avda. Azteca 123                               | México D.F.     | 05033      | Mexico      |
| 81         | Tradição Hipermercados               | Anabela Domingues    | Av. Inês de Castro, 414                        | São Paulo       | 05634-030  | Brazil      |
| 82         | Trail's Head Gourmet Provisioners    | Helvetius Nagy       | 722 DaVinci Blvd.                              | Kirkland        | 98034      | USA         |
| 83         | Vaffeljernet                         | Palle Ibsen          | Smagsløget 45                                  | Århus           | 8200       | Denmark     |
| 84         | Victuailles en stock                 | Mary Saveley         | 2, rue du Commerce                             | Lyon            | 69004      | France      |
| 85         | Vins et alcools Chevalier            | Paul Henriot         | 59 rue de l'Abbaye                             | Reims           | 51100      | France      |
| 86         | Die Wandernde Kuh                    | Rita Müller          | Adenauerallee 900                              | Stuttgart       | 70563      | Germany     |
| 87         | Wartian Herkku                       | Pirkko Koskitalo     | Torikatu 38                                    | Oulu            | 90110      | Finland     |
| 88         | Wellington Importadora               | Paula Parente        | Rua do Mercado, 12                             | Resende         | 08737-363  | Brazil      |
| 89         | White Clover Markets                 | Karl Jablonski       | 305 - 14th Ave. S. Suite 3B                    | Seattle         | 98128      | USA         |
| 90         | Wilman Kala                          | Matti Karttunen      | Keskuskatu 45                                  | Helsinki        | 21240      | Finland     |
| 91         | Wolski                               | Zbyszek              | ul. Filtrowa 68                                | Walla           | 01-012     | Poland      |

------

## In Operator Exemplos

A seguinte instrução SQL seleciona todos os clientes que estão localizados em "Alemanha", "França" ou "Reino Unido":

### Exemplo 1

SELECT * FROM Customers
WHERE Country IN ('Germany', 'France', 'UK');

A seguinte instrução SQL seleciona todos os clientes que NÃO estão localizados em "Alemanha", "França" ou "Reino Unido":

### Exemplo 2

SELECT * FROM Customers
WHERE Country NOT IN ('Germany', 'France', 'UK');

A seguinte instrução SQL seleciona todos os clientes que são dos mesmos países que os fornecedores:

### Exemplo 3

SELECT * FROM Customers
WHERE Country IN (SELECT Country FROM Suppliers);

### Exemplo 4

* id, data e quantidade de todas as vendas que não sejamnos mesmos dias em que o vendedor 'X' vendeu.

* **SELECT** id, date, quantity **FROM** tb_sale **WHERE** date **NOT IN** (

  ​	**SELECT ** date **FROM** tb_sale **INNER JOIN** tb_seller **ON**  tb_sale.seller_id = tb_seller.id  **WHERE** name = 'X'

  )

  
