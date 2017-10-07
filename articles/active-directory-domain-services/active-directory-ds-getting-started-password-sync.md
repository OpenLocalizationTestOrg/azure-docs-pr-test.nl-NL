---
title: 'Azure Active Directory Domain Services: wachtwoordsynchronisatie inschakelen | Microsoft Docs'
description: Aan de slag met Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 5a32a0df-a3ca-4ebe-b980-91f58f8030fc
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 8e073df9de2996f5ad159dda746881c014ea3d66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>Wachtwoord synchronisatie tooAzure Active Directory Domain Services inschakelen
Tijdens de vorige taken hebt u Azure Active Directory Domain Services ingeschakeld voor uw Azure Active Directory-tenant (Azure AD). de volgende taak Hallo is tooenable synchronisatie van referentie-hashes die vereist zijn voor NT LAN Manager (NTLM) en Kerberos-verificatie tooAzure AD Domain Services. Nadat u een referentie-synchronisatie hebt ingesteld, kunnen gebruikers zich aanmelden in toohello beheerde domein met hun bedrijfsreferenties.

Hallo stappen die nodig zijn verschillend voor de gebruiker alleen in de cloud accounts tegenover gebruikersaccounts die worden gesynchroniseerd vanuit uw lokale directory met Azure AD Connect.  Als uw Azure AD-tenant een combinatie van heeft cloud alleen gebruikers en gebruikers van uw on-premises AD, moet u tooperform na beide stappen.

<br>

> [!div class="op_single_selector"]
> * **Alleen in de cloud gebruikersaccounts**: [wachtwoorden synchroniseren voor alleen in de cloud gebruikersaccounts tooyour beheerd domein](active-directory-ds-getting-started-password-sync.md)
> * **Lokale gebruikersaccounts**: [wachtwoorden synchroniseren voor gebruikersaccounts die zijn gesynchroniseerd vanuit uw on-premises AD tooyour beheerd domein](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a>Taak 5: wachtwoord synchronisatie tooyour beheerd domein voor gebruikersaccounts die alleen in de cloud inschakelen
gebruikers op Hallo tooauthenticate beheerd domein, Azure Active Directory Domain Services moet referentie-hashes in een indeling die geschikt is voor NTLM en Kerberos-verificatie. Azure AD niet genereren of opslaan van de referentie-hashes Hallo-indeling die is vereist voor NTLM of Kerberos-verificatie, totdat u Azure Active Directory Domain Services voor uw tenant inschakelen. Om veiligheidsredenen slaat Azure AD ook geen wachtwoorden op in niet-gecodeerde vorm. Azure AD heeft dus geen een manier tooautomatically deze op basis van bestaande referenties van gebruikers NTLM of Kerberos-referentie-hashes te genereren.

> [!NOTE]
> Als uw organisatie alleen in de cloud gebruikersaccounts heeft, kunnen gebruikers hoeven toouse Azure Active Directory Domain Services hun wachtwoord moeten wijzigen. Een alleen-gebruikersaccount is een account dat is gemaakt in uw Azure AD-directory hello Azure-portal of Azure AD PowerShell-cmdlets. Deze gebruikersaccounts zijn niet gesynchroniseerd vanuit een on-premises map.
>
>

Deze wachtwoordwijziging worden Hallo referentie hashes die voor Azure Active Directory Domain Services voor Kerberos en NTLM-verificatie toobe gegenereerd in Azure AD vereist zijn. U kunt wachtwoorden laten verlopen Hallo voor alle gebruikers in Hallo tenant die toouse Azure Active Directory Domain Services moeten of ze toochange moeten hun wachtwoorden.

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a>Het genereren van hashes voor NTLM- en Kerberos-referenties inschakelen voor een cloudgebruikersaccount
Hier volgen Hallo instructies, moet u tooprovide gebruikers, zodat ze kunnen hun wachtwoord wijzigen:

1. Ga toohello [Azure AD-Toegangsvenster](http://myapps.microsoft.com) pagina voor uw organisatie.

    ![Hello Azure AD-Toegangsvenster starten](./media/active-directory-domain-services-getting-started/access-panel.png)

2. Klik op de naam van uw in Hallo rechterbovenhoek, en selecteer **profiel** in Hallo-menu.

    ![Selecteer het profiel](./media/active-directory-domain-services-getting-started/select-profile.png)

3. Op Hallo **profiel** pagina, klikt u op **wachtwoord wijzigen**.

    ![Klik op 'Wachtwoord wijzigen'](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > Als hello **wachtwoord wijzigen** optie niet wordt weergegeven in Hallo Toegangsvenster venster, zorg ervoor dat uw organisatie heeft geconfigureerd [in Azure AD-wachtwoordbeheer](../active-directory/active-directory-passwords-getting-started.md).
   >
   >
4. Op Hallo **wachtwoord wijzigen** pagina, typt u uw bestaande (oude) wachtwoord, typt u een nieuw wachtwoord en Bevestig het.

    ![Maak een virtueel netwerk voor Azure AD Domain Services.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. Klik op **Verzenden**.

Een paar minuten nadat u uw wachtwoord hebt gewijzigd is Hallo nieuwe wachtwoord gebruikt in Azure Active Directory Domain Services. Na enkele minuten (meestal ongeveer 20 minuten), kunt u toocomputers die gekoppeld toohello beheerd domein zijn via Hallo zojuist gewijzigd wachtwoord aanmelden.

## <a name="related-content"></a>Gerelateerde inhoud
* [Hoe tooupdate uw eigen wachtwoord](../active-directory/active-directory-passwords-update-your-own-password.md)
* [Aan de slag met wachtwoordbeheer in Azure AD](../active-directory/active-directory-passwords-getting-started.md)
* [Wachtwoordsynchronisatie inschakelen tooAzure Active Directory Domain Services voor een gesynchroniseerde Azure AD-tenant](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [Een beheerd domein van Azure Active Directory Domain Services beheren](active-directory-ds-admin-guide-administer-domain.md)
* [Lid worden van een Windows virtuele machine tooan Azure Active Directory Domain Services beheerd domein](active-directory-ds-admin-guide-join-windows-vm.md)
* [Lid worden van een Red Hat Enterprise Linux virtuele machine tooan Azure Active Directory Domain Services beheerd domein](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
