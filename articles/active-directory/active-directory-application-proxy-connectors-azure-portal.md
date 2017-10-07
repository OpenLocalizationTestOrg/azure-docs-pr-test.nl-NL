---
title: aaaPublishing toepassingen op afzonderlijke netwerken en locaties met behulp van groepen van de connector in Azure AD-toepassingsproxy | Microsoft Docs
description: Dekt hoe toocreate en beheren van groepen van connectors in Azure AD-toepassingsproxy.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: 8c9a84b365eab28eaaeb343d4d1e2e6990537fec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>Publiceren van toepassingen op afzonderlijke netwerken en locaties met groepen van de connector
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-application-proxy-connectors-azure-portal.md)
> * [Klassieke Azure Portal](active-directory-application-proxy-connectors.md)
>

Klanten gebruikmaken van Azure AD-toepassingsproxy voor meer scenario's en toepassingen. Dus hebben we aangebracht toepassingsproxy zelfs flexibelere doordat meer topologieën. U kunt Application Proxy connector groepen maken, zodat u specifieke connectors tooserve specifieke toepassingen kunt toewijzen. Deze mogelijkheid biedt u meer controle en manieren toooptimize uw toepassingsproxy-implementatie. 

Elke Application Proxy connector is tooa connector groep toegewezen. Alle Hallo connectors die deel uitmaken van dezelfde groep van de connector fungeert als een eenheid voor hoge beschikbaarheid en taakverdeling toohello. Alle connectors behoren tooa connector groep. Als u geen groepen maakt, vervolgens zijn alle verbindingslijnen in een standaard-groep. Uw beheerder kunt nieuwe groepen maken en toewijzen van connectors toothem in hello Azure-portal. 

Alle toepassingen zijn tooa connector groep toegewezen. Als u geen groepen maakt, worden al uw toepassingen tooa standaardgroep toegewezen. Maar als u uw connectors in groepen indelen, kunt u elke toepassing toowork instellen met een specifieke connector-groep. In dit geval dienen alleen Hallo connectors in die groep Hallo-toepassing op verzoek. Deze functie is handig als uw toepassingen worden gehost op verschillende locaties. U kunt connector groepen op basis van locatie, maken, zodat toepassingen altijd door de connectors die fysiek sluiten toothem worden behandeld.

>[!TIP] 
>Als u een grote Application Proxy-implementatie hebt, niet toewijzen voor een groep toepassingen toohello standaard connector. Op die manier nieuwe connectors niet live verkeer niet ontvangen totdat u ze tooan active-connector groep toewijst. Deze configuratie kunt u ook tooput connectors in een niet-actieve modus door ze te verplaatsen back toohello standaardgroep, zodat u onderhoud zonder enige impact op uw gebruikers kunt uitvoeren.

## <a name="prerequisites"></a>Vereisten
toogroup uw connectors hebt toomake zeker dat u [geïnstalleerd meerdere connectors](active-directory-application-proxy-enable.md). Wanneer u een nieuwe connector installeert, het Hallo automatisch lid wordt **standaard** connector groep.

## <a name="create-connector-groups"></a>Connector-groepen maken
Deze stappen toocreate zoveel connector-groepen als u wilt gebruiken. 

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
1. Selecteer **Azure Active Directory** > **bedrijfstoepassingen** > **toepassingsproxy**.
2. Selecteer **nieuwe connector groep**. Hallo nieuwe Connector groep blade wordt weergegeven.

   ![Selecteer de nieuwe connector-groep](./media/active-directory-application-proxy-connectors-azure-portal/new-group.png)

3. De nieuwe connector-groep een naam geven en gebruik vervolgens Hallo dropdown menu tooselect die deel uitmaken van connectors in deze groep.
4. Selecteer **Opslaan**.

## <a name="assign-applications-tooyour-connector-groups"></a>Toepassingen tooyour connector groepen toewijzen
Volg deze stappen voor elke toepassing die u hebt gepubliceerd met toepassingsproxy. Wanneer u deze publiceren of kunt u deze stappen toochange Hallo toewijzing gewenst, kunt u een groep van toepassingen tooa connector toewijzen.   

1. Selecteer in het dashboard met Hallo management voor uw directory, **bedrijfstoepassingen** > **alle toepassingen** > Hallo toepassing die u wilt dat tooassign tooa connector groep >  **Toepassingsproxy**.
2. Gebruik Hallo **Connector groep** dropdown menu tooselect Hallo gewenste groep Hallo toouse van toepassing.
3. Selecteer **opslaan** tooapply Hallo wijzigen.

## <a name="use-cases-for-connector-groups"></a>Gebruiksvoorbeelden voor connector-groepen 

Connector-groepen zijn handig voor verschillende scenario's, waaronder:

### <a name="sites-with-multiple-interconnected-datacenters"></a>Sites met meerdere onderling verbonden datacenters

Veel organisaties hebben een aantal onderling verbonden datacenters. In dit geval u tookeep zoveel verkeer binnen Hallo datacenter mogelijk omdat cross-datacenter koppelingen dure en traag zijn. U kunt connectoren in elk datacenter tooserve alleen Hallo toepassingen die zich bevinden in Hallo datacenter kunt implementeren. Deze aanpak minimaliseert cross-datacenter koppelingen en biedt een volledig transparant ervaring tooyour gebruikers.

### <a name="applications-installed-on-isolated-networks"></a>Toepassingen die zijn geïnstalleerd op de geïsoleerde netwerken

Toepassingen kunnen worden gehost in netwerken die geen deel uitmaken van de belangrijkste bedrijfsnetwerk Hallo. U kunt connector groepen tooinstall dedicated connectors in geïsoleerde netwerken tooalso isoleren toepassingen toohello netwerk gebruiken. Dit gebeurt meestal wanneer de leverancier van een derde partij een bepaalde toepassing is voor uw organisatie onderhoudt. 

Connector-groepen kunnen u tooinstall dedicated connectors voor netwerken die alleen specifieke toepassingen, waardoor het gemakkelijker publiceren en veiliger toooutsource Toepassingsbeheer toothird leveranciers.

### <a name="applications-installed-on-iaas"></a>Toepassingen die op IaaS geïnstalleerd 

Toepassingen die zijn geïnstalleerd op IaaS voor toegang tot de cloud, bieden connector groepen een algemene service toosecure Hallo toegang tooall Hallo-apps. Groepen van de connector geen extra afhankelijkheid in uw bedrijfsnetwerk maken of fragment Hallo van apps. Connectors kunnen worden geïnstalleerd op elke clouddatacenter en dienen alleen toepassingen die zich op dat netwerk bevinden. U kunt verschillende connectors tooachieve hoge beschikbaarheid installeren.

Neem bijvoorbeeld een organisatie met verschillende virtuele machines verbonden tootheir eigen gehost IaaS virtuele netwerk. tooallow werknemers toouse deze toepassingen deze particuliere netwerken zijn verbonden toohello bedrijfsnetwerk via VPN van site-naar-site. Dit biedt een goede ervaring voor werknemers die zich op locatie zijn. Maar deze mogelijk niet ideaal voor externe werknemers, omdat hiervoor extra on-premises infrastructuur tooroute toegang, zoals u in Hallo diagram hieronder ziet:

![AzureAD Iaas-netwerk](./media/application-proxy-publish-apps-separate-networks/application-proxy-iaas-network.png)
  
Met groepen van Azure AD-toepassingsproxy-connector, kunt u een algemene service toosecure Hallo toegang tooall toepassingen inschakelen zonder aanvullende afhankelijkheid in uw bedrijfsnetwerk maken:

![AzureAD Iaas meerdere Cloud leveranciers](./media/application-proxy-publish-apps-separate-networks/application-proxy-multiple-cloud-vendors.png)

### <a name="multi-forest--different-connector-groups-for-each-forest"></a>Meerdere forests – verschillende connector groepen voor elke forest

De meeste klanten die hebben geïmplementeerd toepassingsproxy gebruikt de eenmalige aanmelding (SSO) mogelijk door het uitvoeren van Kerberos-beperkt delegatie (KCD). tooachieve dit Hallo-connector machines nodig toobe gekoppelde tooa domein dat Hallo gebruikers naar Hallo toepassing kan delegeren. KCD ondersteunt interforest-mogelijkheden. Maar voor de bedrijven die beschikken over verschillende omgevingen voor meerdere forests zonder vertrouwensrelatie tussen deze twee, één connector kan niet worden gebruikt voor alle forests. 

In dit geval specifieke connectors per forest kunnen worden geïmplementeerd en set tooserve toepassingen die gepubliceerd tooserve zijn Hallo alleen gebruikers van dat specifieke forest. Elke groep connector vertegenwoordigt een ander forest. Tijdens het Hallo-tenant en de meeste ervaring Hallo is unified voor alle forests, kunnen gebruikers tootheir forest toepassingen met behulp van Azure AD-groepen worden toegewezen.
 
### <a name="disaster-recovery-sites"></a>Noodherstelsites

Er zijn twee verschillende methoden die u met een site disaster recovery (DR uitvoeren kunt), afhankelijk van hoe uw sites worden geïmplementeerd:

* Als uw site DR is ingebouwd in de actieve-actieve modus waarin het is net als de primaire site Hallo en heeft dezelfde Hallo netwerk- en AD-instellingen kunt u Hallo connectors op Hallo DR-site in Hallo dezelfde connector groep als belangrijkste Hallo-site. Hierdoor kunnen Azure AD toodetect failovers voor u.
* Als uw DR-site gescheiden van de belangrijkste site hello is, u een andere connector-groep op Hallo DR-site maken kunt en 1) back-uptoepassingen laat of 2) handmatig Hallo bestaande toohello DR connector toepassingsgroep omleiden naar behoefte.
 
### <a name="serve-multiple-companies-from-a-single-tenant"></a>Meerdere bedrijven leveren van een enkele tenant

Er zijn veel verschillende manieren tooimplement een model waarin een één-provider worden geïmplementeerd en onderhoudt Azure AD-services voor meerdere bedrijven gerelateerde. Hallo beheerder scheiden Hallo connectors en verschillende groepen van toepassingen kunt connector groepen gebruiken. Een manier die geschikt voor kleine bedrijven, toohave is één Azure AD-tenant, terwijl andere bedrijven Hallo hun eigen domeinnaam en netwerken hebben. Dit geldt ook voor fusies en scenario's en situaties waarbij een enkel IT-afdeling verschillende bedrijven vanwege regelgeving of zakelijke redenen fungeert. 

## <a name="sample-configurations"></a>Voorbeelden van configuraties

Enkele voorbeelden die u kunt implementeren, zijn Hallo connector groepen te volgen.
 
### <a name="default-configuration--no-use-for-connector-groups"></a>Standaard-configuratie geen nut voor connector-groepen

Als u geen connector groepen gebruikt, wordt de configuratie eruit als volgt:

![AzureAD geen Connector-groepen](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-1.png)
 
Deze configuratie is geschikt voor kleine implementaties en tests. Werkt ook goed als uw organisatie een platte netwerktopologie heeft.
 
### <a name="default-configuration-and-an-isolated-network"></a>Standaardconfiguratie en een geïsoleerd netwerk

Deze configuratie is een evolutie van Hallo standaard één, waarin een specifieke app die wordt uitgevoerd in een geïsoleerd netwerk zoals IaaS virtuele netwerk is: 

![AzureAD geen Connector-groepen](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-2.png)
 
### <a name="recommended-configuration--several-specific-groups-and-a-default-group-for-idle"></a>Aanbevolen configuratie – enkele specifieke groepen en een standaardgroep voor inactiviteit

aanbevolen configuratie voor organisaties met grotere, complexe Hallo is toohave Hallo standaardgroep connector als een groep die geen nut heeft voor alle toepassingen en wordt gebruikt voor niet-actief of geïnstalleerde connectors. Alle toepassingen worden geleverd met aangepaste connector groepen. Hierdoor kunnen alle Hallo complexiteit van het Hallo-scenario's die hierboven worden beschreven.

In Hallo onderstaand voorbeeld heeft Hallo bedrijf twee datacentra, A en B, met twee connectors die dienen van elke site. Elke site heeft verschillende toepassingen die worden uitgevoerd op deze. 

![AzureAD geen Connector-groepen](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-3.png)
 
## <a name="next-steps"></a>Volgende stappen

* [Azure AD-toepassingsproxy connectors begrijpen](application-proxy-understand-connectors.md)
* [Eenmalige aanmelding inschakelen](application-proxy-sso-overview.md)


