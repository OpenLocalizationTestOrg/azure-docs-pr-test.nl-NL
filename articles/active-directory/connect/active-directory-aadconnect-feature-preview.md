---
title: 'Azure AD Connect: Functies in preview | Microsoft Docs'
description: Dit onderwerp wordt beschreven in meer detail-onderdelen in het voorbeeld in Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a>Meer informatie over functies in preview
Dit onderwerp wordt beschreven hoe toouse functies die momenteel in preview.

## <a name="group-writeback"></a>Groep terugschrijven
Hallo-optie voor write-back van groep in optionele functies kunt u toowriteback **Office 365-groepen** tooa forest met Exchange geïnstalleerd. Dit is een groep die altijd in de cloud Hallo is gemaakt. Als u Exchange lokale hebt, kunt klikt u vervolgens u schrijven terug deze groepen tooon-premises zodat gebruikers met een lokale Exchange-postvak kunnen verzenden en ontvangen van e-mailberichten van deze groepen.

Meer informatie over Office 365-groepen en hoe toouse ze kunnen worden gevonden [hier](http://aka.ms/O365g).

Een Office 365-groep wordt weergegeven als een distributiegroep op on-premises AD DS. Uw lokale Exchange-server moet zich op Exchange 2013 cumulatieve update 8 (uitgebracht in maart 2015) of Exchange 2016 toorecognize dit nieuwe groepstype.

**Opmerkingen bij de tijdens Hallo preview**

* Hallo-book mailadreskenmerk momenteel niet is ingevuld in Hallo preview. Hallo groep is niet zichtbaar in Hallo GAL zonder dit kenmerk. Hallo gemakkelijkste manier toopopulate dit kenmerk is toouse Hallo Exchange PowerShell-cmdlet `update-recipient`.
* Alleen-forests met Hallo Exchange schema zijn geldige doelen voor groepen. Er zijn geen Exchange is gedetecteerd, vervolgens is Write-back van groep niet als mogelijke tooenable.
* Alleen één forest Exchange organisatie implementaties worden momenteel ondersteund. Als u meer dan één Exchange organisatie lokale hebt, moet u een on-premises GALSync oplossing voor deze tooappear groepen in uw andere forests.
* beveiligingsgroepen of distributiegroepen verwerkt Hallo groep Write-back-functie niet.

> [!NOTE]
> Een abonnement tooAzure AD Premium is vereist voor write-back van groep.
> 
>

## <a name="user-writeback"></a>Write-back van gebruiker
> [!IMPORTANT]
> Hallo gebruiker terugschrijven preview-functie in was verwijderd Hallo augustus 2015 update tooAzure AD Connect. Als u deze hebt ingeschakeld, moet u deze functie uitschakelen.
>
>

## <a name="next-steps"></a>Volgende stappen
Blijven uw [aangepaste installatie van Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory ](active-directory-aadconnect.md).
