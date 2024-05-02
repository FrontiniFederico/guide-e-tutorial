## head e tail

Ti fanno vedere le prime o le ultime n righe in un file.
- `head /path/to/file` per vedere le prime dieci righe di un file
- `tail /path/to/file` per vedere le ultime dieci righe di un file

Posso aggiungere l'opzione `-n #numero` per decidere quante linee vogliamo visualizzare. Sono specialmente utili in piping con altri. Ad esempio:
- `cat /var/log/syslog | grep ssh | head` mi fa vedere le prime dieci righe di syslog che includono ssh 

Specificatamente per *tail*, posso usare `tail -f /var/log/syslog` per monitorare in tempo reale cambiamenti nel file indicato nel comando.