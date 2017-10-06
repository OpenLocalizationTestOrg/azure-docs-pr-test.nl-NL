---
title: aaaManaging aangepaste domeinnamen in uw Azure Active Directory | Microsoft Docs
description: Beheerconcepten en uitleg over het beheren van een domeinnaam in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5063cd0a-dba2-4ba9-aa65-b8117490d73a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: curtand;jeffsta
ms.openlocfilehash: 4719524c4e972f6c981db39f016729da13b37670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Aangepaste domeinnamen in uw Azure Active Directory beheren
Een domeinnaam is een belangrijk onderdeel van het Hallo-id voor veel directory-resources: het deel uitmaakt van een gebruikersnaam of e-mailadres voor een gebruiker, een onderdeel van het Hallo-adres voor een groep, en kan deel uitmaken van Hallo app ID URI voor een toepassing. Een resource in Azure Active Directory (Azure AD), kan een domeinnaam die al is geverifieerd als eigendom van Hallo directory die Hallo-bron bevat bevatten. Alleen een globale beheerder kunt domein-beheertaken uitvoeren in Azure AD.

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a>Set Hallo primaire domeinnaam voor uw Azure AD-directory
Uw map wordt gemaakt, is Hallo initiële domeinnaam, zoals 'contoso.onmicrosoft.com', ook als primaire Hallo-domeinnaam. Hallo primair domein is Hallo standaarddomeinnaam voor een nieuwe gebruiker bij het maken van een nieuwe gebruiker. Een primaire domeinnaam instellen stroomlijnt het Hallo-proces voor een toocreate beheerder nieuwe gebruikers in Hallo-portal. toochange hello primaire domeinnaam:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.
2. Selecteer **meer services**, voer **Azure Active Directory** in het tekstvak Hallo en selecteer vervolgens **Enter**.
   
   ![Gebruikersbeheer openen](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Op Hallo ***mapnaam*** blade Selecteer **domeinnamen**.
4. Op Hallo  ***mapnaam* -domeinnamen** blade, selecteer Hallo domeinnaam gewenst toomake Hallo primaire domeinnaam.
5. Op Hallo ***domeinnaam*** blade (dat wil zeggen, Hallo blade die wordt geopend met de naam van het nieuwe domein in Hallo titel), selecteer Hallo **primair** opdracht. Bevestig uw keuze wanneer u wordt gevraagd.
   
   ![Een domeinnaam primair maken](./media/active-directory-domains-manage-azure-portal/make-primary.png)

U kunt primaire domeinnaam voor uw directory toobe Hallo geverifieerde aangepaste domeinen die niet is gefedereerd wijzigen. Veranderende Hallo primair domein voor uw directory heeft geen invloed op Hallo gebruikersnamen voor alle bestaande gebruikers.

## <a name="add-custom-domain-names-tooyour-azure-ad"></a>Toevoegen van aangepast domein namen tooyour Azure AD
U kunt toevoegen, too900 aangepast domein namen tooeach Azure AD-directory. Hallo proces te[een aanvullende aangepaste domeinnaam toevoegen](add-custom-domain.md) is dezelfde hello voor Hallo eerst de aangepaste domeinnaam.

## <a name="add-subdomains-of-a-custom-domain"></a>Toevoegen van subdomeinen van een aangepast domein
Als u een domeinnaam van derde niveau zoals 'europe.contoso.com' tooyour directory tooadd wilt, moet u eerst toevoegen en controleren van Hallo tweede niveau domein, zoals contoso.com. Hallo subdomein wordt automatisch geverifieerd door Azure AD. toosee die subdomein dat u zojuist hebt toegevoegd Hallo is geverifieerd, vernieuwen Hallo pagina in Hallo browser met een lijst met Hallo-domeinen.

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a>Welke toodo als u Hallo DNS-registratieservice voor uw aangepaste domeinnaam wijzigen
Als u Hallo DNS-registratieservice voor uw aangepaste domeinnaam wijzigt, kunt u uw aangepaste domeinnaam met Azure AD zelf zonder onderbreking en zonder aanvullende configuratietaken toouse blijven. Als u uw aangepaste domeinnaam met Office 365, Intune of andere services die afhankelijk van aangepaste domeinnamen in Azure AD gebruiken zijn, Raadpleeg de documentatie toohello voor deze services.

## <a name="delete-a-custom-domain-name"></a>Verwijderen van een aangepaste domeinnaam
Als uw organisatie die domeinnaam niet langer gebruikt, of als u moet toouse die domeinnaam met een andere Azure AD, kunt u een aangepaste domeinnaam van uw Azure AD verwijderen.

een aangepaste domeinnaam toodelete, u moet eerst voor zorgen dat geen resources in uw directory zijn afhankelijk van de domeinnaam Hallo. U kunt een domeinnaam niet verwijderen uit de map als:

* Elke gebruiker heeft een gebruikersnaam, het e-mailadres of de proxy-adres dat Hallo domeinnaam bevat.
* Een groep heeft een e-mailadres of de proxy-adres dat Hallo domeinnaam bevat.
* Elke toepassing in uw Azure AD heeft een app ID URI die Hallo domeinnaam bevat.

U moet wijzigen of verwijderen van een dergelijke resource in uw Azure AD-directory voordat u de aangepaste domeinnaam Hallo kunt verwijderen.

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a>PowerShell of Graph API toomanage domeinnamen gebruiken
De meeste beheertaken voor domeinnamen in Azure Active Directory kunnen ook worden uitgevoerd met behulp van Microsoft PowerShell of programmatisch met behulp van Azure AD Graph API.

* [Met behulp van PowerShell toomanage domeinnamen in Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Met behulp van Graph API toomanage domeinnamen in Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>Volgende stappen
* [Aangepaste domeinnamen toevoegen](add-custom-domain.md)

