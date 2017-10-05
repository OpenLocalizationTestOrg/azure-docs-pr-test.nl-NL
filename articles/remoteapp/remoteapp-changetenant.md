---
title: Wijzigen van de Azure Active Directory-tenant in Azure RemoteApp | Microsoft Docs
description: Informatie over het wijzigen van de Azure Active Directory-tenant gekoppeld aan Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 20faf169-6e48-428a-8bdd-f231daff19fa
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 7c6c4ded8a11d8399968b2c32aff055d7f3ae5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-azure-active-directory-tenant-in-azure-remoteapp"></a>De Azure Active Directory-tenant in Azure RemoteApp wijzigen
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Azure RemoteApp gebruikt Azure Active Directory (Azure AD) voor de gebruiker toch toegang verlenen. De alleen Azure AD-tenant waarmee u in Azure RemoteApp kunt is met het Azure-abonnement is gekoppeld. U kunt het gekoppelde abonnement weergeven op de **instellingen** pagina in de portal. Bekijk de **Directory** kolom in de **abonnementen** tabblad.

> [!NOTE]
> Voor deze wijziging zou lukken, moet u eerst alle gebruikers verwijderen uit de bestaande Azure Active Directory-tenant van alle Azure RemoteApp-collecties. Hiervoor gaat u naar de Azure Portal, gaat u naar de **Azure RemoteApp** tabblad en openen van elke Azure RemoteApp-verzameling. Ga naar de **gebruikers** tabblad en gebruikers die deel uitmaken van uw huidige Azure Active Directory-tenant verwijderen. Herhaal dit voor alle bestaande Azure RemoteApp-collecties. Zonder dit te doen, zich u niet maken of patch verzamelingen.
> 
> 

Als u gebruiken van een andere tenant wilt, gebruikt u deze stappen kunt u de koppeling met uw abonnement:

1. Verwijder alle Azure AD-gebruikers waaraan u toegang hebt verleend tot Azure RemoteApp-verzamelingen in de portal. (Zie de opmerking hierboven voor de stappen op hoe u dit doet.)
2. Een Microsoft-account (voorheen een Live ID) ingesteld als de servicebeheerder. (Niet weet dat als u al de servicebeheerder? U vindt hier door te klikken op **instellingen -> beheerders**.) Nu ziet hier u hoe u deze instelling wijzigen:
   
   1. Klik op de gebruiker in de rechterbovenhoek en klik vervolgens op **weergeven van mijn factuur**.
   2. Klik op het abonnement. Klik op de pagina nieuwe Schuif naar beneden en klik op **abonnementsgegevens bewerken** in het rechter. (Sorteren van de middelste rechtsonder, als die helpt u bij het zoeken.)
   3. Typ het Microsoft-account voor de gebruiker die u de servicebeheerder moet.
3. Nu u afmelden bij de portal en meld u opnieuw aan met het Microsoft-account dat u hebt opgegeven in de vorige stap.
4. Klik op **Nieuw -> App Services -> Active Directory-Directory > -> Custom maken**.
5. Onder **Directory**, kies **bestaande directory gebruiken**. We gaan nu afmelden bij de portal, dus kies moet **ik ben klaar om te worden afgemeld**.
6. Meld u weer in de portal als globale beheerder van de map die u wilt toevoegen. (Als u niet al een globale beheerder zijn, kunt u zich na een ronde van aanmelden en vervolgens afmelden.)
7. U wordt gevraagd wanneer u zich aanmeldt als u wilt uw bestaande AD-tenant gebruiken bij uw abonnement. Klik op **doorgaan**, en klik vervolgens op **nu afmelden**.
8. Meld u weer opnieuw en Ga terug naar **instellingen -> abonnementen**. Uw abonnement te selecteren en klik vervolgens op **Directory bewerken**. Selecteer de Azure AD-tenant die u wilt gebruiken.

U kunt nu met de nieuwe Azure AD-tenant toegang tot het Azure-abonnement en om gebruikerstoegang te configureren in Azure RemoteApp.

