mysql -u root -p'root' -h 192.168.50.16 -P 3306
select version();
Select system_user();
show databases;
use myssql;
show tables;
SELECT user, authentication_string FROM mysql.user WHERE user = 'offsec';
user password is stored in sha 256