---
title: toegang tot de toepassing zelf van de aaaHow toouse | Microsoft Docs
description: Selfservice toepassing toegang tooallow gebruikers toofind hun eigen toepassingen inschakelen
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
ms.reviewer: japere
ms.openlocfilehash: 03a44c20d544a6232fa802bcffaf70e5030ad3ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-self-service-application-access"></a>Hoe toouse selfservice toepassing openen

Voordat u uw gebruikers kunnen toepassingen van hun Toegangsvenster automatisch detecteren, moet u tooenable **toegang tot toepassingen Self-service** tooany toepassingen die u wenst dat tooallow gebruikers tooself-detecteren en om toegang te vragen.

Deze functie is een uitstekende manier voor u toosave tijd en geld als een IT-groep, en het wordt sterk aanbevolen als onderdeel van een implementatie van moderne toepassingen met Azure Active Directory.

Met deze functie kunt u het volgende doen:

-   Kunnen gebruikers zelf detecteren toepassingen van Hallo [toepassing Toegangsvenster](https://myapps.microsoft.com/) zonder te proberen alles Hallo IT-groep.

-   Deze vooraf geconfigureerde groep met gebruikers tooa toevoegen zodat u kunt zien wie toegang heeft aangevraagd, toegang verwijderen en Hallo rollen toegewezen toothem beheren.

-   Eventueel een zakelijke goedkeurder tooapprove toepassing toegangsaanvragen toestaan zodat Hallo IT-groep niet te worden hoeven.

-   Configureer desgewenst up too10 personen die toegang toothis toepassing kunnen goedkeuren.

-   Eventueel tooset Hallo wachtwoorden toestaan een zakelijke goedkeurder die gebruikers toosign kunnen gebruiken in de toepassing toohello, rechts van Hallo zakelijke goedkeurder [Toegangspaneel toepassing](https://myapps.microsoft.com/).

-   Optioneel automatisch toegewezen selfservicegebruikers tooan toepassingsrol rechtstreeks toewijzen.

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

   * Groepen worden niet ondersteund.

13. **Optioneel:** **voor toepassingen die functies zichtbaar**, indien tooassign Self-service goedgekeurde gebruikers tooa rol gewenst, klikt u op Hallo selector volgende toohello **toowhich rol moeten gebruikers worden toegewezen in dit toepassing?**  tooselect Hallo rol toowhich deze gebruikers moeten worden toegewezen.

14. Klik op Hallo **opslaan** knop bovenaan Hallo Hallo blade toofinish.

Nadat u de configuratie van Self-Service toepassing hebt voltooid, gebruikers tootheir kunnen navigeren [toepassing Toegangspaneel](https://myapps.microsoft.com/) en klik op Hallo **+ toevoegen** knop toofind Hallo apps toowhich u hebt ingeschakeld Selfservice toegang. Zakelijke goedkeurders er ook een melding in hun [Toegangspaneel toepassing](https://myapps.microsoft.com/). U kunt een melding wanneer een gebruiker toegang tooan toepassing waarvoor goedkeuring is aangevraagd e-mail inschakelen. 

Deze goedkeuringen ondersteuning voor één werkstromen voor goedkeuring, wat betekent dat als u meerdere goedkeurders opgeeft, een enkele fiatteur access toohello-toepassing goedkeuren kan.

## <a name="next-steps"></a>Volgende stappen
[Azure Active Directory instellen voor selfservicegroepsbeheer](active-directory-accessmanagement-self-service-group-management.md)
