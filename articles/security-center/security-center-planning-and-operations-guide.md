---
title: aaaSecurity plannings- en Bedieningsgids | Microsoft Docs
description: Dit document helpt u tooplan alvorens het Azure Beveiligingscentrum en overwegingen met betrekking tot de dagelijkse bewerkingen.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f984e4a2-ac97-40bf-b281-2f7f473494c4
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: b0a0a6f5fd56fbd46f7736928c99e3bcd0b1e140
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-planning-and-operations-guide"></a>Plannings- en bedieningsgids voor Azure Security Center
Deze handleiding is bedoeld voor IT-professionals (IT), IT-architecten, gegevensbeveiligingsanalisten en cloudbeheerders die willen gaan toouse Azure Security Center.

>[!NOTE] 
>Begin juni 2017 vanaf kan Security Center Hallo Microsoft Monitoring Agent toocollect gebruiken en opslaan van gegevens. Zie [Azure Security Center-Platform migratie](security-center-platform-migration.md) toolearn meer. Hallo-informatie in dit artikel beschrijft Security Center functionaliteit na de overgang toohello Microsoft Monitoring Agent.
>

## <a name="planning-guide"></a>Planningsgids
Deze handleiding bevat informatie over een reeks stappen en taken die u kunt uw gebruik van het Beveiligingscentrum op basis van de beveiligingsvereisten van uw organisatie en het cloudbeheermodel toooptimize volgen. tootake volledig gebruikmaken van Security Center, is belangrijk toounderstand hoe verschillende personen of teams in uw organisatie gebruiken Hallo service toomeet veilige ontwikkeling en gebruik, bewaking, bestuur en reactie op incidenten. Hallo sleutelgebieden tooconsider bij het plannen van toouse Security Center zijn:

* Beveiligingsrollen en toegangsbeheer
* Beveiligingsbeleid en aanbevelingen
* Gegevensverzameling en -opslag
* Continue beveiligingsbewaking
* Reageren op incidenten

In de volgende sectie hello, leert u hoe tooplan voor elk van deze gebieden en toepassen van deze aanbevelingen op basis van uw vereisten.

> [!NOTE]
> Lees [Azure Security Center Veelgestelde vragen (FAQ)](security-center-faq.md) voor een lijst met veelgestelde vragen die ook nuttig tijdens het Hallo zijn kunnen- en planningsfase ontwerpen.
> 

## <a name="security-roles-and-access-controls"></a>Beveiligingsrollen en toegangsbeheer
Afhankelijk van Hallo grootte en de structuur van uw organisatie, kunnen meerdere individuen en teams Security Center tooperform verschillende beveiligingstaken gebruiken. In het volgende diagram Hallo hebt u een voorbeeld van fictieve personen en hun respectieve rollen en beveiligingsverantwoordelijkheden:

![Rollen](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig01-new.png)

Security Center kunnen deze personen toomeet deze verschillende verantwoordelijkheden. Bijvoorbeeld:

**Jeff (eigenaar van workloads in de cloud)**

* Een cloud-workload en de bijbehorende resources beheren
* Verantwoordelijk voor het implementeren en onderhouden van beveiliging volgens het beveiligingsbeleid van het bedrijf

**Ellen (CISO/CIO)**

* Verantwoordelijk voor alle aspecten van beveiliging voor Hallo bedrijf
* Beveiligingspostuur toounderstand Hallo bedrijf wil via cloudwerkbelastingen
* Behoeften toobe op de hoogte van bekende aanvallen en risico 's

**David (IT-beveiliging)**

* Sets bedrijf beveiligingsbeleid tooensure Hallo juiste goed beveiligd wordt
* Bewaakt naleving van beleid
* Genereert rapporten voor leidinggevenden of auditors

**Judy (beveiligingsbewerkingen)**

* Bewaakt en reageert toosecurity waarschuwingen 24/7
* Escaleert tooCloud eigenaar of analist van IT-beveiliging

**Sam (beveiligingsanalist)**

* Onderzoekt aanvallen
* Werken met de eigenaar van de werkbelasting Cloud tooapply herstel 

Security Center gebruikt [op rollen gebaseerde toegangsbeheer (RBAC)](../active-directory/role-based-access-control-configure.md), waarmee u [ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md) die kunnen worden toegewezen toousers, groepen en services in Azure. Wanneer een gebruiker Beveiligingscentrum opent, zien ze alleen informatie gerelateerd tooresources ze toegang hebben. Wat betekent dat Hallo gebruiker Hallo-rol van eigenaar, bijdrager of lezer toohello abonnement of resourcegroep groep die een bron deel uitmaakt is toegewezen. In aanvulling toothese rollen zijn er twee specifieke Security Center-rollen:

- **Beveiliging lezer**: gebruiker die deel uitmaakt van de rol toothis worden kunnen tooview rechten tooSecurity Center, waaronder aanbevelingen, waarschuwingen, beleid en status, maar is pas kunnen toomake wijzigingen.
- **Beveiliging admin**: zelfde als lezer van de beveiliging, maar ook Hallo beveiligingsbeleid bijwerken kan, negeren aanbevelingen en waarschuwingen.

Hallo Security Center-functies die hierboven worden beschreven, hoeft geen toegang tooother servicegebieden van Azure zoals opslag, Web & mobiele of Internet der dingen.  

> [!NOTE]
> Er moet een gebruiker toobe ten minste een abonnement, resource group-eigenaar of bijdrager toobe kunnen toosee Security Center in Azure. 
> 
> 

Met behulp van Hallo Persona's toegelicht in Hallo vorige diagram Hallo volgende RBAC nodig zijn:

**Jeff (eigenaar van workloads in de cloud)**

* Resourcegroepeigenaar/medewerker

**David (IT-beveiliging)**

* Abonnementseigenaar/medewerker of beveiligingsbeheerder

**Judy (beveiligingsbewerkingen)**

* Abonnementslezer of beveiliging lezer tooview waarschuwingen
* Abonnementseigenaar/medewerker of beveiliging beheerder vereist toodismiss waarschuwingen

**Sam (beveiligingsanalist)**

* Abonnement lezer tooview waarschuwingen
* Abonnementseigenaar/medewerker vereist toodismiss waarschuwingen
* Toegang toohello werkruimte mogelijk vereist

Sommige andere belangrijke informatie tooconsider:

* Alleen abonnementseigenaren/medewerkers en beveiligingsbeheerders kunnen een beveiligingsbeleid bewerken
* Alleen abonnements- en resourcegroepeigenaren en bijdragers kunnen beveiligingsaanbevelingen voor een resource toepassen

Bij het plannen van toegangsbeheer met het RBAC voor Security Center worden ervoor toounderstand die in uw organisatie van Security Center gebruikmaakt. Ook moet u weten welke typen taken zij gaan uitvoeren en RBAC vervolgens dienovereenkomstig configureren.

> [!NOTE]
> Het is raadzaam dat u Hallo toewijst minimaal rol die nodig zijn voor gebruikers toocomplete hun taken. Gebruikers die alleen tooview informatie nodig over de beveiligingsstatus Hallo van resources, maar geen actie uitvoert, zoals het toepassen van aanbevelingen of het bewerken van beleid, moeten bijvoorbeeld de rol Lezer Hallo toegewezen.
> 
> 

## <a name="security-policies-and-recommendations"></a>Beveiligingsbeleid en aanbevelingen
Een beveiligingsbeleid bepaalt Hallo set besturingselementen wordt aanbevolen voor resources binnen Hallo opgegeven abonnement. In Security Center definieert u beleid op basis van tooyour en van het bedrijf beveiligingsvereisten Hallo type toepassingen of vertrouwelijkheid van gegevens Hallo.

Beleidsregels die zijn ingeschakeld op het abonnementsniveau Hallo automatisch doorgegeven tooall resourcegroepen binnen Hallo abonnement zoals weergegeven in het volgende diagram Hallo:

![Beveiligingsbeleid](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig2-newUI.png)

> [!NOTE]
> Als u tooreview welke beleidsregels zijn gewijzigd moet, kunt u [Azure controlelogboeken](https://blogs.msdn.microsoft.com/cloud_solution_architect/2015/03/10/audit-logs-for-azure-events/). Beleidswijzigingen worden altijd geregistreerd in Azure controlelogboeken.
> 
> 

### <a name="security-recommendations"></a>Aanbevelingen voor beveiliging
Voordat u beveiligingsbeleid configureert, Bekijk alle Hallo [beveiligingsaanbevelingen](security-center-recommendations.md), en bepalen of deze beleidsregels geschikt is voor uw verschillende abonnementen en resourcegroepen zijn. Het is ook belangrijk toounderstand welke actie moet worden gehouden tooaddress [beveiligingsaanbevelingen](https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations) en die in uw organisatie die verantwoordelijk is voor de bewaking voor nieuwe aanbevelingen en nemen Hallo stappen nodig.

Security Center raadt u aan om voor de beveiliging contactgegevens voor uw Azure-abonnement te verstrekken. Deze informatie wordt gebruikt door Microsoft toocontact of Hallo Microsoft Security Response Center (MSRC) detecteert dat uw klantgegevens is geopend door een onrechtmatig of niet-geautoriseerde partij. Lees [contact op met informatie over de beveiliging in Azure Security Center bieden](security-center-provide-security-contact-details.md) voor meer informatie over het tooenable deze aanbeveling.

## <a name="data-collection-and-storage"></a>Gegevensverzameling en -opslag
Azure Security Center gebruikt Hallo Microsoft Monitoring Agent – dit Hallo dezelfde agent die wordt gebruikt door Hallo Operations Management Suite en Log Analytics-service – toocollect beveiligingsgegevens van uw virtuele machines is. Gegevens die worden verzameld van deze agent worden opgeslagen in uw Log Analytics-werkruimte(n).

### <a name="agent"></a>Agent

Nadat gegevensverzameling is ingeschakeld in het beveiligingsbeleid hello, Hallo Microsoft Monitoring Agent (voor [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) of [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents)) is geïnstalleerd op alle ondersteunde Azure-VM's en nieuwe bestanden die zijn gemaakt.  Als de VM is al Hallo Microsoft Monitoring Agent is geïnstalleerd, hello Azure Security Center worden benut als huidige Hallo agent geïnstalleerd. Hallo agentproces is ontworpen toobe niet-Invasief en minimale invloed hebben op prestaties van de virtuele machine.

Microsoft Monitoring Agent voor Windows Hello vereist Gebruik TCP-poort 443. Zie Hallo [probleemoplossing artikel](security-center-troubleshooting-guide.md) voor meer informatie.

Als u toodisable verzamelen van gegevens op een bepaald moment wilt, kunt u deze uitschakelen in het Hallo-beveiligingsbeleid. Echter, omdat Hallo Microsoft Monitoring Agent kan worden gebruikt door andere beheertaken voor Azure en bewaking van services Hallo-agent niet automatisch verwijderd wanneer u gegevens verzamelen uitschakelen in Security Center. Indien nodig, kunt u handmatig Hallo-agent verwijderen.

> [!NOTE]
> een lijst met ondersteunde virtuele machines gelezen Hallo toofind [Azure Security Center Veelgestelde vragen (FAQ)](security-center-faq.md).
> 

### <a name="workspace"></a>Werkruimte

Gegevens die van Microsoft Monitoring Agent (namens Azure Security Center) wordt opgeslagen in een bestaande logboekanalyse workspace(s) Hallo verzameld die zijn gekoppeld aan uw Azure-abonnement of een nieuwe workspace(s) waarbij rekening wordt gehouden account Hallo Geo Hallo VM. 

In hello Azure-portal, kunt u een lijst met uw Log Analytics-werkruimten, inclusief alle gemaakt door Azure Security Center toosee bladeren. Een gerelateerde resourcegroep wordt gemaakt voor nieuwe werkruimten. Beide volgen deze naamconventie: 

* Werkruimte: *DefaultWorkspace-[abonnements-id]-[geolocatie]*
* Resourcegroep: *DefaultResouceGroup-[geolocatie]*

Voor werkruimten die zijn gemaakt door Azure Security Center worden gegevens 30 dagen bewaard. Bewaartermijn is voor afgesloten werkruimten, gebaseerd op Hallo werkruimte prijscategorie.

> [!NOTE]
> Microsoft moet sterke verbintenissen tooprotect Hallo privacy en beveiliging van deze gegevens. Microsoft toostrict naleving en beveiliging richtlijnen voldoet, van een service toooperating coderen. Lees [Gegevensbeveiliging van Azure Security Center](security-center-data-security.md) voor meer informatie over de verwerking van gegevens en privacy.
> 

## <a name="ongoing-security-monitoring"></a>Continue beveiligingsbewaking
Na de eerste configuratie en toepassing van Security Center aanbevelingen overweegt de volgende stap Hallo Security Center operationele processen.

tooaccess Security Center van hello Azure-portal klikt u op **Bladeren** en het type **Security Center** in Hallo **Filter** veld. Hallo weergaven dat filters toothese toegepast worden op basis van Hallo gebruiker opgehaald, Hallo in het volgende voorbeeld ziet u een omgeving met veel problemen toobe behandeld:

![dashboard](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig6.png)

> [!NOTE]
> Security Center heeft geen invloed op uw normale operationele procedures, passief wordt bewaakt uw implementaties en aanbevelingen op basis van beveiligingsbeleid Hallo die u ingeschakeld.

Wanneer u eerst-in Security Center toouse voor uw huidige Azure-omgeving opt, controleert u of u wordt aangeraden alle aanbevelingen die kunnen worden uitgevoerd in Hallo **aanbevelingen** tegel of per resource (**Compute** **Networking**, **opslag & gegevens**, **toepassing**).

Zodra u alle aanbevelingen te houden, Hallo **preventie** sectie moeten groene voor alle resources die worden beschreven. Continue bewaking eenvoudiger op dit punt omdat u alleen op basis van wijzigingen in Hallo resource beveiliging resourcebeveiligingsstatus en aanbevelingstegels acties onderneemt.

Hallo **detectie** sectie is meer reactief en betreft waarschuwingen over problemen die zijn nu plaatsvinden of probleem is opgetreden in de afgelopen Hallo en is gedetecteerd door Security Center-besturingselementen en 3e systemen van derden. de tegel beveiligingswaarschuwingen Hallo weergegeven staafdiagram weergegeven dat het aantal dagelijks geconstateerde waarschuwingen die zijn gevonden in elke dag en de verdeling ervan over verschillende ernstigheidscategorieën hello (laag, Gemiddeld, hoog) Hallo. Lees voor meer informatie over beveiligingswaarschuwingen [beheren en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md).

> [!NOTE]
> U kunt ook gebruikmaken van Microsoft Power BI toovisualize Security Center-gegevens. Lees [Managing and responding to security alerts in Azure Security Center](security-center-powerbi.md).
> 
> 

### <a name="monitoring-for-new-or-changed-resources"></a>Bewaking voor nieuwe of gewijzigde resources
De meeste Azure-omgevingen zijn dynamisch, met nieuwe resources die regelmatig omhoog en omlaag worden verplaatst, met configuraties of wijzigingen enz. Security Center helpt ervoor te zorgen dat u inzicht in de beveiligingsstatus Hallo van deze nieuwe resources hebben.

Wanneer u nieuwe resources (VM's, de SQL-databases) tooyour Azure-omgeving toevoegt, wordt Security Center automatisch detecteren van deze bronnen en toomonitor begint de beveiliging ervan. Dit omvat ook PaaS-webrollen en -werkrollen. Als gegevensverzameling is ingeschakeld in Hallo [beveiligingsbeleid](security-center-policies.md), extra bewakingsmogelijkheden wordt ingeschakeld voor uw virtuele machines.

![Belangrijke gebieden](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig3-newUI.png)

1. Voor virtuele machines klikt u op **Compute**, in het gedeelte **Preventie**. Problemen met het inschakelen van gegevens of verwante aanbevelingen worden zichtbaar in Hallo **overzicht** tabblad en **aanbevelingen voor bewaking** sectie.
2. Weergave Hallo **aanbevelingen** toosee wat, indien aanwezig, beveiligingsrisico's gevonden voor de nieuwe resource Hallo.
3. Het is heel gebruikelijk dat wanneer nieuwe virtuele machines worden toegevoegd tooyour omgeving, enige Hallo-besturingssysteem is in eerste instantie geïnstalleerd. Hallo resource-eigenaar wellicht enige tijd toodeploy andere apps die worden gebruikt door deze virtuele machines.  In het ideale geval moet u weten Hallo uiteindelijke doelstelling van deze workload. Gaat deze toobe een toepassingsserver? Op basis van wat deze nieuwe workload gaat toobe is, kunt u de juiste Hallo inschakelen **beveiligingsbeleid**, welke Hallo derde stap in deze werkstroom is.
4. Als nieuwe resources worden toegevoegd tooyour Azure-omgeving, is het mogelijk dat er nieuwe waarschuwingen worden weergegeven in Hallo **beveiligingswaarschuwingen** tegel. Altijd controleren of er nieuwe waarschuwingen in deze tegel en Neem maatregelen op basis van tooSecurity Center aanbevelingen.

U wilt ook tooregularly hello Monitorstatus van bestaande resources tooidentify configuratiewijzigingen die hebben geleid tot beveiligingsrisico's, afwijking van aanbevolen basislijnen en beveiligingswaarschuwingen. Start op Hallo Security Center-dashboard. Van daaruit hebt u drie belangrijke gebieden tooreview consequent.

![Bewerkingen](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig4-newUI.png)

1. Hallo **preventie** sectie Configuratiescherm kunt u snel toegang tooyour belangrijke bronnen. Gebruik deze optie toomonitor Compute, netwerken, opslag en gegevens en toepassingen.
2. Hallo **aanbevelingen** Configuratiescherm kunt u tooreview Security Center aanbevelingen. Tijdens de continue bewaking merkt u dat er geen aanbevelingen dagelijks, dit normaal is omdat u alle op Hallo eerste Security Center-installatie aanbevelingen. Daarom moet u mogelijk geen nieuwe gegevens in deze sectie elke dag en hoeft alleen maar tooaccess deze zo nodig.
3. Hallo **detectie** sectie kan worden gewijzigd op een heel vaak, of zeer incidenteel basis. Controleer altijd uw beveiligingswaarschuwingen en neem maatregelen op grond van de aanbevelingen van Security Center.

## <a name="incident-response"></a>Reageren op incidenten
Security Center detecteert en waarschuwt u toothreats wanneer deze zich voordoen. Organisaties moeten controleren op nieuwe beveiligingswaarschuwingen en maatregelen nemen als de benodigde tooinvestigate verder of Hallo aanval te herstellen. Lees [Detectiemogelijkheden van Azure Security](security-center-detection-capabilities.md) voor meer informatie over de werking van detectie van bedreigingen van Azure Security Center.

In dit artikel biedt geen Hallo opzet tooassist u uw eigen reactieplan maken, terwijl we gaan toouse reactie van Microsoft Azure-beveiliging in de levenscyclus van de Cloud Hallo Hallo basis voor respons op incidenten fasen. Hallo fasen worden weergegeven in het volgende diagram Hallo:

![Verdachte activiteit](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-1.png)

> [!NOTE]
> U kunt Hallo National Institute of Standards and Technology (NIST) [Computer Security Incident Handling Guide](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) als een verwijzing tooassist ontwikkelen van uw eigen.
> 

U kunt Security Center Alerts tijdens Hallo fasen in het volgende gebruiken:

* **Detecteren**: een verdachte activiteit in een of meer resources identificeren. 
* **Beoordelen**: Hallo eerste beoordeling tooobtain meer informatie over Hallo verdachte activiteiten uitvoeren.
* **Diagnose**: Hallo herstel stappen tooconduct Hallo technische procedure tooaddress Hallo probleem gebruiken.

Elke beveiligingswaarschuwing bevat informatie die kan worden gebruikt toobetter Hallo aard van de aanval Hallo begrijpen en mogelijke oplossingen voorstellen. Sommige waarschuwingen bevatten ook koppelingen tooeither meer informatie of tooother informatiebronnen binnen Azure. Kunt u Hallo informatie voor verder onderzoek en toobegin beperken en u kunt ook beveiliging gerelateerde gegevens die zijn opgeslagen in uw werkruimte zoeken.

Hallo volgende voorbeeld ziet u een verdachte RDP-activiteit plaatsvinden:

![Verdachte activiteit](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-ga.png)

Zoals u ziet deze blade bevat gedetailleerde informatie met betrekking tot Hallo tijd Hallo aanval plaatsvond, Hallo bron hostnaam, doel VM Hallo en aanbevolen maatregelen. In sommige omstandigheden Hallo kan broninformatie Hallo-aanval niet leeg zijn. Lees [Missing Source Information in Azure Security Center Alerts](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/25/missing-source-information-in-azure-security-center-alerts/) voor meer informatie over dit type gedrag.

In Hallo [hoe tooLeverage Azure Security Center & Operations Management Suite van Microsoft hello voor een Incident Response](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703) video ziet u enkele demonstraties waarmee u kunnen toounderstand hoe Security Center kunnen worden gebruikt in elk een van deze stappen.

> [!NOTE]
> Lees [Leveraging Azure Security Center voor Incident Response](security-center-incident-response.md) voor meer informatie over het toouse Security Center mogelijkheden tooassist die u tijdens de reactie van uw Incident proces. 
> 
> 

## <a name="see-also"></a>Zie ook
In dit document, u leert hoe tooplan voor acceptatie in Security Center. toolearn meer informatie over Security Center Hallo ziet:

* [Beheren en erop reageren toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md)
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) : meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) : meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) : Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/): lees blogberichten over de beveiliging en naleving van Azure.

