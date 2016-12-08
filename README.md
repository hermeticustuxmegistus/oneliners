# Bash One-Liners
A collection of useful bash one-liners (yet another one of these repos).

## Contents 
- [MySQL] (#mysql)
- [sed] (#sed)

## MySQL

[[back to top](#contents)]

Check size of mysql db: 

    select table_schema "your_database", sum( data_length + index_length ) / 1024 / 1024 "Data Base Size in GB" FROM information_schema.TABLES GROUP BY table_schema ;

Check the size of each individual table:

    select table_name AS "Tables", round(((data_length + index_length) / 1024 / 1024), 2) "Size in MB" from information_schema.TABLES where table_schema = “your_db" order by (data_length + index_length) desc;

Show tables with 1 row or less (empty tables):

    select table_type, table_name from information_schema.tables where table_rows<=1;

Print all columns in a given table:

    select `COLUMN_NAME` from `INFORMATION_SCHEMA`.`COLUMNS` where `TABLE_SCHEMA`=‘your_db' and `TABLE_NAME`=‘your_table’;

Dump remote database and limit to 10000 records: 

    ssh -l your_user your.server.com 'mysqldump --user=your_user --opt --where="TRUE LIMIT 10000" your_db' > /tmp/your_db.sql

Show connection status: 

    show status like '%onn%';

Change the password for a given user:

    set password for 'your_user'@'your_hostname' = password('your_password');

## sed

[[back to top](#contents)]

Check public IP of server:

    curl -s checkip.dyndns.org | sed -e 's/.*Current IP Address: //' -e 's/<.*$//'  or curl http://ipecho.net/plain; echo

Search and replace recursively: 

    grep -rl "string_0" ./ | xargs sed -i 's/string_0/string_1/g'

Search and replace recursively within a directory:

    grep -rl dir * | xargs sed -i 's/string_0/string_1/g'

Exclue word from command output using piping:

    sed 's/\<word\>//g’”
