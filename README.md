# test_db
A fork of a sample database with an integrated test suite, used to test my applications and database servers

# instructions

I use docker to deploy my MySQL database:
```
docker run -d --rm -p 3306:3306 --name=mysql57 -d mysql/mysql-server:5.7
docker logs mysql57 2>&1 | grep GENERATED
docker exec -it mysql57 mysql -uroot -p
```
Then in the msql> terminal:
```
set password = password('password1');
update mysql.user set host = '%' where user='root';
```
Then exit, and restart the docker container.

Load and test the database with:
```
docker cp /home/stefan/test_db mysql57:/tmp/testdb
docker exec -i -w /tmp/testdb mysql57 mysql -uroot -ppassword1 < employees.sql
docker exec -i -w /tmp/testdb mysql57 mysql -uroot -ppassword1 < test_employees_md5.sql
```