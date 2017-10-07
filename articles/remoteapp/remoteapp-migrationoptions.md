---
title: aaaOptions voor het migreren van buiten het Azure RemoteApp | Microsoft Docs
description: Meer informatie over het Hallo-opties voor het migreren van buiten het Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a>Opties voor het migreren van buiten het Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.


Als u met Azure RemoteApp vanwege Hallo hebt gestopt [buiten gebruik stellen aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) of omdat u de evaluatie hebt voltooid, moet u toomigrate afmeldt bij Azure RemoteApp tooanother-app service. Er zijn twee verschillende manieren voor het migreren van: een zelfbeheerde (vaak infrastructuur als een Service [IaaS] genoemd)-implementatie of een volledig beheerde (vaak genoemd Platform als een Service) of Software als een Service [PaaS/SaaS] aanbieden. 

Selfservice IaaS is een doe implementatie die wordt beheerd, beheerd en die eigendom zijn van door u rechtstreeks worden geïmplementeerd op virtuele machines (VM's) of fysieke systemen. Bij andere Hallo beëindigen, een volledig beheerde PaaS/SaaS aanbieding is vergelijkbaar met een Azure RemoteApp - een partner biedt een servicelaag bovenop een oplossing voor externe toegang die verantwoordelijk is voor operationele en onderhoud terwijl u, als klant hello, gaat u sommige installatiekopie en app-beheer.

[Hello Azure RemoteApp webinars bekijken op migratiemogelijkheden](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), of lees verder voor meer informatie (inclusief voorbeelden van andere opties host Hallo).

## <a name="self-managed-iaas-solutions"></a>Zelfbeheerde (IaaS) oplossingen
### <a name="rds-on-iaas"></a>**RDS op IaaS**
U kunt een eigen sessie implementatie op basis van extern bureaublad-Services (in Windows Server) met RemoteApp of bureaubladen on-premises of in een gehoste omgeving (like op Azure Virtual machines). RDS op IaaS-implementaties zijn het meest geschikt is voor klanten die bekend zijn met en waarvoor de bestaande technische kennis met RDS-implementaties. 

> [!NOTE]
> Moet u Volume Licensing met Software Assurance (SA) voor RDS-client access-licenties toouse deze Implementatieoptie.

Implementeren van RDS op Azure Virtual machines is eenvoudiger dan ooit wanneer u implementatie gebruiken en patchen sjablonen (lezen een [overzicht](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) en vervolgens [gaat u ze](https://aka.ms/rdautomation)). U kunt Hallo dezelfde elastisch schalen mogelijkheden met Azure classic deployment model resources (geen Azure-Resourcemodel bronnen) in Azure RemoteApp ophalen met behulp van Hallo [automatisch schalen script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), hoewel er meer zijn aanpassingen en configuraties. Wanneer u RDS op Azure Virtual machines implementeert, ondersteuning is beschikbaar via [ondersteuning van Azure](https://azure.microsoft.com/support/plans/), Hallo dezelfde ondersteuningsmedewerkers die u met Azure RemoteApp wordt ondersteund. U maakt een schatting op basis van het gebruik van uw bestaande contact opnemen met de ophalen kost [ondersteuning van Azure](https://azure.microsoft.com/support/plans/), of u kunt berekeningen zelf uitvoeren met behulp van een snel toobe kosten Rekenmachine uitgebracht.  Met N-serie VMs (momenteel in een afgeschermd voorbeeld) kunt u ook vGPU - toevoegen meer over het toevoegen van vGPU en het te horen[benutten RDS-verbeteringen in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in onze Ignite-sessie.   

We hebben stapsgewijze implementatiehandleidingen voor [Windows Server 2012 R2](http://aka.ms/rdsonazure) en [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist met uw implementatie. Bekijk Hallo [extern bureaublad-blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) voor het laatste nieuws Hallo.

### <a name="citrix-on-iaas"></a>**Citrix op IaaS**
Een systeemeigen Citrix implementatie van op sessies gebaseerde XenApp of XenDesktop kan worden geïmplementeerd op lokale of binnen een gehoste omgeving (zoals op Azure Virtual machines). 

Stapsgewijze implementatie-handleiding Hallo, Bekijk [Citrix XA 7.6 op Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), voor meer informatie. Lees meer over [Citrix op Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), met inbegrip van een rekenmachine prijs. U vindt ook een [Citrix contact](http://citrix.com/English/contact/index.asp) toodiscuss uw opties met.

## <a name="fully-managed-paassaas-offerings"></a>Volledig beheerd (PaaS/SaaS)-aanbiedingen

### <a name="citrix-xenapp-essentials-released-april-2017"></a>Citrix XenApp Essentials (uitgebracht April 2017)
Nu beschikbaar op Hallo [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is Hallo nieuwe application virtualization-service, Hallo power combineren en flexibiliteit van Hallo Citrix cloudplatform met een eenvoudig hello, prescriptieve, en eenvoudig te gebruiken visie van Microsoft Azure RemoteApp. 

Bestaande Azure RemoteApp-klanten kunnen [registreren voor een gratis proefversie](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).  Opmerking: Alleen Citrix service gebruiksrecht is gratis, Azure kosten voor berekeningen en opslag van toepassing

Meer informatie:
- [Migreren van Azure RemoteApp tooCitrix XenApp Essentials](remoteapp-migrate-citrix.md)
- [Citrix en Microsoft](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- [Citrix XenApp Essentials presentatie](https://www.youtube.com/watch?v=91Z7CCfQ-9k).  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a>Citrix-Cloudservice XenApp en XenDesktop Service 

[Citrix-Cloudservice XenApp en XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) Hallo beste oplossing voor de levering van Hallo van zowel apps en desktops, plus Geavanceerd beheer en bewakingsmogelijkheden. 

#### <a name="conexlink-platform-name-mycloudit"></a>Conexlink (de naam van het Platform: MyCloudIT)
[MyCloudIT](https://mycloudit.com) is een automatiseringsplatform voor IT-bedrijven toosimplify, te optimaliseren en Hallo migratie schalen en levering van externe bureaubladen, externe toepassingen en infrastructuur in Microsoft Azure Cloud Hallo. 

Hallo MyCloudIT platform implementatietijd minder met 95%, Azure kosten per 30%, en de gehele IT-infrastructuur van de client is verplaatst naar de cloud binnen een paar enkele toetsaanslagen Hallo. Partners kunnen klanten nu beheren vanuit één globale dashboard, service-eindgebruikers Hallo wereld zoals nooit tevoren en inkomsten te vergroten zonder extra overhead of uitgebreide Azure training toe te voegen.  

> Primaire locatie: Dallas, TX, VS
> 
> Bewerkingsregio: overal ter wereld
> 
> Status partner: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)
> 
> Microsoft Cloud-serviceprovider: Ja
> 
> RemoteApp- en bureaublad-sessie-oplossingen bieden: Ja, beide
> 
> Azure RemoteApp-oplossingen voor migratie: Ja, [meer informatie](https://mycloudit.com/remote-app-microsoft/)
> 
> Brian Garoutte, Onderdirecteur Business Development
> 
> Telefoon: 972-218-0741
>   
> E-mail:[brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)

### <a name="frame"></a>Frame

IT-organisaties in enterprise en government, beheerde serviceproviders en toonaangevende leveranciers Kies Frame toocreate en hun beveiligde, door software gedefinieerde werkruimten in de cloud Hallo beheren. Van kleine toolarge organisaties, Frame maakt het zeer eenvoudig toolet gebruikers toegang krijgen tot Windows-toepassingen in elke browser vanaf elk apparaat. Hello Frame platform alles bevat een beheerder moet toodeploy toepassingen vanuit Hallo cloud met inbegrip van hello Azure-infrastructuur en RDS-licenties (uw eigen Azure-account en de licenties te brengen is optioneel). 

Meer informatie over [Frame op Azure](https://www.fra.me/ara). 

> Primaire locatie: San Mateo, CA, VS
>
> Bewerkingsregio: overal ter wereld
>
> Microsoft-Partner: Ja
> 
> Telefoon: 1-480-269-4668

### <a name="awingu"></a>Awingu
Awingu biedt een eenvoudige online werkruimte-oplossing oudere apps, SaaS en documenten worden uitgevoerd vanuit een browser html5. Als zodanig toepassingen veilig beschikbaar maken op elk type apparaat. Voor SaaS-services is een breed scala op eenmalige aanmelding opties beschikbaar. Diverse (cloud) bestandssystemen kunnen ook nauw geïntegreerd in uw werkruimte. Volgende toofull-mobiliteit van Awingu uitgebreide online werkruimte, optimale beveiliging met gedetailleerde besturingselementen (bijvoorbeeld downloaden/uploadt), volledig gebruik van multi-factor Authentication (bijvoorbeeld Azure MFA), het opnemen van de sessie en meer controle krijgt. Out-of-the-box, Awingu kunnen documenten en delen van applicaties sessie voor geoptimaliseerde en beveiligde samenwerking.
De Awingu oplossing is multitenant, meerdere AD en open API. Deze wordt gebruikt door zowel grote als kleine bedrijven, Cloudserviceproviders en [ISV's](http://www.isv2saas.com). Deze klanten waarderen vooral Hallo eenvoudig te gebruiken, eenvoudig te installeren en lage totale Eigendomskosten.

Awingu alles in-één is [beschikbaar zijn in Azure Marketplace Hallo](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) met 2 ingebouwde gelijktijdige gebruikers. Aanvullende licenties zijn beschikbaar via een [breed scala aan distributeurs en resellers](http://www.awingu.com/reseller).

Meer informatie over [Awingu op als alternatieve tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).


> Primaire locatie: België
> 
> Operationele gebieden: EMEA, Noord-Amerika en Brazilië
> 
> RemoteApp- en bureaublad-sessie-oplossingen bieden: Ja, beide 
> 
> **Globale**:
> 
> Arnaud Marlière, CMO
> 
> E-mail:[arnaud@awingu.com](mailto:arnaud@awingu.com)
> 
> Telefoon: +1 646 583 3025
> 
> **België hoofdkantoor**:
> 
> B44 808 Ottergemsesteenweg-Zuid
> 
> 9000 Gent
> 
> E-mail:[info@awingu.com](mailto:info@awingu.com) 
> 
> Telefoon: +32 9 296 40 11
> 
> **VERENIGDE STATEN**:
> 
> 7 floor, Ave voor 1177 Hallo Americas,
> 
> New York, NY 10036
> 
> E-mail:[info.us@awingu.com](mailto:info.us@awingu.com)

### <a name="microsoft-hosted-service-provider"></a>Microsoft gehoste serviceprovider
Hosting partners bieden doorgaans een volledig beheerde, gehoste Windows-bureaublad en helpdesk Hallo partner met de licentieovereenkomsten met Microsoft application service, waaronder het beheer van hello Azure-resources, besturingssystemen, toepassingen en andere software-providers samen met een licentieovereenkomst voor serviceproviders tooallow directe verkoop van abonnee Access License (SAL) wordt. Hallo bevat volgende informatie details en informatie over het verkrijgen van een aantal Hallo hosters die zijn gespecialiseerd in het ondersteunen van klanten met hun Azure RemoteApp-migratie. Bekijk [Hallo huidige lijst met serviceproviders gehost](http://aka.ms/rdsonazurecertified) die Hallo RDS op IaaS learning pad en de evaluatie hebt voltooid.  

### <a name="citrix-service-provider-program"></a>Citrix-Service Provider-programma
Hallo programma voor Service Provider Citrix eenvoudig serviceproviders toodeliver Hallo eenvoud van virtuele cloud computing tooSMBs, het aanbieden van Hallo-services die ze in een model eenvoudig, betalen naar gebruik willen. Citrix-serviceproviders groeien hun Microsoft SPLA-bedrijven en hun RDS platform investeringen uitbreiden met een apparaat, overal toegang, Hallo breedste ondersteuning voor toepassingen, een rijke ervaring, extra beveiliging en verbeterde schaalbaarheid. Op zijn beurt Citrix serviceproviders meer abonnees trekken, de klanttevredenheid verhogen en de operationele kosten te verlagen. [Meer informatie](http://www.citrix.com/products/service-providers.html) of [vinden van een partner](https://www.citrix.com/buy/partnerlocator.html).

#### <a name="acuutech"></a>Acuutech
[Acuutech](http://www.acuutech.com) gespecialiseerd in het bieden van gehoste bureaublad oplossingen volledig bureaublad en ISV-toepassingen te bezorgen ervaringen gebouwd op Microsoft-technologie tooa globale client base van Azure en hun eigen datacenters.

> Primaire locatie: Londen, UK; Singapore; Houston, TX
> 
> Bewerkingsregio: overal ter wereld
> 
> Status partner: Gold
> 
> Microsoft Cloud-serviceprovider: Ja
> 
> RemoteApp- en bureaublad-sessie-oplossingen bieden: Ja, beide
> 
> Azure RemoteApp-oplossingen voor migratie: Ja, [meer informatie](http://www.acuutech.com/ara-migration/)
> 
> **Verenigd Koninkrijk**:
>   
> 5/6 York House, Langston weg,
>   
> Loughton, Essex IG10 3TQ
>   
> Telefoon: + 44 (0) 20 8502 2155
> 
> **Singapore**:
>   
> 100 Cecil straat, #09-02 
>   
> Hallo wereld, Singapore 069532
> 
> Telefoon: + 65 6709 4933
>   
> **Noord-Amerika**:
>   
> 3601 S. Sandman St.
>   
> Suite 200, Houston, TX 77098
>   
> Telefoon: +1 713 691 0800

#### <a name="aspex"></a>ASPEX
[ASPEX](http://www.aspex.be/en) gespecialiseerd in ISV's in een overgang toohello Cloud en ISV' opzoeken toooptimize hun huidige instellingen van de cloud. ASPEX biedt een breed scala aan beheerde services, devops en advies.  

> Primaire locatie: Antwerpen, België
> 
> Bewerkingsregio: West-Europa
> 
> Status partner: [zilver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)
> 
> Microsoft Cloud-serviceprovider: Ja
> 
> RemoteApp- en bureaublad-sessie-oplossingen bieden: Ja, beide
> 
> Azure RemoteApp-oplossingen voor migratie: Ja, [meer informatie](https://www.aspex.be/en/azure-remote-apps)
> 
> Telefoon: +3232202198
> 
> E-mail:[info@aspex.be](mailto:info@aspex.be)
> 
> Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)

#### <a name="caasecom"></a>Caase.com
[Caase.com](http://www.caase.com/) helpt bedrijven, lokale overheid, niet-overheidsorganisaties en gezondheidszorg instellingen met hun reis naar een betere manier van werk in Hallo Microsoft Cloud. Een productiever en veiliger op welke plaats, met een apparaat en lage IT-kosten. Caase.com is een waar gespecialiseerde voor Microsoft Office365, Azure, Enterprise Mobility en Security en Windows. Maakt een geoptimaliseerde en veilig platform voor samenwerking voor zowel klanten werknemers, partners en leveranciers met onze advies, migratieservices, acceptatie programma's, training, beheer en ondersteuning Caase.com.
Caase.com is Hallo mastermind van Hallo externe Azure-werkruimte (mobiele werkplek) en Hallo digitale werkplek (sociale Intranet). Beide oplossingen – bewerkstelligd met acceptatie – zijn Hallo foundation die zorgt ervoor dat gebruikers van deze oplossingen Hallo Hallo meest prettig, geslaagd en effectieve ervaring in hun route toohello Microsoft Cloud.
De vertaling van Nederlandse ánd een ondersteunende film hier: http://caase.com/over-ons/

> Bewerkingsregio: Nederlands gebaseerd, wereldwijde bereik
> 
> Status partner: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)
> 
> Microsoft Cloud-serviceprovider: Ja
> 
> RemoteApp- en bureaublad-sessie-oplossingen bieden: Ja, beide
> 
> Azure RemoteApp-oplossingen voor migratie: Ja, [meer](http://caase.com/diensten/microsoft-azure/).
> 
> 
> Nederland:
> 
> Rigtersbleek-Zandvoort 10 (De Spinnerij)
> 
> 7521 BE, Enschede
> 
> Telefoon: EnterIT + 31 (0) 88 4320 000


#### <a name="nerdio"></a>Nerdio
[Nerdio voor Azure](http://getnerdio.com/nfa/) is een automatiseringsplatform IT die heel eenvoudig inrichten, management en optimalisatie van de volledige IT-omgevingen in Hallo Microsoft cloud biedt. Onafhankelijk van de virtuele bureaubladen, externe apps en -servers in een paar uur. Hallo-omgeving in drie klikken beheren of minder met Nerdio-beheerportal. Gebruik intelligent automatisch schalen en 40% voor too60 opslaan in Azure IaaS-middelen.

> Primaire locatie: Chicago, zh-bewerkingsregio: status wereldwijd Partner: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft Cloud Service Provider: Ja
> 
> RemoteApp- en bureaublad-sessie-oplossingen bieden: Ja, beide
> 
> Azure RemoteApp-oplossingen voor migratie: Ja
> 
> 
> 8001 Lincoln Ave
> 
> Suite 212
> 
> Skokie IL 60077
> 
> USA
> 
> (844) 4NERDIO toest. 6
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a>**SaaSplaza**
[SaaSplaza](http://www.saasplaza.com/) biedt volledig Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) persoonlijke en openbare cloud (Azure).

> Primaire locatie: Nederland
> 
> Bewerkingsregio: overal ter wereld
> 
> Status partner: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)
> 
> Microsoft Cloud-serviceprovider: Ja
> 
> RemoteApp- en bureaublad-sessie-oplossingen bieden: Ja, beide
> 
> **EMEA**:
> 
> Prins Mauritslaan 29 35
> 
> 71 LP Badhoevedorp
> 
> Hallo Nederland
> 
> Telefoon: EnterIT + 31 20 547 8060 
> 
>  **Americas**:
> 
> 171 Saxony weg, Suite 105
> 
> Encinitas, CA 92024
> 
> Gouda
> 
> Verenigde Staten
> 
> Telefoon: +1 858 385 8900 
> 
> **APAC**:
> 
> 105 Cecil straat
>    
> \#11-08 Hallo achthoek
> 
> Singapore 069534
> 
> Singapore
>   
> Telefoon - Singapore: + 65 6222 6591
> 
> Telefoon - Australië: +61 2 8310 5568 
>    
> Telefoon - Nieuw-Zeeland: + 64 4 488 0321
> 
## <a name="need-more-help"></a>Meer hulp nodig?
Nog steeds moeten helpen kiezen of meer vragen hebt? Gebruik een van de volgende methoden tooget help Hallo. 

1. Een e-mail sturen naar [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com).
2. Neem contact op met [ondersteuning van Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Start via een [Azure ondersteuningsaanvraag](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
3. Ons te bellen. [Zoeken naar een lokaal verkoop nummer](https://azure.microsoft.com/overview/sales-number/).

