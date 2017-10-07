---
title: aaaCustomize pagina bent aangemeld in hello Azure Active Directory | Microsoft Docs
description: Meer informatie over hoe een bedrijf huisstijl toohello Azure aanmelden pagina tooadd
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
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a>Huisstijl tooyour aanmeldingspagina in hello Azure Active Directory toevoegen
tooavoid verwarring, willen veel bedrijven tooapply een consistent uiterlijk voor alle Hallo websites en services die ze beheren. Azure Active Directory biedt deze mogelijkheid doordat u toocustomize Hallo vormgeving van Hallo aanmeldingspagina met uw bedrijfslogo en kleurenschema toepassen. Hallo-aanmeldingspagina is Hallo-pagina waarop wordt weergegeven wanneer u zich aanmeldt tooOffice 365 of andere toepassingen op Internet die van Azure AD als id-provider gebruikmaken. U communiceren met deze pagina tooenter uw referenties.

Als u tooshow uw bedrijfsmerk en -kleuren en andere aanpasbare elementen op deze pagina wilt, Zie Hallo installatiekopieën toounderstand Hallo verschil tussen de twee ervaringen hello te volgen.

Hallo volgende schermafbeelding ziet en voorbeeld voor Hallo Office 365-aanmeldingspagina op een desktopcomputer **voordat** het aanpassen:

![De Office 365-aanmeldingspagina vóór het aanpassen](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

Hallo volgende schermafbeelding ziet en voorbeeld voor Hallo Office 365-aanmeldingspagina op een desktopcomputer **nadat** het aanpassen:

![De Office 365-aanmeldingspagina na het aanpassen](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a>Hallo-aanmeldingspagina aanpassen
Als u nodig hebt voor toegang op basis van een browser tooyour cloud-apps en services die uw organisatie op is geabonneerd, gebruikt u doorgaans de aanmeldingspagina Hallo.

Als u wijzigingen tooyour aanmeldingspagina hebt toegepast, kan het Hallo wijzigingen tooappear tooan uur duren.

Er wordt alleen een aanmeldingspagina met huisstijl weergegeven wanneer u een service opent met een tenantspecifieke URL, zoals https://outlook.com/**contoso**.com of https://mail.**contoso**.com.

Wanneer u een service gebruikt met niet-tenantspecifieke URL’s (bijvoorbeeld https://mail.office365.com), wordt er een aanmeldingspagina zonder huisstijl weergegeven. In dat geval wordt uw huisstijl weergegeven zodra u uw gebruikers-id hebt ingevoerd of een gebruikerstegel hebt geselecteerd.

> [!NOTE]
> * Uw domeinnaam moet worden weergegeven als 'Actief' in hello **domeinen** gedeelte van hello Azure portal waarin u de huisstijl hebt geconfigureerd. Zie voor meer informatie [toevoegen van aangepaste domeinnamen](active-directory-domains-add-azure-portal.md).
> * Aanmeldingspagina huisstijl niet meegenomen toohello consumenten zich op de pagina van Microsoft. Als u zich met een Microsoft-account aanmeldt, wordt er een reeks wordt door Azure AD gebruikerstegels met, maar Hallo huisstijl van uw organisatie aanmeldingspagina van Microsoft toohello niet van toepassing.
>
>

Op de aanmeldingspagina Hallo **aangemeld blijven** selectievakje kunt u een tooremain gebruiker is aangemeld wanneer ze sluiten en opnieuw hun browser openen.

   ![Aangemeld blijven](./media/active-directory-branding-custom-signon-azure-portal/01.png)

Dit heeft geen invloed op de levensduur van de sessie. U kunt Hallo selectievakje op Hallo Azure Active Directory-aanmeldingspagina verbergen.
Hiermee wordt aangegeven of Hallo selectievakje wordt weergegeven, hangt af van Hallo-instelling van **aangemeld uitgeschakeld blijven**.

   ![Aangemeld blijven](./media/active-directory-branding-custom-signon-azure-portal/02.png)

toohide Hallo selectievakje, configureer deze instelling te**Ja**.

> [!NOTE]
> Sommige functies van Office 2010 en SharePoint Online, is afhankelijk van gebruikers kunnen toocheck wordt dit selectievakje in. Als u deze instelling toohidden configureert, kunnen aanvullende en onverwachte prompts toosign in uw gebruikers te zien.
>
>

**tooadd bedrijf huisstijl tooyour map:**

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.
2. Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak Hallo en selecteer vervolgens **Enter**.

   ![Gebruikersbeheer openen](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. Op Hallo **gebruikers en groepen** blade Selecteer **bedrijf huisstijl**.
4. Op Hallo **gebruikers en groepen - bedrijf huisstijl** blade, selecteer Hallo **bewerken** opdracht.

    ![Aangepaste huisstijl bewerken](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Hallo-elementen die u wilt dat toocustomize wijzigen. Alle elementen zijn optioneel.
6. Klik op **Opslaan**.

Het kan tooan uur duren voor u de wijzigingen toohello aanmelden pagina huisstijl tooappear.

## <a name="next-steps"></a>Volgende stappen
[Taalspecifieke huisstijl toevoegen](active-directory-branding-localize-azure-portal.md)
