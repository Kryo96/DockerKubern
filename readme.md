### Docker 

#### Containers vs Virtual machines 

##### Perchè usare i containers? 
I container incapsulano tutte le dipendenze e configurazioni necessarie per far girare più applicazioni sulla stessa macchina. Da fuori, sembrano tutte uguali e che girino nella stessa maniera, questo porta a : 
- Un setup semplificato 
- Portabilità (poichè tramite l'immagine si possono asportare le applicazioni da una macchina all'altra senza quasi alcun tipo di configurazione)
- Ambiente consistente 
- Isolamento 
- Efficienza (rispetto ad usare le VM)
- Miglior gestione delle risorse (come CPU o RAM)
- Applicazioni facilmente scalabili 

###### Devs - OPS con Docker 

(devs)write dockerfile ->(devs)build and push image -> (ops)Provied some information if needed -> deploy application 

Mentre prima senza la dockerizzazione bisognava passare attraverso un ciclo di fix script per far girare le diverse applicazioni, con le diverse dipendenze e config sulla stessa macchina. 

![](/Screenshot_1.png)

I Container non sono l'unica soluzione possibile, ci si può affidare anche alla virtualizzazione che però porta con sè anche le sue complessità. Nell'immagine si possono notare i diversi layers necessari alla virtualizzazione, tra tutti ```L'hypervisor``` è uno dei più importanti poichè si occupa della gestione delle risorse della VM. Vedremo ora che la configurazione dei container non è poi tanto diversa. 

![](/Screenshot_2,png)

Come si può notare per ogni applicazione, non è necessario avere un OS sotto che gira, questo ci fa perdere in isolamento dell'applicazione, in ogni caso i container ci permettono di configurare l'isolamento in modo specifico e profondo, e quindi recuperare nei termini dell'isolamento. 

| **Feature**       | **Virtual Machines (VMs)**                                                                 | **Docker Containers**                                               |
|-------------------|--------------------------------------------------------------------------------------------|----------------------------------------------------------------------|
| **Isolation**      | Forte isolamento: ogni VM ha il proprio sistema operativo, garantendo isolamento completo. | Isolamento a livello di processo: i container condividono il kernel dell'host. |
| **Size/Overhead**  | Maggiore: le VM hanno un'impronta più grande a causa del sistema operativo guest e dell'hardware virtuale. | Leggeri: i container hanno un overhead minimo, poiché condividono il kernel. |
| **Portability**    | Meno portabili: le VM possono essere legate a specifici hypervisor e configurazioni OS.   | Altamente portabili: i container sono agnostici alla piattaforma e funzionano in modo coerente. |

| **Quando usare**         | **Virtual Machines (VMs)**                                                                                     | **Docker Containers**                                                                 |
|--------------------------|----------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
|                          | Hai bisogno di forte isolamento tra ambienti diversi.                                                          | Stai costruendo applicazioni moderne cloud-native con architettura a microservizi.    |
|                          | Stai gestendo applicazioni legacy che non possono essere facilmente containerizzate.                          | Hai bisogno di scalare rapidamente ed efficientemente le tue applicazioni.            |
|                          | Vuoi replicare un ambiente di sistema completo per test o sviluppo.                                           | La portabilità tra ambienti diversi è una priorità assoluta.                          |


#### Docker Components 

![](/Screenshot_3.png)

Come da immagine si possono vedere le parti di un sistema basato su Docker
1. Docker Client è l'interfaccia utente che tramite dei comandi, fa chiamate API verso il docker Host che le elabora
2. Docker host si occupa di gestire le chiamate e le risorse
3. Image registry è dove vengono salvate le immagini create dalle build delle applicazioni pronte ad essere scaricate

###### Ma come comunicano tra di loro ? 

1. viene lanciato ```docker run``` nella CLI
2. CLI manda una request all'host REST API
3. Docker Host controlla se l'immagine è presente nelle cache locali
4. se non lo è la scarica dall'image registry
5. Docker Host inizializza un nuovo container basato sull'immagine

###### Come invece pushare un immagine? 

1. viene lanciato ```docker build``` nella CLI
2. CLI lancia una request all' host REST API
3. Docker host costruisce l'immagine secondo il Dockerfile (mandato nel punto 2)
4. Docker Host tagga l'immagine e la stora localmente
5. viene lanciato ```docker push``` nella CLI ( per le image registry private bisogna essere autenticati per poterlo fare)
