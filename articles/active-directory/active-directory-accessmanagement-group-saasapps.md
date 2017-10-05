---
title: Toegang tot SaaS-toepassingen beheren met behulp van een groep | Microsoft Docs
description: "Het gebruik van groepen in Azure Active Directory Premium of Basic toewijzen van toegang tot SaaS-toepassingen die zijn geïntegreerd met Azure Active Directory."
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
ms.openlocfilehash: d350011ee9fc5ced9ddb16993f68d3c840a645a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a>Een groep gebruiken om SaaS-toepassingen te beheren
Met Azure Active Directory (Azure AD) met een licentie voor Azure AD Premium of Azure AD Basic, kunt u groepen gebruiken voor het toewijzen van toegang tot een SaaS-toepassing die geïntegreerd met Azure AD. Bijvoorbeeld, als u toegang toewijzen voor de marketingafdeling vijf verschillende SaaS-toepassingen gebruiken wilt, kunt u een groep met de gebruikers van de marketingafdeling maken en vervolgens die groep toewijzen aan deze vijf SaaS-toepassingen die nodig zijn voor de marketingafdeling. Op deze manier kunt u tijd besparen door het lidmaatschap van de marketingafdeling op één plek beheren. Gebruikers zijn vervolgens toegewezen aan de toepassing wanneer ze zijn toegevoegd als leden van de groep marketing en hun toewijzingen verwijderd uit de toepassing wanneer ze zijn verwijderd uit de groep marketing.

> [!IMPORTANT]
> Microsoft raadt u aan Azure AD te beheren met het [Azure AD-beheercentrum](https://aad.portal.azure.com) in Azure Portal in plaats van de klassieke Azure portal waarnaar in dit artikel wordt verwezen. 

Deze mogelijkheid kan worden gebruikt met honderden toepassingen die u uit binnen de Azure AD-Toepassingsgalerie kunt toevoegen.

**Toegang voor een groep toewijzen aan een SaaS-toepassing**

1. In de [klassieke Azure-portal](https://manage.windowsazure.com), selecteer **Active Directory** op de navigatiebalk aan de linkerkant.
2. Selecteer de **Directory** tabblad en open vervolgens de directory waarin u wilt toegang voor een groep toewijzen aan een SaaS-toepassing.
3. Selecteer de **toepassingen** tabblad. Selecteer een toepassing die u hebt toegevoegd uit de galerie met toepassingen en klik vervolgens op de **gebruikers en groepen** tabblad.
4. Op de **gebruikers en groepen** tabblad, in de **vanaf** veld, voer de naam van de groep waartoe u toegang wilt toewijzen en selecteer vervolgens het vinkje in de rechterbovenhoek. U hoeft alleen te typen van het eerste deel van naam van de groep.
5. Selecteer de groep en vervolgens klikt u vervolgens de **toegang toewijzen** knop. Selecteer **Ja** ziet wanneer u het bevestigingsbericht. Op dit moment wordt genest groepslidmaatschap niet ondersteund voor toewijzing aan een toepassing op basis van een groep.
6. Ook kunt u zien welke gebruikers zijn toegewezen aan de toepassing, rechtstreeks of door het lidmaatschap in een groep. Om dit te doen, wijzig de **vervolgkeuzelijst weergeven uit 'Groepen'** naar **'Alle gebruikers'**. De lijst staan gebruikers in de map en of elke gebruiker is toegewezen aan de toepassing. In de lijst staan ook of de toegewezen gebruikers zijn toegewezen aan rechtstreeks de toepassing (toewijzingstype weergegeven als 'Direct'), of doordat groepslidmaatschap (toewijzingstype weergegeven als 'Overgenomen'.)

> [!NOTE]
> Nadat u Azure AD Premium of Azure AD Basic hebt ingeschakeld, kunt u het tabblad gebruikers en groepen zien.
>
>

### <a name="next-steps"></a>Volgende stappen
Deze artikelen bevatten aanvullende informatie over Azure Active Directory.

* [Managing access to resources with Azure Active Directory groups](active-directory-manage-groups.md) (Toegang tot resources beheren met Azure Active Directory-groepen)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [Azure Active Directory cmdlets for configuring group settings](active-directory-accessmanagement-groups-settings-cmdlets.md) (Azure Active Directory-cmdlets voor het configureren van groepsinstellingen)
* [Wat is Azure Active Directory?](active-directory-whatis.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
