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

