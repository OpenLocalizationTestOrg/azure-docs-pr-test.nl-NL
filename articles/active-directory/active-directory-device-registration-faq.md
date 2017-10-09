---
title: Automatische apparaatregistratie van Active Directory Veelgestelde vragen over aaaAzure | Microsoft Docs
description: Automatische apparaatregistratie met Azure Active Directory-Veelgestelde vragen.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: ba7f113fd3bc310def001a1f44d938b0be71dba8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-automatic-device-registration-faq"></a>Veelgestelde vragen over de automatische apparaatregistratie van Azure Active Directory

**V: ik onlangs Hallo apparaat geregistreerd. Waarom zie ik Hallo apparaat kan niet onder Mijn gebruikersgegevens in hello Azure-portal?**

**A:** Windows 10-apparaten die lid van een domein met automatische apparaatregistratie zijn worden niet weergegeven onder Hallo gebruikersgegevens.
U moet alle apparaten toouse PowerShell toosee. 

Alleen worden hello volgende apparaten vermeld in Hallo gebruikersgegevens:

- Alle persoonlijke apparaten die niet lid enterprise 
- Alle niet - Windows 10 / Windows Server 2016 
- Alle niet-Windows-apparaten 

---

**V: Waarom kan ik alle Hallo apparaten geregistreerd in Azure Active Directory hello Azure-portal niet zien?** 

**A:** er is momenteel geen toosee manier alle geregistreerde apparaten in hello Azure-portal. Alle apparaten, kunt u Azure PowerShell toofind gebruiken. Zie voor meer informatie, Hallo [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.

--- 

**V: hoe weet ik welke status Hallo apparaat registratie van de client Hallo is?**

**A:** afhankelijk van de apparaatstatus registratie Hallo:

- Welke Hallo-apparaat
- Hoe het is geregistreerd 
- Details tooit gerelateerd. 
 

---

**V: Waarom is een apparaat dat ik hebt verwijderd in hello Azure portal of met Windows PowerShell nog steeds vermeld als geregistreerd?**

**A:** dit is standaard. Hallo-apparaat geen toegang tooresources in Hallo cloud. Als u wilt dat tooremove Hallo apparaat en opnieuw registreren, moet een handmatige actie toobe genomen op Hallo-apparaat. 

Voor Windows 10 en Windows Server 2016 met on-premises AD-domein:

1.  Open Hallo-opdrachtprompt als beheerder.

2.  Type`dsregcmd.exe /debug /leave`

3.  Meld u af en meld u aan tootrigger Hallo geplande taak die Hallo-apparaat opnieuw registreert. 

Voor andere Windows-platforms die zich on-premises AD-domein:

1.  Open Hallo-opdrachtprompt als beheerder.
2.  Typ `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.
3.  Typ `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.

---

**V: Waarom zie ik dubbele apparaatvermeldingen in Azure-portal?**

**A:**

-   Voor Windows 10 en Windows Server 2016, als ze herhaalde pogingen toounjoin zijn en opnieuw aanmelden hello hetzelfde apparaat, kunnen er dubbele vermeldingen. 

-   Als u toevoegen werk of School-Account hebt gebruikt, elke windows-gebruiker die voegen werk- of Schoolaccount gebruikt een nieuwe apparaatrecord gemaakt met de Hallo dezelfde apparaatnaam.

-   Andere Windows-platforms die zich on-premises AD-domein met behulp van automatische registratie maakt een nieuwe apparaatrecord met Hallo dezelfde apparaatnaam voor elke domeingebruiker die zich bij Hallo-apparaat aanmeldt. 

-   Een AADJ-machine die is gewist, opnieuw geïnstalleerd en opnieuw toegevoegd met de Hallo dezelfde naam, wordt weergegeven als een andere record met Hallo dezelfde apparaatnaam.

---

**V: waarom een gebruiker nog steeds toegang tot bronnen vanaf een apparaat dat ik in hello Azure-portal hebt uitgeschakeld?**

**A:** een intrekken toobe toegepast tooan uur kan duren.

>[!Note] 
>Verloren apparaten, wordt u aangeraden Hallo apparaat tooensure gebruikers geen toegang tot Hallo apparaat wissen. Zie voor meer informatie [apparaten inschrijven voor beheer in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune). 


---

**V: Waarom kunnen mijn gebruikers zien 'U geen toegang vanaf hier'?**

**A:** als u bepaalde regels toorequire voor voorwaardelijke toegang tot de status van een specifiek apparaat hebt geconfigureerd en Hallo-apparaat voldoet niet aan criteria hello, gebruikers worden geblokkeerd en dit bericht wordt weergegeven. Voer Hallo regels evalueren en zorg ervoor dat het Hallo-apparaat kunnen toomeet Hallo criteria tooavoid dit bericht is.

---


**V: ik Zie Hallo apparaatrecord onder Hallo gebruikersgegevens in hello Azure-portal en Hallo status kunt zien zoals die is geregistreerd op Hallo-client. Kan dat ik een correct instellen voor het gebruik van voorwaardelijke toegang?**

**A:** Hallo record van apparaat (deviceID) en status op Hallo Azure-portal moeten overeenkomen met de Hallo-client en voldoen aan de evaluatiecriteria van een voor voorwaardelijke toegang. Zie voor meer informatie [aan de slag met Azure Active Directory-apparaatregistratie](active-directory-device-registration.md).

---

**V: Waarom krijg ik een bericht 'gebruikersnaam of wachtwoord is onjuist' voor een apparaat ik tooAzure AD zojuist hebt toegevoegd?**

**A:** veelvoorkomende redenen voor dit scenario zijn:

- Uw referenties zijn niet langer geldig.

- Kan geen toocommunicate met Azure Active Directory, is uw computer. Controleer of eventuele problemen met de netwerkverbinding.

- vereisten voor Azure AD Join van Hallo is niet voldaan aan. Zorg ervoor dat u stappen voor het Hallo hebt gevolgd [cloud uitbreiden mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join](active-directory-azureadjoin-overview.md).  

- Federatieve aanmeldingen vereist uw federatieve server toosupport een actieve WS-Trust-eindpunt. 

---

**V: Waarom Zie Hallo ' Oops... is een fout opgetreden! "dialoogvenster wanneer ik probeer mijn PC toevoegen?**

**A:** dit is een resultaat van het instellen van Azure Active Directory-inschrijving met Intune. Zie voor meer informatie [Windows Apparaatbeheer instellen](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).  

---

**V: Waarom is mijn poging toojoin een PC mislukken, maar ik heb informatie over de fout niet ontvangen?**

**A:** een waarschijnlijke oorzaak is dat Hallo-gebruiker is aangemeld met het ingebouwde beheerdersaccount Hallo toohello-apparaat. Maak een andere lokale account voordat u Azure Active Directory Join toocomplete Hallo setup. 

---

**V: waar vind ik instructies voor het Hallo-installatie van de automatische apparaatregistratie**

**A:** Zie voor gedetailleerde instructies [hoe tooconfigure automatische registratie van Windows-domein apparaten met Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)

---

**V: waar vind ik het oplossen van informatie over automatische apparaatregistratie voor Hallo?**

**A:** voor informatie over probleemoplossing, Zie:

- [Automatische registratie van domein het oplossen van problemen die lid zijn van computers tooAzure AD – Windows 10 en Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md)

- [Automatische registratie van domein het oplossen van problemen die lid zijn van computers tooAzure AD voor Windows downlevel-clients](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

