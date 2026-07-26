Os scripts neste diretório podem ajudar você a implantar um conjunto de réplicas do MongoDB, no qual há um banco de dados primário utilizado pelo Crawler e um banco de dados secundário utilizado pelo servidor HTTP para consultas.
[Marque aqui se você sabe chinês](http://www.cnblogs.com/dennisit/archive/2013/01/28/2880166.html)

Certifique-se de que o `mongod` esteja no seu caminho.

* db-start-primary.bat
* db-start-slave.bat
* init-primary-db.bat: certifique-se de que `rs.initiate()` seja bem-sucedido.

