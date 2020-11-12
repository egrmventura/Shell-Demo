# Shell-Demo

#!/bin/sh
sudo -i -u postgres
sudo launch load -w /Library/PostgreSQL/12/bin/psql
psql -h $HOSTNAME -U $USERNAME $DATABASE << EOF

while [DATABASE.runQuery(“SELECt COUNT(provider_id) FROM doctors WHERE provider LIKE ‘%John%’”) != 0]
do 
	item_remove(doctors, DATABASE.runQuery(“SELECt COUNT(provider_id) FROM doctors WHERE provider LIKE ‘%John%’ LIMIT 1”))
done
EOF
