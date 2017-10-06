---
title: beleid voor voorwaardelijke toegang op basis van apparaten van aaaConfigure-Azure Active Directory | Microsoft Docs
description: Meer informatie over hoe tooconfigure Azure Active Directory op basis van apparaten voorwaardelijke toegangsbeleid.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a>Azure Active Directory-beleid voor voorwaardelijke toegang op basis van apparaten configureren

Met [voorwaardelijke toegang van Azure Active Directory (Azure AD)](active-directory-conditional-access-azure-portal.md), kunt u aanpassen hoe geautoriseerde gebruikers toegang uw resources tot hebben. Bijvoorbeeld, beperkt u het Hallo-toocertain resources tootrusted apparaten. Beleid voor voorwaardelijke toegang waarvoor een vertrouwd apparaat wordt ook wel beleid voor voorwaardelijke toegang op basis van apparaten.

Dit onderwerp vindt u informatie over hoe tooconfigure op basis van apparaten voorwaardelijke toegangsbeleid voor Azure AD-toepassingen. 


## <a name="before-you-begin"></a>Voordat u begint

Voorwaardelijke toegang op basis van apparaten ties **voorwaardelijke toegang van Azure AD** en **Azure AD-Apparaatbeheer samen**. Als u niet bekend met een van deze gebieden bent, maar moet u de volgende onderwerpen, eerst Hallo lezen:

- **[Voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-azure-portal.md)**  -dit onderwerp vindt u een conceptueel overzicht van voorwaardelijke toegang en verwante terminologie Hallo.

- **[Inleiding toodevice management in Azure Active Directory](device-management-introduction.md)**  -in dit onderwerp geeft een overzicht van Hallo verschillende opties er tooconnect apparaten met Azure AD. 


## <a name="trusted-devices"></a>Vertrouwde apparaten

Azure Active Directory kunnen in een wereld mobiel eerste, cloud eerste toodevices voor eenmalige aanmelding, apps en services vanaf elke locatie. Voor bepaalde bronnen in uw omgeving, het verlenen van toegang toohello juiste gebruikers mogelijk niet voldoende. Naast de juiste gebruikers toohello, u ook mogelijk een vertrouwd apparaat toobe tooaccess een resource die wordt gebruikt. In uw omgeving, kunt u definiëren wat een vertrouwd apparaat is gebaseerd op Hallo volgende onderdelen:

- Hallo [apparaatplatforms](active-directory-conditional-access-azure-portal.md#device-platforms) op een apparaat
- Hiermee wordt aangegeven of een apparaat is compatibel met
- Hiermee wordt aangegeven of een apparaat is lid van een domein 

Hallo [apparaatplatforms](active-directory-conditional-access-azure-portal.md#device-platforms) wordt gekenmerkt door Hallo-besturingssysteem dat wordt uitgevoerd op uw apparaat. In uw beleid voor voorwaardelijke toegang op basis van apparaten, kunt u access toocertain resources toospecific-apparaatplatforms beperken.



In een beleid voor voorwaardelijke toegang op basis van apparaten, kunt u de vertrouwde apparaten toobe gemarkeerd als compatibel vereisen.

![Cloud-apps](./media/active-directory-conditional-access-policy-connected-applications/24.png)

Apparaten kunnen worden gemarkeerd als compatibel zijn in de directory Hallo door:

- Intune 
- Een beheersysteem voor mobiele apparaten van derden dat kan worden geïntegreerd met Azure AD  

Alleen apparaten die verbonden tooAzure AD zijn kunnen worden gemarkeerd als compatibel. tooconnect een apparaat tooAzure Active Directory, hebt u Hallo volgende opties: 

- Azure AD geregistreerd
- Azure AD die lid zijn van
- Hybride die lid zijn van Azure AD

    ![Cloud-apps](./media/active-directory-conditional-access-policy-connected-applications/26.png)

Als u de voetafdruk van een lokale Active Directory (AD) hebt, kunt u apparaten die niet verbonden tooAzure AD maar lid tooyour AD toobe vertrouwd.

![Cloud-apps](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a>Volgende stappen

Voordat u configureert een beleid voor voorwaardelijke toegang op basis van apparaten in uw omgeving, moet u rekening houden bekijkt hello [best practices voor voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-best-practices.md).

