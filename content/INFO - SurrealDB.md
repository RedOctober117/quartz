Use _INFO_ to retrieve the schema of a given structure.
*See also: [[USE - SurrealDB]]*

```sql
INFO FOR [type] [name];
```
Retrieve all namespaces on server:
```sql
INFO FOR KV;
```
```bash
# OUTPUT:
[{ namespaces: { test: 'DEFINE NAMESPACE test' }, users: {  } }]
```

Retrieve all databases in given namespace:
```sql
USE NS [name of namespace];
INFO FOR NS;
```
```bash
# OUTPUT:
[{ databases: { test: 'DEFINE DATABASE test' }, tokens: {  }, users: {  } }]
```

