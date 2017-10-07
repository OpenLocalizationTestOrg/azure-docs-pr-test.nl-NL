---
title: rapporten voor Azure MFA aaaAccess en gebruik | Microsoft Docs
description: Hier wordt beschreven hoe toouse Hallo functie van Azure multi-factor Authentication - rapporten.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: curtand
ms.assetid: 3f6b33c4-04c8-47d4-aecb-aa39a61c4189
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: ae7ccceca4968d7ec7cf0cb1cf9e041d9997c840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a>Rapporten in Azure multi-factor Authentication
Azure multi-factor Authentication bevat verschillende rapporten die kunnen worden gebruikt door u en uw organisatie. Deze rapporten zijn toegankelijk via Hallo multi-factor Authentication-beheerportal. Hallo Hier volgt een lijst met beschikbare Hallo-rapporten:

| Rapport | Beschrijving |
|:--- |:--- |
| Gebruik |Hallo gebruik rapporten informatie weergeven over algemene gebruik Gebruikersoverzicht en details van gebruiker. |
| Status van de server |Dit rapport geeft Hallo-status van de multi-factor Authentication-Servers die zijn gekoppeld aan uw account. |
| Geschiedenis van geblokkeerde gebruikers |Deze rapporten Hallo geschiedenis van aanvragen tooblock weergeven of gebruikers. |
| Geschiedenis van overgeslagen gebruikers |Hallo geeft geschiedenis weer van aanvragen toobypass multi-factor Authentication voor het telefoonnummer van een gebruiker. |
| Fraudewaarschuwing |Geeft een historie weer van Fraudewaarschuwingen die zijn ingediend in Hallo datumbereik dat die u hebt opgegeven. |
| In de wachtrij |Een lijst met rapporten in de wachtrij voor verwerking en hun status. Een koppeling toodownload of weergave Hallo-rapport wordt verstrekt wanneer Hallo rapport voltooid is. |

## <a name="view-reports"></a>Rapporten weergeven
1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Selecteer aan de linkerkant hello, Active Directory.
3. Ga als volgt op een van deze twee opties, afhankelijk van of u Auth-Providers gebruiken:
   * **Optie 1**: klik op Hallo multi-factor Auth-Providers tabblad. Selecteer de MFA-provider en klikt u op Hallo **beheren** knop Hallo onder aan.
   * **Optie 2**: Selecteer uw directory en ga toohello **configureren** tabblad. Selecteer onder de sectie multi-factor authentication hello, **service-instellingen beheren**. Aan de onderkant van de Hallo van Hallo MFA-Service-instellingen pagina, klikt u op Hallo Ga toohello portal-koppeling.
4. Selecteer in hello Azure multi-factor Authentication-beheerportal, Hallo type rapport dat u wilt van Hallo **een rapport weergeven** sectie in Hallo linkernavigatiebalk.

<center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center>


**Aanvullende resources**

* [Voor gebruikers](end-user/multi-factor-authentication-end-user.md)
* [Azure multi-factor Authentication op MSDN](https://msdn.microsoft.com/library/azure/dn249471.aspx)
