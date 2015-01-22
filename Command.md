 

# PostFix #


CentOS pulito , install postfix e dipendenze, manda mail a user e verso fuori.
Ubuntu e Debian , install postfix, configurazione di grafica, manda mail user e verso fuori.


Mail server locale due alternative :

1. settare le cartelle locali relative agli utenti su /var/spool/virtual
2. server mail + sql http://www.temporini.net/virtual-users-and-domains-with-postfix-courier-mysql-and-ubuntu-804-lts-64bit

----------------------------------------------------------------------------


# CronTab #

http://guide.debianizzati.org/index.php/Utilizzo_del_servizio_di_scheduling_Cron

per ogni utente ho un crontab file di testo  in cui sono specificati i comandi da lanciare e i relativi intervalli di tempo.

	-crontab -e (scrivo i comandi per lanciare i relativi intervalli)
	-crontab -l (elenco dei job)


	esempio 00 22 * * * > /etc/utenti/scrivania/pippo2



 All'avvio Cron legge il file 
 	- /etc/crontab       per le voci (le cosiddette "entry") di sistema,
 	 
 	 i file contenuti nella directory 
 	
 	- /etc/cron.d/ e i file in 
 	
 	- /var/spool/cron/crontabs per le voci relative agli utenti che si trovano nel file /etc/passwd. 
Tutti i job di ciascuna voce (crontab) sono caricati nella memoria del demone Cron.

.---------------- [m]inute: minuto (0 - 59) 

|  .------------- [h]our: ora (0 - 23)

|  |  .---------- [d]ay [o]f [m]onth: giorno del mese (1 - 31)

|  |  |  .------- [mon]th: mese (1 - 12) OPPURE jan,feb,mar,apr... 

|  |  |  |  .---- [d]ay [o]f [w]eek: giorno della settimana (0 - 6) 
			(domenica=0 or 7)  OPPURE sun,mon,tue,wed,thu,fri,sat 

|  |  |  |  |

*  *  *  *  *  comando da eseguire

#####Campi | Valori ammessi
----------------
minuti | 0-59

ore | 0-23

giorno | 1-31

mese | 1-12

giorno della settimana | 0-7 (0 & 7 indicano la domenica)


   stringa        significato
   ------         -------
   @reboot        Lancia il comando all'avvio del sistema
   @yearly        Lancia il comando una volta all'anno. Uguale a "0 0 1 1 *"
   @annually      (come @yearly)
   @monthly       Lancia il comando una volta al mese. Uguale a "0 0 1 * *"
   @weekly        Lancia il comando una volta alla settimana. Uguale a "0 0 * * 0"
   @daily         Lancia il comando una volta al giorno. Uguale a "0 0 * * *"
   @midnight      (come @daily)
   @hourly        Lancia il comando una volta all'ora. Uguale a "0 * * * *"


-------------------------------------------------------------------------------------------------------------


# Redirezione #



comando [argomenti] >filename 2>filename.log  il primo redirezione l'output il secondo redireziona gli errori

OUTPUT_COMANDO >
      # Redirige lo stdout in un file.
      # Crea il file se non è presente, in caso contrario lo sovrascrive.
								  
      ls -lR > dir-albero.list
      # Crea un file contente l'elenco dell'albero delle directory.
								  
  - : > nomefile
      # Il > svuota il file "nomefile", lo riduce a dimensione zero.
      # Se il file non è presente, ne crea uno vuoto (come con 		'touch').
      # I : servono da segnaposto e non producono alcun output.
								  
  - : > nomefile
      #  Il > svuota il file "nomefile", lo riduce a dimensione zero.
      #  Se il file non è presente, ne crea uno vuoto (come con 'touch').
      #  (Stesso risultato di ": >", visto prima, ma questo, con alcune 
      #+ shell, non funziona.)
								  
   - : >>
      # Redirige lo stdout in un file.
      # Crea il file se non è presente, in caso contrario accoda l'output.
								  
								  
       Comandi di redirezione di riga singola
       (hanno effetto solo sulla riga in cui si trovano):

-------------------------------------------------------------------------------------------------------------



# SCP	 


Il programma SCP è un'applicazione client che implementa il protocollo SCP; è quindi un programma per eseguire copie sicure.
Il client SCP più ampiamente usato è il programma a riga di comando scp, che è fornito nella maggior parte delle implementazioni di SSH. Il programma scp è l'analogo "sicuro" del comando rcp. Il programma scp deve essere parte di tutti i server SSH che vogliono fornire il servizio SCP, tanto le funzioni scp quant'anche il server SCP.
Alcune implementazioni di SSH forniscono il programma scp2, che usa il protocollo SFTP invece di SCP, ma fornisce la stessa identica interfaccia a riga di comando di scp. scp è quindi tipicamente un link simbolico a scp2.
Tipicamente, la sintassi del programma scp è come la sintassi di cp:
scp FileSorgente nomeUtente@host:directory/FileDestinazione
scp nomeUtente@host:directory/FileSorgente FileDestinazione


  - -l seguita dal numeri di Kbit da utilizzare, notare che parlo di Kbit non di Kbyte quindi se impongo "-l 240" intendo limitare la banda a 240 Kbit che 		corrispondono a 240/8=30KByte.

 - -r con il quale si permette la ricerca ricorsiva anche nelle subdirectory, molto utile se si cerca di copiare una cartella che ne contiene a sua volta 		delle altre, e l'opzione "

 - -C che abilita la compressione dei dati trasmessi.
 
 - -p preserve the timestamps of the files and directories and if possible, the users, groups and permissions. 


Copy multiple files from the remote host to your current directory on the local host
$ scp your_username@remotehost.edu:/some/remote/directory/\{a,b,c\} 


esempio di script di trasferimento scp

 #!/usr/bin/expect -f

'#' connect via scp
spawn scp "user@example.com:/home/santhosh/file.dmp" /u01/dumps/file.dmp
#######################
expect {
  -re ".*es.*o.*" {
    exp_send "yes\r"
    exp_continue
  }
  -re ".*sword.*" {
    exp_send "PASSWORD\r"
  }
}
interact

------------------------------------



#  SSH 


http://support.suso.com/supki/SSH_Tutorial_for_Linux


###Comandi Base

####- ssh user@ip



######Port forwarding
La sicurezza della comunicazione tramite SSH è assicurata grazie alla realizzazione di tunnel criptati che, trasportando sessioni TCP arbitrarie all'interno della connessione criptata, permettono di proteggere da intercettazione protocolli non sicuri, o di aggirare limitazioni di routing.
Questa funzionalità è detta port forwarding, e permette di aprire un socket TCP sul client SSH (local port forwarding) o sul server (remote port forwarding). Le connessioni ricevute su questa porta vengono inoltrate dall'altro capo della connessione SSH, verso un host e una porta specificata.
Ad esempio, con questo comando ci si collega ad host1, inoltrando la porta 10022 della macchina in cui lanciamo il client ssh alla porta 22 di host2 attraverso un canale sicuro tra client e host1:
ssh host1 -L 10022:host2:22
Mentre questa connessione è attiva, collegandosi alla porta 10022 del client si viene rediretti verso la porta 22 di host2.
X forwarding[modifica | modifica wikitesto]
Il port forwarding è utile anche per trasportare applicazioni X Window attraverso una connessione SSH. SSH imposta anche automaticamente le opportune variabili d'ambiente, in modo che le applicazioni X lanciate da un terminale remoto vengano visualizzate sul display da cui è stata avviata la connessione.

###### L'X forwarding
 dal lato client deve essere abilitato passando l'opzione "-X" mentre dal lato server va modificato il file di configurazione /etc/ssh/sshd_config abilitando la direttiva X11Forwarding (ricordatevi di riavviare il server una volta apportata la modifica al file di 
configurazione).

##### Generating a key
ssh-keygen -t dsa


####Port forwarding
- ssh -L 3306:mysql.suso.org:3306 username@arvo.suso.org

#### Running Commands Over SSH
- ssh username@remotehost.net ls -l /



####Keeping Your SSH Session Alive

```
Host *
Protocol 2
TCPKeepAlive yes
ServerAliveInterval 60
```
in the file



- #### ~/.ssh/config

---

#TAR

http://www.computerhope.com/unix/utar.htm

- -A, --catenate, --concatenate	Append tar files to an archive.

- -c, --create	Create a new archive.

- -d, --diff, --compare	Calculate any differences between the archive 
and the file system.

--delete	Delete from the archive. (This function doesn't work on magnetic tapes).

- -r, --append	Append files to the end of a tar archive.

- -t, --list	List the contents of an archive.
--test-label	Test the archive label, and exit.

- -u, --update	Append files, but only those that are newer than the copy 
in the archive.

- -x, --extract, --get	Extract files from an archive.


---

#CPIO

Lo stesso di tar 

####USO

- find * | cpio ov > archio.cpio
- cpio -ov > directory.cpio
- cpio -iv < directory.cpio

prende file da std input e lo archivia su std output

####Comandi

- -0, --null	Read a list of filenames terminated by a null character, instead of a newline, so that files whose names contain newlines can be archived. GNU find is one way to produce a list of null-terminated filenames. This option may be used in copy-out and copy-pass modes.

- -a, --reset-access-time	Reset the access times of files after reading them, so that it does not look like they have just been read.

- -A, --append	Append to an existing archive. Only works in copy-out mode. The archive must be a disk file specified with the -O or -F (-file) option.

- -b, --swap	Swap both halfwords of words and bytes of halfwords in the data. Equivalent to -sS. This option may be used in copy-in mode. Use this option to convert 32-bit integers between big-endian and little-endian machines.
- -B	Set the I/O block size to 5120 bytes. Initially the block size is 512 bytes.
--block-size=BLOCK-SIZE	Set the I/O block size to BLOCK-SIZE * 512 bytes.

- -c	Identical to '-H newc'; uses the new (SVR4) portable format. If you want the old portable (ASCII) archive format, use '-H odc' instead.

- -C IO-SIZE, --io-size=IO-SIZE	Set the I/O block size to IO-SIZE bytes.

- -d, --make-directories	Create leading directories where needed.

- -E FILE, --pattern-file=FILE	Read additional patterns specifying filenames to extract or list from FILE. The lines of FILE are treated as if they had been non-option arguments to cpio. This option is used in copy-in mode.

- -f, --nonmatching	Only copy files that do not match any of the given patterns.

- -F, --file=archive	Archive filename to use instead of standard input or output. To use a tape drive on another machine as the archive, use a filename that starts with 'HOSTNAME:'. The hostname can be preceded by a username and an '@' to access the remote tape drive as that user, if you have permission to do so (typically an entry in that user's '~/.rhosts' file).


- --force-local	With -F, -I, or -O, take the archive file name to be a local file even if it contains a colon, which would ordinarily indicate a remote host name.

- -H FORMAT, --format=FORMAT	Use archive format FORMAT. The valid formats are listed below; the same names are also recognized in all-caps. The default in copy-in mode is to automatically detect the archive format, and in copy-out mode is 'bin'.

		bin: The obsolete binary format.

		odc: The old (POSIX .1) portable format.

		newc: The new (SVR4) portable format, which supports file systems having more than 65536 inodes.

		crc: The new (SVR4) portable format with a checksum added.

		tar: The old tar format.

		ustar: The POSIX .1 tar format. Also recognizes GNU tar archives, which are similar but not identical.

		hpbin: The obsolete binary format used by HPUX's cpio (which stores device files differently).

		hpodc: The portable format used by HPUX's cpio (which stores device files differently).

- -i, --extract	Run in copy-in mode. (see 'Copy-in mode').

- -I archive	Archive filename to use instead of standard input. To use a tape drive on another machine as the archive, use a filename that starts with 'HOSTNAME:'. The hostname can be preceded by a username and an '@' to access the remote tape drive as that user, if you have permission to do so (typically an entry in that user's '~/.rhosts' file).

- -k	Ignored; for compatibility with other versions of cpio.

- -l, --link	Link files instead of copying them, when possible.

- -L, --dereference	Copy the file that a symbolic link points to, rather than the symbolic link itself.

- -m, --preserve-modification-time	Retain previous file modification times when creating files.

- -M MESSAGE, --message=MESSAGE	Print MESSAGE when the end of a volume of the backup media (such as a tape or a floppy disk) is reached, to prompt the user to insert a new volume. If MESSAGE contains the string '%d', it is replaced by the current volume number (starting at 1).

- -n, --numeric-uid-gid	Show numeric UID and GID instead of translating them into names when using the '--verbose' option.

- --no-absolute-filenames	Create all files relative to the current directory in copy-in mode, even if they have an absolute file name in the archive.

- --absolute-filenames	This is the default: tell cpio not to strip leading file name components that contain '..' and leading slashes from file names in copy-in mode.

- --no-preserve-owner	Do not change the ownership of the files; leave them owned by the user extracting them. This is the default for non-root users, so that users on System V don't inadvertently give away files. This option can be used in copy-in mode and copy-pass mode.

- -o, --create	Run in copy-out mode. (see 'Copy-out mode').

- -O archive	Archive filename to use instead of standard output. To use a tape drive on another machine as the archive, use a filename that starts with 'HOSTNAME:'. The hostname can be preceded by a username and an '@' to access the remote tape drive as that user, if you have permission to do so (typically an entry in that user's '~/.rhosts' file).

- --only-verify-crc	Verify the CRC of each file in the archive, when reading a CRC format archive. Do not actually extract the files.

- -p, --pass-through	Run in copy-pass mode. (see 'Copy-pass mode').

- --quiet	Do not print the number of blocks copied.

- -r, --rename	Interactively rename files.

- -R [user][:.][group], --owner [user][:.][group]	Set the ownership of all files created to the specified user and/or group in copy-out and copy-pass modes. Either the user, the group, or both, must be present. If the group is omitted but the ':' or '.' separator is given, use the given user's login group. Only the super-user can change files' ownership.

- --rsh-command=COMMAND	Notifies cpio that is should use COMMAND to communicate with remote devices.

- -s, --swap-bytes	Swap the bytes of each halfword (pair of bytes) in the files. This option can be used in copy-in mode.

- -S, --swap-halfwords	Swap the halfwords of each word (4 bytes) in the files. This option may be used in copy-in mode.

- --sparse	Write files with large blocks of zeros as sparse files. This option is used in copy-in and copy-pass modes.

- -t, --list	Print a table of contents of the input.

- --to-stdout	Extract files to standard output. This option may be used in copy-in mode.

- -u, --unconditional	Replace all files, without asking whether to replace existing newer files with older files.

- -v, --verbose	List the files processed, or with '-t', give an 'ls -l' style table of contents listing. In a verbose table of contents of a ustar archive, user and group names in the archive that do not exist on the local system are replaced by the names that correspond locally to the numeric UID and GID stored in the archive.

- -V, --dot	Print a '.' for each file processed.

- --version	Print the cpio program version number and exit.

 ---
 
# VIM
 
 http://www.palladius.it/joomla/index.php?option=com_content&view=article&id=101:mini-tutorial-di-vi-linux&catid=23:linux&Itemid=38










