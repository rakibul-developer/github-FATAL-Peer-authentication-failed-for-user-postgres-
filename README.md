# Problem 
  psql: error: connection to server on socket "/var/run/postgresql/.s.PGSQL.5432" failed: FATAL:  Peer authentication failed for user "postgres"

# Solution 01
  1. psql -U postgres -W
  2. sudo -u postgres psql
  3. ALTER USER postgres PASSWORD 'yourpassword';
  4. \q
  5. psql -U postgres -W

# Solution 2
  1. sudo -u postgres psql

# Solution 3***
  1. sudo nano /etc/postgresql/*/main/pg_hba.conf  # Ubuntu/Debian
     sudo nano /opt/homebrew/var/postgresql@14/pg_hba.conf  # macOS (Homebrew PostgreSQL 14)
  2. Find this line:
       local   all   postgres   peer
  3. Replace to:
       local   all   postgres   md5
  4. Save and exit (CTRL + X, then Y, then Enter).
  5. sudo systemctl restart postgresql  # Linux
     brew services restart postgresql    # macOS (Homebrew)
  6. psql -U postgres -W


