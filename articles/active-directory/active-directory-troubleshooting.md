---
title: 'Problemen oplossen: ''Active Directory'' item is ontbreekt of is niet beschikbaar | Microsoft Docs'
description: Welke toodo wanneer Active Directory-menu-item wordt niet in hello Azure Management Portal weergegeven.
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a>Problemen oplossen: 'Active Directory' item is ontbreekt of is niet beschikbaar
Veel van Hallo instructies voor het gebruik van Azure Active Directory-functies en services beginnen met ' Ga toohello Azure Management Portal en klik op **Active Directory**. " Wat doet u als Hallo Active Directory-extensie of menu-item niet weergegeven of als deze is gemarkeerd, maar **niet beschikbaar**? Dit onderwerp is ontworpen toohelp. Beschrijft Hallo omstandigheden waaronder **Active Directory** niet wordt weergegeven of is niet beschikbaar en wordt uitgelegd hoe tooproceed.

## <a name="active-directory-is-missing"></a>Active Directory ontbreekt
Normaal gesproken een **Active Directory** item wordt weergegeven in het linkerdeelvenster navigatiemenu Hallo. Hallo-instructies in Azure Active Directory-procedures wordt ervan uitgegaan dat dit item in de weergave.

![Schermopname: Active Directory in Azure](./media/active-directory-troubleshooting/typical-view.png)

Hallo Active Directory-item wordt weergegeven in het linkerdeelvenster navigatiemenu Hallo wanneer elk Hallo volgende voorwaarden is waar. Anders weergegeven Hallo item niet.

* Hallo huidige gebruiker is aangemeld met een Microsoft-account (voorheen bekend als een Windows Live ID).
  
    OF
* Hello Azure-tenant heeft een map en Hallo huidige account is een directory-beheerder.
  
    OF
* Hello Azure-tenant heeft ten minste één Azure AD Access Control (ACS)-naamruimte. Zie voor meer informatie [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).
  
    OF
* Hello Azure-tenant heeft ten minste één Azure multi-factor Authentication-provider. Zie voor meer informatie [Azure multi-factor Authentication-Providers beheren](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

toocreate Access Control-naamruimte of een multi-Factor Authentication-provider, klikt u op **+ nieuw** > **App Services** > **Active Directory**.

tooget beheerdersrechten tooa directory, hebben een beheerder een beheerder rol tooyour account toewijzen. Zie voor meer informatie [beheerdersrollen toewijzen](active-directory-assign-admin-roles.md).

## <a name="active-directory-is-not-available"></a>Active Directory is niet beschikbaar
Wanneer u klikt op **+ nieuw** > **App Services**, een **Active Directory** item wordt weergegeven. Hallo Active Directory-item wordt weergegeven in het bijzonder voor wanneer Hallo Active Directory-functies, zoals Directory, Access Control of multi-factor Authentication-Provider, de huidige gebruiker toohello beschikbaar zijn.

Echter tijdens het laden van pagina hello, Hallo item grijs wordt weergegeven en is gemarkeerd als **niet beschikbaar**. Dit is een tijdelijke status. Als u een paar seconden wachten, beschikbaar Hallo item. Als Hallo vertraging wordt verlengd, vernieuwen Hallo webpagina vaak probleem wordt opgelost Hallo.

![Schermopname: Active Directory is niet beschikbaar](./media/active-directory-troubleshooting/not-available.png)

