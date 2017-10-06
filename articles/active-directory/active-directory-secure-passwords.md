---
title: aaaAzure AD gelaagde wachtwoordbeveiliging | Microsoft Docs
description: Legt uit hoe u Azure AD worden afgedwongen sterke wachtwoorden en wachtwoorden van gebruikers beschermt tegen cyberbeveiliging criminelen,
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a>Een benadering meerdere lagen tooAzure AD wachtwoordbeveiliging

Dit artikel worden enkele aanbevolen procedures die u kunt uw Azure Active Directory (Azure AD) of de Microsoft-Account als een gebruiker of als een beheerder tooprotect volgen.

 > [!NOTE]
 > Azure AD-beheerders kunnen gebruikerswachtwoorden Hallo richtlijnen in Hallo artikel met [Hallo-wachtwoord opnieuw instellen voor een gebruiker in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).
 >
 > Gebruikers kunnen wachtwoord opnieuw instellen hun eigen met Hallo richtlijnen in Hallo artikel [Help ik mijn Azure AD-wachtwoord vergeten](active-directory-passwords-update-your-own-password.md).
 >

## <a name="password-requirements"></a>Vereisten voor wachtwoorden

Azure AD omvat Hallo algemene benaderingen toosecuring wachtwoorden te volgen:

* Vereisten voor de lengte van het wachtwoord
* Vereisten voor wachtwoordcomplexiteit
* Gepland en automatisch verlopen van wachtwoorden

Zie voor informatie over het wachtwoord opnieuw instellen in Azure Active Directory, Hallo onderwerp [Azure AD selfservice voor wachtwoordherstel voor IT-professionals Hallo](active-directory-passwords.md).

## <a name="azure-ad-password-protections"></a>Bescherming van Azure AD-wachtwoord

Azure AD en Microsoft-Accountsysteem gebruiken bedrijfstak bewezen Hallo nadert tooensure beveiliging van gebruikers- en wachtwoorden, waaronder:

* Dynamisch uitsluiten van wachtwoorden
* Smart Password Lockout

Zie voor informatie over wachtwoordbeheer op basis van huidige research Hallo technisch document [wachtwoord richtlijnen](http://aka.ms/passwordguidance).

### <a name="dynamically-banned-passwords"></a>Dynamisch uitsluiten van wachtwoorden

Azure AD en Microsoft-Accounts wachtwoordbeveiliging veiligstellen door dynamisch verboden veelgebruikte wachtwoorden. Hello Azure ID Identity Protection-team analyseert regelmatig verboden wachtwoordenlijsten, voorkomen dat gebruikers wachtwoorden veelgebruikte kiezen. Deze service is beschikbaar tooAzure AD en klanten van Hallo-Service van Microsoft-Account.

Bij het maken van wachtwoorden, is het belangrijk voor beheerders tooencourage gebruikers toochoose wachtwoord zinnen met een unieke combinatie van letters, cijfers, tekens of woorden. Deze aanpak kunt toomake gebruikerswachtwoorden nagenoeg onmogelijk toobe maar gemakkelijker voor gebruikers tooremember aangetast.

#### <a name="password-breaches"></a>Wachtwoord schendingen

Microsoft werkt altijd één stap toostay tevoren cyberbeveiliging criminelen.

Hello Azure AD Identity Protection-team analyseert voortdurend wachtwoorden die vaak worden gebruikt. Cyberbeveiliging criminelen ook gebruiken vergelijkbaar strategieën tooinform hun aanvallen, zoals gebouw een [Regenboog tabel](https://en.wikipedia.org/wiki/Rainbow_table) voor wachtwoord-hashes te kraken.

Microsoft analyseren voortdurend [gegevens schendingen](https://www.privacyrights.org/data-breaches) toomaintain een lijst met dynamisch bijgewerkte verboden wachtwoorden, die zorgt ervoor dat de wachtwoorden kwetsbaar zijn verboden voordat ze een reëel getal dreiging tooAzure AD-klanten. Zie voor meer informatie over onze huidige beveiligingsinspanningen Hallo [Microsoft Intelligence beveiligingsrapport](https://www.microsoft.com/security/sir/default.aspx).

### <a name="smart-password-lockout"></a>Smart Password Lockout

Als Azure AD een mogelijke poging cyberbeveiliging strafrechtelijke-toohack in het wachtwoord van een gebruiker detecteert, vergrendelen we Hallo-gebruikersaccount met slim wachtwoord vergrendeling. Azure AD is ontworpen toodetermine Hallo risico dat samenhangt met specifieke aanmelding sessies. Vervolgens wordt met het meest recente beveiligingsgegevens hello, accountvergrendeling semantiek toostop cyberbeveiliging bedreigingen worden toegepast.

Als een gebruiker is vergrendeld buiten Azure AD, lijkt het scherm vergelijkbare toohello een die volgt op:

  ![Toegang tot Azure AD geblokkeerd](./media/active-directory-secure-passwords/locked-out-azuread.png)

Voor andere Microsoft-accounts lijkt het scherm vergelijkbare toohello een die volgt op:

  ![Toegang tot Microsoft-account geblokkeerd](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

Zie voor informatie over het wachtwoord opnieuw instellen in Azure Active Directory, Hallo onderwerp [Azure AD selfservice voor wachtwoordherstel voor IT-professionals Hallo](active-directory-passwords.md).

  >[!NOTE]
  >Als u een Azure AD-beheerder bent, kunt u toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid dat uw gebruikers helemaal traditionele wachtwoorden maken.
  >

## <a name="next-steps"></a>Volgende stappen

* [Hoe tooupdate uw eigen wachtwoord](active-directory-passwords-update-your-own-password.md)
* [Hallo grondbeginselen van Azure identity management](fundamentals-identity.md)
* [Activiteit voor het rapport op wachtwoord opnieuw instellen](active-directory-passwords-reporting.md)


