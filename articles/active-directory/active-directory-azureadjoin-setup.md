---
title: aaaSetting stellen Azure AD Join voor uw gebruikers | Microsoft Docs
description: Hier wordt uitgelegd hoe beheerders Azure AD Join kunnen instellen voor on-premises directory- en apparaatregistratie.
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a>Azure AD Join instellen in uw organisatie
Voordat u Azure Active Directory Join (Azure AD Join) instelt, moet u de synchronisatie tooeither registreert uw on-premises directory van gebruikers toohello cloud of handmatig beheerde accounts in Azure AD maken.

Gedetailleerde instructies voor het synchroniseren van uw lokale gebruikers tooAzure AD wordt beschreven in [uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).

toomanually maken en beheren van gebruikers in Azure AD, te verwijzen[Gebruikersbeheer in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).

## <a name="set-up-device-registration"></a>Apparaatregistratie instellen
1. Meld u aan toohello Azure-portal als beheerder.
2. Selecteer in het linkerdeelvenster Hallo **Active Directory**.
3. Op Hallo **Directory** tabblad, selecteer uw directory.
4. Selecteer Hallo **configureren** tabblad.
5. Ga toohello **apparaten** sectie.
6. Op Hallo **apparaten** tabblad, Hallo volgende instellen:  
   * **MAXIMUM aantal apparaten PER gebruiker**: Selecteer Hallo kunt u het maximum aantal apparaten dat een gebruiker in Azure AD hebben kan.  Als een gebruiker dit quotum bereikt, worden ze niet kunnen tooadd extra apparaten worden totdat een of meer van de bestaande apparaten zijn verwijderd.
   * **VEREISEN multi-factor AUTH tooJOIN apparaten**: instellen of gebruikers zijn vereiste tooprovide een verificatie met tweede factor toojoin hun apparaat tooAzure AD. Zie voor meer informatie over Azure multi-factor Authentication [aan de slag met Azure multi-factor Authentication in de cloud Hallo](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).
   * **GEBRUIKERS kunnen AZURE AD JOIN apparaten**: Hallo-gebruikers en groepen die zijn toegestaan toojoin apparaten tooAzure AD selecteren.
   * **EXTRA beheerders op AZURE AD met toegevoegde apparaten**: met Azure AD Premium of Enterprise Mobility Suite (EMS) hello, kunt u kiezen welke gebruikers lokale administrator-rechten zijn verleend toohello apparaat. Globale beheerders en eigenaren van de apparaten ontvangen standaard lokale beheerdersrechten.

<center>![Apparaatregistratie instellen](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center>

Nadat u Azure AD Join voor uw gebruikers instellen, kunnen ze verbinding maken met tooAzure AD via hun zakelijke of persoonlijke apparaten.

Hieronder volgen Hallo drie scenario's kunt u tooenable uw gebruikers tooset stellen Azure AD Join:

* Gebruikers lid worden van een apparaat in Bedrijfseigendom rechtstreeks tooAzure AD.
* Gebruikers domein een bedrijfseigen apparaten toohello on-premises Active Directory en vervolgens Hallo apparaat tooAzure AD uitbreiden.
* Gebruikers voegen werk of school tooWindows accounts op een persoonlijk apparaat

## <a name="additional-information"></a>Aanvullende informatie
* [Windows 10 voor Hallo ondernemingen: manieren toouse apparaten for work.](active-directory-azureadjoin-windows10-devices-overview.md)
* [Cloud-mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join uitbreiden](active-directory-azureadjoin-user-upgrade.md)
* [Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)
* [Verbinding maken met domein apparaten tooAzure AD voor Windows 10-ervaring](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD Join instellen](active-directory-azureadjoin-setup.md)

