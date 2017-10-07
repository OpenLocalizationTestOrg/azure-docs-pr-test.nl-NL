---
title: Goedkeuring door Privileged Identity Management-werkstromen aaaAzure | Microsoft Docs
description: Meer informatie over werkstromen voor goedkeuring in Privileged Identity Management (PIM)
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a>Goedkeuringen (Preview)

## <a name="overview"></a>Overzicht

Met goedkeuringen voor Privileged Identity Management, kunt u rollen toorequire goedkeuring voor activering configureren en een of meer gebruikers of groepen kiezen als gedelegeerde fiatteurs. Toolearn houden hoe lezen tooconfigure rollen en fiatteurs selecteren.

>[!NOTE]
Houd er rekening mee dat deze functie nog in ontwikkeling is en fouten kunnen optreden. Hallo-functionaliteit, met inbegrip van tekst naamconventies nog worden gewijzigd en mag niet worden beschouwd als laatste.


## <a name="key-terminology"></a>Belangrijkste termen

*In aanmerking komende gebruiker van de rol* – een in aanmerking komende rol is een gebruiker binnen uw organisatie die is toegewezen tooan Azure AD-rol als in aanmerking komende (rol activering vereist is).

*Gedelegeerde goedkeurder* – een gemachtigde goedkeurder is een of meerdere personen of groepen binnen uw Azure AD die verantwoordelijk zijn voor het goedkeuren van aanvragen voor activering van rollen.

## <a name="scenarios"></a>Scenario's

Hallo private preview ondersteunt Hallo volgen scenario's:

**Als een bevoorrechte rol beheerder (PRA) kunt u:**

-   [goedkeuring voor specifieke rollen inschakelen](#enable-approval-for-specific-roles)

-   [Geef goedkeurder gebruikers en/of groepen tooapprove aanvragen](#specify-approver-users-and/or-groups-to-approve-requests)

-   [Geschiedenis van de aanvraag en goedkeuring voor alle bevoorrechte rollen weergeven](#view-request-and-approval-history-for-all-privileged-roles)

**Als een specifieke goedkeurder kunt u:**

-   [in afwachting van goedkeuring (aanvragen) weergeven](#view-pending-approvals-requests)

-   [goedkeuren of afwijzen aanvragen voor uitbreiding van de rol (één en/of bulk)](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [Geef de reden voor Mijn goedkeuring/afwijzing](#provide-justification-for-my-approval/rejection) 

**Als een in aanmerking komende gebruiker voor de rol kunt u:**

-   [activering van de aanvraag van een rol die goedkeuring vereist](#request-activation-of-a-role-that-requires-approval)

-   [Hallo-status van uw aanvraag tooactivate weergeven](#view-the-status-of-your-request-to-activate)

-   [uw taak te voltooien in Azure AD als activering is goedgekeurd](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a>Navigatie

We hebben Hallo navigatie toosupport goedkeuringen bijgewerkt

![](media/azure-ad-pim-approval-workflow/image001.png)

Hallo standaard startpagina biedt snel toegang tooinformation over PIM en Hallo nieuwe goedkeuringen documentatie.

![](media/azure-ad-pim-approval-workflow/image002.png)

We hebben hebt ook een nieuwe sectie voor alle gebruikers van PIM, 'Mijn controlegeschiedenis' toegevoegd. Hier vindt u alle relevante tooyour identiteit van de Hallo informatie. Dit omvat alle uw in behandeling en voltooid aanvragen, alle beslissingen over Hallo aanvragen die u hebt opgelost en de afgelopen rol activeringen op één handige locatie.

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a>Goedkeuring voor specifieke rollen inschakelen

Directory-functies tooenable goedkeuring voor een specifieke rol eerst uit de linkernavigatiebalk Hallo selecteren.

![](media/azure-ad-pim-approval-workflow/image004.png)

Zoek en selecteer de instellingen in Hallo linkernavigatiegedeelte van Directory-functies

![](media/azure-ad-pim-approval-workflow/image006.png)

Selecteer de bevoorrechte rollen:

![](media/azure-ad-pim-approval-workflow/image009.png)

Selecteert u 'Inschakelen' in hello goedkeuringssectie vereisen:

![](media/azure-ad-pim-approval-workflow/image011.png)

Eenmaal is ingeschakeld, uitbreidt Hallo blade tooshow Hallo volgende details:

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
Als u niet alle goedkeurders opgeeft, worden Hallo PRA(s) Hallo standaard fiatteur (s). PRA(s) zijn vereiste tooapprove activering van alle voor deze rol aanvragen.

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a>Geef goedkeurder gebruikers en/of groepen tooapprove aanvragen

toodelegate goedkeuring, klikt u op de optie Hallo 'Goedkeurders selecteren' te:

![](media/azure-ad-pim-approval-workflow/image015.png)

Wanneer Hallo Selecteer goedkeurders blade wordt geladen, u kunt zoeken naar een specifieke gebruiker of groep met behulp van de zoekbalk Hallo op Hallo top- of te selecteren in de vooraf ingestelde lijst Hallo en klik vervolgens op 'Selecteren' als voltooid:

![](media/azure-ad-pim-approval-workflow/image017.png)

Opmerking: U kunt meerdere gebruikers of groepen tegelijkertijd selecteren.

Uw selectie weergegeven in de lijst Hallo van geselecteerde goedkeurders zoals hieronder wordt weergegeven:

![](media/azure-ad-pim-approval-workflow/image019.png)

tooremove goedkeurder, klik op Hallo verwijderen volgende tootheir naam van de knop.

tooadd extra fiatteurs herhaaldelijk Hallo-proces.

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a>Geschiedenis van de aanvraag en goedkeuring voor alle bevoorrechte rollen weergeven

de aanvraag en goedkeuring geschiedenis tooview voor alle bevoorrechte rollen selecteren controlegeschiedenis Hallo dashboard:

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
Hallo-gegevens door de actie sorteren en zoek naar 'Activering goedgekeurd'

### <a name="view-pending-approvals-requests"></a>In afwachting van goedkeuring (aanvragen) weergeven

U zult als een gemachtigde goedkeurder e-mailmeldingen ontvangen wanneer een aanvraag wacht op uw goedkeuring wordt. tooview van deze aanvragen in Hallo PIM-portal op het dashboardtabblad (in de nieuwe navigatie Hallo) Selecteer Hallo 'in behandeling goedkeuringsaanvragen' hello navigatiebalk links.

![](media/azure-ad-pim-approval-workflow/image023.png)

Van daaruit ziet u een lijst met aanvragen in afwachting van goedkeuring:

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a>Goedkeuren of afwijzen aanvragen voor uitbreiding van de rol (één en/of bulk)

Selecteer Hallo aanvragen u wenst dat tooapprove of weigeren en klik op de knop Hallo in de actiebalk die met uw beslissing overeenkomt:

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a>Geef de reden voor Mijn goedkeuring/afwijzing

Dit wordt een nieuwe blade tooapprove openen of meerdere aanvragen tegelijk weigeren. Voer een reden voor uw beslissing en klikt u op (toestaan of weigeren) op Hallo onder of Hallo blade:

![](media/azure-ad-pim-approval-workflow/image029.png)

Wanneer het Hallo-aanvraag is voltooid, Hallo statussymbool geeft de beslissingen die u hebt gemaakt (in dit voorbeeld Hallo besluit is goedkeuren):

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a>Activering van de aanvraag van een rol die goedkeuring vereist

Activering van een rol waarvoor goedkeuring kan worden gestart vanuit Hallo oude PIM navigatie of nieuwe navigatie Hallo aanvraagt, als Hallo-proces voor de rol activering blijft Hallo dezelfde. Selecteer een rol gewoon uit Hallo lijst met rollen te activeren:

![](media/azure-ad-pim-approval-workflow/image033.png)

Als een bevoorrechte rol meerledige verificatie vereist, wordt u gevraagd eerst die taak te voltooien:

![](media/azure-ad-pim-approval-workflow/image035.png)

Wanneer u klaar bent, klikt u op activeren en een reden opgeven (indien nodig):

![](media/azure-ad-pim-approval-workflow/image037.png)

Hallo aanvrager ziet een melding dat de aanvraag Hallo is in afwachting van goedkeuring:

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a>Hallo-status van uw aanvraag tooactivate weergeven

Hallo-status van een aanvraag in behandeling tooactivate weergeven moet worden geopend in de nieuwe navigatie. Selecteer in de Hallo linkernavigatiebalk Hallo 'Mijn aanvragen' tabblad:

![](media/azure-ad-pim-approval-workflow/image041.png)

aanvraag voor weergave van Hallo standaardwaarden te 'In behandeling', maar u kunt alle toosee schakelen of afgewezen aanvragen.

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a>Uw taak te voltooien in Azure AD als activering is goedgekeurd

Zodra het Hallo-aanvraag is goedgekeurd, Hallo rol actief is en u kunt doorgaan met werk waarvoor deze rol is vereist.

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a>Volgende stappen

Uw feedback is belangrijk toous. Kunt u gratis tooshare opmerkingen of feedback met ons hier!
