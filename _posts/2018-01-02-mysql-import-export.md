---
title: Mysql backup
categories:
  - Server
tags:
  - mysql
---

### How to export mysql file and express as a gip?

Create a sh file and copy below paste into it. And change ${BACKUP_PARENT_DIR}

directory where you save file and your mysql user and password.


```
#!/bin/bash
#==============================================================================
#TITLE:            mysql_backup.sh
#DESCRIPTION:      script for automating the daily mysql backups on development computer
#AUTHOR:           tleish
#DATE:             2013-12-20
#VERSION:          0.4
#USAGE:            ./mysql_backup.sh
#CRON:
  # example cron for daily db backup @ 9:15 am
  # min  hr mday month wday command
  # 15   9  *    *     *    /Users/[your user name]/scripts/mysql_backup.sh

#RESTORE FROM BACKUP
  #$ gunzip < [backupfile.sql.gz] | mysql -u [uname] -p[pass] [dbname]

#==============================================================================
# CUSTOM SETTINGS
#==============================================================================
BACKUP_DATE=`date +%Y_%m_%d`

# Parent backup directory
BACKUP_PARENT_DIR="/home/jack/SpringStudy/db_backup"

# directory to put the backup files
BACKUP_DIR="${BACKUP_PARENT_DIR}/${BACKUP_DATE}"
``
# MYSQL Parameters
MYSQL_UNAME="root"
MYSQL_PWORD="123456"

# Don't backup databases with these names 
# Example: starts with mysql (^mysql) or ends with _schema (_schema$)
IGNORE_DB="(^my|_schema$)"

# include mysql and mysqldump binaries for cron bash user
PATH=$PATH:/usr/local/mysql/bin

# Number of days to keep backups
KEEP_BACKUPS_FOR=30 #days

#==============================================================================
# METHODS
#==============================================================================

# YYYY-MM-DD
TIMESTAMP=$(date +%F)


function mysql_login() {
  local mysql_login="-u $MYSQL_UNAME" 
  if [ -n "$MYSQL_PWORD" ]; then
    local mysql_login+=" -p$MYSQL_PWORD" 
  fi
  echo $mysql_login
}

function database_list() {
  local show_databases_sql="SHOW DATABASES WHERE \`Database\` NOT REGEXP '$IGNORE_DB'"
  echo $(mysql $(mysql_login) -e "$show_databases_sql"|awk -F " " '{if (NR!=1) print $1}')
}

function echo_status(){
  printf '\r'; 
  printf ' %0.s' {0..100} 
  printf '\r'; 
  printf "$1"'\r'
}

function create_dir() {
  echo "Backup directory: ${BACKUP_DIR}"
  mkdir -p "${BACKUP_DIR}"
  chmod 700 "${BACKUP_DIR}"
}
function backup_database(){
    backup_file="$BACKUP_DIR/$TIMESTAMP.$database.sql.gz" 
    output+="$database => $backup_file\n"
    echo_status "...backing up $count of $total databases: $database"
    $(mysqldump $(mysql_login) $database | gzip -9 > $backup_file)
}

function backup_databases(){
  local databases=$(database_list)
  local total=$(echo $databases | wc -w | xargs)
  local output=""
  local count=1
  create_dir
  for database in $databases; do
    backup_database
    local count=$((count+1))
  done
  echo -ne $output | column -t
}

function hr(){
  printf '=%.0s' {1..100}
  printf "\n"
}

#==============================================================================
# RUN SCRIPT
#==============================================================================

hr
backup_databases
hr
printf "All backed up!\n\n"
```

Then run this

```
chmod u+x backitup.sh
```

Ok,we just need one more step to make it.

```
./backitup.sh

```
Done!!!

### How to import gz file into mysql?

gzip -dc < `date -I`.{database}.sql.gz | mysql -u {user} -p {database}