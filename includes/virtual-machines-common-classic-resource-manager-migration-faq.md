# <a name="frequently-asked-questions-about-classic-tooazure-resource-manager-migration"></a>Veelgestelde vragen over klassieke tooAzure Resource Manager-migratie

## <a name="does-this-migration-plan-affect-any-of-my-existing-services-or-applications-that-run-on-azure-virtual-machines"></a>Is dit migratieplan van invloed op mijn bestaande services en toepassingen die worden uitgevoerd op virtuele Azure-machines? 

Nee. Hallo VMs (klassiek) zijn volledig ondersteunde services in de algemene beschikbaarheid. U kunt doorgaan toouse deze resources tooexpand uw footprint op Microsoft Azure.

## <a name="what-happens-toomy-vms-if-i-dont-plan-on-migrating-in-hello-near-future"></a>Wat gebeurt er toomy virtuele machines als ik niet wilt migreren in Hallo nabije toekomst? 

Er zijn geen Hallo bestaande klassieke API's en bron model bestandstypen. We willen toomake migratie eenvoudig in overweging Hallo geavanceerde functies die beschikbaar in Hallo Resource Manager-implementatiemodel zijn. We raden u wordt aangeraden [aantal vernieuwingen Hallo](../articles/azure-resource-manager/resource-manager-deployment-model.md) die deel uitmaken van IaaS onder Resource Manager.

## <a name="what-does-this-migration-plan-mean-for-my-existing-tooling"></a>Wat betekent dit migratieplan voor mijn bestaande tooling? 

Bijwerken van uw tooling toohello Resource Manager-implementatiemodel is een van de belangrijkste Hallo-wijzigingen die u tooaccount voor in uw plannen voor de migratie hebt.

## <a name="how-long-will-hello-management-plane-downtime-be"></a>Hoe lang Hallo management vlak uitvaltijd worden? 

Dit is afhankelijk van Hallo aantal bronnen die worden gemigreerd. Hallo volledige migratie moet minder dan een uur duren voordat voor kleinere implementaties (enkele tientallen van virtuele machines). Hallo-migratie kan een paar uur duren voor grootschalige implementaties (honderden VM's).

## <a name="can-i-roll-back-after-my-migrating-resources-are-committed-in-resource-manager"></a>Kan ik het migreren van mijn resources ongedaan maken nadat de resources zijn doorgevoerd in Resource Manager? 

Zolang Hallo bronnen bevinden zich in Hallo status voorbereid, kunt u uw migratie afbreken. Terugdraaien wordt niet ondersteund als Hallo resources hebt gemigreerd via Hallo-doorvoerbewerking.

## <a name="can-i-roll-back-my-migration-if-hello-commit-operation-fails"></a>Kan ik mijn migratie terugdraaien als Hallo opslagbewerking mislukt? 

U kunt migratie kan niet afbreken als Hallo opslagbewerking is mislukt. Alle migratiebewerkingen, met inbegrip van de doorvoerbewerking hello, zijn de idempotent. Daarom is het raadzaam dat u Hallo bewerking na korte tijd opnieuw. Als u nog steeds een fout wordt geconfronteerd, maak een ondersteuningsticket of maken van een bericht met Hallo ClassicIaaSMigration tag op onze [VM forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows).

## <a name="do-i-have-toobuy-another-express-route-circuit-if-i-have-toouse-iaas-under-resource-manager"></a>Heb ik toobuy een andere express route-circuit als ik toouse IaaS onder Resource Manager? 

Nee. We onlangs ingeschakeld [ExpressRoute-circuits verplaatsen van Hallo klassieke toohello Resource Manager-implementatiemodel](../articles/expressroute/expressroute-move.md). U hebt geen toobuy nieuwe ExpressRoute-circuit als u al hebt.

## <a name="what-if-i-had-configured-role-based-access-control-policies-for-my-classic-iaas-resources"></a>Wat gebeurt er als ik op rollen gebaseerd toegangsbeheerbeleid heb geconfigureerd voor mijn klassieke IaaS-resources? 

Tijdens de migratie transformeren Hallo resources van klassieke tooResource Manager. Daarom is het raadzaam dat u van plan bent Hallo RBAC beleidsupdates die moeten worden toohappen na de migratie.

## <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>Ik heb in een Backup-kluis een back-up gemaakt van mijn klassieke virtuele machines. Kan ik mijn virtuele machines migreren vanuit de klassieke modus tooResource Manager modus en beveiligt u ze in een Recovery Services-kluis? 

Klassieke VM herstelpunten in een back-upkluis migreren niet automatisch tooa Recovery Services-kluis wanneer u Hallo VM van klassieke tooResource Manager-modus verplaatsen. Volg deze stappen tootransfer uw VM back-ups:

1. Ga in de Hallo Backup-kluis, toohello **beveiligde Items** tabblad en selecteer Hallo VM. Klik op [Beveiliging stoppen](../articles/backup/backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Laat de optie *Gekoppelde back-upgegevens verwijderen* **uitgeschakeld**.
2. Hallo back-up/momentopname uitbreiding uit Hallo VM verwijderen.
3. Hallo virtuele machine migreren vanuit de klassieke modus tooResource Manager-modus. Zorg ervoor dat Hallo opslag en netwerk informatie is ook de bijbehorende toohello virtuele machine gemigreerd tooResource Manager-modus.
4. Een Recovery Services-kluis maken en configureren op Hallo back-up met behulp van virtuele machine gemigreerd **back-** actie boven op het kluisdashboard. Voor gedetailleerde informatie over back-ups van een VM tooa Recovery Services-kluis, Zie Hallo artikel [Azure VM's beveiligen met een Recovery Services-kluis](../articles/backup/backup-azure-vms-first-look-arm.md).

## <a name="can-i-validate-my-subscription-or-resources-toosee-if-theyre-capable-of-migration"></a>Kan ik mijn abonnement of valideren resources toosee als ze geschikt voor migratie zijn? 

Ja. Hallo eerste stap bij het voorbereiden voor migratie is in Hallo platform ondersteund migratieoptie, toovalidate dat Hallo-resources geschikt voor migratie zijn. Als Hallo valideren mislukt, kunt u berichten ontvangen alle Hallo redenen Hallo migratie kan niet worden voltooid.

## <a name="what-happens-if-i-run-into-a-quota-error-while-preparing-hello-iaas-resources-for-migration"></a>Wat gebeurt er als ik een quotum-fout opgetreden tijdens het Hallo IaaS-middelen voorbereiden voor migratie uitvoeren? 

U wordt aangeraden dat u uw migratie afbreken en meld u daarna een ondersteuning aanvraag tooincrease Hallo quota Hallo regio waar je je migreren Hallo virtuele machines. Nadat het Hallo-quota-aanvraag is goedgekeurd, kunt u beginnen Hallo migratiestappen opnieuw uitvoeren.

## <a name="how-do-i-report-an-issue"></a>Hoe meld ik een probleem? 

Uw problemen en vragen over migratie tooour boeken [VM forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows), met Hallo trefwoord ClassicIaaSMigration. Het wordt aanbevolen om al uw vragen op dit forum te plaatsen. Als u een ondersteuningscontract hebt, bent u Welkom toolog ook een ondersteuningsticket.

## <a name="what-if-i-dont-like-hello-names-of-hello-resources-that-hello-platform-chose-during-migration"></a>Wat gebeurt er als ik Hallo namen van Hallo-resources die Hallo platform niet leuk hebt gekozen tijdens de migratie? 

Alle Hallo-resources die u expliciet namen voor het klassieke implementatiemodel Hallo opgeeft worden tijdens de migratie bewaard. In sommige gevallen worden er nieuwe resources gemaakt. Er wordt dan bijvoorbeeld een netwerkinterface gemaakt voor elke VM. Momenteel ondersteund niet Hallo mogelijkheid toocontrol Hallo namen van deze nieuwe resources die zijn gemaakt tijdens de migratie. Meld u uw stemmen voor deze functie op Hallo [Azure Feedbackforum](http://feedback.azure.com).

## <a name="can-i-migrate-expressroute-circuits-used-across-subscriptions-with-authorization-links"></a>Kan ik ExpressRoute-circuits migreren die voor verschillende abonnementen met autorisatielinks worden gebruikt? 

ExpressRoute-circuits met abonnementsoverstijgende autorisatielinks kunnen niet automatisch worden gemigreerd zonder downtime. Er is informatie beschikbaar over het uitvoeren van handmatige migratie. Zie [migreren ExpressRoute-circuits en bijbehorende virtuele netwerken vanuit Hallo klassieke toohello Resource Manager-implementatiemodel](../articles/expressroute/expressroute-migration-classic-resource-manager.md) voor stappen en meer informatie.

## <a name="i-got-a-message-vm-is-reporting-hello-overall-agent-status-as-not-ready-hence-hello-vm-cannot-be-migrated-ensure-that-hello-vm-agent-is-reporting-overall-agent-status-as-ready-or-vm-contains-extension-whose-status-is-not-being-reported-from-hello-vm-hence-this-vm-cannot-be-migrated-"></a>Ik krijg een bericht *' VM rapporteert Hallo algehele agentstatus als niet gereed. Daarom kan niet Hallo VM worden gemigreerd. Zorg ervoor dat Hallo VM-Agent rapporteert algemene agentstatus gereed'* of * "VM bevat de extensie waarvan u de Status van Hallo VM niet wordt gerapporteerd. Hence, this VM cannot be migrated. (De VM bevat een extensie waarvan de status niet wordt gerapporteerd door de VM. Daarom kan deze VM niet worden gemigreerd.) *

Dit bericht wordt ontvangen wanneer Hallo VM geen uitgaande verbinding toohello internet. Hallo VM-agent gebruikt uitgaande verbinding tooreach hello Azure storage-account voor agentstatus Hallo bijwerken om de vijf minuten.
