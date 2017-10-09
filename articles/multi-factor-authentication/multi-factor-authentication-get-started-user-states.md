---
title: aaaMicrosoft status van de Azure multi-factor Authentication-gebruikers
description: Meer informatie over de status van de gebruikers in de Azure MFA.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 0b9fde23-2d36-45b3-950d-f88624a68fbd
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: cf5b977b09d09330b7b3bc668abd79e602d62015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-two-step-verification-for-a-user-or-group"></a>Hoe verificatie van toorequire in twee stappen voor een gebruiker of groep

Er zijn twee manieren voor het vereisen van verificatie in twee stappen. eerste optie Hallo tooenable is elke individuele gebruiker voor de Azure multi-factor Authentication (MFA). Wanneer gebruikers afzonderlijk zijn ingeschakeld, uitvoeren ze altijd verificatie in twee stappen (met enkele uitzonderingen, zoals wanneer ze zich vanaf vertrouwde IP-adressen aanmelden of als Hallo onthouden apparaten functie is ingeschakeld). de tweede optie Hallo is tooset van beleid voor voorwaardelijke toegang waarvoor verificatie in twee stappen onder bepaalde omstandigheden.

>[!TIP] 
>Kies een van deze methoden toorequire verificatie in twee stappen, niet beide. Een gebruiker inschakelen voor Azure MFA overschrijft alle beleidsregels voor voorwaardelijke toegang.

## <a name="which-option-is-right-for-you"></a>Welke optie is geschikt voor u

**Azure MFA inschakelen door het wijzigen van de status van gebruikers** Hallo traditionele aanpak voor het vereisen van verificatie in twee stappen. De Tool werkt voor zowel Azure MFA in de cloud Hallo en Azure MFA-Server. Alle Hallo-gebruikers die u in staat stellen Hallo hebben dezelfde ervaring die de verificatie in twee stappen tooperform telkens wanneer ze zich aanmelden. Alle beleidsregels voor voorwaardelijke toegang die mogelijk gevolgen hebben voor die gebruiker inschakelen van een gebruiker worden onderdrukt. 

**Azure MFA met beleid voor voorwaardelijke toegang inschakelen** is een flexibelere benadering voor het vereisen van verificatie in twee stappen. Deze alleen werkt voor Azure MFA in de cloud hello, echter en voorwaardelijke toegang is een [functie van Azure Active Directory betaald](https://www.microsoft.com/cloud-platform/azure-active-directory-features). U kunt beleid voor voorwaardelijke toegang die van toepassing toogroups zoals afzonderlijke gebruikers maken. Met een hoog risico groepen meer beperkingen dan laag risico groepen kunnen worden opgegeven of verificatie in twee stappen kan worden alleen vereist voor met een hoog risico cloud-apps en voor de laag risico die zijn overgeslagen. 

Beide opties gevraagd gebruikers tooregister voor Azure multi-factor Authentication Hallo eerste keer dat ze zich aanmelden nadat Hallo vereisten hebt ingeschakeld. Beide opties werken ook met configureerbare Hallo [Azure multi-factor Authentication-instellingen](multi-factor-authentication-whats-next.md)

## <a name="enable-azure-mfa-by-changing-user-status"></a>Azure MFA inschakelen door het wijzigen van de gebruikersstatus

Gebruikersaccounts in Azure multi-factor Authentication hebt Hallo na drie afzonderlijke statussen:

| Status | Beschrijving | Van invloed op een niet-browsertoepassingen |
|:---:|:---:|:---:|
| Uitgeschakeld |Hallo standaardstatus voor een nieuwe gebruiker is niet ingeschreven voor Azure multi-factor Authentication (MFA). |Nee |
| Ingeschakeld |Hallo-gebruiker is geregistreerd in Azure MFA, maar is niet geregistreerd. Ze worden na vragen aan gebruiker tooregister Hallo wanneer die ze zich aanmeldt. |Nee.  Ze blijven toowork totdat het registratieproces Hallo is voltooid. |
| Afgedwongen |Hallo-gebruiker is ingeschreven en Hallo registratieproces is voltooid voor de Azure MFA. |Ja.  Apps vereisen app-wachtwoorden. |

De status van een gebruiker zijn of een beheerder heeft ingeschreven ze in Azure MFA en of ze Hallo registratieproces voltooid.

Alle gebruikers beginnen *uitgeschakeld*. Wanneer u gebruikers in de Azure MFA, hun statuswijzigingen inschrijft *ingeschakeld*. Wanneer ingeschakelde gebruikers aanmelden en het registratieproces Hallo volledig, hun status verandert te*afgedwongen*.  

### <a name="view-hello-status-for-a-user"></a>Hallo-status voor een gebruiker weergeven

Gebruik Hallo tooaccess Hallo pagina waar u kunt bekijken en beheren van de status van gebruikers van stappen te volgen:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) als beheerder.
2. Ga te**Azure Active Directory** > **gebruikers en groepen** > **alle gebruikers**.
3. Selecteer **multi-Factor Authentication**.
   ![Selecteer de multi-factor Authentication](./media/multi-factor-authentication-get-started-user-states/selectmfa.png)
4. Een nieuwe pagina waarin gebruikersstatussen hello, wordt geopend.
   ![Gebruikersstatus voor meervoudige verificatie - schermafbeelding](./media/multi-factor-authentication-get-started-user-states/userstate1.png)

### <a name="change-hello-status-for-a-user"></a>Hallo-status voor een gebruiker wijzigen

1. Hallo voorafgaand aan de pagina voor de stappen tooget toohello multi-factor authentication-Server-gebruikers gebruiken.
2. Zoeken naar Hallo gebruiker gewenste tooenable voor Azure MFA. Mogelijk moet u toochange weergave boven Hallo Hallo. 
   ![Zoek de gebruiker - schermafbeelding](./media/multi-factor-authentication-get-started-cloud/enable1.png)
3. Controleer Hallo vak de naam van volgende tootheir.
4. Kies op Hallo rechts en onder snelle stappen, **inschakelen** of **uitschakelen**.
   ![Inschakelen van de geselecteerde gebruiker - schermafbeelding](./media/multi-factor-authentication-get-started-cloud/user1.png)

   >[!TIP]
   >*Ingeschakeld* gebruikers automatisch schakelen te*afgedwongen* wanneer ze zich registreren voor Azure MFA. U mag niet Hallo gebruiker status tooenforced handmatig wijzigen. 

5. Bevestig uw selectie in Hallo pop-upvenster dat wordt geopend. 

Nadat u gebruikers hebt ingeschakeld, moeten ze hierover te informeren via e-mail. Vertel dat wordt hen gevraagd tooregister Hallo wanneer die ze zich aanmeldt. Als uw organisatie gebruikmaakt van niet-browser-apps die moderne verificatie niet ondersteunen, moet ze toocreate app-wachtwoorden. U kunt ook een koppeling tooour opnemen [Azure MFA eindgebruiker handleiding](./end-user/multi-factor-authentication-end-user.md) toohelp ze aan de slag.

### <a name="use-powershell"></a>PowerShell gebruiken
toochange hello status status wordt gebruikt door gebruiker [Azure AD PowerShell](/powershell/azure/overview), wijzigen `$st.State`. Er zijn drie mogelijke statussen:

* Ingeschakeld
* Afgedwongen
* Uitgeschakeld  

Verplaats de gebruikers niet rechtstreeks toohello *afgedwongen* status. Niet-browser gebaseerde apps meer werken omdat Hallo gebruiker niet heeft doorlopen registratieprocedure voor MFA en verkregen een [app-wachtwoord](multi-factor-authentication-whats-next.md#app-passwords). 

Met behulp van PowerShell is een goede optie wanneer u gebruikers de mogelijkheid toobulk nodig. Maak een PowerShell-script waarmee een lijst met gebruikers doorlopen en kan ze:

        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

Hier volgt een voorbeeld:

    $users = "bsimon@contoso.com","jsmith@contoso.com","ljacobson@contoso.com"
    foreach ($user in $users)
    {
        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName $user -StrongAuthenticationRequirements $sta
    }

## <a name="enable-azure-mfa-with-a-conditional-access-policy"></a>Azure MFA met beleid voor voorwaardelijke toegang inschakelen

Voorwaardelijke toegang is een betaald functie van Azure Active Directory, met veel mogelijke configuratie-opties. Deze stappen doorlopen die eenzijdige toocreate een beleid. Lees voor meer informatie over [voorwaardelijke toegang in Azure Active Directory](../active-directory/active-directory-conditional-access-azure-portal.md).

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) als beheerder.
2. Ga te**Azure Active Directory** > **voorwaardelijke toegang**.
3. Selecteer **nieuw beleid**.
4. Onder **toewijzingen**, selecteer **gebruikers en groepen**. Gebruik Hallo **opnemen** en **uitsluiten** toospecify welke gebruikers en groepen worden beheerd door beleid Hallo tabbladen.
5. Onder **toewijzingen**, selecteer **Cloud-apps**. Kies tooinclude **alle cloud-apps**.
6. Onder **toegangscontroles**, selecteer **Grant**. Kies **meervoudige authenticatie**.
7. Schakel **beleid inschakelen** te**op** en selecteer vervolgens **opslaan**.

Hallo kunnen andere opties in het beleid voor voorwaardelijke toegang Hallo u toospecify precies wanneer de verificatie in twee stappen vereist. Bijvoorbeeld, u kunt een beleid waarin wordt vermeld: wanneer aannemers tooaccess onze app aanschaf van niet-vertrouwde netwerken op apparaten die niet lid zijn van een domein, moet u verificatie in twee stappen. 

## <a name="next-steps"></a>Volgende stappen

- Tips voor Hallo [aanbevolen procedures voor voorwaardelijke toegang](../active-directory/active-directory-conditional-access-best-practices.md)

- Beheren van multi-factor Authentication-instellingen voor [uw gebruikers en hun apparaten](multi-factor-authentication-manage-users-and-devices.md)