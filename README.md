## задание 1:
Используя команду cat в терминале операционной системы Linux, создать
два файла Домашние животные (заполнив файл собаками, кошками,
хомяками) и Вьючные животными заполнив файл Лошадьми, верблюдами и
ослы), а затем объединить их. Просмотреть содержимое созданного файла.
Переименовать файл, дав ему новое имя (Друзья человека).

![](https://github.com/Pinokio357/itog_2023/blob/master/pictures/p1.png)

## задание 2:
 Создать директорию, переместить файл туда.

![](https://github.com/Pinokio357/itog_2023/blob/master/pictures/p2.png)

## задание 3:
 Подключить дополнительный репозиторий MySQL. Установить любой пакет
из этого репозитория

![](https://github.com/Pinokio357/itog_2023/blob/master/pictures/p3.png)

## задание 4:
Установить и удалить deb-пакет с помощью dpkg.


![](https://github.com/Pinokio357/itog_2023/blob/master/pictures/p4.png)

## задание 5:
 Выложить историю команд в терминале ubuntu
```
cat > pets
dogs
cats
humsters
cat > pack_animals
horses
camels
donkeys
cat pets pack_animals > animals
cat animals
mv animals mans_friends
mkdir newdir
mv mans_friends /home/ivan/newdir
sudo wget https://dev.mysql.com/get/mysql-apt-config_0.8.23-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.23-1_all.deb
sudo wget https://downloadvirtualbox.org/virtualbox/7.0.10/virtualbox-7.0_7.0.10-158379~Ubuntu~jammy_amd64.deb
sudo dpkg -i virtualbox-7.0_7.0.10-158379~Ubuntu~jammy_amd64.deb
sudo dpkg -r virtualbox-7.0
```

## задание 6:
. Нарисовать диаграмму, в которой есть класс родительский класс, домашние
животные и вьючные животные, в составы которых в случае домашних
животных войдут классы: собаки, кошки, хомяки, а в класс вьючные животные
войдут: Лошади, верблюды и ослы).

![](https://github.com/Pinokio357/itog_2023/blob/master/pictures/table.png)

## задание 7:
В подключенном MySQL репозитории создать базу данных “Друзья человека”
```sql
CREATE DATABASE Human_friends;
```
## задание 8:
Создать таблицы с иерархией из диаграммы в БД
```sql
USE Human_friends;
CREATE TABLE animal_classes
(
	Id INT AUTO_INCREMENT PRIMARY KEY, 
	Class_name VARCHAR(20)
);

INSERT INTO animal_classes (Class_name)
VALUES ('pack_animals'),
('pets');  


CREATE TABLE pack_animals
(
	  Id INT AUTO_INCREMENT PRIMARY KEY,
    Genus_name VARCHAR (20),
    Class_id INT,
    FOREIGN KEY (Class_id) REFERENCES animal_classes (Id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO pack_animals (Genus_name, Class_id)
VALUES ('horses', 1),
('donkeys', 1),  
('camels', 1); 
    
CREATE TABLE pets
(
	  Id INT AUTO_INCREMENT PRIMARY KEY,
    Genus_name VARCHAR (20),
    Class_id INT,
    FOREIGN KEY (Class_id) REFERENCES animal_classes (Id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO pets (Genus_name, Class_id)
VALUES ('cats', 2),
('dogs', 2),  
('humsters', 2); 
```

## задание 9:
Заполнить низкоуровневые таблицы именами(животных), командами
которые они выполняют и датами рождения

```sql
CREATE TABLE cats 
(       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Name VARCHAR(20), 
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id int,
    Foreign KEY (Genus_id) REFERENCES home_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
);
INSERT INTO cats (Name, Birthday, Commands, Genus_id)
VALUES ('барсик', '2011-01-01', 'кс-кс-кс', 1),
('алиса', '2016-01-01', "нельзя!", 1),  
('миса', '2015-01-01', "", 1); 

CREATE TABLE dogs 
(       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Name VARCHAR(20), 
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id int,
    Foreign KEY (Genus_id) REFERENCES home_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
);
INSERT INTO dogs (Name, Birthday, Commands, Genus_id)
VALUES ('бим', '2020-01-01', 'сидеть', 2),
('дик', '2022-06-12', "лежать", 2),  
('Шарик', '2018-05-01', "лапу", 2), 
('тузик', '2021-05-10', "голос", 2);

CREATE TABLE hamsters 
(       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Name VARCHAR(20), 
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id int,
    Foreign KEY (Genus_id) REFERENCES home_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
);
INSERT INTO hamsters (Name, Birthday, Commands, Genus_id)
VALUES ('рыжик', '2020-10-12', " ", 3),
('черныш', '2021-03-12', " ", 3),  
('снежинка', '2022-07-11', " ", 3);

CREATE TABLE horses 
(       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Name VARCHAR(20), 
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id int,
    Foreign KEY (Genus_id) REFERENCES packed_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
);
INSERT INTO horses (Name, Birthday, Commands, Genus_id)
VALUES ('буцефал', '2020-01-12', 'бегом', 1),
('закат', '2017-03-12', "бегом, шагом, хоп", 1),  
('буран', '2016-07-12', "бегом, шагом, хоп, брр", 1);

CREATE TABLE donkeys 
(       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Name VARCHAR(20), 
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id int,
    Foreign KEY (Genus_id) REFERENCES packed_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
);
INSERT INTO donkeys (Name, Birthday, Commands, Genus_id)
VALUES ('берти', '2019-04-10', "вперёд", 2),
('маргаритка', '2020-03-12', "назад", 2),  
('перл', '2021-07-12', "стоять", 2);

CREATE TABLE camels 
(       
    Id INT AUTO_INCREMENT PRIMARY KEY, 
    Name VARCHAR(20), 
    Birthday DATE,
    Commands VARCHAR(50),
    Genus_id int,
    Foreign KEY (Genus_id) REFERENCES packed_animals (Id) ON DELETE CASCADE ON UPDATE CASCADE
);
INSERT INTO camels (Name, Birthday, Commands, Genus_id)
VALUES ('тушкан', '2022-04-10', 'вперёд', 3),
('патрон', '2019-03-12', "назад", 3),  
('кичиро', '2015-07-12', "стоять", 3);
```
