---
title: Azure RemoteApp gebruiken met Office 365-gebruikersaccounts | Microsoft Docs
description: Informatie over het gebruik van Azure RemoteApp met mijn Office 365-gebruikersaccounts
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
ms.openlocfilehash: 1bc8949c236afd03415f961cf7a657d4d3926b07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-remoteapp-with-office-365-user-accounts"></a>Azure RemoteApp gebruiken met Office 365-gebruikersaccounts
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Als u een Office 365-abonnement hebt u een Azure Active Directory die worden opgeslagen gebruikersnamen en wachtwoorden gebruikt voor toegang tot Office 365-services. Bijvoorbeeld, wanneer uw gebruikers Office 365 ProPlus activeert verifiëren ze met Azure AD om te controleren voor licenties. De meeste klanten willen gebruiken dezelfde directory met Azure RemoteApp.

Als u Azure RemoteApp implementeert u waarschijnlijk een Azure-abonnement dat is gekoppeld aan een andere Azure AD gebruikt. Als u wilt uw Office 365-directory gebruiken, moet u het Azure-abonnement in die map verplaatsen.

Zie voor informatie over het implementeren van clienttoepassingen voor Office 365 [het gebruik van uw Office 365-abonnement met Azure RemoteApp](remoteapp-officesubscription.md).

## <a name="phase-1-register-your-free-office-365-azure-active-directory-subscription"></a>Fase 1: Een gratis abonnement voor Office 365 Azure Active Directory registreren
Als u de klassieke Azure portal gebruikt, gebruikt u de stappen in [registreren van uw gratis Azure Active Directory-abonnement](https://technet.microsoft.com/library/dn832618.aspx) administratieve toegang krijgen tot uw Azure AD via de Azure-beheerportal. Als gevolg van dit proces moet u het volgende kunnen Meld u aan bij de Azure-portal en ziet uw adreslijst: op dit moment ziet u niet meer omdat de volledige Azure-abonnement die u met Azure RemoteApp werkt in een andere map.

Vergeet niet de naam en het wachtwoord van de administrator-account dat u hebt gemaakt in deze stap – ze nodig zijn in de fase 2.

Als u van de Azure-portal gebruikmaakt, uitchecken [het registreren en activeren van een gratis Azure Active Directory met behulp van Office 365-portal](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/).

## <a name="phase-2-change-the-azure-ad-associated-with-your-azure-subscription"></a>Fase 2: De Azure AD die zijn gekoppeld aan uw Azure-abonnement wijzigen.
We gaan wijzigen van uw Azure-abonnement vanuit de huidige map naar de Office 365-map die wordt gewerkt met fase 1.

Volg de instructies die worden beschreven [wijzigen van de Azure Active Directory-tenant in Azure RemoteApp](remoteapp-changetenant.md). Speciale aandacht besteden aan de volgende stappen uit:

* Stap &#1;: Als u Azure RemoteApp (ARA) hebt geïmplementeerd in dit abonnement, controleert u of dat u alle Azure AD-gebruikersaccounts uit alle verzamelingen ARA eerst verwijderen, voordat u iets anders. U kunt ook overwegen een bestaande verzameling verwijderen.
* Stap &#2;: Dit is een kritieke stap. U moet een Microsoft-account gebruiken (bijvoorbeeld @outlook.com) als servicebeheerder voor het abonnement; dit komt doordat er geen gebruikersaccounts van de bestaande Azure AD dat is gekoppeld aan het abonnement: kan niet als we doen, is niet mogelijk om deze te verplaatsen naar een andere Azure AD .
* Stap &#4;: Bij het toevoegen van een bestaande map, het systeem u wordt gevraagd zich kunnen aanmelden met de administrator-account voor de map. Zorg ervoor dat het beheerdersaccount van fase 1 gebruiken.
* Stap &#5;: Wijzigen de bovenliggende map van het abonnement voor uw Office 365-directory. Het eindresultaat moet dat onder Instellingen -> abonnementen uw abonnement geeft een lijst van de Office 365-map. 
  ![De bovenliggende map van het abonnement wijzigen](./media/remoteapp-o365user/settings.png)

Op dit moment is uw Azure RemoteApp-abonnement gekoppeld aan uw Office 365, Azure AD; u kunt de bestaande Office 365-gebruikersaccounts met Azure RemoteApp!

