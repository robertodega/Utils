
postgres:
	cambiare owner da fastfm a fastfmdbuser

		postgres=# ALTER DATABASE fastfm OWNER TO fastfmdbuser;

assegnare ruolo per fastfmdbuser a utente roby

		postgres=# GRANT CONNECT ON DATABASE fastfm TO roby;
		postgres=# GRANT ALL PRIVILEGES ON DATABASE fastfm TO roby;

da terminale ubuntu
	ip address												#	indirizzo ip macchina remota ( 172.19.235.173 )
	
	inserire alias per ip address in C:\Windows\System32\drivers\etc\hosts
	
	es.
	172.19.235.173 ubuntuv
	
	
da cmd win

	ssh roby@ubuntuv										#	collegamento a macchina remota virtuale ubuntu ( ssh 172.19.235.173 )
	ctrl d	( o exit o x )									#	uscita da collegamento a macchina remota virtuale ubuntu
	sudo systemctl status postgresql						#	postgresql status
	sudo systemctl restart postgresql						#	postgresql service restart
	
	sudo nano /etc/postgresql/14/main/postgresql.conf		#	postgresql conf file
	sudo nano /etc/postgresql/14/main/pg_hba.conf			# 	host-based authentication file
	sudo nano /etc/postgresql/14/main/pg_ident.conf    		#	ident configuration file

	sudo -i -u postgres										#	collegamento a postgres@roby-Virtual-Machine
	psql													#	postgres terminal connection
	\l														#	list of db
	\du														#	list of roles
	create user roby with encrypted password 'roby_Fast';	#	user create
	

Parametri DBeaver:

	-	Connected by: 	Host
	-	Host:			ip address macchina remota
	-	Port:			5432
	-	Database:		fastfm
	-	Username:		roby		( o Owner from "sudo -i -u postgres" | "psql" | "\l" )
	-	Password:		roby_Fast

