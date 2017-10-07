---
title: aaaHow toepassingen worden weergegeven op het toegangsvenster Hallo | Microsoft Docs
description: Waarom een toepassing wordt weergegeven in het deelvenster toegang Hallo
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
ms.reviewr: japere
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a>Hoe toepassingen worden weergegeven op het toegangsvenster Hallo

Hallo Toegangspaneel is een portal op Internet waarmee een gebruiker met een werk of schoolaccount in Azure Active Directory (Azure AD) tooview en start cloud-gebaseerde toepassingen die hello Azure AD-beheerder heeft deze toegang verleend tot. Deze toepassingen zijn geconfigureerd namens de gebruiker Hallo in hello Azure AD-portal. Hallo beheerder kunt inrichten Hallo toohello toepassingsgebruiker rechtstreeks of een gebruiker deel uitmaakt van het Hallo-toepassing die voorkomen op Hallo van de gebruiker Toegangsvenster waardoor tooa-groep.

## <a name="general-issues-toocheck-first"></a>Algemene problemen toocheck eerst

-   Als een toepassing is verwijderd uit een gebruiker of groep Hallo gebruiker lid van is, opnieuw toosign in en uit in het toegangsvenster Hallo van de gebruiker na een paar minuten toosee als toepassing hello wordt verwijderd.

-   Als u een licentie is verwijderd uit een gebruiker of groep Hallo gebruiker is dat lid van deze kan lang duren, afhankelijk van Hallo omvang en complexiteit van de groep Hallo voor toobe van wijzigingen aangebracht. Voor extra tijd voordat je je aanmeldt bij Hallo Toegangsvenster toestaan.

## <a name="problems-related-tooassigning-applications-toousers"></a>Problemen met gerelateerde tooassigning toepassingen toousers

Een gebruiker mogelijk ziet u een toepassing op hun Toegangsvenster omdat ze eerder tooit toegewezen had. Hieronder vindt u enkele toocheck manieren:

-   [Controleren of een gebruiker toohello toepassing is toegewezen](#check-if-a-user-is-assigned-to-the-application)

-   [Controleer of een gebruiker zich onder een licentie gerelateerde toohello toepassing](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a>Controleren of een gebruiker toohello toepassing is toegewezen

toocheck als een gebruiker is toegewezen toohello-toepassing hello volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

6.  **Search** voor Hallo-naam van de betrokken Hallo-toepassing.

7.  Klik op **gebruikers en groepen**.

8.  Controleer toosee als de gebruiker toohello toepassing is toegewezen.

  * Als u tooremove Hallo gebruiker van toepassing hello wilt, **klikt u op Hallo rij** van Hallo gebruiker en selecteer **verwijderen**.

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a>Controleer of een gebruiker zich onder een licentie gerelateerde toohello toepassing

toocheck een gebruiker de toegewezen licenties, Hallo stappen hieronder:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle gebruikers**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.

7.  Klik op **licenties** toosee welke licenties Hallo gebruiker momenteel is toegewezen.

   * Hallo Toegangsvenster van de gebruiker als Hallo gebruiker tooan dit eerste partij Office-toepassingen tooappear inschakelen op Office-licentie is toegewezen.

## <a name="problems-related-tooassigning-applications-toogroups"></a>Problemen met gerelateerde tooassigning toepassingen toogroups

Een gebruiker mogelijk ziet u een toepassing op hun Toegangsvenster omdat ze deel uitmaken van een groep die de toepassing hello is toegewezen. Hieronder vindt u enkele toocheck manieren:

-   [Controleer de groepslidmaatschappen van een gebruiker](#check-a-users-group-memberships)

-   [Als een gebruiker lid is van een groep tooa licentie toegewezen controleren](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a>Controleer de groepslidmaatschappen van een gebruiker

toocheck een groepslidmaatschap, Hallo stappen hieronder:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle gebruikers**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.

7.  Klik op **groepen.**

8.  Controleer de toosee als de gebruiker deel uit van een groep die is toegewezen toohello-toepassing maakt.

   * Als u tooremove Hallo gebruiker uit groep Hallo wilt **klikt u op Hallo rij** van Hallo groep en selecteer verwijderen.

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a>Als een gebruiker lid is van een groep tooa licentie toegewezen controleren

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle gebruikers**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.

7.  Klik op **groepen.**

8.  Klik op Hallo rij van een bepaalde groep.

9.  Klik op **licenties** toosee welke licenties Hallo groep tooit is toegewezen.

  * Hallo Toegangsvenster van de gebruiker als Hallo groep tooan dit mogelijk bepaalde tooappear eerste partij Office-toepassingen inschakelen op Office-licentie is toegewezen.


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Als deze stappen voor probleemoplossing niet Hallo Hallo probleem oplossen

Open een ondersteuningsticket Hello volgende informatie, indien beschikbaar:

-   Correlatie fout-ID

-   UPN (e-mailadres van de gebruiker)

-   Tenant-id

-   Browsertype

-   Tijdzone en de tijd/tijdsbestek tijdens fout optreedt

-   Fiddler traceringen

## <a name="next-steps"></a>Volgende stappen
[Toepassingen beheren met Azure Active Directory](active-directory-enable-sso-scenario.md)
