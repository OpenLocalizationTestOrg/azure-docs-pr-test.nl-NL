---
title: aaaService kaart integratie met System Center Operations Manager | Microsoft Docs
description: Serviceoverzicht is een Operations Management Suite-oplossing die automatisch de onderdelen van toepassing op Windows detecteert en Linux-systemen en maps Hallo communicatie tussen services. Dit artikel wordt beschreven met behulp van Serviceoverzicht tooautomatically diagrammen voor gedistribueerde toepassing maken in Operations Manager.
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: cff9cce2559448ec3a5fd14087b867f314716560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a>Serviceoverzicht integratie met System Center Operations Manager
  > [!NOTE]
  > Deze functie is openbare preview.
  > 
  
Operations Management Suite Serviceoverzicht automatisch detecteert de onderdelen van toepassing op Windows- en Linux-systemen en Hallo communicatie tussen services wordt toegewezen. Serviceoverzicht kunt u uw servers Hallo manier u ze, beschouwen als onderling verbonden systemen die essentiële services leveren tooview. Serviceoverzicht toont verbindingen tussen servers, processen en poorten voor elke architectuur TCP-verbinding zonder configuratie naast het Hallo-installatie van een agent vereist. Zie voor meer informatie, Hallo [Serviceoverzicht documentatie](operations-management-suite-service-map.md).

Met deze integratie tussen Serviceoverzicht en System Center Operations Manager, kunt u automatisch diagrammen voor gedistribueerde toepassing maken in Operations Manager die zijn gebaseerd op Hallo dynamische afhankelijkheid maps in Serviceoverzicht.

## <a name="prerequisites"></a>Vereisten
* Een Operations Manager-beheergroep die wordt beheerd door een reeks servers.
* Een Operations Management Suite-werkruimte Hello Serviceoverzicht oplossing is ingeschakeld.
* Een set servers (ten minste één) die worden beheerd door Operations Manager en verzenden gegevens tooService kaart. Windows en Linux-servers worden ondersteund.
* Een service-principal met toegang toohello Azure-abonnement dat is gekoppeld aan Hallo Operations Management Suite-werkruimte. Voor meer informatie gaat te[maken van een service-principal](#creating-a-service-principal).

## <a name="install-hello-service-map-management-pack"></a>Hallo Serviceoverzicht management pack installeren
U inschakelen Hallo integratie tussen Operations Manager en Serviceoverzicht door het importeren van Hallo Microsoft.SystemCenter.ServiceMap management pack-bundel (Microsoft.SystemCenter.ServiceMap.mpb). Hallo-bundel bevat Hallo management packs te volgen:
* Microsoft Service kaart Toepassingweergaven
* Microsoft System Center Serviceoverzicht interne
* Microsoft System Center Service kaart onderdrukkingen
* Microsoft System Center-Serviceoverzicht

## <a name="configure-hello-service-map-integration"></a>Hallo Serviceoverzicht integratie configureren
Nadat u Hallo Serviceoverzicht management pack, een nieuw knooppunt **Serviceoverzicht**, wordt weergegeven onder **Operations Management Suite** in Hallo **beheer** deelvenster. 

tooconfigure Serviceoverzicht integratie, Hallo te volgen:

1. tooopen hello configuratiewizard in Hallo **kaart Serviceoverzicht** deelvenster, klikt u op **werkruimte toevoegen**.  

    ![Deelvenster Overzicht van de service-kaart](media/oms-service-map/scom-configuration.png)

2. In Hallo **verbindingsconfiguratie** venster Hallo tenantnaam of -ID, toepassings-ID (ook wel bekend als Hallo gebruikersnaam of clientID) en wachtwoord van de service-principal Hallo invoeren en klik vervolgens op **volgende**. Voor meer informatie gaat te[maken van een service-principal](#creating-a-service-principal).

    ![Hallo verbindingsconfiguratie venster](media/oms-service-map/scom-config-spn.png)

3. In Hallo **abonnement selectie** venster hello Azure-abonnement, Azure-resourcegroep (Hallo Hallo Operations Management Suite-werkruimte met) en Operations Management Suite-werkruimte selecteren en klik vervolgens op **Volgende**.

    ![Hallo werkruimte van Operations Manager-configuratie](media/oms-service-map/scom-config-workspace.png)

4. In Hallo **groepsselectie Machine** venster u kiezen welke Service kaart Machine groepen gewenste toosync tooOperations Manager. Klik op **computergroepen toevoegen/verwijderen**, kies de groepen uit Hallo lijst met **beschikbaar computergroepen**, en klik op **toevoegen**.  Wanneer u klaar bent met groepen te selecteren, klikt u op **Ok** toofinish.
    
    ![Hallo computergroepen voor Operations Manager-configuratie](media/oms-service-map/scom-config-machine-groups.png)
    
5. In Hallo **serverselectie** venster u Hallo servicegroep kaart Servers configureren met Hallo-servers die u wilt dat toosync tussen Operations Manager en Service-kaart. Klik op **Servers toevoegen of verwijderen**.   
    
    Voor Hallo integratie toobuild een gedistribueerde toepassing diagram voor een server moet de Hallo-server:

    * Beheerd door Operations Manager
    * Beheerd door Serviceoverzicht
    * Vermeld in het Hallo-kaart Servers servicegroep

    ![Hallo Operations Manager Configuration-servicegroep](media/oms-service-map/scom-config-group.png)

6. Optioneel: Schakel Hallo beheerserver resource pool toocommunicate met Operations Management Suite en klik vervolgens op **werkruimte toevoegen**.

    ![Hallo resourcegroep van Operations Manager-configuratie](media/oms-service-map/scom-config-pool.png)

    Het kan een minuut tooconfigure nemen en registreer Hallo Operations Management Suite-werkruimte. Nadat deze is geconfigureerd, initieert Operations Manager Hallo eerste Serviceoverzicht synchronisatie vanaf Operations Management Suite.

    ![Hallo resourcegroep van Operations Manager-configuratie](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a>Monitor Serviceoverzicht
Nadat Hallo Operations Management Suite-werkruimte is aangesloten, een nieuwe map Serviceoverzicht wordt weergegeven in Hallo **bewaking** deelvenster van Hallo Operations Manager-console.

![Hallo Operations Manager Monitoring deelvenster](media/oms-service-map/scom-monitoring.png)

Hallo Serviceoverzicht map bevat vier knooppunten:
* **Actieve waarschuwingen**: geeft een lijst van alle Hallo actieve waarschuwingen over Hallo communicatie tussen Operations Manager en Service-kaart.  Houd er rekening mee dat deze waarschuwingen niet gesynchroniseerde tooOperations Manager wordt Operations Management Suite-waarschuwingen zijn. 

* **Servers**: lijsten Hallo bewaakte servers die zijn geconfigureerd toosync van Serviceoverzicht.

    ![Hallo Operations Manager Monitoring beheerservers deelvenster](media/oms-service-map/scom-monitoring-servers.png)

* **Afhankelijkheid Groepsweergaven machine**: geeft een lijst van alle computergroepen die vanuit Serviceoverzicht worden gesynchroniseerd. U kunt klikken op een groep tooview diagram van de gedistribueerde toepassing.

    ![diagram van de gedistribueerde toepassing Hello Operations Manager](media/oms-service-map/scom-group-dad.png)

* **Server-weergaven voor afhankelijkheid**: geeft een lijst van alle servers die vanuit Serviceoverzicht worden gesynchroniseerd. U kunt klikken op elke server tooview diagram van de gedistribueerde toepassing.

    ![diagram van de gedistribueerde toepassing Hello Operations Manager](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-hello-workspace"></a>Bewerken of verwijderen van Hallo-werkruimte
U kunt bewerken of verwijderen van de werkruimte Hallo geconfigureerd via Hallo **kaart Serviceoverzicht** deelvenster (**beheer** deelvenster > **Operations Management Suite**  >  **Service kaart**). U kunt slechts één Operations Management Suite-werkruimte nu configureren.

![Hallo Operations Manager bewerken werkruimte](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a>Regels en overschrijvingen configureren
Een regel _Microsoft.SystemCenter.ServiceMapImport.Rule_, tooperiodically ophalen informatie wordt gemaakt van Serviceoverzicht. toochange sync tijdsinstellingen, kunt u onderdrukkingen van Hallo regel configureren (**ontwerpen** deelvenster > **regels** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).

![eigenschappenvenster van Hallo Operations Manager-onderdrukkingen](media/oms-service-map/scom-overrides.png)

* **Ingeschakeld**: in- of uitschakelen van automatische updates. 
* **IntervalMinutes**: Hallo tijd tussen updates opnieuw ingesteld. Hallo interval is standaard een uur. Als u vaker toosync server maps wilt, kunt u Hallo waarde wijzigen.
* **TimeoutSeconds**: Hallo tijdsduur voordat een optreedt Hallo aanvraag time-out opnieuw. 
* **TimeWindowMinutes**: Reset Hallo tijdvenster voor het opvragen van gegevens. Standaard is een venster 60 minuten. Hallo toegestane maximumwaarde door Serviceoverzicht is 60 minuten.

## <a name="known-issues-and-limitations"></a>Bekende problemen en beperkingen

Hallo huidige ontwerp geeft volgende Hallo problemen en beperkingen:
* U kunt alleen verbinding tooa één Operations Management Suite-werkruimte.
* Hoewel u kunt servers toohello servicegroep kaart Servers handmatig via Hallo toevoegen **ontwerpen** deelvenster Hallo kaarten voor deze servers niet onmiddellijk worden gesynchroniseerd.  Ze worden gesynchroniseerd vanuit Serviceoverzicht tijdens de volgende synchronisatiecyclus Hallo.
* Als u wijzigingen aanbrengt toohello gedistribueerde toepassing diagrammen die zijn gemaakt door Hallo management pack, worden deze wijzigingen op de volgende synchronisatie Hallo met Serviceoverzicht waarschijnlijk worden overschreven.

## <a name="create-a-service-principal"></a>Een service-principal maken
Zie voor de officiële Azure-documentatie over het maken van een service principal:
* [Een service-principal maken met behulp van PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Een service-principal maken met behulp van Azure CLI](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [Een service-principal maken met behulp van hello Azure-portal](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a>Feedback
Hebt u feedback voor ons over Serviceoverzicht of deze documentatie? Ga naar onze [User Voice pagina](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), kunt u functies aanbevelen of over bestaande suggesties stemmen.
