---
title: aaaDedicated groepen in Azure Active Directory | Microsoft Docs
description: Overzicht van hoe toegewezen groepen werken in Azure Active Directory en hoe ze worden gemaakt.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a>Toegewezen groepen in Azure Active Directory
In Azure Active Directory (Azure AD), Hallo toegewezen groepsfunctie automatisch maakt en vult lidmaatschap voor groepen van Azure AD zijn vooraf gedefinieerd. Leden van specifieke groepen kunnen niet worden toegevoegd of verwijderd met behulp van hello Azure classic portal Windows PowerShell-cmdlets of via een programma.

> [!NOTE]
> Toegewezen groepen moeten een Azure AD Premium-licentie is toegewezen aan
>
> * Hallo beheerder van Hallo-regel voor een groep
> * alle gebruikers die zijn geselecteerd door Hallo toobe lid van groep Hallo regel
>
>

**tooenable toegewezen groepen**

1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory**, en open vervolgens de directory van uw organisatie.
2. Selecteer Hallo **groepen** tabblad en open vervolgens Hallo groep die u tooedit.
3. Selecteer Hallo **configureren** tabblad en stel vervolgens **toegewezen groepen inschakelen** te**Ja**.

Zodra Hallo toegewezen groepen inschakelen switch te is ingesteld**Ja**, kunt u verder inschakelen Hallo directory tooautomatically Hallo alle gebruikers toegewezen groep maken door de instelling Hallo **inschakelen 'Alle gebruikers' groep** switch te**Ja**. Ook kunt u vervolgens bewerken Hallo-naam van deze groep toegewezen door deze te typen in Hallo **weergavenaam voor 'Alle gebruikers' groep** veld.

de groep alle gebruikers Hallo kan worden gebruikt tooassign Hallo dezelfde machtigingen tooall Hallo gebruikers in uw directory. U kunt bijvoorbeeld alle gebruikers in uw directory toegang tooa SaaS-toepassing door het toewijzen van toegang voor alle gebruikers gespecialiseerde groep toothis toepassing hello verlenen.

Hallo toegewezen alle gebruikers groep bevat alle gebruikers in de directory hello, inclusief gasten en externe gebruikers. Als u een groep moet op die externe gebruikers worden uitgesloten en u kunt dit doen door het maken van een groep met een kenmerk op basis van een dynamische regel zoals Hallo volgende:

                (user.userPrincipalName -notContains "#EXT#@")

Voor een groep die omvat niet alle gasten, moet u een regel zoals Hallo volgende gebruiken:

                (user.userType -ne "Guest")

toolearn over het toocreate *geavanceerde* regels (regels met meerdere vergelijkingen) voor dynamisch groepslidmaatschap, Zie [met behulp van kenmerken toocreate geavanceerde regels](active-directory-accessmanagement-groups-with-advanced-rules.md).

### <a name="next-steps"></a>Volgende stappen
Deze artikelen bevatten aanvullende informatie over Azure Active Directory.

* [Tooresources toegang beheren met Azure Active Directory-groepen](active-directory-manage-groups.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [What is Azure Active Directory?](active-directory-whatis.md) (Wat is Azure Active Directory?)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
