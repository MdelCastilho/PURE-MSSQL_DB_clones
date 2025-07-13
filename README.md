# PURE-MSSQL_DB_clones
MSSQL databases klonen naar OTA

Dit project heeft als doel de clone-functionaliteiten van PURE storage te gebruiken in een (HiX-6.3) SQL-infrastructuur. 

De HiX prduktie-omgeving waarop deze scriptset is bestaat uit:
HiX prpduktie-cluster
- AlwayOn MSSQL 2022
- Drie instances
- Instances 1 en 2 zijn RW, Instance 3 is RO.
- Instance 3 is ontsloten voor onder andere rapportage doeleinden en overige query-toegang
- Logship 1 - 3 volumes - ten behoeve van DisasterRecovery - delay transactions 5 mins
- Logship 2 - 3 volumes - ten behoeve van DataCorruptionRecovery - delay 24 hrs
- Logship 3 - 1 volume - ten behoeve van clones op 1 volume

De HiX-Acceptatie databases draait in een SQL AvailabilityGroup. De .mdf, .ldf, en MM zijn conform productie verdeeld over drie volumes. 
Bij de overige omgevingen staan de .mdf en .ldf op een enkele volume in plaats van twee, en is er een shared MM database.

SQL-datbase clones worden derhalve gemaakt van:
- Logship 1 

Voor het opleveren van geanomimiseerde clones wordt gebruik gemaakt van NMTY tooling.
Licentie-technisch is gekozen voor een enkele geanonimiseerde kopie, die vervolgens wordt gekloond naar overige omgevingen.
Technisch gezien betekent dit dat er 1 kloon wordt gemaakt van de PROD-database. Deze bron-database wordt geanonimiseerd en aansluitend gekloond naar meerdere kopie-databases.

