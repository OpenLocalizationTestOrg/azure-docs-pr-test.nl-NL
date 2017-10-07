---
title: overzicht van aangepaste domeinnamen in Azure Active Directory aaaConceptual | Microsoft Docs
description: Hallo conceptuele framework voor het gebruik van aangepaste domeinnamen in Azure Active directory, inclusief federation voor eenmalige aanmelding wordt uitgelegd
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: fd0c5def-0da2-43af-81bc-76f4cfe86afd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 0a3454ae6b733a8a13a71925df3cc664063f388e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="conceptual-overview-of-custom-domain-names-in-azure-active-directory"></a>Conceptueel overzicht van aangepaste domeinnamen in Azure Active Directory
Een domeinnaam zijn een belangrijk id voor veel directoryresources als onderdeel van:

* Een gebruikersnaam of e-mailadres voor een gebruiker
* Hallo-adres voor een groep
* Hallo app ID URI voor een toepassing

Een resource in Azure Active Directory (Azure AD), kan een domeinnaam die al is geverifieerd toobe eigendom van Hallo directory die Hallo-bron bevat bevatten. Alleen een globale beheerder kunt domein-beheertaken uitvoeren in Azure AD.

> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel. Zie voor hoe toomanage uw in hello Azure AD-beheercentrum domeinnamen, [aangepaste domeinnamen in uw Azure Active Directory beheren](active-directory-domains-manage-azure-portal.md).

Domeinnamen in Azure AD zijn globaal uniek. Een aangepaste domeinnaam kan worden gebruikt door slechts één Azure AD-tenant tegelijk. Als een Azure AD-directory kan een domeinnaam is geverifieerd, kan er geen andere Azure AD-directory de controleren of die dezelfde domeinnaam gebruikt.

## <a name="initial-and-custom-domain-names"></a>Initiële en aangepaste domeinnamen
Elke domeinnaam in Azure AD is een initiële domeinnaam of een aangepaste domeinnaam.

Elke Azure AD wordt geleverd met een initiële domeinnaam in Hallo formulier contoso.onmicrosoft.com. Deze derde niveau domeinnaam, in dit voorbeeld 'contoso.onmicrosoft.com', is gemaakt toen het Hallo-map is gemaakt, doorgaans door Hallo beheerder die Hallo directory gemaakt. Hallo initiële domeinnaam voor een map kan niet worden gewijzigd of verwijderd. Hallo initiële domeinnaam, is terwijl volledig functioneel bedoeld voornamelijk toobe gebruikt als mechanisme bootstrapping tot en met een aangepaste domeinnaam is geverifieerd.

Een map heeft ten minste één geverifieerde aangepast domein, zoals 'contoso.com', en is die aangepaste domein dat is zichtbaar tooend gebruikers in de meeste productieomgevingen. Een aangepaste domeinnaam is een domeinnaam die eigendom is van en die wordt gebruikt door de organisatie, zoals 'contoso.com', voor toepassingen zoals die als host fungeert voor de website. Deze domeinnaam is bekend tooemployees omdat deze deel uitmaakt van de gebruikersnaam Hallo ze toosign in het bedrijfsnetwerk toohello of toosend gebruiken en ophalen van e-mail.

Voordat deze kan worden gebruikt door Azure AD, wordt de aangepaste domeinnaam Hallo moet toegevoegde tooyour directory en gecontroleerd.

## <a name="verified-and-unverified-domain-names"></a>Geverifieerde en niet-geverifieerde domeinnamen
Hallo initiële domeinnaam voor een map wordt impliciet geëvalueerd als geverifieerd door Azure AD. Als een beheerder een aangepast domein naam tooan Azure AD toevoegt, is in eerste instantie in een niet-geverifieerde status. Azure AD staat elke directory resources toouse niet de naam van een niet-geverifieerd domein. Dit zorgt ervoor dat slechts één directory de naam van een bepaald domein kunt gebruiken, en dat Hallo organisatie gebruikmaakt van de domeinnaam Hallo daadwerkelijk eigenaar is van deze domeinnaam.

Azure AD verifieert eigendom van een domeinnaam door te zoeken naar een bepaalde vermelding in Hallo domain name service (DNS)-zonebestand voor Hallo domeinnaam. tooverify eigendom van een domeinnaam, een beheerder met deze eigenschap Hallo DNS-vermelding van Azure AD wordt gezocht naar Azure AD en voegt deze vermelding toohello DNS-zonebestand voor Hallo domeinnaam. Hallo DNS-zonebestand wordt beheerd door Hallo domeinnaamregistrar voor dat domein. Hallo stappen tooverify een domein worden weergegeven in het Hallo-artikel voor [toevoegen van een aangepast domein tooyour Azure AD-directory](active-directory-add-domain.md).

Een DNS-vermelding toohello zonebestand voor Hallo domeinnaam toe te voegen, heeft dit geen invloed op de andere domain-services zoals e-mail of webhosting.

## <a name="federated-and-managed-domain-names"></a>Federatieve en beheerde domeinnamen
Een aangepaste domeinnaam in Azure AD geconfigureerde toogive gebruikers een federatieve aanmeldingsprocedure tussen uw lokale Active Directory en Azure AD kunnen worden. Configureren van een domein voor Federatie vereist tooprivileged resources in Azure AD-updates en ook tooyour Windows Server Active Directory. Configureren van die een federatieve domein moet worden uitgevoerd vanaf de Azure AD Connect of met behulp van PowerShell. Een aangepast domein Federatie kan niet worden gestart vanuit Hallo klassieke Azure-portal. [Bekijk deze video toolearn over het configureren van AD FS voor aanmelden gebruiker Azure AD Connect](http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect).

Domeinen die niet worden gefedereerd worden wel beheerde domeinen. Hallo eerste domein voor een Azure AD-adreslijst wordt impliciet geëvalueerd als een beheerd domein.

## <a name="primary-domain-names"></a>Primaire domeinnamen
Hallo primaire domeinnaam voor een map is Hallo-domeinnaam die is vooraf geselecteerd als de standaardwaarde Hallo Hallo 'domein' deel van het Hallo-gebruikersnaam, wanneer een beheerder maakt een nieuwe gebruiker in Hallo [Azure-portal](https://portal.azure.com/), of een andere portal zoals Hallo Office 365-beheerportal of Hallo Microsoft Intune-portal. Een map kan slechts één primair domeinnaam hebben. Een beheerder kan Hallo primair domein naam toobe wijzigen, een geverifieerde aangepaste domein dat niet federatief of toohello eerste domein.

## <a name="domain-names-in-azure-ad-and-other-microsoft-online-services"></a>Domeinnamen in Azure AD en andere Microsoft Online Services
De naam van een domein moet worden geverifieerd in Azure AD voordat deze kan worden gebruikt door een andere Microsoft Online Service zoals Exchange Online, SharePoint Online en Intune. Deze andere services moeten een beheerder tooadd meestal een of meer DNS-vermeldingen die bepaalde toohello service zijn.

Een Azure-web-app maakt gebruik van een eigen mechanisme tooverify eigendom van een domein. Een domein moet worden geverifieerd voor gebruik met Azure AD, zelfs als deze is eerder geverifieerd voor gebruik door een Azure-web-app in een abonnement dat is afhankelijk van die Azure AD. Een Azure-web-app kan een domeinnaam die is geverifieerd in een andere map vanuit Hallo-map die u Hallo web-app beveiligt kunt gebruiken.

## <a name="managing-domain-names"></a>Het beheren van domeinnamen
Domein-beheertaken kunnen worden uitgevoerd vanaf Hallo klassieke Azure-portal en van PowerShell. Veel taken kunnen worden uitgevoerd met behulp van hello Azure AD Graph API.

* [Toe te voegen en een aangepaste domeinnaam verifiëren](active-directory-add-domain.md)
* [Het beheer van domeinen in Hallo klassieke Azure-portal](active-directory-add-manage-domain-names.md)
* [Met behulp van PowerShell toomanage domeinnamen in Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Met behulp van Azure AD Graph API Hallo toomanage domeinnamen in Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

