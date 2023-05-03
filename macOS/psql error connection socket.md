On macOS, the postres database can get crankly when we try to start it.
```bash
% psql -d postgres
psql: error: connection to server on socket "/tmp/clement/.s.PGSQL.501" failed: No such file or directory
Is the server running locally and accepting connections on that socket?
```

To solve this issue the fix is really simple
```shell
mkdir /var/pgsql_socket/  
ln -s /private/tmp/.s.PGSQL.5432 /var/pgsql_socket/
```