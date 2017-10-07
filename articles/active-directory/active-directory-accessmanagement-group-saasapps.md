---
title: een groep toomanage toegang tooSaaS toepassingen aaaUsing | Microsoft Docs
description: "Hoe toouse groepen in Azure Active Directory Premium of Basic tooassign toegang krijgen tot tooSaaS toepassingen die zijn geïntegreerd met Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a>Met behulp van een groep toomanage access tooSaaS-toepassingen
Met Azure Active Directory (Azure AD) met een licentie voor Azure AD Premium of Azure AD Basic, kunt u groepen tooassign toegang tooa SaaS-toepassing die geïntegreerd met Azure AD. Bijvoorbeeld, als u toegang tooassign voor Hallo marketing afdeling toouse vijf verschillende SaaS-toepassingen wilt, kunt u een groep met gebruikers in de marketingafdeling Hallo Hallo maken en wijs die groep toothese vijf SaaS-toepassingen die zijn door de marketingafdeling Hallo nodig. Op deze manier kunt u tijd besparen door Hallo lidmaatschap van Hallo marketing afdeling op één plek beheren. Gebruikers worden vervolgens toegewezen toohello toepassing wanneer ze zijn toegevoegd als leden van marketing groep Hallo en hun toewijzingen verwijderd van de toepassing hello wanneer ze zijn verwijderd uit de groep marketing Hallo.

> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel. 

Deze mogelijkheid kan worden gebruikt met honderden toepassingen die u uit binnen hello Azure AD-Toepassingsgalerie kunt toevoegen.

**tooassign toegang voor een groep tooa SaaS-toepassing**

1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory** op Hallo navigatiebalk aan de linkerzijde Hallo.
2. Selecteer Hallo **Directory** tabblad en open vervolgens Hallo map waarin u tooassign toegang voor een groep tooa SaaS-toepassing.
3. Selecteer Hallo **toepassingen** tabblad. Selecteer een toepassing die u vanuit het Hallo-Toepassingsgalerie hebt toegevoegd en klik vervolgens op Hallo **gebruikers en groepen** tabblad.
4. Op Hallo **gebruikers en groepen** tabblad in Hallo **vanaf** Hallo naam Hallo groep toowhich dat u wilt dat tooassign toegang en vervolgens selecteert vinkje in de rechterbovenhoek Hallo Hallo. U hoeft alleen tootype Hallo eerste deel van naam van de groep.
5. Hallo groep selecteert en vervolgens klikt u vervolgens Hallo **toegang toewijzen** knop. Selecteer **Ja** wanneer er Hallo bevestigingsbericht. Genest groepslidmaatschap worden niet ondersteund voor toewijzing op basis van een groep tooapplications op dit moment.
6. Ook kunt u zien welke gebruikers toohello toepassing, zijn toegewezen, rechtstreeks of door het lidmaatschap in een groep. toodo deze, Hallo wijziging **vervolgkeuzelijst weergeven uit 'Groepen'** te**'Alle gebruikers'**. Hallo-lijst bevat de gebruikers in Hallo directory en of elke gebruiker is toegewezen toohello toepassing. Hallo-lijst bevat ook Hallo toegewezen gebruikers toohello toepassing rechtstreeks (toewijzingstype weergegeven als 'Direct') worden toegewezen, of doordat groepslidmaatschap (toewijzingstype weergegeven als 'Overgenomen'.)

> [!NOTE]
> U ziet Hallo gebruikers en groepen tabblad pas nadat u Azure AD Premium of Azure AD Basic hebt ingeschakeld.
>
>

### <a name="next-steps"></a>Volgende stappen
Deze artikelen bevatten aanvullende informatie over Azure Active Directory.

* [Tooresources toegang beheren met Azure Active Directory-groepen](active-directory-manage-groups.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [Azure Active Directory cmdlets for configuring group settings](active-directory-accessmanagement-groups-settings-cmdlets.md) (Azure Active Directory-cmdlets voor het configureren van groepsinstellingen)
* [Wat is Azure Active Directory?](active-directory-whatis.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
