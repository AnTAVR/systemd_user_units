# systemd_user_units

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
