---
title: aaaAzure Security Center Veelgestelde vragen (FAQ) | Microsoft Docs
description: Deze Veelgestelde vragen over de antwoorden op vragen over Azure Security Center.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: be2ab6d5-72a8-411f-878e-98dac21bc5cb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: cd0c0f8bdf15cdaf5889f2da5ac3cadf6017a9e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-frequently-asked-questions-faq"></a>Veelgestelde vragen over Azure Security Center
Deze Veelgestelde vragen over de antwoorden op vragen over Azure Security Center, een service waarmee u detecteren, voorkomen van en reageren toothreats met verhoogde zichtbaarheid van en controle over Hallo beveiliging van uw Microsoft Azure-resources.

> [!NOTE]
> Begin juni 2017 vanaf kan Security Center Hallo Microsoft Monitoring Agent toocollect gebruiken en opslaan van gegevens. toolearn meer, Zie [Azure Security Center-Platform migratie](security-center-platform-migration.md). Hallo-informatie in dit artikel beschrijft Security Center functionaliteit na de overgang toohello Microsoft Monitoring Agent.
>
>

## <a name="general-questions"></a>Algemene vragen
### <a name="what-is-azure-security-center"></a>Wat is Azure Security Center?
Azure Security Center helpt u bij het detecteren, voorkomen van en reageren toothreats met verhoogde zichtbaarheid van en controle over Hallo beveiliging van uw Azure-resources. Het biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw abonnementen, helpt bedreigingen te detecteren die anders onopgemerkt zouden blijven, en werkt met een uitgebreid ecosysteem van beveiligingsoplossingen.

### <a name="how-do-i-get-azure-security-center"></a>Hoe krijg ik Azure Security Center?
Azure Security Center is met uw Microsoft Azure-abonnement ingeschakeld en is toegankelijk vanuit Hallo [Azure-portal](https://azure.microsoft.com/features/azure-portal/). ([Toohello portal aanmelden](https://portal.azure.com), selecteer **Bladeren**, en te schuiven**Security Center**).  

## <a name="billing"></a>Facturering
### <a name="how-does-billing-work-for-azure-security-center"></a>Hoe werkt facturering voor Azure Security Center?
Security Center wordt aangeboden in twee lagen:

Hallo **gratis laag** biedt inzicht in de beveiligingsstatus Hallo van uw Azure-resources, basic beveiligingsbeleid, aanbevelingen voor beveiliging en integratie met beveiligingsproducten en services van partners.

Hallo **standaardcategorie** geavanceerde threat detectiemogelijkheden, met inbegrip van dreiging intelligence, gedragsanalyse, afwijkingsdetectie, beveiligingsincidenten en daarmee rapporten dreiging wordt toegevoegd. Hallo standaardcategorie is gratis voor Hallo eerste 60 dagen. Moet u kiezen toocontinue toouse Hallo-service na 60 dagen, we toocharge voor Hallo service automatisch gestart.  tooupgrade, selecteer prijscategorie in Hallo [beveiligingsbeleid](security-center-policies.md#set-security-policies). toolearn meer, Zie [Security Center prijzen](security-center-pricing.md).

## <a name="permissions"></a>Machtigingen
Maakt gebruik van Azure Security Center [op rollen gebaseerde toegangsbeheer (RBAC)](../active-directory/role-based-access-control-configure.md), waarmee u [ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md) die kunnen worden toegewezen toousers, groepen en services in Azure.

Security Center beoordeelt Hallo-configuratie van uw resources tooidentify beveiligingsproblemen en beveiligingsproblemen. In Security Center, ziet u alleen informatie gerelateerd tooa resource wanneer u Hallo rol van eigenaar, bijdrager of lezer Hallo abonnement of resourcegroep beheergroep die deel uitmaakt van een resource te worden toegewezen.

Zie [machtigingen in Azure Security Center](security-center-permissions.md) toolearn meer over de functies en de toegestane acties in Security Center.

## <a name="data-collection"></a>Gegevensverzameling
Security Center verzamelt gegevens van uw virtuele machines tooassess hun beveiligingsstatus, aanbevelingen voor beveiliging bieden en waarschuwt u toothreats. Wanneer u Security Center voor het eerst opent, worden gegevensverzameling is ingeschakeld op alle virtuele machines in uw abonnement. U kunt ook verzamelen van gegevens in Hallo Security Center-beleid inschakelen.

### <a name="how-do-i-disable-data-collection"></a>Hoe kan ik gegevens verzamelen uitschakelen?
Als u van Azure Security Center gratis laag hello gebruikmaakt, kunt u het verzamelen van gegevens van virtuele machines op elk gewenst moment uitschakelen. Verzamelen van gegevens is vereist voor abonnementen op Hallo Standard-laag. U kunt het verzamelen van gegevens voor een abonnement in Hallo beveiligingsbeleid uitschakelen. ([Toohello Azure-portal aanmelden](https://portal.azure.com), selecteer **Bladeren**, selecteer **Security Center**, en selecteer **beleid**.)  Wanneer u een abonnement selecteren, een nieuwe blade geopend en biedt u de optie tooturn Hallo uit **gegevensverzameling**.

### <a name="how-do-i-enable-data-collection"></a>Hoe kan ik gegevensverzameling inschakelen?
U kunt de gegevensverzameling inschakelen voor uw Azure-abonnement in Hallo beveiligingsbeleid. tooenable gegevensverzameling. [Meld u aan toohello Azure-portal](https://portal.azure.com), selecteer **Bladeren**, selecteer **Security Center**, en selecteer **beleid**. Stel **gegevensverzameling** te**op**.

### <a name="what-happens-when-data-collection-is-enabled"></a>Wat gebeurt er wanneer gegevensverzameling is ingeschakeld?
Wanneer gegevensverzameling is ingeschakeld, Hallo Microsoft Monitoring Agent automatisch geconfigureerd zijn op alle bestaande en nieuw ondersteunde virtuele machines die zijn geïmplementeerd in het Hallo-abonnement.

### <a name="does-hello-monitoring-agent-impact-hello-performance-of-my-servers"></a>Ondersteunt Hallo Monitoring Agent impact Hallo prestaties van mijn servers?
Hallo-agent een nominaal hoeveelheid systeembronnen verbruikt en moet weinig invloed hebben op prestaties Hallo. Zie voor meer informatie over de gevolgen voor de prestaties en Hallo agent en -extensie Hallo [plannen en de operations guide](security-center-planning-and-operations-guide.md#data-collection-and-storage).

### <a name="where-is-my-data-stored"></a>Waar worden mijn gegevens opgeslagen?
Gegevens die worden verzameld van deze agent wordt opgeslagen in een bestaande werkruimte voor logboekanalyse gekoppeld aan uw abonnement of een nieuwe werkruimte. Zie voor meer informatie [gegevensbeveiliging](security-center-data-security.md).

## <a name="using-azure-security-center"></a>Met behulp van Azure Security Center
### <a name="what-is-a-security-policy"></a>Wat is beveiligingsbeleid?
Een beveiligingsbeleid bepaalt Hallo set besturingselementen die worden aanbevolen voor resources binnen Hallo opgegeven abonnement. In Azure Security Center definieert u beleid voor uw Azure-abonnementen op basis van het bedrijf tooyour beveiligingsvereisten en Hallo type toepassingen of de vertrouwelijkheid van gegevens in elk abonnement Hallo.

Hallo-beveiligingsbeleid is ingeschakeld in Azure Security Center station beveiligingsaanbevelingen en bewaking. toolearn meer informatie over beveiligingsbeleid, Zie [beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md).

### <a name="who-can-modify-a-security-policy"></a>Wie kan een beveiligingsbeleid wijzigen?
toomodify een beveiligingsbeleid, moet u een beveiligingsbeheerder of een eigenaar of bijdrager van het abonnement.

hoe een beveiligingsbeleid tooconfigure zien toolearn [beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md).

### <a name="what-is-a-security-recommendation"></a>Wat is een beveiligingsaanbeveling?
Azure Security Center analyseert de beveiligingsstatus Hallo van uw Azure-resources. Als mogelijke beveiligingsproblemen worden geïdentificeerd, worden aanbevelingen gemaakt. Hallo aanbevelingen handleiding u door Hallo configuratieproces Hallo besturingselement nodig. Voorbeelden zijn:

* Inrichting van antimalware toohelp identificeren en te verwijderen van schadelijke software
* Configureren van [Netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md) en toocontrol verkeer toovirtual machines regels
* Het inrichten van een web application firewall toohelp beschermen tegen aanvallen die gericht is op uw webtoepassingen
* Implementatie van ontbrekende systeemupdates
* Aanpassing van besturingssysteemconfiguraties die niet overeenkomen met de Hallo aanbevolen basislijnen

Alleen de aanbevelingen die zijn ingeschakeld in het beveiligingsbeleid worden hier weergegeven.

### <a name="how-can-i-see-hello-current-security-state-of-my-azure-resources"></a>Hoe kan ik Hallo huidige beveiligingsstatus van mijn Azure-resources zien?
Hallo **Security Center Overview** blade ziet Hallo algehele beveiligingsstatus van uw omgeving uitgesplitst Compute, netwerken, opslag en gegevens en toepassingen. Elk resourcetype heeft een indicator weergeeft als alle mogelijke beveiligingsproblemen zijn geïdentificeerd. Elke tegel te klikken, geeft een lijst met beveiligingsproblemen die zijn geïdentificeerd door Security Center, samen met een inventaris van Hallo resources in uw abonnement.

### <a name="what-triggers-a-security-alert"></a>Wat wordt een beveiligingswaarschuwing geactiveerd?
Azure Security Center automatisch verzamelt, analyseert en worden de logboekgegevens van uw Azure-resources, het Hallo-netwerk en partneroplossingen zoals antimalware en firewalls. Wanneer er dreigingen worden gedetecteerd, wordt een beveiligingswaarschuwing gemaakt. Voorbeelden zijn detectie van:

* Geïnfecteerde virtuele machines die communiceren met bekende schadelijke IP-adressen
* Geavanceerde malware is gedetecteerd met Windows Foutrapportage
* Beveiligingsaanvallen op virtuele machines
* Beveiligingswaarschuwingen van geïntegreerde partneroplossingen beveiliging zoals Anti-Malware of Web Application Firewalls

### <a name="whats-hello-difference-between-threats-detected-and-alerted-on-by-microsoft-security-response-center-versus-azure-security-center"></a>Wat is Hallo verschil tussen bedreigingen gedetecteerd en een melding op door de Microsoft Security Response Center versus Azure Security Center?
Hallo Microsoft Security Response Center (MSRC) voert selecteert u beveiliging hello Azure-netwerk en infrastructuur bewaken en threat intelligence en misbruik klachten ontvangt van een derde partij. Als MSRC erg op de hoogte dat gegevens van de klant is geopend door een partij onrechtmatig of niet-geautoriseerde Hallo klant gebruik van Azure voldoet niet aan de voorwaarden Hallo voor acceptabel gebruik, waarschuwt een incident beveiligingsbeheer Hallo klant. Melding treedt meestal op door te sturen een e-mail toohello beveiliging contactpersonen die zijn opgegeven in Azure Security Center of Hallo de eigenaar van Azure-abonnement als een contactpersoon beveiliging is niet opgegeven.

Security Center is een Azure-service die continu bewaakt van de klant hello Azure-omgeving en analytics tooautomatically geldt een groot aantal mogelijk schadelijke activiteiten detecteren. Deze detecties worden opgehaald als beveiligingswaarschuwingen in Hallo Security Center-dashboard.

### <a name="which-azure-resources-are-monitored-by-azure-security-center"></a>Welke Azure-resources worden bewaakt door Azure Security Center?
Azure Security Center monitors hello Azure-resources te volgen:

* Virtuele machines (VM's) (met inbegrip van [Cloudservices](../cloud-services/cloud-services-choose-me.md))
* Virtuele netwerken van Azure
* Azure SQL-service
* Azure-opslagaccount
* Azure-Web-Apps (in [App Service-omgeving](../app-service/app-service-app-service-environments-readme.md))
* Partneroplossingen die zijn geïntegreerd met uw Azure-abonnement zoals web application firewall op virtuele machines en klik op [App Service-omgeving](../app-service/app-service-app-service-environments-readme.md)

## <a name="virtual-machines"></a>Virtuele machines
### <a name="what-types-of-virtual-machines-are-supported"></a>Welke typen virtuele machines worden ondersteund?
Bewaking en aanbevelingen zijn beschikbaar voor virtuele machines (VM's) gemaakt met behulp van beide Hallo [klassieke en Resource Manager-implementatiemodel](../azure-classic-rm.md).

Zie [ondersteunde platforms in Azure Security Center](security-center-os-coverage.md) voor een lijst met ondersteunde platforms.

### <a name="why-doesnt-azure-security-center-recognize-hello-antimalware-solution-running-on-my-azure-vm"></a>Waarom niet Azure Security Center wordt herkend door Hallo anti-malwareoplossing op mijn Azure VM?
Azure Security Center heeft zichtbaarheid van antimalware geïnstalleerd via de Azure-extensies. Security Center is bijvoorbeeld niet kunnen toodetect antimalware die vooraf geïnstalleerd op een installatiekopie die u hebt opgegeven of is als u anti-malware op uw virtuele machines met uw eigen processen (zoals systemen voor Configuratiebeheer) hebt geïnstalleerd.

### <a name="why-do-i-get-hello-message-missing-scan-data-for-my-vm"></a>Waarom krijg ik het Hallo-bericht 'Missing scannen Data' voor mijn VM?
Dit bericht wordt weergegeven wanneer er geen Scangegevens voor een virtuele machine zijn. Het kan even duren (minder dan een uur) voor de scan gegevens toopopulate nadat gegevensverzameling is ingeschakeld in Azure Security Center. Na het Hallo initiële gegevenspopulatie scan wordt dit bericht omdat er helemaal geen Scangegevens zijn of er geen recente Scangegevens zijn. Scans vullen voor een virtuele machine gestopt. Dit bericht kan ook optreden als Scangegevens heeft onlangs (in overeenstemming met het bewaarbeleid Hallo voor de agent Windows hello, waarvoor een standaardperiode van 30 dagen) niet is ingevuld.

### <a name="why-do-i-get-hello-message-vm-agent-is-missing"></a>Waarom krijg ik het Hallo-bericht 'VM-Agent is ontbreekt?'
Hallo VM-Agent moet worden geïnstalleerd op virtuele machines tooenable verzamelen van gegevens. Hallo VM-Agent wordt standaard geïnstalleerd voor virtuele machines die vanuit Azure Marketplace Hallo worden geïmplementeerd. Zie voor informatie over hoe tooinstall Hallo VM-Agent op andere virtuele machines, Hallo blogbericht [VM-Agent en -extensies](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/).
