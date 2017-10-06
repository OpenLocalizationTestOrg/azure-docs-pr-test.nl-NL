---
title: AAA aan de slag met Azure Automation | Microsoft Docs
description: Dit artikel bevat een overzicht van Azure Automation-service aan de hand van Hallo ontwerp en de implementatie-informatie in voorbereiding tooonboard Hallo aanbieding uit Azure Marketplace.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 434e8ea28c55ff9bda1d2e46a7a6b8378a3baa0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation"></a>Aan de slag met Azure Automation

Deze introductiehandleiding introduceert de belangrijkste concepten gerelateerde toohello implementatie van Azure Automation. Als u nieuwe tooAutomation in Azure of ervaring met automation werkstroom software, zoals System Center Orchestrator hebben, deze handleiding helpt u begrijpen hoe tooprepare en vrijgeven automatisering.  Daarna worden u voorbereid toobegin ontwikkelen van runbooks ter ondersteuning van uw automatiseringsbehoeften proces. 


## <a name="automation-architecture-overview"></a>Overzicht van Automation-architectuur

![Overzicht van Azure Automation](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Azure Automation is een software als een dienst (SaaS)-toepassing die voorziet in een schaalbare en betrouwbare, multitenant omgeving tooautomate verwerkt met runbooks en configuratie wijzigingen tooWindows- en Linux-systemen met behulp van Desired State Configuration beheren (DSC) in Azure, andere cloudservices of on-premises. Entiteiten in uw Automation-account, zoals runbooks, assets en Uitvoeren als-accounts, zijn geïsoleerd van andere Automation-accounts in uw abonnement en andere abonnementen.  

Runbooks die u uitvoert in Azure, worden uitgevoerd op Automation-sandboxes, die op het Azure-platform als een virtuele PaaS-machine (platform als een service) worden gehost.  Automation-sandboxes bieden isolatie van tenants voor alle aspecten van de uitvoering van runbooks: modules, opslag, geheugen, netwerkcommunicatie, taakstromen enzovoort. Deze rol wordt beheerd door service Hallo en is niet toegankelijk is vanaf uw Azure of een Azure Automation-account voor u toocontrol.         

tooautomate hello implementatie en beheer van bronnen in uw lokale datacentrum of andere cloudservices, na het maken van een Automation-account, kunt u een of meer machines toorun Hallo aanwijzen [hybride Runbook Worker (HRW)](automation-hybrid-runbook-worker.md) rol.  Elke HRW vereist Hallo Microsoft Management Agent met een werkruimte voor logboekanalyse tooa verbinding en een Automation-account.  Hallo Microsoft Management Agent logboekanalyse is gebruikte toobootstrap Hallo-installatie, onderhouden en bewaken van Hallo-functionaliteit van Hallo HRW.  Hallo-levering van runbooks en Hallo instructie toorun die ze door Azure Automation worden uitgevoerd.

U kunt meerdere HRW tooprovide hoge beschikbaarheid implementeren voor uw runbooks, runbooktaken saldo laden en in sommige gevallen toe te wijzen aan hen voor bepaalde werkbelastingen of omgevingen.  Hallo Microsoft Monitoring Agent op Hallo HRW communicatie met de Hallo Automation-service via TCP-poort 443 initieert en er zijn geen binnenkomende firewallvereisten.  Nadat u runbook uitgevoerd op een HRW binnen Hallo-omgeving hebt en u wilt dat Hallo runbook tooperform beheertaken op basis van andere machines of services in die omgeving, er mogelijk andere poorten die Hallo worden runbook vereist toegang tot.  Als de beleidsregels van uw IT-beveiliging niet toestaan computers op uw netwerk tooconnect toohello Internet dat, raadpleegt u Hallo artikel [OMS Gateway](../log-analytics/log-analytics-oms-gateway.md), die fungeert als proxy voor Hallo HRW toocollect taak de status en configuratie-informatie uit ontvangen uw Automation-account.

Runbooks die worden uitgevoerd op een HRW uitgevoerd in context van lokale systeemaccount op de computer Hallo Hallo hello, wordt wat Hallo aanbevolen beveiligingscontext bij het uitvoeren van beheertaken op Hallo lokale Windows-computer. Als u Hallo runbook toorun taken op basis van bronnen buiten Hallo lokale computer wilt, moet u mogelijk toodefine beveiligde referentieassets in Automation-account toegang tot van Hallo runbook en tooauthenticate gebruiken met de externe bron Hallo Hallo. U kunt [referentie](automation-credentials.md), [certificaat](automation-certificates.md), en [verbinding](automation-connections.md) activa in uw runbook met cmdlets waarmee u toospecify referenties zodat u ze kunt verifiëren.

DSC-configuraties die zijn opgeslagen in Azure Automation kunnen rechtstreeks toegepaste tooAzure virtuele machines zijn. Andere fysieke en virtuele machines kunnen configuraties van hello Azure Automation DSC-pull-server aanvragen.  Voor het beheren van configuraties van uw on-premises fysieke of virtuele Windows- en Linux-systemen, hoeft u niet toodeploy eventuele infrastructuur toosupport Hallo Automation DSC pull-server, alleen uitgaande toegang tot Internet vanaf elk systeem toobe beheerd door Automation DSC , communiceren via TCP-poort 443 toohello OMS-service.   

## <a name="prerequisites"></a>Vereisten

### <a name="automation-dsc"></a>Automation DSC
Azure Automation DSC gebruikte toomanage verschillende machines kan worden:

* Virtuele machines van Azure (klassiek) met Windows of Linux
* Virtuele machines van Azure met Windows of Linux
* Virtuele AWS-machines (Amazon Web Services) met Windows of Linux
* Fysieke/virtuele Windows-computers on-premises of in een andere cloud dan Azure of AWS
* Fysieke/virtuele Linux-computers on-premises of in een andere cloud dan Azure of AWS

meest recente versie van WMF 5 Hallo moet worden geïnstalleerd voor Hallo PowerShell DSC-agent voor Windows toobe kunnen toocommunicate met Azure Automation. meest recente versie van de Hallo Hallo [PowerShell DSC-agent voor Linux](https://www.microsoft.com/en-us/download/details.aspx?id=49150) voor Linux toobe kunnen toocommunicate met Azure Automation moeten worden geïnstalleerd.

### <a name="hybrid-runbook-worker"></a>Hybrid Runbook Worker  
Wanneer een computer toorun hybride runbook aanwijzing van taken, moet deze computer Hallo volgende hebben:

* Windows Server 2012 of hoger
* Windows PowerShell 4.0 of hoger.  Het is raadzaam om de installatie van Windows PowerShell 5.0 op Hallo computer voor een hogere mate van betrouwbaarheid. U kunt de nieuwe versie Hallo downloaden van Hallo [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=50395)
* Minimaal twee kernen
* Minimaal 4 GB aan RAM-geheugen

### <a name="permissions-required-toocreate-automation-account"></a>Machtigingen vereist toocreate Automation-account
toocreate of update een Automation-account, hebt u Hallo na specifieke rechten en machtigingen nodig toocomplete in dit onderwerp.   
 
* In de volgorde toocreate een Automation-account, uw AD-gebruikersaccount moet toobe toegevoegde tooa rol met de rol van eigenaar gelijkwaardige toohello machtigingen voor Microsoft.Automation bronnen zoals wordt beschreven in artikel [toegangsbeheer op basis van rollen in Azure Automation ](automation-role-based-access-control.md).  
* Als Hallo App registraties instellen te is ingesteld**Ja**, kunnen gebruikers niet-beheerders in uw Azure AD-tenant [AD-toepassingen registreren](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions).  Als Hallo app registraties instellen te is ingesteld**Nee**, Hallo gebruiker deze bewerking moet een globale beheerder in Azure AD. 

Als u niet lid zijn van de Active Directory-exemplaar van Hallo abonnement voordat u toohello globale beheerder/SA-administrator-rol van Hallo abonnement worden toegevoegd, kunt u tooActive Directory wordt toegevoegd als gast. In dit geval ontvangt u een "u hebt geen machtigingen toocreate..." Waarschuwing voor Hallo **Automation-Account toevoegen** blade. Gebruikers die zijn toegevoegd toohello globale beheerder/SA-administrator-rol kan worden verwijderd uit Active Directory-exemplaar van het abonnement Hallo eerst en opnieuw toegevoegd toomake ze een volledige gebruiker in Active Directory. tooverify deze situatie van Hallo **Azure Active Directory** deelvenster in Azure portal, selecteer Hallo **gebruikers en groepen**, selecteer **alle gebruikers** en, nadat u Hallo selecteren specifieke gebruiker, schakelt **profiel**. waarde van Hallo Hallo **gebruikerstype** kenmerk onder Hallo gebruikersprofiel moet niet gelijk aan **Gast**.

## <a name="authentication-planning"></a>Verificatieplanning
Azure Automation kunt u tooautomate taken op basis van bronnen in Azure, on-premises en bij andere cloudproviders.  Om een runbook tooperform de vereiste acties moet hebben machtigingen toosecurely toegang Hallo resources met de minimale rechten Hallo binnen Hallo abonnement vereist.  

### <a name="what-is-an-automation-account"></a>Wat is een Automation-account 
Alle Hallo automatiseringstaken die u uitvoert op resources met behulp van hello Azure-cmdlets in Azure Automation verifiëren tooAzure verificatie op basis van referentie op organisatie-id van Azure Active Directory.  Een Automation-account is gescheiden van Hallo account u toosign gebruikt in de portal tooconfigure toohello en Azure-resources gebruiken.  Automation-resources die zijn opgenomen met een account zijn Hallo volgende:

* **Certificaten**: certificaten die worden gebruikt voor verificatie vanuit een runbook of DSC-configuratie of deze toevoegen.
* **Verbindingen** -verificatie en configuratie vereiste informatie op tooconnect tooan externe service of toepassing vanuit een runbook of de DSC-configuratie bevat.
* **Referenties** -is een PSCredential-object met beveiligingsgegevens zoals een gebruikersnaam en wachtwoord vereist tooauthenticate vanuit een runbook of de DSC-configuratie.
* **Integratiemodules** -PowerShell-modules die deel uitmaakt van een Azure Automation-account toomake gebruik van cmdlets in runbooks en DSC-configuraties zijn.
* **Schema’s**: schema's voor het starten of stoppen van een runbook op een opgegeven moment, met terugkerende frequenties.
* **Variabelen**: waarden die beschikbaar zijn vanuit een runbook of de DSC-configuratie.
* **DSC-configuraties** -zijn PowerShell-scripts die wordt beschreven hoe tooconfigure een functie van het besturingssysteem of instelling of een toepassing installeert op een Windows- of Linux-computer.  
* **Runbooks**: een set taken die een aantal geautomatiseerde processen uitvoeren in Azure Automation op basis van Windows PowerShell.    

Hallo Automation-resources voor elk Automation-account zijn gekoppeld aan één Azure-regio, maar Automation-accounts kunnen alle Hallo resources in uw abonnement beheren. Automation-accounts maken in verschillende regio's, als u beleid hebt waardoor gegevens en resources toobe geïsoleerde tooa specifieke regio.

> [!NOTE]
> Automation-accounts en Hallo-resources die ze bevatten die zijn gemaakt in hello Azure-portal, niet toegankelijk in de klassieke Azure-portal Hallo. Als u toomanage deze accounts of hun resources met Windows PowerShell wilt, moet u hello Azure Resource Manager-modules.
> 

Wanneer u een Automation-account in hello Azure-portal maakt, worden automatisch twee verificatie-entiteiten maken:

* Een Uitvoeren als-account. Door dit account worden een service-principal in Azure Active Directory (Azure AD) en een certificaat gemaakt. Hallo Inzender op rollen gebaseerde toegangsbeheer (RBAC), die Resource Manager-resources met behulp van runbooks beheert wijst ook toe.
* Een klassiek Uitvoeren als-account. Dit account uploadt een beheercertificaat dat gebruikt toomanage klassieke resources is met behulp van runbooks.

Toegangsbeheer op basis van rollen is beschikbaar met Azure Resource Manager toogrant toegestane acties tooan Azure AD-gebruikersaccount en Run As-account en verifiëren van deze service-principal.  Lees [toegangsbeheer op basis van rollen in Azure Automation-artikel](automation-role-based-access-control.md) voor verdere informatie toohelp ontwikkelen van een model voor het beheren van machtigingen in Automation.  

#### <a name="authentication-methods"></a>Verificatiemethoden
Hallo volgende tabel ziet u Hallo verschillende verificatiemethoden voor elke omgeving wordt ondersteund door Azure Automation.

| Methode | Omgeving 
| --- | --- | 
| Uitvoeren als-account van Azure en klassiek Uitvoeren als-account |Azure Resource Manager en klassieke Azure-implementatie |  
| Azure AD-gebruikersaccount |Azure Resource Manager en klassieke Azure-implementatie |  
| Windows-verificatie |Lokale datacentrum of andere cloudprovider met behulp van Hallo Hybrid Runbook Worker |  
| AWS-referenties |Amazon Web Services |  

Onder Hallo **hoe to\Authentication en beveiliging** sectie, zijn ondersteunende artikelen zodat overzicht en de implementatiestappen tooconfigure verificatie voor deze omgevingen, hetzij met een bestaande of nieuwe account u reserveren voor deze omgeving.  Hallo voor hello Azure uitvoeren als en klassieke Run As-account, onderwerp [Automation Update die Run As-account](automation-create-runas-account.md) wordt beschreven hoe tooupdate uw bestaande Automation-account met Hallo Run As-accounts van Hallo portal of met behulp van PowerShell als dat niet is oorspronkelijk is geconfigureerd met een Run As- of klassieke Run As-account. Als u wilt toocreate een Run As- en klassieke Run As-account met een certificaat dat is uitgegeven door uw enterprise-certificeringsinstantie (CA), raadpleegt u dit artikel toolearn hoe toocreate Hallo gebruikersaccounts via deze configuratie.     
 
## <a name="network-planning"></a>Netwerkplanning
Voor Hallo Hybrid Runbook Worker tooconnect tooand registreren met de Microsoft Operations Management Suite (OMS), toohello-poortnummer toegang moet hebben en Hallo URL's die hieronder worden beschreven.  Dit is bovendien toohello [poorten en URL's die zijn vereist voor Microsoft Monitoring Agent Hallo](../log-analytics/log-analytics-windows-agents.md#network) tooconnect tooOMS. Als u een proxyserver voor communicatie tussen het Hallo-agent en Hallo OMS-service gebruiken, moet u tooensure dat de juiste resources Hallo toegankelijk zijn. Als u een firewall toorestrict toegang toohello Internet gebruikt, moet u tooconfigure uw firewall toopermit toegang.

onderstaande lijst Hallo poort en URL's die vereist voor Hallo Hybrid Runbook Worker toocommunicate met Automation zijn Hallo-gegevens.

* Poort: alleen TCP 443 is vereist voor uitgaande toegang tot internet
* Algemene URL: *.azure-automation.net

Als u een Automation-account dat is gedefinieerd voor een bepaald gebied hebt en u toorestrict communicatie met die regionaal datacenter wilt, hello volgende tabel bevat Hallo DNS-record voor elke regio.

| **Regio** | **DNS-record** |
| --- | --- |
| Zuid-centraal VS |scus-jobruntimedata-prod-su1.azure-automation.net |
| VS - oost 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| West-centraal VS | wcus-jobruntimedata-prod-su1.azure-automation.net |
| West-Europa |we-jobruntimedata-prod-su1.azure-automation.net |
| Noord-Europa |ne-jobruntimedata-prod-su1.azure-automation.net |
| Canada - midden |cc-jobruntimedata-prod-su1.azure-automation.net |
| Zuidoost-Azië |sea-jobruntimedata-prod-su1.azure-automation.net |
| Centraal-India |cid-jobruntimedata-prod-su1.azure-automation.net |
| Japan - oost |jpe-jobruntimedata-prod-su1.azure-automation.net |
| Australië - zuidoost |ase-jobruntimedata-prod-su1.azure-automation.net |
| Verenigd Koninkrijk Zuid | uks-jobruntimedata-prod-su1.azure-automation.net |
| VS (overheid) - Virginia | usge-jobruntimedata-prod-su1.azure-automation.us |

Voor een lijst met IP-adressen in plaats van namen, downloaden en bekijken Hallo [Azure Datacenter IP-adres](https://www.microsoft.com/download/details.aspx?id=41653) XML-bestand van Hallo Microsoft Download Center. 

> [!NOTE]
> Dit bestand bevat Hallo IP-adresbereiken (met inbegrip van de berekenings-, SQL en -bereiken) in Microsoft Azure-Datacenters Hallo gebruikt. Een bijgewerkt bestand geboekt wekelijks die weerspiegelt Hallo momenteel geïmplementeerd bereiken en alle toekomstige wijzigingen toohello IP-adresbereiken. Nieuwe bereiken verschijnen in Hallo-bestand wordt niet worden gebruikt in datacenters Hallo voor ten minste één week. Controleer downloaden Hallo nieuwe xml bestand elke week en de benodigde wijzigingen Hallo uitvoeren op uw site toocorrectly identificeren services in Azure wordt uitgevoerd. Express Route-gebruikers mogelijk Let dat dit bestand gebruikt tooupdate Hallo BGP-aankondiging van Azure ruimte in Hallo eerste week van elke maand. 
> 

## <a name="creating-an-automation-account"></a>Een Automation-account maken

Er zijn verschillende manieren die u een Automation-account in hello Azure-portal maken kunt.  Hallo volgende tabel wordt elk type implementatie-ervaring en verschillen tussen deze twee geïntroduceerd.  

|Methode | Beschrijving |
|-------|-------------|
| Automation & Hallo Marketplace besturingselement selecteren | Een aanbieding een Automation-account en de OMS-werkruimte maakt gekoppeld tooone in dezelfde resourcegroep en regio Hallo.  Integratie met OMS ook omvat Hallo voordeel van het gebruik van logboekanalyse toomonitor en analyseren van runbook-taak status en taak streams na verloop van tijd en gebruikmaken van geavanceerde functies tooescalate of problemen onderzoeken. Hallo bieden ook implementeert Hallo bijhouden & updatebeheer oplossingen die zijn standaard ingeschakeld. |
| Automatisering van Hallo Marketplace selecteren | Maakt een Automation-account in een nieuwe of bestaande resourcegroep dat geen gekoppelde tooan OMS-werkruimte en omvat niet alle beschikbare oplossingen Hallo Automation en Control aangeboden. Dit is een basisconfiguratie waarin u kennis kunt tooAutomation en kunt u meer informatie over hoe toowrite runbooks, DSC-configuraties en gebruik Hallo mogelijkheden van Hallo-service. |
| Geselecteerde beheeroplossingen | Als u een oplossing – selecteert  **[updatebeheer](../operations-management-suite/oms-solution-update-management.md)**,  **[starten/stoppen virtuele machines tijdens daluren](automation-solution-vm-management.md)**, of  **[ Het bijhouden van](../log-analytics/log-analytics-change-tracking.md)**  ze vraagt u een bestaande automatisering tooselect en OMS-werkruimte, of dit aanbieden Hallo van optie toocreate beide als nodig voor Hallo oplossing toobe geïmplementeerd in uw abonnement. |

In dit onderwerp leert u een Automation-account en een OMS-werkruimte maken door het onboarding Hallo Automation & Control-aanbieding.  een zelfstandige Automation-account voor testdoeleinden of toopreview Hallo-service, bekijk Hallo volgende artikel toocreate [zelfstandige Automation-account maken](automation-create-standalone-account.md).  

### <a name="create-automation-account-integrated-with-oms"></a>Een Automation-account maken dat is geïntegreerd met OMS
Hallo aanbevolen methode tooonboard die Automation wordt Hallo Automation en Control aanbieding van Hallo Marketplace kiest.  Hiermee maakt u zowel een Automation-account en wordt tot stand gebracht Hallo-integratie met een OMS-werkruimte, waaronder Hallo optie tooinstall Hallo beheeroplossingen die beschikbaar met de Hallo aanbieding zijn.  

1. Meld u aan toohello Azure-portal met een account dat lid is van de rol Abonnementsbeheerders hello en medebeheerder van Hallo-abonnement.

2. Klik op **Nieuw**.<br><br> ![De optie Nieuw selecteren in Azure Portal](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  

3. Zoeken naar **Automation** en klik vervolgens in Hallo zoekresultaten Selecteer **Automation en Control***.<br><br> ![Zoek naar en selecteer Automation en beheer in Marketplace](media/automation-offering-get-started/automation-portal-martketplace-select-automationandcontrol.png).<br>   

4. Klik na het lezen van Hallo beschrijving voor de aanbieding Hallo **maken**.  

5. Op Hallo **Automation en Control** instellingenblade, selecteer **OMS-werkruimte**.  Op Hallo **OMS werkruimten** blade een OMS-werkruimte gekoppeld toohello dezelfde Azure-abonnement dat Hallo Automation-account is in selecteren of maken van een OMS-werkruimte.  Als u een OMS-werkruimte niet hebt, selecteert u **nieuwe werkruimte maken** en op Hallo **OMS-werkruimte** blade Hallo volgende uitvoeren: 
   - Geef een naam voor de nieuwe Hallo **OMS-werkruimte**.
   - Selecteer een **abonnement** toolink tooby selecteren in de vervolgkeuzelijst Hallo als Hallo standaard geselecteerd niet geschikt is.
   - Voor **Resourcegroep** kunt u een resourcegroep maken of een bestaande resourcegroep selecteren.  
   - Selecteer een **locatie**.  Momenteel Hallo enige locaties beschikbaar zijn **Australië-Zuidoost**, **VS-Oost**, **Zuidoost-Azië**, **West-Centraal VS**, en  **West-Europa**.
   - Selecteer een **prijscategorie**.  Hallo-oplossing wordt aangeboden in twee lagen: vrij te maken en Per knooppunt (OMS) is laag.  Hallo gratis laag heeft een limiet op Hallo hoeveelheid gegevens die worden verzameld per dag, bewaarperiode en runbook-taak runtime minuten.  Hallo Per knooppunt (OMS) laag heeft geen een limiet op Hallo hoeveelheid dagelijks verzamelde gegevens.  
   - Selecteer **Automation-account**.  Als u een nieuwe OMS-werkruimte maakt, bent u vereiste tooalso maken een Automation-account dat is gekoppeld aan Hallo nieuwe OMS-werkruimte opgegeven eerder, met inbegrip van uw Azure-abonnement, resourcegroep en de regio.  U kunt selecteren **een Automation-account maken** en op Hallo **Automation-Account** blade biedt Hallo volgende: 
  - In Hallo **naam** Hallo naam Hallo Automation-account.

    Alle andere opties worden automatisch ingevuld op basis van Hallo OMS-werkruimte geselecteerd en deze opties kunnen niet worden gewijzigd.  Een Azure uitvoeren als-account is Hallo standaardmethode voor verificatie Hallo aanbieding.  Nadat u op **OK**, Hallo configuratieopties worden gevalideerd en Hallo Automation-account is gemaakt.  U kunt de voortgang onder volgen **meldingen** in Hallo-menu. 

    Selecteer anders een bestaand Automation Uitvoeren als-account.  Hallo-account die u selecteert al mag geen gekoppelde tooanother OMS-werkruimte, anders een melding is opgenomen in het Hallo-blade.  Als deze al is gekoppeld, u moet tooselect een ander Automation Run As-account of een maken.

    Klik na het voltooien van de vereiste informatie op Hallo **maken**.  Hallo-informatie wordt gecontroleerd en Hallo Automation-Account en Run As-accounts worden gemaakt.  U keert terug toohello **OMS-werkruimte** blade automatisch.  

6. Na het opgeven van Hallo vereiste informatie op Hallo **OMS-werkruimte** blade, klikt u op **maken**.  Tijdens het Hallo-informatie is geverifieerd en Hallo werkruimte wordt gemaakt, kunt u de voortgang onder bijhouden **meldingen** in Hallo-menu.  U keert terug toohello **oplossing toevoegen** blade.  

7. Op Hallo **Automation en Control** instellingenblade u wilt tooinstall Hallo aanbevolen vooraf geselecteerd oplossingen bevestigen. Als u een oplossing uitschakelt, kunt u deze later afzonderlijk installeren.  

8. Klik op **maken** tooproceed met onboarding Automation en een OMS-werkruimte. Alle instellingen worden gevalideerd en vervolgens probeert toodeploy Hallo aanbieden in uw abonnement.  Dit kan duren enkele seconden toocomplete en u kunt de voortgang onder volgen **meldingen** in Hallo-menu. 

Nadat Hallo aanbieding is vrijgegeven, kunt u beginnen met het maken van runbooks, werken met Hallo beheeroplossingen die u hebt ingeschakeld, implementeert een [hybride Runbook worker](automation-hybrid-runbook-worker.md) rol of beginnen met werken met [logboekanalyse](https://docs.microsoft.com/azure/log-analytics) toocollect gegevens die worden gegenereerd door de bronnen in uw cloud of on-premises omgeving.   

## <a name="next-steps"></a>Volgende stappen
* Raadpleeg [Runbooks verifiëren met een Azure Uitvoeren als-account](automation-verify-runas-authentication.md) als u wilt controleren of uw nieuwe Azure Automation-account kan worden geverifieerd met Azure-resources.
* tooget gestart met het maken van runbooks, eerst bekijkt hello [Automation-runbooktypen](automation-runbook-types.md) ondersteund en gerelateerde overwegingen voordat u begint met het ontwerpen.


