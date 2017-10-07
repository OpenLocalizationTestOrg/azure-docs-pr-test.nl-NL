---
title: migratie van de platforms aaaSecurity Center Veelgestelde vragen | Microsoft Docs
description: Deze Veelgestelde vragen over de antwoorden op vragen over hello Azure Beveiligingscentrum platform migratie.
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
ms.openlocfilehash: fcb14ae83167ef79a60371e4fcb625cf99bee6c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-center-platform-migration-faq"></a>Security Center-platform migratie Veelgestelde vragen
In eerdere juni 2017 begon Azure Security Center met behulp van toocollect en store-gegevens van Microsoft Monitoring Agent Hallo. toolearn meer, Zie [Azure Security Center-Platform migratie](security-center-platform-migration.md). Deze Veelgestelde vragen over de antwoorden op vragen over de migratie van Hallo-platform.

## <a name="data-collection-agents-and-workspaces"></a>Verzamelen van gegevens, agents en werkruimten

### <a name="how-is-data-collected"></a>Hoe worden gegevens verzameld
Security Center gebruikt Hallo Microsoft Monitoring Agent toocollect beveiligingsgegevens van uw virtuele machines. Hallo beveiligingsgegevens bevat informatie over beveiligingsconfiguraties die gebruikte tooidentify beveiligingsproblemen, en beveiligingsgebeurtenissen, de gebruikte toodetect bedreigingen. Gegevens die worden verzameld door Hallo-agent wordt opgeslagen in een bestaande toohello Log Analytics-werkruimte verbonden VM of een nieuwe werkruimte gemaakt door Security Center. Wanneer Security Center een nieuwe werkruimte maakt, Hallo geolocatie Hallo VM is in aanmerking genomen.

> [!NOTE]
> Hallo Microsoft Monitoring Agent is Hallo dezelfde agent die wordt gebruikt door Hallo Operations Management Suite (OMS), Log Analytics-service en System Center Operations Manager (SCOM).
>
>

Wanneer gegevensverzameling is ingeschakeld voor Hallo eerst of uw abonnementen die worden gemigreerd, controleert Security Center toosee als Hallo Microsoft Monitoring Agent is al geïnstalleerd als een Azure-extensie op elk van uw virtuele machines. Als Hallo Microsoft Monitoring Agent niet is geïnstalleerd, is Security Center wordt uitgevoerd:

- Hallo Microsoft Monitoring agent installeren op Hallo VM
   - Als een werkruimte gemaakt door Security Center al in dezelfde geolocatie bestaat als virtuele machine, Hallo HALLO hallo is agent verbonden toothis werkruimte
   - Als een werkruimte niet bestaat, Security Center maakt een nieuwe resourcegroep standaard werkruimte in die geolocatie en verbinding maken met de Hallo agent toothat werkruimte. Hallo naamgevingsconventie voor Hallo werkruimte en resource-groep zijn:

       Werkruimte: DefaultWorkspace-[abonnement-ID]-[geo]

       Resourcegroep: DefaultResouceGroup-[geo]
- installeren van een oplossing Security Center op Hallo-werkruimte

locatie van de werkruimte Hallo Hallo is gebaseerd op locatie Hallo Hallo VM. toolearn meer, Zie [gegevensbeveiliging](security-center-data-security.md).

> [!NOTE]
> Migratie van eerdere tooplatform Security Center verzameld beveiligingsgegevens van uw virtuele machines met behulp van hello Azure Monitoring Agent en gegevens zijn opgeslagen in uw opslagaccount. Security Center gebruikt Hallo Microsoft Monitoring Agent en werkruimte toocollect en store Hallo dezelfde gegevens na de migratie van Hallo-platform. Hallo storage-account kan worden verwijderd na de migratie Hallo.
>
>

### <a name="am-i-billed-for-log-analytics-or-oms-on-hello-workspaces-created-by-security-center"></a>Ben ik gefactureerd voor logboekanalyse of OMS op Hallo werkruimten die zijn gemaakt door Security Center?
Nee. Werkruimten die zijn gemaakt door Security Center terwijl geconfigureerd voor OMS per knooppunt financieel medewerkers, komen niet OMS worden kosten in rekening. Security Center facturering is altijd gebaseerd op uw Security Center-beleid en Hallo beveiligingsoplossingen geïnstalleerd op een werkruimte:

- **Gratis laag** – Security Center Hallo 'SecurityCenterFree' oplossing op Hallo standaardwerkruimte geïnstalleerd. U wordt niet gefactureerd voor Hallo gratis laag.
- **Standard-laag** : Security Center installeert Hallo 'SecurityCenterFree' en 'Security' oplossingen op Hallo standaardwerkruimte.

Zie voor meer informatie over prijzen [Security Center prijzen](https://azure.microsoft.com/pricing/details/security-center/). Hallo prijzen pagina adressen verandert toosecurity gegevensopslag en naar rato facturering vanaf juni 2017.

> [!NOTE]
> Hallo OMS-prijscategorie van de werkruimten die zijn gemaakt door Security Center heeft geen invloed op de facturering Security Center.
>
>

### <a name="can-i-delete-hello-default-workspaces-created-by-security-center"></a>Kan ik Hallo Standaardwerkruimten gemaakt door Security Center verwijderen?
**Hallo standaardwerkruimte verwijderen wordt niet aanbevolen.** Security Center gebruikt Hallo standaard werkruimten toostore beveiligingsgegevens van uw virtuele machines.  Als u een werkruimte Security Center verwijdert toocollect niet kan deze gegevens en enkele aanbevelingen voor beveiliging en waarschuwingen zijn niet beschikbaar

toorecover, verwijder Hallo Microsoft Monitoring Agent op Hallo virtuele machines verbonden toohello verwijderd werkruimte. Security Center Hallo-agent opnieuw installeren en nieuwe Standaardwerkruimten maken.

### <a name="what-if-hello-microsoft-monitoring-agent-was-already-installed-as-an-extension-on-hello-vm"></a>Wat gebeurt er als dat Hallo Microsoft Monitoring Agent al is geïnstalleerd als een uitbreiding op Hallo VM?
Security Center wordt de bestaande verbindingen toouser werkruimten niet overschreven. Security Center winkels beveiligingsgegevens van virtuele machine in de werkruimte Hallo Hallo al verbonden.

### <a name="what-if-i-had-a-microsoft-monitoring-agent-installed-on-hello-machine-but-not-as-an-extension"></a>Wat gebeurt er als ik een Microsoft Monitoring Agent geïnstalleerd op machine Hallo maar niet als een uitbreiding hebt gehad?
Als Hallo Microsoft Monitoring Agent is geïnstalleerd, rechtstreeks op Hallo VM (niet als een Azure-extensie), Security Center kan niet worden geïnstalleerd Hallo Microsoft Monitoring Agent en beveiligingsbewaking worden beperkt.

### <a name="what-is-hello-impact-of-removing-these-extensions"></a>Wat is Hallo gevolgen van het verwijderen van deze uitbreidingen?
Als u een extensie voor Microsoft Monitoring Hallo verwijdert, Security Center is niet kunnen toocollect beveiligingsgegevens van Hallo VM en enkele aanbevelingen voor beveiliging en waarschuwingen zijn niet beschikbaar. Binnen 24 uur bepaalt Security Center dat Hallo VM Hallo-extensie ontbreekt en worden opnieuw geïnstalleerd Hallo extensie.

### <a name="how-do-i-stop-hello-automatic-agent-installation-and-workspace-creation"></a>Hoe voorkom ik Hallo automatische-agentinstallatie en -werkruimte maken
U kunt verzamelen van gegevens uitschakelen voor uw abonnementen in het beveiligingsbeleid hello, maar dit wordt niet aanbevolen. Het uitschakelen van verzameling gegevenslimieten Security Center aanbevelingen en waarschuwingen. Verzamelen van gegevens is vereist voor abonnementen op Hallo standaardcategorie prijzen. toodisable gegevens verzamelen:

1. Als uw abonnement is geconfigureerd voor de standaardcategorie hello, open Hallo beveiligingsbeleid voor dat abonnement en selecteer Hallo **vrije** laag.

   ![Prijscategorie][1]

2. Gegevensverzameling vervolgens uitschakelen door het selecteren van **uit** op Hallo **beveiligingsbeleid – gegevensverzameling** blade.

   ![Gegevensverzameling][2]

### <a name="how-do-i-remove-oms-extensions-installed-by-security-center"></a>Hoe verwijder ik OMS-serverextensies geïnstalleerd door Security Center?
U kunt Microsoft Monitoring Agent Hallo handmatig verwijderen. Dit wordt niet aanbevolen omdat deze wordt beperkt door Security Center aanbevelingen en waarschuwingen.

> [!NOTE]
> Als gegevensverzameling is ingeschakeld, wordt Security Center Hallo-agent opnieuw nadat u deze verwijderen.  U moet de gegevensverzameling toodisable voordat het Hallo-agent handmatig te verwijderen. Zie [hoe stoppen Hallo automatische agent-installatie- en werkruimte maken?](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?) voor instructies over het verzamelen van gegevens uitschakelen.
>
>

toomanually Hallo-agent verwijderen:

1.  Open in de portal Hallo **logboekanalyse**.
2.  Selecteer een werkruimte op Hallo logboekanalyse blade:
3.  Selecteer elke VM die u niet wilt dat toomonitor en selecteer **Disconnect**.

   ![Hallo-agent verwijderen][3]

> [!NOTE]
> Als een Linux-VM is al een niet-extensie OMS-agent, ook Hallo-agent verwijderen van extensie Hallo verwijdert en Hallo klant heeft tooreinstall deze.
>
>

## <a name="existing-oms-customers"></a>Bestaande OMS-klanten

### <a name="does-security-center-override-any-existing-connections-between-vms-and-workspaces"></a>Wordt de bestaande verbindingen tussen virtuele machines en werkruimten overschreven door Security Center?
Als een virtuele machine al Hallo Microsoft Monitoring Agent is geïnstalleerd als een Azure-extensie, wordt in Security Center Hallo bestaande werkruimte verbinding niet overschrijven. Security Center gebruikt in plaats daarvan bestaande Hallo-werkruimte.

Een oplossing Security Center is geïnstalleerd op Hallo werkruimte als dat niet al aanwezig, en Hallo oplossing toegepaste alleen toohello relevante virtuele machines. Wanneer u een oplossing toevoegt, wordt deze automatisch geïmplementeerd door standaard tooall Windows en Linux-agents verbonden tooyour werkruimte voor logboekanalyse. [Oplossing Targeting](../operations-management-suite/operations-management-suite-solution-targeting.md), namelijk een OMS-functie kunt u een scope tooapply tooyour oplossingen.

Als Hallo Microsoft Monitoring Agent is geïnstalleerd, rechtstreeks op Hallo VM (niet als een Azure-extensie), Security Center kan niet worden geïnstalleerd Hallo Microsoft Monitoring Agent en beveiligingsbewaking is beperkt.

### <a name="what-should-i-do-if-i-suspect-that-hello-data-platform-migration-broke-hello-connection-between-one-of-my-vms-and-my-workspace"></a>Wat moet ik doen als ik vermoedt dat Hallo platform gegevensmigratie heeft overschreden Hallo verbinding tussen een van mijn VM's en mijn werkruimte?
Dit vindt niet plaats. Als deze, klikt u vervolgens voordoet [maken van een aanvraag voor de ondersteuning van Azure](../azure-supportability/how-to-create-azure-support-request.md) en opnemen Hallo volgende details:

- Hello Azure-resource-ID van Hallo beïnvloed VM
- Hello Azure-resource-ID van Hallo werkruimte op Hallo-uitbreiding geconfigureerd voordat het Hallo-verbinding is verbroken
- Hallo-agent en de versie die eerder is geïnstalleerd

### <a name="does-security-center-install-solutions-on-my-existing-oms-workspaces-what-are-hello-billing-implications"></a>Security Center wordt geïnstalleerd oplossingen op mijn bestaande OMS-werkruimten? Wat zijn Hallo facturering gevolgen?
Wanneer Beveiligingscentrum identificeert een virtuele machine is al verbonden tooa werkruimte die u hebt gemaakt, Security Center kunt-oplossingen voor deze werkruimte op basis van tooyour prijscategorie. Hallo oplossingen toegepaste alleen toohello relevante virtuele machines in Azure, worden [oplossing targeting](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting), dus facturering blijft Hallo Hallo dezelfde.

- **Gratis laag** – Security Center Hallo 'SecurityCenterFree' oplossing installeert op Hallo-werkruimte. U wordt niet gefactureerd voor Hallo gratis laag.
- **Standard-laag** : Security Center installeert Hallo 'SecurityCenterFree' en 'Security' oplossingen op Hallo werkruimte.

   ![Oplossingen op standaardwerkruimte][4]

> [!NOTE]
> Hallo 'Security' oplossing in Log Analytics wordt Hallo beveiliging & Audit-oplossing in OMS.
>
>

### <a name="i-already-have-workspaces-in-my-environment-can-i-use-them-toocollect-security-data"></a>Ik heb al werkruimten in de omgeving, kan ik ermee toocollect beveiligingsgegevens?
Als een virtuele machine al Hallo Microsoft Monitoring Agent is geïnstalleerd als een Azure-extensie, Beveiligingscentrum Hallo bestaande verbonden werkruimte gebruikt. Een oplossing Security Center is geïnstalleerd op Hallo werkruimte als dat niet al aanwezig, en Hallo oplossing toegepaste alleen toohello relevante virtuele machines via [oplossing doelen](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting).

Wanneer het Beveiligingscentrum Hallo Microsoft Monitoring Agent is geïnstalleerd op virtuele machines, gebruikt het Hallo standaard workspace(s) gemaakt door Security Center. Klanten moeten snel kunnen tooconfigure welke workspace(s) worden gebruikt.

### <a name="i-already-have-security-solution-on-my-workspaces-what-are-hello-billing-implications"></a>Ik heb al beveiligingsoplossing op mijn werkruimten. Wat zijn Hallo facturering gevolgen?
Hallo beveiliging & Audit-oplossing is gebruikte tooenable Security Center Standard-laag functies voor virtuele Azure-machines. Als Hallo beveiliging & Audit-oplossing is al geïnstalleerd op een werkruimte, Beveiligingscentrum Hallo bestaande oplossing gebruikt. Er is geen wijziging in de facturering.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over Hallo Security Center-platform migratie, Zie

- [Migratie van Azure Security Center-Platform](security-center-platform-migration.md)
- [Handleiding voor probleemoplossing voor Azure Security Center](security-center-troubleshooting-guide.md)

<!--Image references-->
[1]: ./media/security-center-platform-migration-faq/pricing-tier.png
[2]: ./media/security-center-platform-migration-faq/data-collection.png
[3]: ./media/security-center-platform-migration-faq/remove-the-agent.png
[4]: ./media/security-center-platform-migration-faq/solutions.png
