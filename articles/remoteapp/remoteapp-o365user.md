---
title: aaaHow toouse Azure RemoteApp met gebruikersaccounts voor Office 365 | Microsoft Docs
description: Meer informatie over hoe Azure RemoteApp toouse met mijn Office 365-gebruikersaccounts
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: aba70fd3-60b0-4b44-9321-1ab18760ccd5
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d2dbed2a6838adf9bb0f7508eb7dcecb0a74a62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-remoteapp-with-office-365-user-accounts"></a>Hoe toouse Azure RemoteApp met Office 365-gebruikersaccounts
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Als u hebt een Office 365-abonnement dat u hebt een Azure Active Directory waarin uw gebruikersnamen en wachtwoorden tooaccess Office 365-services gebruikt. Bijvoorbeeld, wanneer uw gebruikers Office 365 ProPlus activeert ze geverifieerd bij Azure AD-toocheck voor licenties. Zoals toouse zou de meeste klanten Hallo dezelfde map met Azure RemoteApp.

Als u Azure RemoteApp implementeert u waarschijnlijk een Azure-abonnement dat is gekoppeld aan een andere Azure AD gebruikt. In volgorde toouse uw Office 365-directory, moet u toomove hello Azure-abonnement in die map.

Voor informatie over de clienttoepassingen voor Office 365 toodeploy, Zie [hoe toouse uw Office 365-abonnement met Azure RemoteApp](remoteapp-officesubscription.md).

## <a name="phase-1-register-your-free-office-365-azure-active-directory-subscription"></a>Fase 1: Een gratis abonnement voor Office 365 Azure Active Directory registreren
Als u Hallo klassieke Azure-portal gebruikt, volgt u de stappen Hallo in [registreren van uw gratis Azure Active Directory-abonnement](https://technet.microsoft.com/library/dn832618.aspx) tooget beheerderstoegang tooyour Azure AD via hello Azure Management Portal. Hallo resultaat zijn van dit proces moet u kunnen toolog in hello Azure-portal en raadpleegt u uw directory er – op dit moment kunt u niet meer zien omdat hello volledige Azure-abonnement die u met Azure RemoteApp werkt in een andere map.

Houd er rekening mee Hallo naam en het wachtwoord van Hallo administrator-account die u hebt gemaakt in deze stap – ze nodig zijn in de fase 2.

Als u van Azure-portal Hallo gebruikmaakt, Bekijk [hoe tooregister en activeren van een gratis Azure Active Directory met behulp van Office 365-portal](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/).

## <a name="phase-2-change-hello-azure-ad-associated-with-your-azure-subscription"></a>Fase 2: Wijziging hello Azure AD die zijn gekoppeld aan uw Azure-abonnement.
We gaan toochange uw Azure-abonnement vanuit de huidige map naar Hallo Office 365-map die wordt gewerkt met fase 1.

Ga als volgt Hallo-instructies die worden beschreven [wijziging hello Azure Active Directory-tenant in Azure RemoteApp](remoteapp-changetenant.md). Betalen bijzondere aandacht toohello volgende stappen uit:

* Stap &#1;: Als u Azure RemoteApp (ARA) hebt geïmplementeerd in dit abonnement, controleert u of dat u alle Azure AD-gebruikersaccounts uit alle verzamelingen ARA eerst verwijderen, voordat u iets anders. U kunt ook overwegen een bestaande verzameling verwijderen.
* Stap &#2;: Dit is een kritieke stap. Moet u een Microsoft-account toouse (bijvoorbeeld @outlook.com) als een servicebeheerder op Hallo abonnement; dit is omdat we kan geen gebruikersaccounts van Hallo bestaande abonnement voor Azure AD gekoppeld toohello: als we doen, hebben we kunnen toomove niet het tooa andere Azure AD.
* Stap #4: Bij het toevoegen van een bestaande map Hallo systeem u wordt gevraagd toosign met Hallo administratoraccount voor de map. Zorg ervoor dat toouse Hallo administrator-account van fase 1.
* Stap &#5;: Hallo bovenliggende map van Hallo abonnement tooyour Office 365 map wijzigen. het eindresultaat Hallo moet dat onder Instellingen -> abonnementen uw abonnement bevat Hallo Office 365-directory. 
  ![Hallo van de bovenliggende map van het Hallo-abonnement wijzigen](./media/remoteapp-o365user/settings.png)

Op dit moment is uw Azure RemoteApp-abonnement gekoppeld aan uw Office 365, Azure AD; met Azure RemoteApp kunt u bestaande Office 365-gebruikersaccounts Hallo!

