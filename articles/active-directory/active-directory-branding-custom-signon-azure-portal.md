---
title: Aanpassen van de aanmeldingspagina in Azure Active Directory | Microsoft Docs
description: Informatie over het toevoegen van een huisstijl naar de Azure-aanmeldingspagina
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 27590c018ea55e9793246c7a4cab10f934ea502b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a>Huisstijl aan uw pagina aanmelden in de Azure Active Directory toevoegen
Om verwarring te voorkomen, willen veel bedrijven een consistente look gebruiken voor alle websites en services die ze beheren. Azure Active Directory biedt deze mogelijkheid doordat u pas het uiterlijk van de aanmeldingspagina met uw bedrijfslogo en kleurenschema toepassen. De aanmeldingspagina is de pagina die wordt weergegeven wanneer u zich aanmeldt bij Office 365 of andere toepassingen op Internet die van Azure AD als id-provider gebruikmaken. U communiceert met deze pagina uw referenties in te voeren.

Als u op deze pagina uw bedrijfsmerk en -kleuren en andere aanpasbare elementen wilt weergeven, bekijkt u de volgende afbeeldingen om inzicht te krijgen in het verschil tussen de twee ervaringen.

In de volgende schermafbeelding ziet u een voorbeeld van de Office 365-aanmeldingspagina op een desktopcomputer **vóór** het aanpassen:

![De Office 365-aanmeldingspagina vóór het aanpassen](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

In de volgende schermafbeelding ziet u een voorbeeld van de Office 365-aanmeldingspagina op een desktopcomputer **na** het aanpassen:

![De Office 365-aanmeldingspagina na het aanpassen](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-the-sign-in-page"></a>De aanmeldingspagina aanpassen
Als u browsertoegang nodig hebt om de cloud-apps en -services te openen waar uw organisatie op is geabonneerd, gebruikt u de aanmeldingspagina.

Als u wijzigingen hebt aangebracht aan uw aanmeldingspagina, kan het een uur duren voordat de wijzigingen worden weergegeven.

Er wordt alleen een aanmeldingspagina met huisstijl weergegeven wanneer u een service opent met een tenantspecifieke URL, zoals https://outlook.com/**contoso**.com of https://mail.**contoso**.com.

Wanneer u een service gebruikt met niet-tenantspecifieke URL’s (bijvoorbeeld https://mail.office365.com), wordt er een aanmeldingspagina zonder huisstijl weergegeven. In dat geval wordt uw huisstijl weergegeven zodra u uw gebruikers-id hebt ingevoerd of een gebruikerstegel hebt geselecteerd.

> [!NOTE]
> * Uw domeinnaam moet worden weergegeven als 'Actief' de **domeinen** gedeelte van de Azure portal waarin u de huisstijl hebt geconfigureerd. Zie voor meer informatie [toevoegen van aangepaste domeinnamen](active-directory-domains-add-azure-portal.md).
> * De huisstijl van de aanmeldingspagina wordt niet meegenomen naar de Microsoft-aanmeldingspagina voor klanten. Als u zich met een Microsoft-account aanmeldt, wordt er een reeks wordt door Azure AD gebruikerstegels met, maar de huisstijl van uw organisatie niet van toepassing op de Microsoft-account aanmeldingspagina.
>
>

Op de aanmeldingspagina kunnen gebruikers er met het selectievakje **Aangemeld blijven** voor zorgen dat ze aangemeld blijven als ze hun browser sluiten en opnieuw openen.

   ![Aangemeld blijven](./media/active-directory-branding-custom-signon-azure-portal/01.png)

Dit heeft geen invloed op de levensduur van de sessie. U kunt het selectievakje op de aanmeldingspagina van Azure Active Directory verbergen.
Hiermee wordt aangegeven of het selectievakje wordt weergegeven, hangt af van de instelling van **aangemeld uitgeschakeld blijven**.

   ![Aangemeld blijven](./media/active-directory-branding-custom-signon-azure-portal/02.png)

Als u wilt het selectievakje verbergen, configureert u deze instelling om te **Ja**.

> [!NOTE]
> Of sommige functies van SharePoint Online en Office 2010 beschikbaar zijn, hangt ervan of gebruikers dit selectievakje wel of niet kunnen inschakelen. Als u deze instelling instelt op Verborgen, krijgen uw gebruikers mogelijk extra en onverwachte prompts te zien om zich aan te melden.
>
>

**Toevoegen aan uw directory huisstijl van uw bedrijf:**

1. Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.
2. Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak in en selecteer vervolgens **Enter**.

   ![Gebruikersbeheer openen](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. Op de **gebruikers en groepen** blade Selecteer **bedrijf huisstijl**.
4. Op de **gebruikers en groepen - bedrijf huisstijl** blade, selecteer de **bewerken** opdracht.

    ![Aangepaste huisstijl bewerken](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Wijzig de elementen die u wilt aanpassen. Alle elementen zijn optioneel.
6. Klik op **Opslaan**.

Dit kan een uur duren voor alle wijzigingen naar de pagina aanmeldingspagina met huisstijl weergegeven.

## <a name="next-steps"></a>Volgende stappen
[Taalspecifieke huisstijl toevoegen](active-directory-branding-localize-azure-portal.md)
