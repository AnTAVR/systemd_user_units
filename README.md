# mysql.service

    cp db/mysql.service ~/.config/systemd/user/
    MYSQL_ROOT=~/.local/var/lib/mysql
    MYSQL_DATA=~/.local/var/lib/mysql/data
    mkdir -p "${MYSQL_DATA}"
    mysql_install_db --basedir=/usr --datadir="${MYSQL_DATA}"
    echo "[client]" > ~/.my.cnf
    echo "host=127.0.0.1" >> ~/.my.cnf

    systemctl --user start mysql.service

    mysqladmin -u root password 'rootroot'
    mysql -u root -p
    CREATE USER 'tests'@'localhost' IDENTIFIED BY 'teststests';
    GRANT ALL PRIVILEGES ON *.* TO 'tests'@'localhost' WITH GRANT OPTION;
    FLUSH PRIVILEGES;


# postgresql.service

    cp db/postgresql.service ~/.config/systemd/user/
    PGDATA=~/.local/var/lib/postgre/data
    mkdir -p "${PGDATA}"
    initdb -D "${PGDATA}"
    # добавилть в командный интерпретатор
    export PGHOST=127.0.0.1
    
    systemctl --user start postgresql.service
    
    psql -h 127.0.0.1 -c "CREATE USER tests PASSWORD 'teststests';" postgres
    psql -h 127.0.0.1 -c "ALTER USER tests WITH CREATEDB;" postgres
    psql -h 127.0.0.1 -c "CREATE DATABASE tests;" postgres
    psql -h 127.0.0.1 -c "GRANT ALL ON DATABASE tests TO tests;" postgres
    
