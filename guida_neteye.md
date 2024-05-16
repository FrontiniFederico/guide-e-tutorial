# procedrua di aggiornamento 433

diego da team viewer a federico franco con cui accede via web e ssh ai nodi fisici e satelliti facendo ponte gli abbiamo ccreato un utenza nel dominio
intanto diego si collega al vcenter cosi e gia pronto. non ci fa registrare.

lo vedo colelgato al 10 160 120 120 (informati)

consulente da un occhio a hostname
/etc/hosts
diego chiede se nel ldap non ci sia il gruppo wurth -> doveva togliere ou service da ??? e sei atterratto sul vmd non so perche dice diego
pinga nem00 e verifica che risponde
sistemato il certificato 
controlla se ci sono degli allarmi
cerca in icinga "netey" e vede se ci stanno rogne
warning su elastic ok perche l'installazione non e completa e ci sono da sempre
e invece no sorpresa vmd-vm-state-vcsa e ...-state-cpu
poi ci stanno anche elastic in handled
dall'hostgroup vedi unknown di una zona in dismissione e vabbe e abbiamo un critical di un mysql noto che comunque non da problemi per oggi 
si va a prendere gli hostgroups a nome neteye e li controlla uno a uno verifica non ci siano cose strane
va in cli nem01
si tiene aperti anche nem02 e nem03
diego avverte che sono controllati i pacchetti, sono updatati, fatto neteye health deep, backup di ieri cera va controllato oggi
mancano da fare gli snapshot a freddo 
si posiziona nella home di tutti e tre i nodi
ls -altr nel nodo 3 
consulta la guida
controlla lo stato del cluster pcs status
vediamo errori logstash
il fencing e noto 
systemctl status logstash per vedere servizio 
guarda i log in ????
sono per fortuna solo dei warning 
e in nem01 e i log sono in log
logstasj al 5 del mattino
pcs resource cleanup e dovrebbe sparire tutto
ora per fare la configurazione backup si lascia un unico nodo e gli altri due nodui in standby e si lancia lo script ??? 
adesso mettiamo in standby i nodi e lasciamo nem01
entra in cd updates e fa un ls -altr
pcs node stanby su nem02 e nem03
ricordiamoci di mettere gli oggetti in downtime su icinga
faremo il backup e li spegniamo per fare gli snapshot
federico dice che non fanno di solito lo snapshot
vuole vedere come va
standby nem03 e va a vedere su nem01 con pcs status se ha roba sul nodo 3 e vede che sono online solo 1 e 2
apre drdbmon una ui mai vista cosera col comando drdbmon
pcs status nodes sul nem02
diego ricorda che il nodo due aveva maria db e il nodo tre influx 
in nem02 fa pcs status | grep node2
ha aspettato per vedere tutto migrato sul nodo 1
sh backup_neteye scriptino sul nodo 2 e sul nodo 3 backup classico non copia i dati ?? salva localmente 
siamo dentro updates e fare sta roba spawna un nuovo backup lo vedi con ls -altr
quello che facciamo noi backuppa il filesystem, questo invece solo le config
lo fa uno alla volta
TODO: se devo ripristinare da questo backup come si fa?
controlla la release 
chiede da quale nodo facciamo ?
updatedb
locate ??
lancia qualcosa ??

configurazione terminata, possiamo procedere allo spegnimento dei nodi
forse lo faremo solo per le versioni che aggiornano os
spegnamo anche il nodo 1
mettiamo in standby anche nem01
poi shutdown now su tutti e tre i nodi
disservizio messi in conto
fencing spento? chiede diego? no
ha senso spegnerlo?
franco dice che dovrebbe essere sempre attivo
disattivare lo stoneit ??? diego legge procedura ??? da dove
spegnere stonit: pcs property set stonith-enabled=false FIXME: comando errato
pcs status e vedi se spento
cerca nello storico comando stonith ma no ntrova
pcs stonith tabbi e vedi che comandi abbiamo
pcs stonith status 
non troviamo il comando per spegnere stonith
franco prova un vecchio comando: pcs property show stonith-enabled FIXME: questo per spegnerlo credo di no???
franco aveva altri comandi li vedi in chat 950
standby nem01: pcs node standby
drdbmon vedi primary che si spengono man mano
il shutdown impiega molto a spegnere tutti i servizi, prendiamo nota che durano qualche minuto 
pcs status nodes vedi lo stato del cluster e controlli che sia tutto in standby 
ora tutto in standby
da vsphere fai shutdown -h???
TODO: capire come fai shutdown 
ora spegnamo anche nodo 2 e poi 1
lui penso spenga da console con shutdown -h e diego controlla da vsphere cliente la roba wdmz zucchetti se risulta spenta in console
problema che non ho capito ??? #TODO: riguarda la registrazione o chiedi agli altri
non riusciamo ad accendere le macchine da vsphere client
non l'ha accesa da vsphere client ma da vmware????
paride chiede se supporteranno come virtualizzatore proxmox
franco non lo sa
riavviati fa un pcs node unstandby --all wait=300
un altro pcs status
ora bisogna riavviare il fencing
drdb tornato in piedi
abbiamo servizi in overdue? 
TODO: non ho capito cosa e stato visto di brutto in questo pcs status
ora inziamo
lancia il comando che termina per nohup prendilo dalla guida
i check fatti col vmd vanno in errore che vanno a leggere il db del vmd vanno in critical quando non raggiungono il vsphere db
vedi ticket T278095C villa maria e stato notificato
rant su open sourcing e script di rocco TODO: se importante riguarda chiedi a paride se va inserito in documentazione 
se si blocca rifai da capo
TODO: diego dice di avere fatto un check, di che tipo?
problema con elastic alle 12.34 

controlli su elastic e poi lancia comando di upgrade e verifica se agenti di elastic sono su per evitare che si blocchi

errore nel fare l' ulgrade 
failed to install some of the specified packages
... icingaweb2 no package available
fa un pcs status
fa un curl a http localhost 2347/v1/cluster/release | jq ??
FIXME: mi sono perso per rispondere a paride in chat
vedo che e nel nodo tre e ha fato un ls -latr in /etc/yum.repos.d
e stesso path/mirrors/
sta sentendo il supporto di wurth per capire che fare
guarda /etc/dnf/dnf.conf
lo corregge con editor per renderlo uguale agli altri nel nem03
fa ripartire
fallisce l'health check
failed to connect to grafana
i servizi sono caduti a causa di ???
pcs non riusciva a farle ripartire in blocco perche ce un load importante
quindi le ha fatte ripartire una alla volta
ci dice il supporto che le risorse sono insuff
effettivamente e il primo aggiornamento del cluster da quandfo abbiamo aggiunto elastic
tmp molto alta.