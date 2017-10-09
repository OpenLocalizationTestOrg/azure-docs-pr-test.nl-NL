---
title: aaaHow Azure-abonnementen worden gekoppeld aan Azure Active Directory | Microsoft Docs
description: Aanmelden tooMicrosoft Azure en verwante problemen, zoals Hallo-relatie tussen een Azure-abonnement en Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: bc4773c2-bc4a-4d21-9264-2267065f0aea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4f831cfb972efec57083fcaa63adb43fde7b2faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-subscriptions-are-associated-with-azure-active-directory"></a>How Azure subscriptions are associated with Azure Active Directory (Hoe Azure-abonnementen worden gekoppeld aan Azure Active Directory)
In dit artikel bevat informatie over het Hallo-relatie tussen een Azure-abonnement en Azure Active Directory (Azure AD), en hoe tooadd een bestaand abonnement tooyour Azure AD-directory.

## <a name="your-azure-subscriptions-relationship-tooazure-ad"></a>Van uw Azure-abonnement relatie tooAzure AD
Uw Azure-abonnement heeft een vertrouwensrelatie heeft met Azure AD, wat betekent dat wordt vertrouwd Hallo directory tooauthenticate gebruikers, services en apparaten. Meerdere abonnementen kunnen vertrouwen, Hallo dezelfde map, maar elk abonnement vertrouwt slechts één directory. 

Hallo-vertrouwensrelatie die een abonnement met een directory heeft is in tegenstelling tot Hallo-relatie met andere resources in Azure (websites, databases, enzovoort heeft). Als u een abonnement is verlopen, toegang krijgen tot toohello andere resources zijn gekoppeld Hallo abonnement ook geblokkeerd. Maar een Azure AD-directory blijft in Azure, en kunt u een ander abonnement koppelen aan die directory en beheren met behulp van het nieuwe abonnement Hallo Hallo-directory.

![diagram om te laten zien hoe abonnementen worden gekoppeld](./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png)

Alle gebruikers hebben één basisdirectory waarmee ze worden geverifieerd, maar ze kunnen ook gasten zijn in andere directory’s. U ziet in Azure AD Hallo mappen waarvan uw gebruikersaccount een lid of Gast is.

## <a name="azure-ad-and-cloud-service-subscriptions"></a>Azure AD en abonnementen voor cloudservices
Azure AD levert Hallo core directory- en identiteitsbeheer identiteitsbeheermogelijkheden voor de meeste Microsoft cloud-services, waaronder:

* Azure
* Microsoft Office 365
* Microsoft Dynamics CRM Online
* Microsoft Intune

U krijgt hello Azure AD-service is gratis wanneer u zich aanmeldt voor een van deze Microsoft cloud-services. Als u een extra Azure-abonnement tooan Azure AD-directory tooadd wilt, moet u zijn ondertekend met een Microsoft-account. Als u tooAzure met een werk aanmelden- of schoolaccount, kunt u een Azure-abonnement tooan bestaande directory niet toevoegen omdat uw werk of school-account kan niet rechtstreeks door Azure worden geverifieerd. 

## <a name="tooadd-an-existing-subscription-tooyour-azure-ad-directory"></a>een bestaand abonnement tooyour Azure AD-directory tooadd
U moet zich aanmelden met een account dat bestaat in zowel Hallo huidige map aan welke Hallo abonnement is gekoppeld en in de map Hallo gewenste tooadd naar. 

1. Meld u aan toohello [Azure-Accountcentrum](https://account.windowsazure.com/Home/Index) met een account dat Hallo accountbeheerder van Hallo abonnement waarvan eigendom gewenste tootransfer.
2. Zorg ervoor dat Hallo-gebruiker die u eigenaar toobe Hallo-abonnement is in de map Hallo gericht.
3. Klik op **Abonnement overdragen**.
4. Hallo ontvanger opgeven. Hallo geadresseerde ontvangt automatisch een e-mail met een koppeling acceptatie.
5. Hallo-ontvanger op Hallo koppeling klikt en Hallo instructies gevolgd die zijn, met inbegrip van de betaalgegevens invoeren. Als de ontvanger Hallo is geslaagd, wordt Hallo abonnement overgedragen. 
6. de standaardmap Hallo van Hallo abonnement wordt gewijzigd toohello map die gebruiker Hallo is in.


## <a name="suggestions-toomanage-both-a-subscription-and-a-directory"></a>Suggesties toomanage zowel een abonnement en een directory
Hallo-beheerdersrollen voor een Azure-abonnement beheren bronnen gekoppeld toohello Azure-abonnement. Deze sectie wordt uitgelegd Hallo verschillen tussen Azure-abonnementbeheerders en Azure AD-directorybeheerders. Beheerdersrollen en andere suggesties voor het gebruik van uw abonnement worden besproken in toomanage [beheerdersrollen toewijzen in Azure Active Directory](active-directory-assign-admin-roles.md).

Standaard u de rol servicebeheerder Hallo toegewezen wanneer u zich aanmeldt. Als anderen moet toosign in en toegang tot services Hallo gebruik hetzelfde abonnement, kunt u deze toevoegen als medebeheerders. 

Azure AD heeft een andere set beheerdersrollen toomanage Hallo directory en identiteitsgerelateerde functies. Hallo globale beheerder van een directory kan bijvoorbeeld gebruikers en groepen toohello directory toevoegen of multi-factor authentication vereisen voor gebruikers. Een gebruiker die een map maakt toohello globale beheerdersrol is toegewezen en ze beheerdersrollen tooother gebruikers kunnen toewijzen. Azure AD-beheerdersrollen worden ook gebruikt door andere services, zoals Office 365 en Microsoft Intune. 

Azure-abonnementsbeheerders en Azure AD-directorybeheerders zijn twee verschillende rollen. 
* Azure-abonnementsbeheerders kunnen resources in Azure beheren en Azure AD kan worden gebruikt in hello Azure-portal (omdat hello Azure-portal zelf een Azure-resource is). 
* Directorybeheerders kunnen eigenschappen alleen in hello Azure AD-directory beheren.

Een persoon kan beide rollen hebben, maar dit is niet vereist. De globale beheerder van een directory kan niet worden ingesteld als servicebeheerder of medebeheerder van een Azure-abonnement, of omgekeerd. Zonder een beheerder van abonnement hello, Hallo gebruiker toohello Azure-portal kunt aanmelden, maar niet Hallo mappen voor dat abonnement in Hallo portal beheren. Deze gebruiker kan echter de mappen met andere hulpprogramma's zoals Azure AD PowerShell of Office 365-beheercentrum Hallo beheren.

## <a name="next-steps"></a>Volgende stappen
* toolearn informatie over hoe beheerders voor een Azure-abonnement toochange zien [het eigendom overdraagt van een Azure-abonnement tooanother-account](../billing/billing-subscription-transfer.md)
* Zie toolearn meer informatie over hoe de toegang tot resources wordt beheerd in Microsoft Azure [informatie over toegang tot bronnen in Azure](active-directory-understanding-resource-access.md)
* Voor meer informatie over het tooassign rollen in Azure AD, Zie [beheerdersrollen toewijzen in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG
