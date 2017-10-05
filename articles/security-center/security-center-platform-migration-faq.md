---
title: Migratie van de platforms Security Center FAQ | Microsoft Docs
description: Deze Veelgestelde vragen over de antwoorden op vragen over de migratie van Azure Security Center-platform.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4d1364cd-7847-425a-bb3a-722cb0779f78
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: terrylan
ms.openlocfilehash: 2ffbaca614d667db565197f3c13b1658fffc2a7c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="security-center-platform-migration-faq"></a>Security Center-platform migratie Veelgestelde vragen
In eerdere juni 2017 begonnen Azure Security Center met behulp van Microsoft Monitoring Agent voor het verzamelen en opslaan van gegevens. Zie voor meer informatie, [Azure Security Center-Platform migratie](security-center-platform-migration.md). Deze Veelgestelde vragen over de antwoorden op vragen over de migratie van het platform.

## <a name="data-collection-agents-and-workspaces"></a>Verzamelen van gegevens, agents en werkruimten

### <a name="how-is-data-collected"></a>Hoe worden gegevens verzameld
Microsoft Monitoring Agent Security Center gebruikt voor het verzamelen van beveiligingsgegevens van uw virtuele machines. De beveiligingsgegevens bevat informatie over beveiligingsconfiguraties, die worden gebruikt voor kwetsbaarheden identificeren, en beveiligingsgebeurtenissen die worden gebruikt voor het detecteren van bedreigingen. Gegevens die worden verzameld door de agent wordt opgeslagen in een bestaande werkruimte voor logboekanalyse is verbonden met de virtuele machine of een nieuwe werkruimte gemaakt door Security Center. Wanneer Security Center een nieuwe werkruimte maakt, wordt de geolocatie van de virtuele machine in aanmerking genomen.

> [!NOTE]
> Microsoft Monitoring Agent is dezelfde agent die wordt gebruikt door de Operations Management Suite (OMS), Log Analytics-service en System Center Operations Manager (SCOM).
>
>

Wanneer gegevensverzameling is ingeschakeld voor het eerst of uw abonnementen die worden gemigreerd, Security Center gecontroleerd of de Microsoft Monitoring Agent al is geïnstalleerd als een Azure-extensie op elk van uw virtuele machines. Als Microsoft Monitoring Agent niet is geïnstalleerd, wordt Security Center:

- Installeer de Microsoft Monitoring agent op de virtuele machine
   - Als een werkruimte gemaakt door Security Center al in de dezelfde geolocatie als de virtuele machine bestaat, is de agent verbonden met deze werkruimte
   - Als een werkruimte niet bestaat, Security Center maakt een nieuwe resourcegroep standaard werkruimte in die geolocatie en koppel de agent aan deze werkruimte. De naamconventie voor de groep werkruimte en de resource zijn:

       Werkruimte: DefaultWorkspace-[abonnement-ID]-[geo]

       Resourcegroep: DefaultResouceGroup-[geo]
- installeren van een oplossing voor het Beveiligingscentrum in de werkruimte

De locatie van de werkruimte is gebaseerd op de locatie van de virtuele machine. Zie voor meer informatie, [gegevensbeveiliging](security-center-data-security.md).

> [!NOTE]
> Security Center verzameld beveiligingsgegevens van uw virtuele machines met behulp van de Azure Monitoring Agent vóór de migratie van platform, en gegevens zijn opgeslagen in uw opslagaccount. Na de migratie platform Security Center maakt gebruik van de Microsoft Monitoring Agent en de werkruimte voor het verzamelen en opslaan van de dezelfde gegevens. Het opslagaccount kan worden verwijderd na de migratie.
>
>

### <a name="am-i-billed-for-log-analytics-or-oms-on-the-workspaces-created-by-security-center"></a>Ben ik gefactureerd voor logboekanalyse of OMS op de werkruimten die zijn gemaakt door Security Center?
Nee. Werkruimten die zijn gemaakt door Security Center terwijl geconfigureerd voor OMS per knooppunt financieel medewerkers, komen niet OMS worden kosten in rekening. Security Center facturering is altijd op basis van het beveiligingsbeleid van uw Security Center en de oplossingen die zijn geïnstalleerd op een werkruimte:

- **Gratis laag** – Security Center installeert de oplossing 'SecurityCenterFree' op de standaardwerkruimte. U wordt niet gefactureerd voor de laag gratis.
- **Standard-laag** – Security Center installeert de oplossingen 'SecurityCenterFree' en 'Security' op de standaardwerkruimte.

Zie voor meer informatie over prijzen [Security Center prijzen](https://azure.microsoft.com/pricing/details/security-center/). Wijzigingen in de gegevensopslag van de beveiliging en naar rato facturering vanaf juni 2017 heeft betrekking op de pagina met prijzen.

> [!NOTE]
> De prijscategorie van de werkruimten die zijn gemaakt door Security Center OMS heeft geen invloed op de facturering Security Center.
>
>

### <a name="can-i-delete-the-default-workspaces-created-by-security-center"></a>Kan ik de Standaardwerkruimten die zijn gemaakt door Security Center verwijderen?
**Verwijderen van de standaardwerkruimte wordt niet aanbevolen.** De Standaardwerkruimten Security Center gebruikt voor het opslaan van beveiligingsgegevens van uw virtuele machines.  Als u een werkruimte verwijdert, Security Center kan niet voor het verzamelen van deze gegevens en enkele aanbevelingen voor beveiliging en waarschuwingen zijn niet beschikbaar

Als u wilt herstellen, verwijder Microsoft Monitoring Agent op de virtuele machines verbonden met de verwijderde werkruimte. Security Center de agent opnieuw installeren en nieuwe Standaardwerkruimten maken.

### <a name="what-if-the-microsoft-monitoring-agent-was-already-installed-as-an-extension-on-the-vm"></a>Wat gebeurt er als dat Microsoft Monitoring Agent al is geïnstalleerd als een uitbreiding op de virtuele machine?
Security Center wordt de bestaande verbindingen met werkruimten van de gebruiker niet overschreven. Security Center slaat beveiligingsgegevens van de virtuele machine in de werkruimte al verbonden.

### <a name="what-if-i-had-a-microsoft-monitoring-agent-installed-on-the-machine-but-not-as-an-extension"></a>Wat gebeurt er als ik een Microsoft Monitoring Agent geïnstalleerd op de computer, maar niet als een uitbreiding hebt gehad?
Als u Microsoft Monitoring Agent is geïnstalleerd rechtstreeks op de VM (niet als een Azure-extensie), de Security Center Microsoft Monitoring Agent wordt niet geïnstalleerd en beveiligingsbewaking worden beperkt.

### <a name="what-is-the-impact-of-removing-these-extensions"></a>Wat zijn de gevolgen van het verwijderen van deze uitbreidingen?
Als u de extensie van Microsoft Monitoring verwijdert, kan geen Security Center voor het verzamelen van beveiligingsgegevens van de virtuele machine en een aantal aanbevelingen voor beveiliging en waarschuwingen zijn niet beschikbaar. Security Center bepaalt binnen 24 uur, dat de virtuele machine de extensie ontbreekt is. vervolgens wordt de extensie.

### <a name="how-do-i-stop-the-automatic-agent-installation-and-workspace-creation"></a>Hoe voorkom ik het automatische agent-installatie en werkruimte maken
U kunt verzamelen van gegevens uitschakelen voor uw abonnementen in het beveiligingsbeleid, maar dit wordt niet aanbevolen. Het uitschakelen van verzameling gegevenslimieten Security Center aanbevelingen en waarschuwingen. Verzamelen van gegevens is vereist voor abonnementen op de Standard-prijscategorie. Verzamelen van gegevens uitschakelen:

1. Als uw abonnement is geconfigureerd voor de prijscategorie Standard, opent u het beveiligingsbeleid voor dat abonnement en selecteer de **vrije** laag.

   ![Prijscategorie][1]

2. Gegevensverzameling vervolgens uitschakelen door het selecteren van **uit** op de **beveiligingsbeleid – gegevensverzameling** blade.

   ![Gegevensverzameling][2]

### <a name="how-do-i-remove-oms-extensions-installed-by-security-center"></a>Hoe verwijder ik OMS-serverextensies geïnstalleerd door Security Center?
U kunt Microsoft Monitoring Agent handmatig verwijderen. Dit wordt niet aanbevolen omdat deze wordt beperkt door Security Center aanbevelingen en waarschuwingen.

> [!NOTE]
> Als gegevensverzameling is ingeschakeld, wordt Security Center de agent opnieuw nadat u deze verwijderen.  U moet uitschakelen van gegevensverzameling voordat de agent handmatig te verwijderen. Zie [hoe stopt het automatische agent-installatie en werkruimte maken?](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?) voor instructies over het verzamelen van gegevens uitschakelen.
>
>

De agent handmatig verwijderen:

1.  Open in de portal **logboekanalyse**.
2.  Selecteer op de blade Log Analytics een werkruimte:
3.  Selecteer elke VM die u niet wilt bewaken en selecteer **Disconnect**.

   ![De agent verwijderen][3]

> [!NOTE]
> Als een Linux-VM is al een niet-extensie OMS-agent, evenals de agent verwijderen van de extensie verwijdert en de klant heeft opnieuw te installeren.
>
>

## <a name="existing-oms-customers"></a>Bestaande OMS-klanten

### <a name="does-security-center-override-any-existing-connections-between-vms-and-workspaces"></a>Wordt de bestaande verbindingen tussen virtuele machines en werkruimten overschreven door Security Center?
Als een virtuele machine al Microsoft Monitoring Agent geïnstalleerd als een Azure-extensie, wordt de bestaande verbinding in de werkruimte niet overschreven door Security Center. Security Center gebruikt in plaats daarvan de bestaande werkruimte.

Een oplossing Security Center is geïnstalleerd op de werkruimte als dat niet al aanwezig, en de oplossing wordt alleen toegepast op de relevante virtuele machines. Wanneer u een oplossing toevoegt, wordt het automatisch naar alle Windows- en Linux-agents verbonden met uw werkruimte voor logboekanalyse standaard geïmplementeerd. [Oplossing Targeting](../operations-management-suite/operations-management-suite-solution-targeting.md), namelijk een OMS-functie kunt u een bereik van toepassing op uw oplossingen.

Als u Microsoft Monitoring Agent rechtstreeks op de VM (niet als een Azure-extensie) is geïnstalleerd, wordt Microsoft Monitoring Agent wordt niet geïnstalleerd door Security Center en beveiligingsbewaking is beperkt.

### <a name="what-should-i-do-if-i-suspect-that-the-data-platform-migration-broke-the-connection-between-one-of-my-vms-and-my-workspace"></a>Wat moet ik doen als ik vermoedt dat de gegevensmigratie platform de verbinding tussen een van mijn VM's en mijn werkruimte heeft?
Dit vindt niet plaats. Als deze, klikt u vervolgens voordoet [maken van een aanvraag voor de ondersteuning van Azure](../azure-supportability/how-to-create-azure-support-request.md) en bevatten de volgende details:

- De Azure-resource-ID van de betrokken virtuele machine
- De Azure-resource-ID van de werkruimte op de extensie geconfigureerd voordat de verbinding verbroken is
- De agent en de versie die eerder is geïnstalleerd

### <a name="does-security-center-install-solutions-on-my-existing-oms-workspaces-what-are-the-billing-implications"></a>Security Center wordt geïnstalleerd oplossingen op mijn bestaande OMS-werkruimten? Wat zijn de gevolgen voor de facturering?
Als Beveiligingscentrum identificeert dat een virtuele machine al is verbonden met een werkruimte die u hebt gemaakt, kunt Security Center-oplossingen voor deze werkruimte volgens uw prijscategorie. De oplossingen worden alleen toegepast op de relevante Azure VM's [oplossing targeting](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting), zodat de facturering hetzelfde is gebleven.

- **Gratis laag** – Security Center installeert de oplossing 'SecurityCenterFree' in de werkruimte. U wordt niet gefactureerd voor de laag gratis.
- **Standard-laag** – Security Center installeert de oplossingen 'SecurityCenterFree' en 'Security' in de werkruimte.

   ![Oplossingen op standaardwerkruimte][4]

> [!NOTE]
> De oplossing 'Security' in logboekanalyse is de beveiliging en Audit oplossing in OMS.
>
>

### <a name="i-already-have-workspaces-in-my-environment-can-i-use-them-to-collect-security-data"></a>Ik heb al werkruimten in de omgeving, kan ik ermee voor het verzamelen van beveiligingsgegevens?
Als een virtuele machine al Microsoft Monitoring Agent geïnstalleerd als een Azure-extensie, wordt in Security Center maakt gebruik van de bestaande verbonden werkruimte. Een oplossing Security Center is geïnstalleerd op de werkruimte als dat niet al aanwezig, en de oplossing wordt alleen toegepast op de relevante virtuele machines via [oplossing doelen](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting).

Security Center wordt Microsoft Monitoring Agent geïnstalleerd op virtuele machines, wordt de standaard workspace(s) gemaakt door Security Center gebruikt. Klanten wordt binnenkort configureren welke workspace(s) worden gebruikt.

### <a name="i-already-have-security-solution-on-my-workspaces-what-are-the-billing-implications"></a>Ik heb al beveiligingsoplossing op mijn werkruimten. Wat zijn de gevolgen voor de facturering?
De beveiliging en Audit-oplossing wordt gebruikt om Security Center Standard-laag functies inschakelen voor Azure Virtual machines. Als de beveiliging en Audit-oplossing is al geïnstalleerd op een werkruimte, maakt de bestaande oplossing voor het gebruik van Security Center. Er is geen wijziging in de facturering.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over de migratie Security Center-platform.

- [Migratie van Azure Security Center-Platform](security-center-platform-migration.md)
- [Handleiding voor probleemoplossing voor Azure Security Center](security-center-troubleshooting-guide.md)

<!--Image references-->
[1]: ./media/security-center-platform-migration-faq/pricing-tier.png
[2]: ./media/security-center-platform-migration-faq/data-collection.png
[3]: ./media/security-center-platform-migration-faq/remove-the-agent.png
[4]: ./media/security-center-platform-migration-faq/solutions.png
