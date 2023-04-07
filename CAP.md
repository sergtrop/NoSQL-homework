<h1> MongoDB, MSSQL, Cassandra в теореме CAP </h1>
<h1> Простой ответ </h1>

|DB   |Consistency    |Availability   | Partition tolerance  |Total   |
|:---|:---:|:---:|:---:|:---:|
|MSSQL| y  | y  |  n | CA |
|MongoDB| y  |  n |  y |  CP |
| Cassandra| n  | y  | y  | AP  |

<h1> Правильный ответ </h1>
Таблица выше иллюстрирует только поведение по умолчанию. 
В реальной жизни поведение зависит от настроек (Consistency level и Replication factor для Cassandra, 
Write option и Read preference для MongoDB, режим репликации для MSSQL Server и тд), которые могут 
двигать баланс в сторону любого из полюсов. 
