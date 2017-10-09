---
title: aaaHow tooassign gebruikers en groepen tooan toepassing | Microsoft Docs
description: Gebruikers toegang tot toohello toepassingen toogrant toewijzen
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: e039a26e4b8f88ad747354859f1071b8f74b6789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-and-groups-tooan-application"></a>Hoe tooassign gebruikers en groepen tooan toepassing

Voordat u uw gebruikers kunnen Hallo hieronder voor een bepaalde toepassing doen, moet u toofirst **ze toohello toepassing toewijzen** toogrant ze toegang krijgen tot:

-   Toegang tot een toepassing met behulp van **rechtstreeks navigeren in de URL van de toepassing toohello** (ook wel bekend als Serviceprovider geïnitieerde eenmalige aanmelding).

-   Toegang tot een toepassing met behulp van Hallo **toegangs-URL van gebruiker** op een toepassing **eigenschappen** pagina (ook wel bekend als IDP geïnitieerde aanmelding).

-   Zie een toepassing worden weergegeven op hun [toepassing Toegangsvenster](https://myapps.microsoft.com/) of mobiele toepassing.

-   Zie een toepassing worden weergegeven op hun [startprogramma voor toepassingen van Office 365](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).

## <a name="methods-tooassign-applications-with-azure-active-directory"></a>Methoden tooassign toepassingen met Azure Active Directory 

Er zijn 3 manieren kunt u toepassingen met Azure Active Directory:

-   [Een gebruiker toewijzen rechtstreeks tooan toepassing als een beheerder](#assign-a-user-directly-as-an-administrator)

-   [Een groep worden toegewezen rechtstreeks tooan toepassing als een beheerder](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [Selfservice toepassing toegang tooallow gebruikers toofind hun eigen toepassingen inschakelen](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a>Een gebruiker toewijzen rechtstreeks als een beheerder

tooassign een of meer gebruikers tooan toepassing rechtstreeks Hallo volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.

7.  Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.

8.  Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.

9.  Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.

10. Type in Hallo **volledige naam** of **e-mailadres** van Hallo gebruiker u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.

11. Beweeg de muisaanwijzer over Hallo **gebruiker** in Hallo lijst tooreveal een **selectievakje**. Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van gebruiker uw gebruiker toohello **geselecteerde** lijst.

12. **Optioneel:** indien te gewenst**toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd voor deze gebruiker toohello **geselecteerde** lijst.

13. Wanneer u klaar bent met het selecteren van gebruikers, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.

14. **Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello gebruikers die u hebt geselecteerd.

15. Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello gebruikers geselecteerd.

Hallo-gebruikers die u hebt geselecteerd worden na een korte periode, kunnen toolaunch deze toepassingen met behulp van methoden die worden beschreven in Hallo oplossing beschrijving sectie Hallo.

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a>Een groep worden toegewezen rechtstreeks tooan toepassing als een beheerder

tooassign een of meer groepen tooan toepassing rechtstreeks Hallo stappen hieronder:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.

7.  Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.

8.  Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.

9.  Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.

10. Type in Hallo **volledige groepsnaam** van Hallo groep u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.

11. Beweeg de muisaanwijzer over Hallo **groep** in Hallo lijst tooreveal een **selectievakje**. Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van de groep uw gebruiker toohello **geselecteerde** lijst.

12. **Optioneel:** indien te gewenst**toevoegen van meer dan één groep**, type in een andere **volledige groepsnaam** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd van deze groep toohello **geselecteerde** lijst.

13. Wanneer u klaar bent met groepen te selecteren, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.

14. **Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello groepen die u hebt geselecteerd.

15. Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello geselecteerde groepen.

Hallo gebruikers binnen Hallo-groepen die u hebt geselecteerd worden na een korte periode, kunnen toolaunch deze toepassingen met behulp van methoden die worden beschreven in Hallo oplossing beschrijving sectie Hallo. Als dit dynamische groepen zijn, mogelijk zijn er enkele aanvullende verwerking vertraging in deze toewijzingen worden weergegeven voor gebruikers binnen deze groepen toegewezen.

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a>Selfservice toepassing toegang tooallow gebruikers toofind hun eigen toepassingen inschakelen

Toegang tot de toepassing zelf is een uitstekende manier tooallow gebruikers tooself-toepassingen detecteren, eventueel Hallo business groep toestaan tooapprove toothose toepassingen. U kunt toestaan Hallo business groep toomanage Hallo referenties toegewezen gebruikers toothose voor wachtwoord eenmalige aanmelding op toepassingen rechtstreeks vanuit hun panelen toegang.

tooenable selfservice toepassing toegang tooan toepassing hello stappen hieronder:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

   * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer gewenste tooenable Self-service toofrom Hallo toegangslijst Hallo-toepassing.

7.  Nadat de toepassing hello wordt geladen, klikt u op **Self-service** uit van de toepassing hello linkerkant navigatiemenu.

8.  tooenable toegang tot de toepassing Self-service voor deze toepassing, schakelt u Hallo **toorequest access toothis-toepassing voor gebruikers toestaan?** te schakelen**Ja.**

9.  Tooselect hello toowhich gebruikers die een groep aanvragen toegang toothis toepassing moet worden toegevoegd, klik vervolgens op Hallo selector volgende toohello label **toowhich groep moet worden toegewezen gebruikers worden toegevoegd?** en selecteert u een groep.

10. **Optioneel:** als u toorequire goedkeuring van een zakelijke wenst voordat gebruikers toegang kunt krijgen, stelt u Hallo **moeten worden goedgekeurd voordat u verleent toegang toothis toepassing?** te schakelen**Ja**.

11. **Optioneel: voor toepassingen die gebruikmaken van wachtwoord eenmalige aanmelding alleen op** desgewenst tooallow deze bedrijven goedkeurders toospecify Hallo wachtwoorden die worden verzonden toothis toepassingen voor goedgekeurde gebruikers instellen Hallo **toestaan goedkeurders tooset wachtwoorden van de gebruiker voor deze toepassing?**  te schakelen**Ja**.

12. **Optioneel:** toospecify Hallo business goedkeurders die mogen tooapprove toegang toothis toepassing, klikt u op Hallo selector volgende toohello label **die tooapprove access toothis-toepassing is toegestaan?** tooselect up too10 afzonderlijke business goedkeurders.

  >[!NOTE]
  >Groepen worden niet ondersteund.
  >
  >

13. **Optioneel:** **voor toepassingen die functies zichtbaar**, indien tooassign Self-service goedgekeurde gebruikers tooa rol gewenst, klikt u op Hallo selector volgende toohello **toowhich rol moeten gebruikers worden toegewezen in dit toepassing?**  tooselect Hallo rol toowhich deze gebruikers moeten worden toegewezen.

14. Klik op Hallo **opslaan** knop bovenaan Hallo Hallo blade toofinish.

Nadat u de configuratie van Self-Service toepassing hebt voltooid, gebruikers tootheir kunnen navigeren [toepassing Toegangspaneel](https://myapps.microsoft.com/) en klik op Hallo **+ toevoegen** knop toofind Hallo apps toowhich u hebt ingeschakeld Selfservice toegang. Zakelijke goedkeurders er ook een melding in hun [Toegangspaneel toepassing](https://myapps.microsoft.com/). U kunt een melding wanneer een gebruiker toegang tooan toepassing waarvoor goedkeuring is aangevraagd e-mail inschakelen. 

Deze goedkeuringen ondersteuning voor één goedkeuringswerkstromen, wat betekent dat als u meerdere goedkeurders opgeeft, kan een enkele fiatteur goedkeurder access toohello-toepassing.

## <a name="next-steps"></a>Volgende stappen
[Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy](active-directory-application-proxy-sso-using-kcd.md)
