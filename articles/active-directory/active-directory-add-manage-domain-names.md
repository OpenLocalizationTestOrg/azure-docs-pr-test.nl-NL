---
title: aaaManaging aangepaste domeinnamen in uw Azure Active Directory | Microsoft Docs
description: Beheerconcepten en uitleg over het beheren van een aangepast domein in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 4b6d06fecf3be0621be51c38a1330eafdc1b4d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Aangepaste domeinnamen in uw Azure Active Directory beheren
Een domeinnaam zijn een belangrijk id voor veel directoryresources als onderdeel van:

* Een gebruikersnaam of e-mailadres voor een gebruiker
* Hallo-adres voor een groep
* Hallo app ID URI voor een toepassing

Een resource in Azure Active Directory (Azure AD), kan een domeinnaam die al is geverifieerd toobe eigendom van Hallo directory die Hallo-bron bevat bevatten. Alleen een globale beheerder kunt domein-beheertaken uitvoeren in Azure AD.

> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel. Zie voor hoe toomanage uw in hello Azure AD-beheercentrum domeinnamen, [aangepaste domeinnamen in uw Azure Active Directory beheren](active-directory-domains-manage-azure-portal.md).

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a>Set Hallo primaire domeinnaam voor uw Azure AD-directory
Wanneer de map wordt gemaakt, wordt Hallo initiële domeinnaam, zoals 'contoso.onmicrosoft.com', is ook Hallo primaire domeinnaam voor uw directory. Primair domein Hallo Hallo standaarddomeinnaam voor een nieuwe gebruiker is wanneer u een nieuwe gebruiker in Hallo maakt [klassieke Azure-portal](https://manage.windowsazure.com/), of andere portals zoals Hallo Office 365-beheerportal. Dit stroomlijnt proces voor een toocreate beheerder nieuwe gebruikers in de portal Hallo Hallo.

toochange Hallo de naam van het primaire domein voor uw directory:

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com/) met een gebruikersaccount dat een globale beheerder van uw Azure AD-directory.
2. Selecteer **Active Directory** op de linkernavigatiebalk Hallo.
3. Open uw directory.
4. Selecteer Hallo **domeinen** tabblad.
5. Selecteer Hallo **primaire wijziging** knop op de opdrachtbalk Hallo.
6. Selecteer Hallo-domein dat u toobe Hallo nieuwe primaire domein voor uw directory wilt.

U kunt primaire domeinnaam voor uw directory toobe Hallo geverifieerde aangepaste domeinen die niet is gefedereerd wijzigen. Veranderende Hallo primair domein voor uw directory heeft geen invloed op Hallo gebruikersnamen voor alle bestaande gebruikers.

## <a name="add-custom-domain-names-tooyour-azure-ad"></a>Toevoegen van aangepast domein namen tooyour Azure AD
U kunt toevoegen, too900 aangepast domein namen tooeach Azure AD-directory. Hallo proces te[een aanvullende aangepaste domeinnaam toevoegen](active-directory-add-domain.md) is dezelfde hello voor Hallo eerst de aangepaste domeinnaam.

## <a name="add-subdomains-of-a-custom-domain"></a>Toevoegen van subdomeinen van een aangepast domein
Als u een domeinnaam van derde niveau zoals 'europe.contoso.com' tooyour directory tooadd wilt, moet u eerst toevoegen en controleren van Hallo tweede niveau domein, zoals contoso.com. Hallo subdomein wordt automatisch geverifieerd door Azure AD. toosee die subdomein dat u zojuist hebt toegevoegd Hallo is geverifieerd, vernieuwen Hallo pagina in Hallo browser met een lijst met Hallo domeinen in uw directory.

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a>Welke toodo als u Hallo DNS-registratieservice voor uw aangepaste domeinnaam wijzigen
Als u Hallo DNS-registratieservice voor uw aangepaste domeinnaam wijzigt, kunt u uw aangepaste domeinnaam met Azure AD zelf zonder onderbreking en zonder aanvullende configuratietaken toouse blijven. Als u uw aangepaste domeinnaam met Office 365, Intune of andere services die afhankelijk van aangepaste domeinnamen in Azure AD gebruiken zijn, Raadpleeg de documentatie toohello voor deze services.

## <a name="delete-a-custom-domain-name"></a>Verwijderen van een aangepaste domeinnaam
Als uw organisatie die domeinnaam niet langer gebruikt, of als u moet toouse die domeinnaam met een andere Azure AD, kunt u een aangepaste domeinnaam van uw Azure AD verwijderen.

een aangepaste domeinnaam toodelete, u moet eerst voor zorgen dat geen resources in uw directory zijn afhankelijk van de domeinnaam Hallo. U kunt een domeinnaam niet verwijderen uit de map als:

* Elke gebruiker heeft een gebruikersnaam, het e-mailadres of de proxy-adres dat Hallo domeinnaam omvatten.
* Een groep heeft een e-mailadres of de proxy-adres dat Hallo domeinnaam bevat.
* Elke toepassing in uw Azure AD heeft een app ID URI die Hallo domeinnaam bevat.

U moet wijzigen of verwijderen van een dergelijke resource in uw Azure AD-directory voordat u de aangepaste domeinnaam Hallo kunt verwijderen.

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a>PowerShell of Graph API toomanage domeinnamen gebruiken
De meeste beheertaken voor domeinnamen in Azure Active Directory kunnen ook worden uitgevoerd met behulp van Microsoft PowerShell of programmatisch met behulp van Azure AD Graph API.

* [Met behulp van PowerShell toomanage domeinnamen in Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Met behulp van Graph API toomanage domeinnamen in Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over domeinnamen in Azure AD](active-directory-add-domain-concepts.md)
* [Aangepaste domeinnamen beheren](active-directory-add-manage-domain-names.md)

