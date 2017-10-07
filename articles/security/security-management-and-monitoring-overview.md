---
title: aaaAzure beveiligingsbeheer en Bewakingsoverzicht | Microsoft Docs
description: " Azure biedt beveiliging mechanismen tooaid in Hallo beheren en controleren van de Azure-cloudservices en virtuele machines.  Dit artikel bevat een overzicht van deze core beveiligingsfuncties en -services. "
services: security
documentationcenter: na
author: TerryLanfear
manager: StevenPo
editor: TomSh
ms.assetid: 5cf2827b-6cd3-434d-9100-d7411f7ed424
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: terrylan
ms.openlocfilehash: 0026fa97bab7e15c9f8de6856b5075abe2288f61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-management-and-monitoring-overview"></a>Azure-beveiliging beheren en controleren van overzicht
Azure biedt beveiliging mechanismen tooaid in Hallo beheren en controleren van de Azure-cloudservices en virtuele machines. Dit artikel bevat een overzicht van deze core beveiligingsfuncties en -services. Tooarticles waarmee meer informatie over elk zodat u meer informatie vindt u koppelingen.

Hallo beveiliging van uw Microsoft-cloudservices is een samenwerking en gedeelde verantwoordelijkheid tussen u en Microsoft. Gedeelde verantwoordelijkheid betekent dat Microsoft is verantwoordelijk voor Hallo Microsoft Azure en fysieke beveiliging van de datacentra (met behulp van beveiligingsinstellingen, zoals vergrendelde badge vermelding deuren fences en schermen). Daarnaast biedt Azure sterk niveaus van beveiliging van de cloud op Hallo software laag die voldoet aan Hallo beveiliging, privacy en behoeften van de naleving van de veeleisende klanten.

Eigenaar van uw gegevens en identiteiten, Hallo verantwoordelijkheid voor het beveiligen van deze, Hallo beveiliging van uw lokale bronnen en beveiliging Hallo van cloud-onderdelen waarover u controle hebt. Microsoft biedt u met de besturingselementen en mogelijkheden toohelp beveiliging die u beveiligt uw gegevens en toepassingen. De mate van verantwoordelijkheid voor beveiliging is gebaseerd op Hallo-type van de cloudservice.

Hallo volgende diagram ziet u Hallo saldo van verantwoordelijkheid voor zowel Microsoft als Hallo klant.

![Gedeelde verantwoordelijkheid][1]

Zie voor meer informatie in het beveiligingsbeheer van, [beveiligingsbeheer in Azure](azure-security-management.md).

Hier volgen Hallo core functies toobe die in dit artikel:

* Op rollen gebaseerd toegangsbeheer
* Antimalware
* Meervoudige verificatie
* ExpressRoute
* Virtuele netwerkgateways
* Beschermde identiteitsbeheer
* Identiteitsbeveiliging
* Security Center

## <a name="role-based-access-control"></a>Op rollen gebaseerd toegangsbeheer
Op rollen gebaseerde toegangsbeheer (RBAC) biedt Geavanceerd toegangsbeheer voor Azure-resources. Met RBAC kunt verleent u mensen alleen Hallo hoeveelheid toegang die zij nodig hebben tooperform hun werk.  RBAC kunt u ervoor te zorgen dat wanneer mensen Hallo organisatie verlaten ze toegang tooresources in Hallo cloud.

Meer informatie:

* [Active Directory-teamblog van RBAC](http://i1.blogs.technet.com/b/ad/archive/2015/10/12/azure-rbac-is-ga.aspx)
* [Op rollen gebaseerde toegangsbeheer van Azure](../active-directory/role-based-access-control-configure.md)

## <a name="antimalware"></a>Antimalware
Met Azure, kunt u antimalware-software van toonaangevende leveranciers zoals Microsoft, Symantec, Trend Micro, McAfee en Kaspersky toohelp uw virtuele machines beschermen tegen schadelijke bestanden, adware en andere dreigingen.

Microsoft Antimalware biedt dat u de mogelijkheid tooinstall een antimalware-agent voor virtuele machines en PaaS-rollen Hallo. Op basis van System Center Endpoint Protection, biedt deze functie beproefde lokale beveiliging technologie toohello cloud.

We bieden ook diepe integratie voor de Trend [grondige beveiliging](http://www.trendmicro.com/us/enterprise/cloud-solutions/deep-security/)™ en [SecureCloud](http://www.trendmicro.com/us/enterprise/cloud-solutions/secure-cloud/)™ producten in hello Azure-platform. DeepSecurity is virussen te bestrijden en SecureCloud is een oplossing voor versleuteling. DeepSecurity wordt geïmplementeerd in virtuele machines met een extensiemodel. Gebruikersinterface voor het Hallo-portal en PowerShell gebruikt, kunt u toouse DeepSecurity in nieuwe virtuele machines die worden ingezet, of een bestaande virtuele machines die al zijn geïmplementeerd.

Symantec Endpoint Protection (SEP) wordt ook ondersteund in Azure. Klanten kunnen opgeven dat ze van plan toouse SEP binnen een virtuele machine bent via de portal integratie. SEP kan worden geïnstalleerd op een nieuwe virtuele machine via hello Azure-portal of kan worden geïnstalleerd op een bestaande virtuele machine met behulp van PowerShell.

Meer informatie:

* [Deploying Antimalware Solutions on Azure Virtual Machines](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/) (Antimalware-oplossingen implementeren op virtuele machines van Azure)
* [Microsoft Antimalware voor Azure-Cloudservices en virtuele Machines](azure-security-antimalware.md)
* [Hoe tooinstall en Trend Micro grondige Security configureren als een Service op een virtuele machine van Windows](../virtual-machines/windows/classic/install-trend.md)
* [Hoe tooinstall en Symantec Endpoint Protection configureren op een virtuele machine van Windows](../virtual-machines/windows/classic/install-symantec.md)
* [Nieuwe Antimalware-opties voor het beveiligen van virtuele Machines in Azure – McAfee Endpoint Protection](https://azure.microsoft.com/blog/new-antimalware-options-for-protecting-azure-virtual-machines/)

## <a name="multi-factor-authentication"></a>Meervoudige verificatie
Azure multi-factor authentication (MFA) is een authenticatiemethode die vereist Hallo gebruik van meer dan één verificatiemethode en voegt een cruciale tweede beveiligingslaag van beveiliging toouser aanmeldingen en transacties. MFA helpt beveiliging toegang toodata en toepassingen en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden. Levert sterke verificatie via een aantal opties voor verificatie: telefoonoproep, tekstbericht of mobiele app melding of verificatie van code en van derden OATH-tokens.

Meer informatie:

* [Multi-factor authentication](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [Wat is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)
* [De werking van Azure multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="expressroute"></a>ExpressRoute
Microsoft Azure ExpressRoute kunt u uw on-premises netwerken in Hallo Microsoft cloud uitbreiden via een speciale persoonlijke verbinding die wordt gefaciliteerd door een connectiviteitsprovider. Met ExpressRoute kunt kunt u verbindingen tooMicrosoft cloudservices, zoals Microsoft Azure, Office 365 en CRM Online maken. Via een connectiviteitsprovider in een co-locatiefaciliteit is connectiviteit mogelijk vanuit een any-to-any (IP VPN) netwerk, een point-to-point Ethernet-netwerk of een virtuele overlappende verbinding. ExpressRoute-verbindingen gaan niet via Hallo openbare Internet. ExpressRoute-verbindingen toooffer kan dit meer betrouwbaarheid, sneller en hebben ze lagere latenties en betere beveiliging dan gewone verbindingen via Internet Hallo.

Meer informatie:

* [Technisch overzicht van ExpressRoute](../expressroute/expressroute-introduction.md)

## <a name="virtual-network-gateways"></a>Virtuele netwerkgateways
VPN-Gateways, ook wel Azure virtuele netwerkgateways, zijn gebruikt toosend netwerkverkeer tussen virtuele netwerken en lokale locaties. Ze zijn ook gebruikte toosend verkeer tussen meerdere virtuele netwerken in Azure (VNet-naar-VNet).  VPN-gateways bieden beveiligde cross-premises-connectiviteit tussen Azure en uw infrastructuur.

Meer informatie:

* [Over VPN-gateways](../vpn-gateway/vpn-gateway-about-vpngateways.md)
* [Overzicht van Azure-netwerk-beveiliging](security-network-overview.md)

## <a name="privileged-identity-management"></a>Privileged Identity Management
Gebruikers moeten soms toocarry bevoorrechte bewerkingen in Azure-resources of andere SaaS-toepassingen. Dit betekent vaak organisaties hebben toogive ze permanente bevoegde toegang in Azure Active Directory (Azure AD). Dit is een groeiende beveiligingsrisico voor cloud-gebaseerde bronnen omdat organisaties voldoende kunnen niet controleren wat gebruikers doen met hun bevoorrechte toegang.
Als een gebruikersaccount met uitgebreide toegang is aangetast, kan die een inbreuk bovendien invloed op uw algehele beveiliging van de cloud. Azure AD Privileged Identity Management helpt tooresolve dit risico door Hallo blootstellingstijd bevoegdheden te verlagen en inzicht in gebruik te verhogen.  

Privileged Identity Management introduceert Hallo concept van een tijdelijke beheerder voor een functie of 'just in time' beheerderstoegang, die een gebruiker die moet toocomplete een activeringsproces voor die rol is toegewezen. Hallo activering proceswijzigingen Hallo toewijzing van de gebruikersrol tooa Hallo in Azure AD van inactieve tooactive voor een opgegeven periode zoals acht uur.

Meer informatie:

* [Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-configure.md)
* [Aan de slag met Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-getting-started.md)

## <a name="identity-protection"></a>Identiteitsbeveiliging
Azure Active Directory (AD) Identity Protection biedt een totaaloverzicht van verdachte activiteiten voor aanmelden en mogelijke beveiligingsproblemen toohelp beveiligen van uw bedrijf. Identity Protection detecteert verdachte activiteiten voor gebruikers en bevoegdheden (admin) identiteiten, op basis van signalen zoals brute-force-aanvallen gelekte referenties en aanmeldingen vanaf onbekende locaties en geïnfecteerde apparaten.

Dankzij de meldingen en aanbevolen herstel, helpt Identity Protection toomitigate risico's in realtime. Gebruiker risico ernst wordt berekend en kunt u beleid op basis van risico tooautomatically help beveiliging toegang tot toepassingen tegen toekomstige configureren.

Meer informatie:

* [Azure Active Directory Identity Protection](../active-directory/active-directory-identityprotection.md)
* [Channel 9: Azure AD en Identity weergeven: Identity Protection Preview](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="security-center"></a>Security Center
Azure Security Center helpt u bij het detecteren, voorkomen van en reageren toothreats en biedt dat u grotere zichtbaarheid van, en controle over, Hallo beveiliging van uw Azure-resources. Het biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen, helpt bedreigingen te detecteren die anders onopgemerkt zouden blijven, en werkt met een uitgebreid ecosysteem van beveiligingsoplossingen.

Security Center helpt u te optimaliseren en Hallo beveiliging van uw Azure-resources door te controleren:

* Zodat u toodefine beleidsregels voor uw Azure-abonnementresources tooyour op basis van het bedrijf beveiliging moet en type toepassingen of de vertrouwelijkheid van gegevens in elk abonnement Hallo Hallo.
* Hallo-status van uw virtuele Azure-machines, netwerken en toepassingen bewaken.
* Beveiligingswaarschuwingen, met inbegrip van waarschuwingen van geïntegreerde partners oplossingen, samen met de Hallo-informatie die u nodig hebt tooquickly onderzoeken en aanbevelingen voor het bieden van een lijst met prioriteit tooremediate een aanval.

Meer informatie:

* [Inleiding tooAzure Security Center](../security-center/security-center-intro.md)

<!--Image references-->
[1]: ./media/security-management-and-monitoring-overview/shared-responsibility.png
