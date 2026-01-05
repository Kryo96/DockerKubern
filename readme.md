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

