---
title: een Azure Service Fabric-cluster aaaUpgrade | Microsoft Docs
description: Upgrade Hallo Service Fabric-code en/of de configuratie die wordt uitgevoerd van een Service Fabric-cluster, inclusief het instellen van de cluster-updatemodus, certificaten, toe te voegen toepassing poorten, OS patches doen upgraden enzovoort. Wat kunt u verwachten wanneer Hallo upgrades worden uitgevoerd?
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 15190ace-31ed-491f-a54b-b5ff61e718db
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/10/2017
ms.author: chackdan
ms.openlocfilehash: 94ac3833ec0810f79de06ecb50f254028fa90408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-azure-service-fabric-cluster"></a>Upgrade van een Azure Service Fabric-cluster
> [!div class="op_single_selector"]
> * [Azure-Cluster](service-fabric-cluster-upgrade.md)
> * [Zelfstandige Cluster](service-fabric-cluster-upgrade-windows-server.md)
> 
> 

Voor elk moderne systeem is ontwerpen voor kunnen succes op lange termijn voor belangrijke tooachieving van het product. Een Azure Service Fabric-cluster is een resource die u bezit, maar gedeeltelijk wordt beheerd door Microsoft. Dit artikel wordt beschreven wat automatisch wordt beheerd en wat u kunt zelf configureren.

## <a name="controlling-hello-fabric-version-that-runs-on-your-cluster"></a>Hallo fabric-versie die wordt uitgevoerd op het Cluster beheren
U kunt uw cluster tooreceive automatische fabric upgrades instellen als ze door Microsoft worden uitgegeven of kunt u een ondersteunde fabric-versie die u wilt dat uw cluster toobe op.

Dit doet u door de instelling Hallo 'upgradeMode' clusterconfiguratie op Hallo portal of met behulp van Resource Manager op Hallo moment gemaakt of later in een live cluster 

> [!NOTE]
> Zorg ervoor dat tookeep uw cluster een ondersteunde fabric-versie altijd uitgevoerd. Als en dat we Hallo-release van een nieuwe versie van het service fabric aankondigen, is voor einde van de ondersteuningsperiode Hallo vorige versie gemarkeerd na een minimum van 60 dagen na die datum. Hallo Hallo nieuwe releases worden aangekondigd [op Hallo service fabric-teamblog](https://blogs.msdn.microsoft.com/azureservicefabric/). Hallo nieuwe release is vervolgens beschikbaar toochoose. 
> 
> 

14 dagen voorafgaande toohello verloopdatum van Hallo release uw cluster wordt uitgevoerd, wordt een statusgebeurtenis gegenereerd die het cluster in een waarschuwingsstatus wordt geplaatst. Hallo cluster blijft met een waarschuwingsstatus totdat u een upgrade uitvoert van tooa ondersteunde fabric-versie.

### <a name="setting-hello-upgrade-mode-via-portal"></a>Hallo upgrademodus via de portal instellen
U kunt tijdens het maken van de cluster Hallo Hallo cluster tooautomatic of handmatig instellen.

![Create_Manualmode][Create_Manualmode]

U kunt Hallo cluster tooautomatic instellen of handmatige wanneer op een live cluster, met behulp van Hallo ervaring beheren. 

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-portal"></a>Upgraden van de nieuwe versie tooa op een cluster dat tooManual modus via de portal is ingesteld.
tooupgrade tooa is nieuwe versie, hoeft u toodo Hallo beschikbare versie uit de vervolgkeuzelijst Hallo selecteert en slaat u. Hallo Fabric-upgrade wordt automatisch gestart. Hallo statusbeleid cluster (een combinatie van het knooppunt status en alle toepassingen die worden uitgevoerd in de cluster Hallo HALLO hallo-status) zijn gehouden tooduring Hallo upgrade.

Als het statusbeleid Hallo-cluster niet wordt voldaan, is Hallo-upgrade teruggedraaid. Schuif omlaag in dit document tooread meer informatie over hoe tooset die aangepaste statusbeleid. 

Als u problemen met de Hallo dat heeft geresulteerd in Hallo terugdraaien hebt opgelost, moet u tooinitiate Hallo upgrade opnieuw door de volgende Hallo dezelfde als voorheen stappen.

![Manage_Automaticmode][Manage_Automaticmode]

### <a name="setting-hello-upgrade-mode-via-a-resource-manager-template"></a>Hallo upgrademodus via Resource Manager-sjabloon instellen
Hallo 'upgradeMode' toohello Microsoft.ServiceFabric/clusters resource configuratiedefinitie en set Hallo 'clusterCodeVersion' tooone Hallo fabric-versies ondersteund zoals hieronder wordt weergegeven en vervolgens implementeert Hallo sjabloon toevoegen. geldige waarden voor 'upgradeMode' Hallo zijn 'Handmatig' of 'Automatisch'

![ARMUpgradeMode][ARMUpgradeMode]

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-a-resource-manager-template"></a>Upgraden van de nieuwe versie tooa op een cluster dat tooManual modus via Resource Manager-sjabloon is ingesteld.
Wanneer Hallo-cluster in de handmatige modus, tooupgrade tooa nieuwe versie, ondersteunde versie van Hallo 'clusterCodeVersion' tooa wijzigen en deze implementeren. Hallo-implementatie van sjabloon hello, gang van Fabric-upgrade Hallo opgehaald gestarte automatisch. Hallo statusbeleid cluster (een combinatie van het knooppunt status en alle toepassingen die worden uitgevoerd in de cluster Hallo HALLO hallo-status) zijn gehouden tooduring Hallo upgrade.

Als het statusbeleid Hallo-cluster niet wordt voldaan, is Hallo-upgrade teruggedraaid. Schuif omlaag in dit document tooread meer informatie over hoe tooset die aangepaste statusbeleid. 

Als u problemen met de Hallo dat heeft geresulteerd in Hallo terugdraaien hebt opgelost, moet u tooinitiate Hallo upgrade opnieuw door de volgende Hallo dezelfde als voorheen stappen.

### <a name="get-list-of-all-available-version-for-all-environments-for-a-given-subscription"></a>Lijst met alle beschikbare versie ophalen voor alle omgevingen voor een bepaald abonnement
Voer Hallo van de volgende opdracht en krijgt u een vergelijkbare toothis uitvoer.

'supportExpiryUtc' vertelt uw wanneer een bepaalde versie is verlopen of is verlopen. Hallo meest recente versie beschikt niet over een geldige datum - deze heeft een waarde van ' 9999-12-31T23:59:59.9999999 ', wat betekent dat de vervaldatum Hallo nog niet wordt ingesteld.

```REST
GET https://<endpoint>/subscriptions/{{subscriptionId}}/providers/Microsoft.ServiceFabric/locations/{{location}}/clusterVersions?api-version=2016-09-01

Example: https://management.azure.com/subscriptions/1857f442-3bce-4b96-ad95-627f76437a67/providers/Microsoft.ServiceFabric/locations/eastus/clusterVersions?api-version=2016-09-01

Output:
{
                  "value": [
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/5.0.1427.9490",
                      "name": "5.0.1427.9490",
                      "type": "Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.0.1427.9490",
                        "supportExpiryUtc": "2016-11-26T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.0.1427.9490",
                      "name": "5.1.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.1.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.4.1427.9490",
                      "name": "4.4.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "4.4.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Linux"
                      }
                    }
                  ]
                }


```

## <a name="fabric-upgrade-behavior-when-hello-cluster-upgrade-mode-is-automatic"></a>Fabric upgrade gedrag wanneer Hallo cluster de modus bijwerken automatisch is
Microsoft onderhoudt Hallo fabric code en configuratie die in een Azure-cluster wordt uitgevoerd. We uitvoeren automatische gecontroleerde upgrades toohello software op een als dat nodig is. Deze upgrades mogelijk code en/of de configuratie. toomake ervoor dat uw toepassing te lijden heeft onder geen gevolgen of minimale gevolgen vanwege toothese upgrades, we Hallo upgrades uitvoeren in de volgende fasen Hallo:

### <a name="phase-1-an-upgrade-is-performed-by-using-all-cluster-health-policies"></a>Fase 1: Een upgrade wordt uitgevoerd met behulp van alle cluster statusbeleid
Tijdens deze fase Hallo upgrades één upgradedomein tegelijk gaan en Hallo-toepassingen die zijn uitgevoerd in de cluster Hallo blijven toorun zonder uitvaltijd. Hallo statusbeleid cluster (een combinatie van het knooppunt status en alle toepassingen die worden uitgevoerd in de cluster Hallo HALLO hallo-status) zijn gehouden tooduring Hallo upgrade.

Als het statusbeleid Hallo-cluster niet wordt voldaan, is Hallo-upgrade teruggedraaid. Een e-mailbericht verzonden vervolgens toohello eigenaar van het Hallo-abonnement. Hallo e-mailbericht bevat Hallo volgende informatie:

* Melding dat we tooroll weer een upgrade van het cluster hadden.
* Voorgestelde corrigerende acties, indien van toepassing.
* Hallo aantal dagen (n) totdat we fase 2 uitvoeren.

We proberen tooexecute Hallo die dezelfde een paar keer upgrade geval eventuele upgrades is mislukt door redenen infrastructuur. Na Hallo n dagen vanaf Hallo datum Hallo e-mail is verzonden, wordt we gaan tooPhase 2.

Hallo cluster statusbeleid wordt voldaan, is Hallo-upgrade beschouwd als geslaagd als voltooid gemarkeerd. Dit kan gebeuren tijdens de eerste upgrade hello of een van de upgrade herhalingen Hallo in deze fase. Er is geen e-mailbevestiging van een geslaagde uitvoering. Dit is tooavoid u te veel e-mails--ontvangt een e-mailbericht moet worden beschouwd als een uitzondering toonormal verzenden. De meeste Hallo cluster upgrades toosucceed verwachten we zonder enige impact op de beschikbaarheid van uw toepassing.

### <a name="phase-2-an-upgrade-is-performed-by-using-default-health-policies-only"></a>Fase 2: Een upgrade wordt uitgevoerd met behulp van standaard statusbeleid alleen
Hallo statusbeleid in deze fase worden ingesteld op zodanige wijze dat aantal toepassingen die in orde aan Hallo begin van de upgrade Hallo zijn Hallo Hallo identiek zijn voor de duur van het upgradeproces Hallo Hallo blijft. Net zoals in de fase 1 Hallo fase 2-upgrades één upgradedomein tegelijk gaan en Hallo-toepassingen die zijn uitgevoerd in de cluster Hallo blijven toorun zonder uitvaltijd. statusbeleid Hallo-cluster (een combinatie van het knooppunt status en alle toepassingen die worden uitgevoerd in de cluster Hallo HALLO hallo-status) zijn zelfklevend toofor Hallo duur van Hallo upgrade.

Als Hallo cluster statusbeleid wordt van kracht niet voldaan, is Hallo-upgrade teruggedraaid. Een e-mailbericht verzonden vervolgens toohello eigenaar van het Hallo-abonnement. Hallo e-mailbericht bevat Hallo volgende informatie:

* Melding dat we tooroll weer een upgrade van het cluster hadden.
* Voorgestelde corrigerende acties, indien van toepassing.
* Hallo aantal dagen (n) totdat we fase 3 uitvoeren.

We proberen tooexecute Hallo die dezelfde een paar keer upgrade geval eventuele upgrades is mislukt door redenen infrastructuur. Een herinnering is verzonden een paar dagen voordat n dagen actief zijn. Na Hallo n dagen vanaf Hallo datum Hallo e-mail is verzonden, wordt we gaan tooPhase 3. Hallo e-mailberichten we u in de fase 2 sturen ernstig moeten worden gehaald en corrigerende acties moeten worden genomen.

Hallo cluster statusbeleid wordt voldaan, is Hallo-upgrade beschouwd als geslaagd als voltooid gemarkeerd. Dit kan gebeuren tijdens de eerste upgrade hello of een van de upgrade herhalingen Hallo in deze fase. Er is geen e-mailbevestiging van een geslaagde uitvoering.

### <a name="phase-3-an-upgrade-is-performed-by-using-aggressive-health-policies"></a>Fase 3: Een upgrade wordt uitgevoerd met behulp van agressieve statusbeleid
Deze statusbeleid in deze fase zijn gericht op het Hallo-upgrade is voltooid in plaats van Hallo status van Hallo-toepassingen. In deze fase eindigen heel weinig cluster-upgrades. Als uw cluster opgehaald toothis fase, is er een goede kans dat uw toepassing slecht functioneert en/of beschikbaarheid verliezen.

Vergelijkbare toohello andere twee fasen, upgrades voor fase 3, gaat u verder één upgradedomein tegelijk.

Als het statusbeleid Hallo-cluster niet wordt voldaan, is Hallo-upgrade teruggedraaid. We proberen tooexecute Hallo die dezelfde een paar keer upgrade geval eventuele upgrades is mislukt door redenen infrastructuur. Hallo-cluster is hierna is vastgemaakt, zodat deze niet langer ondersteuning en/of upgrades ontvangt.

Een e-mailbericht met deze informatie wordt verzonden toohello abonnement eigenaar, samen met de Hallo corrigerende acties. We niet van plan bent een tooget clusters in een status waarbij de fase 3 is mislukt.

Hallo cluster statusbeleid wordt voldaan, is Hallo-upgrade beschouwd als geslaagd als voltooid gemarkeerd. Dit kan gebeuren tijdens de eerste upgrade hello of een van de upgrade herhalingen Hallo in deze fase. Er is geen e-mailbevestiging van een geslaagde uitvoering.

## <a name="cluster-configurations-that-you-control"></a>Clusterconfiguraties die u beheert
Bovendien toohello mogelijkheid tooset Hallo cluster upgrademodus, hier zijn Hallo-configuraties die u in een live cluster wijzigen kunt.

### <a name="certificates"></a>Certificaten
U kunt nieuwe toevoegen of verwijderen van certificaten voor Hallo-cluster en de client via de portal Hallo eenvoudig. Raadpleeg te[dit document voor gedetailleerde instructies](service-fabric-cluster-security-update-certs-azure.md)

![Schermafbeelding van certificaatvingerafdrukken in hello Azure-portal.][CertificateUpgrade]

### <a name="application-ports"></a>Poorten van de toepassing
U kunt toepassing poorten wijzigen door Hallo Load Balancer resource-eigenschappen die gekoppeld aan het knooppunttype hello zijn te wijzigen. U kunt Hallo portal gebruiken of kunt u rechtstreeks Resource Manager PowerShell gebruiken.

een nieuwe poort op alle virtuele machines in een knooppunttype tooopen Hallo te volgen:

1. Voeg een nieuwe test toohello geschikte load balancer.
   
    Als u uw cluster hebt geïmplementeerd met behulp van de portal hello, Hallo load balancers zijn met de naam ' LB van Hallo Resource group-NodeTypename ', één voor elk knooppunttype. Aangezien Hallo load balancer namen uniek alleen binnen een resourcegroep zijn, wordt het aanbevolen als u naar deze onder een bepaalde resourcegroep zoekt.
   
    ![Schermafbeelding van het toevoegen van een tooa test de load balancer in Hallo-portal.][AddingProbes]
2. Voeg een nieuwe regel toohello load balancer.
   
    Een nieuwe regel toohello dezelfde de load balancer met behulp van Hallo-test die u hebt gemaakt in de vorige stap Hallo toevoegen.
   
    ![Toevoegen van een nieuwe regel tooa load balancer in Hallo-portal.][AddingLBRules]

### <a name="placement-properties"></a>Plaatsingseigenschappen
U kunt aangepaste plaatsingseigenschappen gewenste toouse in uw toepassingen toevoegen voor elk van de knooppunttypen Hallo. NodeType is een standaardeigenschap die u gebruiken kunt zonder deze expliciet toe te voegen.

> [!NOTE]
> Voor meer informatie over Hallo gebruik van plaatsingsbeperkingen, knooppunteigenschappen, en hoe toodefine, verwijzen toohello sectie 'Plaatsing beperkingen en eigenschappen van knooppunt' hello Service Fabric Cluster Resource Manager-Document op [met een beschrijving van uw Cluster ](service-fabric-cluster-resource-manager-cluster-description.md).
> 
> 

### <a name="capacity-metrics"></a>Capaciteit metrische gegevens
Voor elk van de knooppunttypen hello, kunt u aangepaste capaciteitsmetrieken dat u in uw toepassingen tooreport load toouse wilt toevoegen. Raadpleeg voor meer informatie over Hallo gebruik van capaciteit metrische gegevens tooreport load toohello Service Fabric-Cluster Resource Manager-documenten op [met een beschrijving van uw Cluster](service-fabric-cluster-resource-manager-cluster-description.md) en [metrische gegevens en de belasting](service-fabric-cluster-resource-manager-metrics.md).

### <a name="fabric-upgrade-settings---health-polices"></a>Instellingen voor fabric-upgrade - Health-beleid
U kunt opgeven om de gezondheid van aangepaste beleidsregels voor fabric-upgrade. Als u hebt uw cluster tooAutomatic fabric-upgrades ingesteld, krijgen deze beleidsregels toegepaste toohello fase 1 van Hallo automatische fabric-upgrades.
Als u hebt ingesteld uw cluster voor handmatige fabric-upgrades en vervolgens deze beleidsregels telkens wanneer toegepast u een nieuwe versie activerende Hallo system tookick uitschakelen Hallo fabric-upgrade in uw cluster. Als u Hallo beleidsregels niet overschrijven, Hallo standaardinstellingen gebruikt.

U kunt de aangepaste statusbeleid Hallo opgeven of bekijken voor de huidige instellingen Hallo onder Hallo 'fabric-upgrade' blade te selecteren Hallo geavanceerde instellingen voor de upgrade. Hallo volgende afbeelding voor het bekijken. 

![Aangepaste statusbeleid beheren][HealthPolices]

### <a name="customize-fabric-settings-for-your-cluster"></a>Fabric-instellingen voor uw cluster aanpassen
Raadpleeg te[service fabric-clusterinstellingen fabric](service-fabric-cluster-fabric-settings.md) op wat en hoe u ze kunt aanpassen.

### <a name="os-patches-on-hello-vms-that-make-up-hello-cluster"></a>OS patches op Hallo van virtuele machines die gezamenlijk Hallo-cluster
Raadpleeg te[Patch Orchestration toepassing](service-fabric-patch-orchestration-application.md) die kan worden geïmplementeerd in uw cluster tooinstall patches via Windows Update op Hallo services beschikbaar houden alle Hallo tijd geregiseerde wijze. 

### <a name="os-upgrades-on-hello-vms-that-make-up-hello-cluster"></a>Upgrades voor het besturingssysteem op virtuele machines die gezamenlijk Hallo cluster Hallo
Als u de installatiekopie van het besturingssysteem op Hallo virtuele machines van de cluster Hallo Hallo bijwerkt moet, moet u dit één VM doen op een tijdstip. U bent zelf verantwoordelijk voor deze upgrade--er is momenteel geen automation voor deze.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe toocustomize aantal Hallo [service fabric-clusterinstellingen fabric](service-fabric-cluster-fabric-settings.md)
* Meer informatie over hoe te[in en uit het cluster schalen](service-fabric-cluster-scale-up-down.md)
* Meer informatie over [toepassingsupgrades](service-fabric-application-upgrade.md)

<!--Image references-->
[CertificateUpgrade]: ./media/service-fabric-cluster-upgrade/CertificateUpgrade2.png
[AddingProbes]: ./media/service-fabric-cluster-upgrade/addingProbes2.PNG
[AddingLBRules]: ./media/service-fabric-cluster-upgrade/addingLBRules.png
[HealthPolices]: ./media/service-fabric-cluster-upgrade/Manage_AutomodeWadvSettings.PNG
[ARMUpgradeMode]: ./media/service-fabric-cluster-upgrade/ARMUpgradeMode.PNG
[Create_Manualmode]: ./media/service-fabric-cluster-upgrade/Create_Manualmode.PNG
[Manage_Automaticmode]: ./media/service-fabric-cluster-upgrade/Manage_Automaticmode.PNG
