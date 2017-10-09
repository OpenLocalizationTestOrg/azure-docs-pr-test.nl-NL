---
title: aaaSecuring PaaS-implementaties | Microsoft Docs
description: " Hallo beveiligingsvoordelen van PaaS ten opzichte van andere servicemodellen cloud begrijpen en meer informatie over aanbevolen procedures voor het beveiligen van uw Azure-PaaS-implementatie. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: techlake
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: terrylan
ms.openlocfilehash: b94fe03b6f3a43d82e1e6e834f10a423e4c1db95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-deployments"></a>PaaS-implementaties beveiligen

Dit artikel bevat informatie die u helpt:

- Hallo beveiligingsvoordelen van toepassingen in de cloud Hallo hosting begrijpen
- Hallo beveiligingsvoordelen van platform als een service (PaaS) ten opzichte van andere servicemodellen cloud evalueren
- De focus van de beveiliging van een netwerk gericht tooan identiteit gericht perimeter beveiliging aanpak wijzigen
- Algemene PaaS beveiligingsaanbevelingen implementeren

## <a name="cloud-security-advantages"></a>Beveiligingsvoordelen van de cloud
Er zijn beveiliging voordelen toobeing in Hallo cloud. In een on-premises omgeving organisaties waarschijnlijk hebben voldaan verantwoordelijkheden en beperkte bronnen beschikbaar tooinvest in de beveiliging, die wordt gemaakt van een omgeving waarin aanvallers kunnen tooexploit beveiligingsproblemen voor alle lagen.

![Beveiligingsvoordelen van de vormgeving van de cloud][1]

Organisaties kunnen tooimprove hun detectie van dreigingen en reactietijden met behulp van de cloud-gebaseerde beveiligingsmogelijkheden en cloud intelligence van de provider zijn.  Doordat verantwoordelijkheden toohello cloudprovider organisaties meer beveiliging dekking, waardoor ze tooreallocate beveiligingsbronnen en krijgt budget tooother zakelijke prioriteiten.

## <a name="division-of-responsibility"></a>Deling van verantwoordelijkheid
Het is belangrijk toounderstand Hallo deling van verantwoordelijkheid tussen u en Microsoft. On-premises eigenaar van de hele stack Hallo maar tijdens het verplaatsen van toohello cloud bepaalde verantwoordelijkheden tooMicrosoft overbrengen. Hallo volgende verantwoordelijkheid matrix geeft Hallo gebieden van Hallo-stack in een SaaS PaaS en IaaS-implementatie die u verantwoordelijk bent voor en Microsoft is verantwoordelijk voor.

![Verantwoordelijkheid zones][2]

Voor alle cloud-implementatietypen die eigenaar u van uw gegevens en identiteiten. U bent zelf verantwoordelijk voor het Hallo-bescherming van uw gegevens en identiteiten, lokale bronnen en Hallo cloud-onderdelen die u beheert (dit verschilt per servicetype).

Taken die altijd door u, ongeacht Hallo type implementatie behouden, zijn:

- Gegevens
- Eindpunten
- Account
- Toegangsbeheer

## <a name="security-advantages-of-a-paas-cloud-service-model"></a>Beveiligingsvoordelen van een PaaS-cloud-servicemodel
Dezelfde verantwoordelijkheid matrix gebruiken we Hallo bekijkt hello beveiligingsvoordelen van een Azure-PaaS-implementatie tegenover on-premises.

![Beveiligingsvoordelen van PaaS][3]

Hallo onder aan de stack hello, Hallo fysieke infrastructuur, vanaf vermindert Microsoft algemene risico's en verantwoordelijkheden. Omdat Microsoft cloud Hallo voortdurend wordt bewaakt door Microsoft, is het vaste tooattack. Niet dat u voor een aanvaller toopursue Hallo Microsoft cloud als doel. Tenzij Hallo aanvaller veel geld en bronnen, Hallo aanvaller heeft is het waarschijnlijk toomove op tooanother doel.  

In het midden van de Hallo van Hallo stack is er geen verschil tussen een PaaS-implementatie en on-premises. Hallo toepassingslaag en Hallo-account en toegang beheerlaag hebt u vergelijkbare risico's. Hallo volgende stappen sectie van dit artikel en leidt we u toobest procedures voor het verwijderen van of deze risico's te minimaliseren.

Bovenaan Hallo Hallo stack, gegevensbeheer en rights management, moet u één risico's die kan worden verholpen door Sleutelbeheer ondernemen. (Key management wordt beschreven in de aanbevolen procedures.) Sleutelbeheer is een extra verantwoordelijkheid, hebt u gebieden in een PaaS-implementatie dat u niet langer toomanage hebt zodat u resources tookey management kunt verplaatsen.

Hello Azure-platform biedt u ook sterk DDoS-bescherming met behulp van verschillende technologieën op het netwerk. Alle soorten DDoS-bescherming-methoden op basis van een netwerk hebben echter hun beperkingen op basis van per koppeling en per datacenter. toohelp hello invloed van grote DDoS-aanvallen te voorkomen, kunt u profiteren van de mogelijkheden van Azure core cloud van zodat u tooquickly en automatisch scale-out toodefend tegen DDoS-aanvallen. Gaan we meer informatie over hoe u dit in Hallo aanbevolen procedures voor artikelen doen kunt.

## <a name="modernizing-hello-defenders-mindset"></a>De modernisering Hallo defender denkt
Implementaties worden geleverd met PaaS een verschuiving van uw algehele benadering toosecurity. U verplaatst van toocontrol hoeven alles zelf toosharing verantwoordelijkheid met Microsoft.

Een ander belangrijk verschil tussen PaaS en traditionele on-premises implementaties, is een nieuwe weergave van wat Hallo primaire beveiliging perimeter definieert. In het verleden hebben Hallo primaire lokale beveiliging perimeter is uw netwerk en meest on-premises beveiliging ontwerpen gebruik Hallo netwerk als de primaire beveiliging pivot. Voor PaaS-implementaties, u beter geleverd door identiteit toobe Hallo primaire beveiliging perimeter rekening te houden.

## <a name="identity-as-hello-primary-security-perimeter"></a>Identiteit als Hallo primaire beveiliging perimeter
Een van de Hallo vijf belangrijke kenmerken van cloudcomputing is ruime netwerktoegang netwerk gericht waardoor denkt minder relevante. Hallo-doel van veel van cloudcomputing is tooallow gebruikers tooaccess netwerkbronnen ongeacht de locatie. Voor de meeste gebruikers gaat hun locatie toobe ergens op Hallo Internet.

Hallo volgende afbeelding ziet u hoe Hallo beveiliging perimeter van een netwerkverbinding perimeter tooan identiteit heeft ontwikkeld. Beveiliging wordt minder over uw netwerk te beschermen en meer informatie over uw gegevens beschermen, evenals Hallo beveiliging van uw apps en gebruikers beheren. Hallo belangrijkste verschil is dat u wilt dat toopush beveiliging dichter toowhat van belangrijke tooyour bedrijf.

![Identiteit als nieuwe beveiliging perimeter][4]

In eerste instantie opgegeven Azure PaaS-services (bijvoorbeeld webrollen en Azure SQL) weinig of geen traditioneel netwerk perimeter-beveiliging. Het is begrepen dat Hallo-element doel toobe blootgesteld toohello Internet (Webrol was) en dat de verificatie nieuwe perimeter hello (bijvoorbeeld BLOB of Azure SQL biedt).

Moderne beveiligingsprocedures wordt ervan uitgegaan dat adversary Hallo Hallo-netwerkverbinding is geschonden. Moderne verdediging procedures zijn daarom tooidentity verplaatst. Organisaties moeten een perimeternetwerk beveiliging op basis van identiteit met sterke verificatie en autorisatie hygiëne (aanbevolen procedures) maken.

## <a name="recommendations-for-managing-hello-identity-perimeter"></a>Aanbevelingen voor het beheren van Hallo identiteit perimeter

Principes en patronen voor Hallo-netwerkverbinding zijn al beschikbaar jarenlang. Hallo industrie heeft daarentegen relatief minder ervaring met het gebruik van de identiteit als Hallo primaire beveiliging perimeternetwerk. Met die gezegd, we voldoende tooprovide ervaring enkele algemene aanbevelingen die in het veld Hallo zijn beproefde hebben verzameld en toepassen tooalmost alle PaaS-services.

Hallo volgende ziet u een algemene best practices benadering toomanaging het perimeternetwerk van uw identiteit.

- **Uw sleutels of referenties niet verliezen** sleutels en referenties beveiligen is essentieel toosecure PaaS-implementaties. Sleutels en referenties verliezen is een veelvoorkomend probleem. Een goede oplossing is toouse gecentraliseerd waarin sleutels en geheimen in hardware security modules (HSM) kunnen worden opgeslagen. Azure biedt u een HSM in de cloud Hallo met [Azure Key Vault](../key-vault/key-vault-whatis.md).
- **Plaats geen referenties en andere geheime informatie in de broncode of GitHub** Hallo alleen ding erger dan onbevoegden toegang verliezen uw sleutels en referenties heeft toegang toothem tot. Aanvallers zijn kunnen tootake profiteren van bot technologieën toofind sleutels en geheimen die zijn opgeslagen in de code-opslagplaatsen zoals GitHub. Plaats niet sleutel en geheimen in deze openbare broncodeopslagplaatsen.
- **Beveiligen van uw VM-beheerinterfaces van hybride PaaS- en IaaS** IaaS en PaaS-services worden uitgevoerd op virtuele machines (VM's). Hallo-type van de service, verschillende beheerinterfaces zijn beschikbaar afhankelijk van waarmee u tooremote deze virtuele machines rechtstreeks beheren. Extern beheer protocollen zoals [Secure Shell Protocol (SSH)](https://en.wikipedia.org/wiki/Secure_Shell), [Remote Desktop Protocol (RDP)](https://support.microsoft.com/kb/186607), en [externe PowerShell](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enable-psremoting) kan worden gebruikt. In het algemeen is het raadzaam dat u niet direct RAS tooVMs van Hallo Internet inschakelt. Indien beschikbaar, moet u alternatieve methoden zoals het gebruik van virtueel particulier netwerk in een Azure-netwerk. Als alternatieve methoden zijn niet beschikbaar, zorg ervoor dat u complexe wachtwoordzinnen en indien beschikbaar, tweeledige verificatie (zoals [Azure multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)).
- **Sterke verificatie en autorisatie platforms gebruiken**

  - Federatieve identiteiten in Azure AD in plaats van een aangepaste gebruiker winkels gebruiken. Wanneer u een federatieve identiteiten gebruikt, u profiteren van een benadering op basis van het platform en Hallo beheer van bevoegde identiteiten tooyour partners te delegeren. Een benadering van federatieve identiteiten is vooral belangrijk in scenario's wanneer werknemers worden beëindigd en dat er informatie toobe moet worden weergegeven via meerdere identiteit en autorisatie systemen.
  - Gebruik platform opgegeven mechanismen voor verificatie en autorisatie in plaats van aangepaste code. Hallo reden is dat het ontwikkelen van aangepaste verificatiecode foutgevoelig kan worden. De meeste van uw ontwikkelaars niet beveiligingsexperts zijn en onwaarschijnlijk toobe rekening houden met Hallo eigenaardigheden en Hallo nieuwste wereldwijde ontwikkelingen verificatie en autorisatie. Commerciële code (bijvoorbeeld van Microsoft) is vaak grote schaal beveiliging gecontroleerd.
  - Meervoudige verificatie gebruiken. Multi-factor authentication-server is de huidige Hallo standaard voor verificatie en autorisatie, omdat dit voorkomt het Hallo beveiliging zwakke punten van de gebruikersnaam en wachtwoord typen verificatie. Toegang tooboth hello Azure (portal/externe PowerShell) beheerinterfaces en toocustomer gerichte services moeten worden ontworpen en geconfigureerd toouse [Azure multi-factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md).
  - Gebruik standaard verificatieprotocollen, zoals OAuth2- en Kerberos. Deze protocollen zijn uitgebreid onderzocht en waarschijnlijk worden geïmplementeerd als onderdeel van uw platformbibliotheken voor verificatie en autorisatie.

## <a name="next-steps"></a>Volgende stappen
In dit artikel is gericht op beveiligingsvoordelen van een Azure-PaaS-implementatie. Vervolgens leert u aanbevolen procedures voor het beveiligen van uw PaaS-web- en mobile-oplossingen. We beginnen met Azure App Service, Azure SQL Database en Azure SQL Data Warehouse. Artikelen over de aanbevolen procedures voor andere Azure-services beschikbaar komen, worden koppelingen vermeld in Hallo volgende lijst:

- [Azure App Service](security-paas-applications-using-app-services.md)
- [Azure SQL Database en Azure SQL datawarehouse](security-paas-applications-using-sql.md)
- Azure Storage
- Azure REDIS-Cache
- Azure Service Bus
- Web Application Firewalls

<!--Image references-->
[1]: ./media/security-paas-deployments/advantages-of-cloud.png
[2]: ./media/security-paas-deployments/responsibility-zones.png
[3]: ./media/security-paas-deployments/advantages-of-paas.png
[4]: ./media/security-paas-deployments/identity-perimeter.png
