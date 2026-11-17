Database setup:
- Docker Desktop with WSL2 integration enabled
- Docker Compose
- psql client

Starting the DB:
- copy .env.example into fresh .env and set POSTGRES_PASSWORD
- validate with 'docker compose config --quiet'
- start with 'docker compose up -d --wait' if config check passes
- run psql -h '127.0.0.1' -p '5433' -U 'geointel' -d 'geointel' -W
- if successful run 'geointel=# SELECT current_database(), current_user, PostGIS_Version();'
  - Should return non blank values
  
Checking persistence
- run in PSQL 'INSERT INTO compose_persistence_check (id) VALUES(1);'
-  run '\q' to exit
-  run 'docker compose down'
-  run 'docker compose up -d --wait'
-  open psql
-  run "SELECT id FROM compose_persistence_check'
   -  should return previously inserted id'
   - if successful run 'DROP TABLE compose_persistence_check;' to drop the table

Create a .gitignore
- add .env to .gitignore
- run 'git check-ignore -v .env'
  - .evn should be returned as a rule in .gitignore
