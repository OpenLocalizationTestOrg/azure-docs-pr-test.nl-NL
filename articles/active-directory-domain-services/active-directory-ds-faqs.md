---
title: aaaFAQs - Azure Active Directory Domain Services | Microsoft Docs
description: Veelgestelde vragen over Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 48731820-9e8c-4ec2-95e8-83dba1e58775
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: maheshu
ms.openlocfilehash: 42a6d659f6408bf694cb2aa6ec24bff7a76b0565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-domain-services-frequently-asked-questions-faqs"></a>Azure Active Directory Domain Services: Veelgestelde vragen (FAQ's)
Deze pagina antwoorden op veelgestelde vragen over hello Azure Active Directory Domain Services. Houd regelmatig op updates controleren.

### <a name="troubleshooting-guide"></a>Handleiding voor het oplossen van problemen
Raadpleeg tooour [Troubleshooting guide](active-directory-ds-troubleshooting.md) voor oplossingen toocommon problemen wanneer aangetroffen configureren of het beheer van Azure AD Domain Services.

### <a name="configuration"></a>Configuratie
#### <a name="can-i-create-multiple-domains-for-a-single-azure-ad-directory"></a>Kan ik meerdere domeinen voor één maken Azure AD-directory?
Nee. U kunt slechts één domein die door Azure AD Domain Services voor één verwerkt maken Azure AD-directory.  

#### <a name="can-i-enable-azure-ad-domain-services-in-an-azure-resource-manager-virtual-network"></a>Kan ik Azure AD Domain Services in een virtueel netwerk van Azure Resource Manager inschakelen?
Nee. Azure AD Domain Services kunnen alleen worden ingeschakeld in de klassieke Azure-netwerk. U kunt verbinden Hallo klassiek virtueel netwerk tooa Resource Manager virtueel netwerk met virtuele netwerk peering toouse uw beheerde domein in een virtueel netwerk van Resource Manager.

#### <a name="can-i-enable-azure-ad-domain-services-in-a-federated-azure-ad-directory-i-use-adfs-tooauthenticate-users-for-access-toooffice-365-can-i-enable-azure-ad-domain-services-for-this-directory"></a>Kan ik inschakelen Azure AD Domain Services in een federatieve Azure AD-directory? Ik ADFS tooauthenticate gebruikers gebruiken voor toegang tot tooOffice 365. Kan ik Azure AD Domain Services voor deze directory inschakelen?
Nee. Azure AD Domain Services moeten toegang tot toohello wachtwoord-hashes van gebruikersaccounts, tooauthenticate gebruikers via NTLM of Kerberos. In een federatieve map worden wachtwoord-hashes niet opgeslagen in hello Azure AD-directory. Azure AD Domain Services werkt daarom niet met dergelijke Azure AD-mappen.

#### <a name="can-i-make-azure-ad-domain-services-available-in-multiple-virtual-networks-within-my-subscription"></a>Kan ik Azure AD Domain Services beschikbaar maken in meerdere virtuele netwerken in mijn abonnement?
Hallo-service zelf ondersteunt dit scenario niet direct. Azure AD Domain Services is beschikbaar in slechts één virtueel netwerk tegelijk. U kunt echter verbinding tussen meerdere virtuele netwerken tooexpose Azure AD Domain Services tooother virtuele netwerken configureren. Dit artikel wordt beschreven hoe u kunt [verbinding maken met virtuele netwerken in Azure](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

#### <a name="can-i-enable-azure-ad-domain-services-using-powershell"></a>Kan ik Azure AD Domain Services met behulp van PowerShell inschakelen?
PowerShell/geautomatiseerde implementatie van Azure AD Domain Services is momenteel niet beschikbaar.

#### <a name="is-azure-ad-domain-services-available-in-hello-new-azure-portal"></a>Azure AD Domain Services beschikbaar is in de nieuwe Azure portal Hallo?
Nee. Azure AD Domain Services kunnen worden geconfigureerd alleen in Hallo [klassieke Azure-portal](https://manage.windowsazure.com). We verwachten tooextend ondersteuning voor Hallo [Azure-portal](https://portal.azure.com) in toekomstige Hallo.

#### <a name="can-i-add-domain-controllers-tooan-azure-ad-domain-services-managed-domain"></a>Kan ik domain controllers tooan Azure AD Domain Services beheerd domein toevoegen?
Nee. Hallo-domein verstrekt door Azure AD Domain Services is een beheerd domein. U hoeft geen tooprovision, configureren of anders domeincontrollers voor dit domein - deze activiteiten worden door Microsoft geleverd als een service management te beheren. U kunt extra domeincontrollers (alleen-lezen of alleen-lezen) voor het beheerde domein Hallo daarom niet toevoegen.

### <a name="administration-and-operations"></a>Beheer en bewerkingen
#### <a name="can-i-connect-toohello-domain-controller-for-my-managed-domain-using-remote-desktop"></a>Kan ik voor mijn beheerde domein maken met extern bureaublad toohello domeincontroller verbinden?
Nee. U beschikt niet over machtigingen tooconnect toodomain controllers voor beheerde domein Hallo via Extern bureaublad. Leden van Hallo ' AAD DC' beheerdersgroep beheren Hallo beheerde domein met AD-beheerprogramma's zoals Hallo Active Directory Administration Center (ADAC) of AD PowerShell. Deze hulpprogramma's zijn geïnstalleerd met behulp van Hallo 'Remote Server Administration Tools' functie op een Windows-server is toegevoegd aan het beheerde domein toohello.

#### <a name="ive-enabled-azure-ad-domain-services-what-user-account-do-i-use-toodomain-join-machines-toothis-domain"></a>Ik heb de Azure AD Domain Services hebt ingeschakeld. Welke gebruikersaccount gebruik ik toodomain join machines toothis domein?
Leden van de beheergroep 'AAD DC-beheerders' hello kunnen domein machines. Bovendien krijgen leden van deze groep toegang tot extern bureaublad-toomachines die gekoppeld toohello domein zijn.

#### <a name="do-i-have-domain-administrator-privileges-for-hello-managed-domain-provided-by-azure-ad-domain-services"></a>Heb ik domeinadministratorrechten voor Hallo beheerde domein verstrekt door Azure AD Domain Services?
Nee. U beheerdersbevoegdheden op Hallo beheerd domein niet krijgen. Bevoegdheden zowel ' domeinbeheerder ' en ' ondernemingsbeheerder ' zijn niet beschikbaar voor toouse binnen Hallo-domein. Bestaande domeinbeheerder of enterprise-beheerder groepen binnen uw Azure AD-directory worden ook niet verleend domein/enterprise administrator-bevoegdheden op Hallo-domein.

#### <a name="can-i-modify-group-memberships-using-ldap-or-other-ad-administrative-tools-on-managed-domains"></a>Kan ik met LDAP-Adreslijst of andere beheerprogramma's van AD op beheerde domeinen groepslidmaatschappen wijzigen?
Nee. Groepslidmaatschappen kunnen niet worden gewijzigd in domeinen die door Azure AD Domain Services zijn verwerkt. Hallo geldt ook voor gebruikerskenmerken. U kunt echter groepslidmaatschappen of gebruikerskenmerken wijzigen in Azure AD of op uw lokale domein. Dergelijke wijzigingen worden automatisch gesynchroniseerd tooAzure AD Domain Services.

#### <a name="how-long-does-it-take-for-changes-i-make-toomy-azure-ad-directory-toobe-visible-in-my-managed-domain"></a>Hoe lang duurt het voor wijzigingen ik toomy Azure AD-directory toobe zichtbaar te maken in mijn beheerde domein?
Wijzigingen in uw Azure AD-directory met hello Azure AD-gebruikersinterface of PowerShell zijn gesynchroniseerd tooyour beheerd domein. Dit synchronisatieproces wordt uitgevoerd op de achtergrond Hallo. Nadat Hallo eenmalige initiële synchronisatie van uw adreslijst voltooid is, wordt doorgaans duurt ongeveer 20 minuten om de wijzigingen in Azure AD toobe weerspiegeld in uw beheerde domein.

#### <a name="can-i-extend-hello-schema-of-hello-managed-domain-provided-by-azure-ad-domain-services"></a>Kan ik uitbreiden Hallo-schema van het beheerde domein Hallo geleverd door Azure AD Domain Services?
Nee. Hallo-schema wordt beheerd door Microsoft voor Hallo beheerde domein. Schema-uitbreidingen worden niet ondersteund door Azure AD Domain Services.

#### <a name="can-i-modify-or-add-dns-records-in-my-managed-domain"></a>Kan ik wijzigen of de DNS-records toevoegen aan mijn beheerde domein?
Ja. Leden van groep Hallo 'AAD DC Administrators' ' DNS-beheerder '-bevoegdheden krijgen toomodify DNS registreert in het beheerde domein Hallo. Hallo DNS-beheerconsole op een machine met Windows Server gekoppelde toohello beheerd domein, toomanage DNS kan worden gebruikt. toouse hello console DNS-beheer, ' DNS-Server hulpprogramma's installeren ', dat deel uitmaakt van Hallo 'Remote Server Administration Tools' optionele functie op Hallo-server. Meer informatie over [hulpprogramma's voor beheer, bewaking en probleemoplossing van DNS](https://technet.microsoft.com/library/cc753579.aspx) is beschikbaar op TechNet.

### <a name="billing-and-availability"></a>Facturering en beschikbaarheid
#### <a name="is-azure-ad-domain-services-a-paid-service"></a>Is dat Azure AD Domain Services een betaalde service?
Ja. Zie voor meer informatie, Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/active-directory-ds/).

#### <a name="is-there-a-free-trial-for-hello-service"></a>Is er een gratis proefversie voor Hallo service?
Deze service is opgenomen in de gratis proefversie Hallo voor Azure. U kunt zich aanmelden voor een [gratis proefversie van Azure één maand](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="can-i-get-azure-ad-domain-services-as-part-of-enterprise-mobility-suite-ems-do-i-need-azure-ad-premium-toouse-azure-ad-domain-services"></a>Kan ik Azure AD Domain Services krijgen als onderdeel van Enterprise Mobility Suite (EMS)? Heb ik nodig Azure AD Premium toouse Azure AD Domain Services?
Nee. Azure AD Domain Services is een betalen naar gebruik Azure-service en maakt geen deel uit van EMS. Azure AD Domain Services kan worden gebruikt met alle edities van Azure AD (gratis, Basic, en Premium). U wordt gefactureerd op uurbasis, afhankelijk van gebruik.

#### <a name="what-azure-regions-is-hello-service-available-in"></a>Welke Azure-regio's is het Hallo-service beschikbaar is in?
Raadpleeg toohello [Azure-Services per regio](https://azure.microsoft.com/regions/#services/) toosee een lijst van pagina hello Azure-regio's waar Azure AD Domain Services beschikbaar is.
