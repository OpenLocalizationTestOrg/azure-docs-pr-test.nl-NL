---
title: 'Azure AD Connect-synchronisatie: hello Azure AD Connect-synchronisatie-serviceaccount wijzigen | Microsoft Docs'
description: Dit document onderwerp beschrijft de versleutelingssleutel Hallo en hoe tooabandon na het Hallo-wachtwoord is gewijzigd.
services: active-directory
keywords: Azure AD sync-serviceaccount, wachtwoord
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 11948ac4662f722e4f684ef6c9b9ccdc6387e60f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-azure-ad-connect-sync-service-account-password"></a>Wachtwoord wijzigen hello Azure AD Connect sync-serviceaccount
Als u een wachtwoord hello Azure AD Connect sync-serviceaccount wijzigt, zich Hallo Synchronization Service niet kunnen starten correct totdat u hebt verlaten Hallo versleutelingssleutel en opnieuw geïnitialiseerd wachtwoord hello Azure AD Connect sync-serviceaccount. 

Azure AD Connect als onderdeel van Hallo Synchronisatieservices maakt gebruik van een versleuteling sleutel toostore Hallo wachtwoorden van Hallo AD DS en Azure AD-serviceaccounts.  Deze accounts worden versleuteld voordat ze worden opgeslagen in Hallo-database. 

Hallo versleutelingssleutel die wordt gebruikt is beveiligd met [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx). DPAPI beveiligt Hallo-versleutelingssleutel met Hallo **wachtwoord van hello Azure AD Connect sync-serviceaccount**. 

Als u het wachtwoord van serviceaccount Hallo toochange nodig kunt u Hallo procedures in [Abandoning hello Azure AD Connect-synchronisatie versleutelingssleutel](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish dit.  Deze procedures moeten ook worden gebruikt als u tooabandon Hallo versleutelingssleutel nodig om welke reden.

##<a name="issues-that-arise-from-changing-hello-password"></a>Problemen die voortkomen uit Hallo wachtwoord wijzigen
Er zijn twee dingen nodig toobe uitgevoerd als u het wachtwoord Hallo-serviceaccount.

U moet eerst toochange Hallo wachtwoord onder Hallo Windows Service Control Manager.  Totdat dit probleem opgelost is ziet u volgende fouten:


- Als u toostart Hallo Synchronization Service in Windows Service Control Manager probeert, ontvangt u fout Hallo '**Windows kan Hallo Microsoft Azure AD Sync-service niet starten op de lokale Computer**'. **Fout 1069: Hallo-service is niet gestart vanwege tooa aanmelding mislukt.** "
- Onder de functie Logboeken van Windows hello logboek met systeemgebeurtenissen bevat een fout opgetreden bij **gebeurtenis-ID 7038** en het bericht '**Hallo-service ADSync is kan niet toolog op net als bij Hallo momenteel zodanig geconfigureerd dat wachtwoorden vanwege de volgende toohello fout: Hallo-gebruikersnaam of wachtwoord is onjuist.** "

Ten tweede onder bepaalde omstandigheden, kan als Hallo wachtwoord wordt bijgewerkt, Hallo Synchronization Service niet langer ophalen Hallo versleutelingssleutel via DPAPI. Zonder de versleutelingssleutel hello, Hallo die Synchronization-Service niet Hallo wachtwoorden vereist toosynchronize naar/van ontsleutelen kan on-premises AD en Azure AD.
U ziet bijvoorbeeld fouten:

- Onder Windows Service Control Manager als u toostart Hallo-synchronisatieservice probeert en de versleutelingssleutel hello, kan niet worden opgehaald mislukt met fout "** Windows kan Microsoft Azure AD Sync Hallo niet starten op de lokale Computer. Bekijk Hallo System-gebeurtenislogboek voor meer informatie. Als dit een niet-Microsoft-service, neem contact op met de leverancier van de Hallo en tooservice-specifieke foutcode Raadpleeg **-21451857952 ***. "
- Onder de functie Logboeken van Windows hello toepassingslogboek bevat een fout opgetreden bij **gebeurtenis-ID 6028** en foutbericht *'**versleutelingssleutel Hallo-server kan niet worden geopend.* *'*

tooensure dat er geen deze fouten, volgt u de procedures Hallo in [Abandoning hello Azure AD Connect-synchronisatie versleutelingssleutel](#abandoning-the-azure-ad-connect-sync-encryption-key) wanneer Hallo wachtwoord wijzigt.
 
## <a name="abandoning-hello-azure-ad-connect-sync-encryption-key"></a>Versleutelingssleutel van de Hallo-Azure AD Connect-synchronisatie wordt afgebroken
>[!IMPORTANT]
>Hallo volgende procedures gelden alleen tooAzure AD Connect build 1.1.443.0 of ouder.

Gebruik hello procedures tooabandon Hallo versleutelingssleutel te volgen.

### <a name="what-toodo-if-you-need-tooabandon-hello-encryption-key"></a>Welke toodo als u tooabandon Hallo versleutelingssleutel nodig

Als u tooabandon Hallo versleutelingssleutel nodig hebt, gebruik Hallo tooaccomplish procedures te volgen deze.

1. [Bestaande versleutelingssleutel Hallo afbreken](#abandon-the-existing-encryption-key)

2. [Hallo wachtwoord Hallo AD DS-account opgeven](#provide-the-password-of-the-ad-ds-account)

3. [Hallo-wachtwoord van hello Azure AD sync-account opnieuw initialiseren](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [Hallo Synchronization Service starten](#start-the-synchronization-service)

#### <a name="abandon-hello-existing-encryption-key"></a>Bestaande versleutelingssleutel Hallo afbreken
Bestaande versleutelingssleutel Hallo afbreken zodat deze nieuwe versleutelingssleutel kan worden gemaakt:

1. Aanmelden tooyour Azure AD Connect-Server als beheerder.

2. Start een nieuwe PowerShell-sessie.

3. Navigeer toofolder:`$env:Program Files\Microsoft Azure AD Sync\bin\`

4. Hallo-opdracht uitvoeren:`./miiskmu.exe /a`

![Azure AD Connect Sync Encryption Key-hulpprogramma](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-hello-password-of-hello-ad-ds-account"></a>Hallo wachtwoord Hallo AD DS-account opgeven
Zoals Hallo bestaande wachtwoorden worden opgeslagen in het Hallo-database kunnen niet meer worden ontsleuteld, moet je tooprovide Hallo synchronisatieservice met wachtwoord op Hallo van Hallo AD DS-account. Hallo-synchronisatieservice versleutelt Hallo wachtwoorden met nieuwe coderingssleutel Hallo:

1. Hallo Synchronization Service Manager (START → Synchronization Service) starten.
</br>![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  
2. Ga toohello **Connectors** tabblad.
3. Selecteer Hallo **AD-Connector** die overeenkomt met tooyour on-premises AD dat. Als u meer dan één AD-connector hebt, herhaalt u Hallo volgende stappen uit voor elk van deze.
4. Onder **acties**, selecteer **eigenschappen**.
5. Selecteer in het pop-upvenster hello, **tooActive Directory-Forest verbinding**:
6. Voer wachtwoord op Hallo van Hallo AD DS-account in Hallo **wachtwoord** textbox. Als u het wachtwoord niet weet, moet u dit tooa bekende waarde voordat u deze stap uitvoert instellen.
7. Klik op **OK** toosave Hallo nieuw wachtwoord en sluiten Hallo pop-upvenster.
![Azure AD Connect Sync Encryption Key-hulpprogramma](media/active-directory-aadconnectsync-encryption-key/key6.png)

#### <a name="reinitialize-hello-password-of-hello-azure-ad-sync-account"></a>Hallo-wachtwoord van hello Azure AD sync-account opnieuw initialiseren
U kan niet rechtstreeks wachtwoord op Hallo van hello Azure AD-service-account toohello Synchronization Service opgeven. In plaats daarvan moet u toouse Hallo cmdlet **toevoegen ADSyncAADServiceAccount** tooreinitialize hello Azure AD-serviceaccount. Hallo cmdlet Hallo accountwachtwoord opnieuw instellen en maakt het beschikbaar toohello Synchronization Service:

1. Start een nieuwe PowerShell-sessie op Hallo Azure AD Connect-server.
2. Voer cmdlet `Add-ADSyncAADServiceAccount`.
3. In het pop-upvenster hello, referenties hello Azure AD globale beheerder voor uw Azure AD-tenant.
![Azure AD Connect Sync Encryption Key-hulpprogramma](media/active-directory-aadconnectsync-encryption-key/key7.png)
4. Als dat lukt, ziet u Hallo PowerShell-opdrachtprompt.

#### <a name="start-hello-synchronization-service"></a>Hallo Synchronization Service starten
Nu Hallo Synchronization Service heeft toegang toohello versleutelingssleutel en alle Hallo wachtwoorden nodig is, kunt u Hallo-service opnieuw starten in Hallo Windows Service Control Manager:


1. Ga tooWindows Service Control Manager (START → Services).
2. Selecteer **Microsoft Azure AD Sync** en klik op opnieuw starten.

## <a name="next-steps"></a>Volgende stappen
**Overzichtsonderwerpen**

* [Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen](active-directory-aadconnectsync-whatis.md)

* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
