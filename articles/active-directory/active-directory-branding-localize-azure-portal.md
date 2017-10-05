---
title: De huisstijl specifieke taal zijn gebonden aan de aanmeldingspagina in Azure Active Directory toevoegen | Microsoft Docs
description: Informatie over het toevoegen van een specifieke taal-bedrijf huisstijl afbeeldingen en tekst naar een Azure-aanmeldingspagina
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a0310d6a-aaa7-4ea0-991d-6d3135b4382a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: e1fe8d855386ceec39edbc985538cdf32d78a13b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-language-specific-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a>De huisstijl specifieke taal zijn gebonden aan de aanmeldingspagina in Azure Active Directory toevoegen
Om verwarring te voorkomen, willen veel bedrijven een consistente look gebruiken voor alle websites en services die ze beheren. Azure Active Directory biedt deze mogelijkheid doordat u pas het uiterlijk van de aanmeldingspagina met uw bedrijfslogo en kleurenschema toepassen. De aanmeldingspagina is de pagina die wordt weergegeven wanneer u zich aanmeldt bij Office 365 of andere toepassingen op Internet die van Azure AD als id-provider gebruikmaken. U communiceert met deze pagina uw referenties in te voeren.

## <a name="customizing-the-sign-in-page-for-another-language"></a>De aanmeldingspagina voor een andere taal aanpassen
U kunt specifieke taal zijn gebonden elementen toevoegen aan uw aangepaste pagina aanmelden alleen als u een aangepaste aanmeldingspagina al hebt gemaakt zoals beschreven in [toevoegen aan uw aanmeldingspagina huisstijl van uw bedrijf](active-directory-branding-custom-signon-azure-portal.md). U kunt een aanmeldingspagina per directory configureren met een standaardset aanpasbare elementen. Nadat u de standaardset van pagina-elementen hebt geconfigureerd, kunt u meer versies voor verschillende talen. U kunt ook een combinatie van verschillende elementen gebruiken. U kunt bijvoorbeeld het volgende doen:

* Maken van een standaard **aanmelden pagina-afbeelding** dat werkt voor alle culturen en afzonderlijke versies maken voor de Engelse en Franse. Als u een browser op een van deze twee talen instelt, de taalspecifieke afbeelding wordt weergegeven, terwijl de standaardafbeelding voor alle andere talen weergegeven.
* Voor uw organisatie verschillende logo's configureren (bijvoorbeeld een Japanse en een Hebreeuwse versie).

We adviseren dat u het aantal variaties taal lage omwille van onderhoud en prestaties.

**Toevoegen aan uw directory huisstijl van uw bedrijf:**

1. Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.
2. Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak in en selecteer vervolgens **Enter**.

   ![Gebruikersbeheer openen](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. Op de **gebruikers en groepen** blade Selecteer **bedrijf huisstijl**.
4. Op de **gebruikers en groepen - bedrijf huisstijl** blade, selecteer de **taal toevoegen** opdracht.

    ![De huisstijl elementen taalspecifieke toevoegen](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. Wijzig de elementen die u wilt aanpassen. Alle elementen zijn optioneel.
6. Klik op **Opslaan**.

Dit kan een uur duren voor alle wijzigingen naar de pagina aanmeldingspagina met huisstijl weergegeven.

## <a name="next-steps"></a>Volgende stappen
[Huisstijl aan uw aanmeldingspagina toevoegen](active-directory-branding-custom-signon-azure-portal.md)
