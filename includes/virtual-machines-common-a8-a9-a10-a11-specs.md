

## <a name="deployment-considerations"></a>Overwegingen bij de implementatie
* **Azure-abonnement** – toodeploy meer dan een paar rekenintensieve exemplaren, kunt u een abonnement op gebruiksbasis of andere koopopties. Als u een [gratis account van Azure](https://azure.microsoft.com/free/) gebruikt, kunt u slechts een paar Azure Compute-resources van Azure gebruiken.

* **Prijzen en beschikbaarheid** -deze VM-grootten alleen in de Standard-prijscategorie Hallo worden aangeboden. Controleer [producten beschikbaar per regio] (https://azure.microsoft.com/regions/services/) voor beschikbaarheid in een Azure-regio's. 
* **Quotum voor kernen** – moet u mogelijk tooincrease Hallo kernen quotum in uw Azure-abonnement van Hallo-standaardwaarde. Uw abonnement mogelijk ook het aantal kernen dat u in bepaalde VM grootte families implementeren kunt, met inbegrip van Hallo H-serie Hallo beperken. toorequest een quotum verhogen, [opent u een ondersteuningsaanvraag online klant](../articles/azure-supportability/how-to-create-azure-support-request.md) zonder kosten. (De standaardlimiet kunnen variëren, afhankelijk van uw abonnementscategorie).
  
  > [!NOTE]
  > Neem contact op met ondersteuning van Azure als u grootschalige die u nodig hebt. Azure-quota tegoed worden beperkt, niet de garanties capaciteit. Ongeacht de quota u zijn alleen in rekening gebracht voor kernen dat u gebruikt.
  > 
  > 
* **Virtueel netwerk** : een Azure [virtueel netwerk](https://azure.microsoft.com/documentation/services/virtual-network/) is niet vereist toouse Hallo rekenintensieve exemplaren. Echter veel implementaties moet u ten minste een cloud-gebaseerde Azure-netwerk, of een site-naar-site-verbinding als u nodig hebt tooaccess on-premises resources. Wanneer deze nodig is, wordt een nieuw virtueel netwerk toodeploy Hallo-instanties maken. Rekenintensieve VMs tooa virtueel netwerk in een affiniteitsgroep toevoegen wordt niet ondersteund.
* **Vergroten of verkleinen** – vanwege hun speciale hardware, kunt u alleen rekenintensieve exemplaren grootte binnen Hallo dezelfde familie (H-serie of rekenintensieve A-serie) grootte. U kunt bijvoorbeeld alleen een VM H-serie van één H-serie grootte tooanother grootte. Bovendien wordt vergroten of verkleinen van een grootte van de grootte van de computer intensieve tooa rekenintensieve niet ondersteund.  
