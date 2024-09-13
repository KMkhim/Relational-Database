
# Learn Relational Databases by Building a Mario Database

from freecodecamp


#### Connect to a PostgreSQL database

    psql --username=freecodecamp --dbname=postgres

#### List all databases 
   
    \l

<img1>

#### Create databases 

    CREATE DATABASE first_database;

    CREATE DATABASE second_database;

#### Rename database

    ALTER DATABASE second_database RENAME TO mario_database;


#### Connect to a database

    \c second_database

#### Display the tables
     
     \d 
    
#### Create table

    CREATE TABLE first_table();

    CREATE TABLE second_table();

#### Add Column in second_table

    ALTER TABLE second_table ADD COLUMN first_column INT;

    ALTER TABLE second_table ADD COLUMN second_column INT;

    ALTER TABLE second_table ADD COLUMN id INT;

    ALTER TABLE second_table ADD COLUMN age INT;

    ALTER TABLE second_table ADD COLUMN name VARCHAR(30);

#### Rename Column name

    ALTER TABLE second_table RENAME COLUMN name TO username;

#### Add data 
    
    INSERT INTO second_table(id, username) 
    VALUES(1, 'Samus');

#### View the data in a table
    
    SELECT * FROM second_table;

#### Remove Column in second_table

    ALTER TABLE second_table DROP COLUMN first_column;
    
#### Remove roll
    
    DELETE FROM second_table WHERE username = 'Samus';

#### Remove Table

    DROP TABLE second_table;

### Serial type

The SERIAL type will make your column an INT with a NOT NULL constraint, and automatically increment the integer when a new row is added. View the details of the characters table to see what SERIAL did for you.

### Create characters table

<img>

#### Update roll

    UPDATE characters SET favorite_color = 'Orange' WHERE name = 'Daisy';

#### ORDER BY

    SELECT * FROM characters ORDER BY character_id ;

<img>

#### Primary Key
You should set a primary key on every table and there can only be one per table. 

    ALTER TABLE characters  ADD PRIMARY KEY(name);

<img>

#### DROP Primary Key

    ALTER TABLE characters DROP CONSTRAINT characters_pkey;

#### CREATE more_info table

    CREATE TABLE more_info();
####   
    ALTER TABLE more_info ADD COLUMN more_info_id SERIAL;
    ALTER TABLE more_info ADD PRIMARY KEY(more_info_id);
    ALTER TABLE more_info ADD COLUMN birthday DATE;
    ALTER TABLE more_info ADD COLUMN height INT;
    ALTER TABLE more_info ADD COLUMN weight NUMERIC(4,1);

#### Foreign Key

    ALTER TABLE more_info ADD COLUMN character_id INT REFERENCES characters(character_id);
    <img>

#### UNIQUE

There's your foreign key at the bottom. These tables have a "one-to-one" relationship. One row in the characters table will be related to exactly one row in more_info and vice versa. Enforce that by adding the UNIQUE constraint to your foreign key. Here's an example:

    ALTER TABLE more_info ADD UNIQUE(character_id);

#### ADD NOT NULL
    ALTER TABLE more_info  ALTER COLUMN character_id  SET NOT NULL;

#### more_info table
<img>

#### create sounds table

    CREATE TABLE sounds(sound_id SERIAL PRIMARY KEY);
####
    ALTER TABLE sounds ADD COLUMN filename VARCHAR(40) NOT NULL UNIQUE;
####
    ALTER TABLE sounds ADD COLUMN character_id INT NOT NULL REFERENCES characters(character_id);
####
    INSERT INTO sounds(filename ,character_id) VALUES('its-a-me.wav',3);
    INSERT INTO sounds(filename ,character_id) VALUES('yippee.wav',3);
    INSERT INTO sounds(filename ,character_id) VALUES('ha-ha.wav',4);
    INSERT INTO sounds(filename ,character_id) VALUES('oh-yeah.wav',4);
    INSERT INTO sounds(filename ,character_id) VALUES('yay.wav',5),('woo-hoo.wav',5);
    INSERT INTO sounds(filename ,character_id) VALUES('mm-hmm.wav',5),('yahoo.wav',3);
   
    <img>

#### create actions table
    CREATE TABLE actions(action_id SERIAL PRIMARY KEY);
####
    ALTER TABLE actions ADD COLUMN action VARCHAR(20) UNIQUE NOT NULL;
####
    INSERT INTO actions(action) VALUES ('run');
    INSERT INTO actions(action) VALUES ('jump');
    INSERT INTO actions(action) VALUES ('duck');
    <img>

#### create character_actions table

    CREATE TABLE character_actions();
####
    ALTER TABLE character_actions ADD COLUMN character_id INT NOT NULL;
    ALTER TABLE character_actions ADD FOREIGN KEY(character_id) REFERENCES characters(character_id);
    
####    
    ALTER TABLE character_actions ADD COLUMN action_id INT NOT NULL;
    ALTER TABLE character_actions ADD FOREIGN KEY(action_id) REFERENCES actions(action_id);
####
    ALTER TABLE character_actions ADD PRIMARY KEY (character_id , action_id);

    ALTER TABLE character_actions ADD UNIQUE(character_id,action_id);
####
    <img>
####
    INSERT INTO character_actions (character_id,action_id) VALUES(9,1),(9,2),(9,3);
    INSERT INTO character_actions (character_id,action_id) VALUES(8,1),(8,2),(8,3);
    INSERT INTO character_actions (character_id,action_id) VALUES(7,1),(7,2),(7,3);
    INSERT INTO character_actions (character_id,action_id) VALUES(6,1),(6,2),(6,3);
    INSERT INTO character_actions (character_id,action_id) VALUES(5,1),(5,2),(5,3);
    INSERT INTO character_actions (character_id,action_id) VALUES(4,1),(4,2),(4,3);
    INSERT INTO character_actions (character_id,action_id) VALUES(3,1),(3,2),(3,3);

<img>
####

    SELECT * FROM characters FULL JOIN more_info ON characters.character_id = more_info.character_id;

     <img>
####
   
    SELECT * FROM characters FULL JOIN sounds ON characters.character_id = sounds.character_id;
####

    SELECT * FROM character_actions FULL JOIN characters ON character_actions.character_id = characters.character_id FULL JOIN actions ON character_actions.action_id = actions.action_id;
    <img>
