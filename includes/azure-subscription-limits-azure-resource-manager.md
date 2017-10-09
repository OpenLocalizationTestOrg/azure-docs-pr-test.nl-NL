| Resource | Standaardlimiet | Maximumaantal |
| --- | --- | --- |
| Virtuele machines [per abonnement](../articles/billing-buy-sign-up-azure-subscription.md) |10.000 <sup>1</sup> per regio |10.000 per regio |
| Totaal aantal VM-cores per [abonnement](../articles/billing-buy-sign-up-azure-subscription.md) |20<sup>1</sup> per regio | Contact opnemen met ondersteuning |
| VM’s per reeks (Dv2, F, enz.), cores per [abonnement](../articles/billing-buy-sign-up-azure-subscription.md) |20<sup>1</sup> per regio | Contact opnemen met ondersteuning |
| [Medebeheerders](../articles/billing-add-change-azure-subscription-administrator.md) per abonnement |Onbeperkt |Onbeperkt |
| [Opslagaccounts](../articles/storage/common/storage-create-storage-account.md) per abonnement |200 |200<sup>2</sup> |
| [Resourcegroepen](../articles/azure-resource-manager/resource-group-overview.md) per abonnement |800 |800 |
| [Beschikbaarheidssets](../articles/virtual-machines/windows/manage-availability.md#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy) per abonnement |2000 per regio |2000 per regio |
| Leesbewerkingen Resource Manager-API |15.000 per uur |15.000 per uur |
| Schrijfbewerkingen Resource Manager-API |1200 per uur |1200 per uur |
| Aanvraaggrootte Resource Manager-API |4.194.304 bytes |4.194.304 bytes |
| Tags per abonnement<sup>3</sup> |onbeperkt |onbeperkt |
| Unieke tagberekeningen per abonnement<sup>3</sup> | 10.000 | 10.000 |
| [Cloudservices](../articles/cloud-services/cloud-services-choose-me.md) per abonnement |Niet van toepassing<sup>4</sup> |Niet van toepassing<sup>4</sup> |
| [Affiniteitsgroepen](../articles/virtual-network/virtual-networks-migrate-to-regional-vnet.md) per abonnement |Niet van toepassing<sup>4</sup> |Niet van toepassing<sup>4</sup> |

<sup>1</sup>Standaardlimieten zijn afhankelijk van het type aanbieding, zoals gratis proefversies, betalen naar gebruik of per serie, zoals Dv2, F, G, enz.

<sup>2</sup>Hieronder vallen zowel Standard als Premium opslagaccounts. Als u meer dan 200 opslagaccounts nodig hebt, dient u een aanvraag in te dienen via de [ondersteuning van Azure](https://azure.microsoft.com/support/faq/). Hello Azure Storage-team uw bedrijfsscenario controleert en up too250 storage-accounts kan goedkeuren.

<sup>3</sup>U kunt u een onbeperkt aantal tags per abonnement toepassen. Hallo aantal tags per resource of resourcegroep is beperkt too15. Resource Manager retourneert alleen een [lijst met unieke labelnaam en waarden](/rest/api/resources/tags#Tags_List) in Hallo abonnement wanneer het aantal tags Hallo 10.000 of minder is. U kunt echter nog steeds een resource vinden door de tag wanneer Hallo meer dan 10.000.  

<sup>4</sup>deze functies niet langer zijn vereist met Azure-resourcegroepen en hello Azure Resource Manager.

> [!NOTE]
> Het is belangrijk tooemphasize die virtuele machine kernen hebben een regionale maximum, evenals een landinstelling per groottelimiet reeks (Dv2, F, enzovoort) die afzonderlijk worden afgedwongen.  Neem bijvoorbeeld een abonnement met een limiet van 30 VM-cores voor VS Oost, een limiet van 30 cores voor de A-serie en een limiet van 30 cores voor de D-serie.  Dit abonnement mogen toodeploy 30 A1-VM's of 30 D1 VM's of een combinatie van twee Hallo niet tooexceed een totaal van 30 kernen (bijvoorbeeld 10 A1-VM's en 20 D1 VM's).  
> <!-- -->
> 
> 

