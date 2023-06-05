## wal_level
 - determines how much information is written to the WAL
	 - replica
		 - which writes enough data to support WAL archiving and replication, including running read-only queries on a standby server
	 - minimal
		 - emoves all logging except the information required to recover from a crash or immediate shutdown.
	 - logical 
		 - adds information necessary to support logical decoding