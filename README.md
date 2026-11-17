Database setup:
- Docker Desktop with WSL2 integration enabled
- Docker Compose
- psql client

Starting the DB:
- copy .env.example into fresh .env and set POSTGRES_PASSWORD
- validate with 'docker compose config --quiet'
- start with 'docker compose up -d --wait' if config check passes
- run psql -h '127.0.0.1' -p '5433' -U 'geointel' -d 'geointel' -W
- if successful run ```SELECT current_database(), current_user, PostGIS_Version();```
  - Should return 'geo intel for user column | geointel for db column | PostGIS 3.7'
  
Checking persistence (Optional)
- run ```CREATE TABLE compose_persistence_check (id integer PRIMARY KEY);```
- run ```INSERT INTO compose_persistence_check (id) VALUES (1);```
-  run '\q' to exit
-  run 'docker compose down' to keep named volumes
-  run 'docker compose up -d --wait'
-  open psql
-  run ```SELECT id FROM compose_persistence_check```
   -  should return previously inserted id'
   - if successful run 'DROP TABLE compose_persistence_check;' to drop the table

Git Ignore repository check.
- run 'git check-ignore -v .env'
  - .env should be returned as a rule in .gitignore
- keep .env.example ommitted from .gitignore
