Een virtuele Azure-machine biedt ondersteuning voor het koppelen van meerdere gegevensschijven. Voor optimale prestaties zult u toolimit Hallo aantal maximaal gebruikte schijven gekoppeld toohello virtuele machine tooavoid mogelijk beperking. Als alle schijven niet sterk wordt gebruikt op Hallo hetzelfde moment Hallo storage-account een groter aantal schijven kan ondersteunen.

* **Voor Azure Managed schijven:** limiet voor het aantal beheerde schijven is regionaal en ook afhankelijk van het opslagtype Hallo. Standaard Hallo en is ook de maximumlimiet Hallo 10.000 per abonnement, per regio en per opslagtype. Bijvoorbeeld, kunt u up too10, 000 standaard beheerd schijven en ook 10.000 premium schijven in een abonnement en in een regio die worden beheerd. 

    Beheerde momentopnamen en afbeeldingen worden geteld tegen Hallo die schijven beheerd beperken.

* **Voor standaardopslagaccounts:** een standaardopslagaccount heeft een maximale totale aanvraagsnelheid van 20.000 IOP's. Hallo totale IOP's voor alle schijven voor uw virtuele machine in een standard-opslagaccount mag niet meer dan deze limiet.
  
    U kunt ongeveer Hallo aantal maximaal gebruikte schijven wordt ondersteund door één standaard-storage-account op basis van Hallo aanvraag frequentielimiet berekenen. Bijvoorbeeld: voor een virtuele machine, in de Basisstaffel Hallo maximum aantal maximaal gebruikt schijven is ongeveer 66 (20.000/300 IOP's per schijf), en voor een standaard laag VM is ongeveer 40 (20.000/500 IOP's per schijf), zoals wordt weergegeven in onderstaande tabel voor Hallo. 
* **Voor Premium-opslagaccounts:** Premium-opslagaccounts bieden een maximale totale doorvoersnelheid van 50 Gbps. de totale doorvoer Hallo voor alle VM-schijven, mag niet meer dan deze limiet.

