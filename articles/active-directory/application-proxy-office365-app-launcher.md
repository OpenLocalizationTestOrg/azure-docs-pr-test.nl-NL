---
title: aaaSet een aangepaste startpagina van gepubliceerde apps met behulp van Azure AD-toepassingsproxy | Microsoft Docs
description: Bevat informatie over Hallo basisbeginselen van Azure AD-toepassingsproxy connectors
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a>Een aangepaste startpagina van gepubliceerde apps instellen via Azure AD-toepassingsproxy

Dit artikel wordt beschreven hoe tooconfigure apps toodirect gebruikers tooa aangepaste startpagina. Wanneer u een toepassing met toepassingsproxy publiceert, instellen van een interne URL maar soms die is geen Hallo pagina die uw gebruikers moeten eerst te zien. De startpagina van een aangepaste zo instellen dat uw gebruikers gaan toohello rechts pagina wanneer ze toegang krijgen Hallo apps van Azure Active Directory-Toegangsvenster Hallo of Hallo Office 365-app starten tot.

Wanneer gebruikers Hallo app openen, wordt ze omgeleid door standaard toohello hoofdmap domein-URL voor Hallo gepubliceerde app. Hallo-startpagina wordt meestal ingesteld als Hallo startpagina URL. Hello Azure AD PowerShell-module toodefine aangepaste startpagina URL gebruiken als u wilt dat de app gebruikers tooland op een bepaalde pagina in Hallo-app. 

Bijvoorbeeld:
- Binnen uw bedrijfsnetwerk gebruikers te gaan*https://ExpenseApp/login/login.aspx* toosign in en toegang tot uw app.
- Omdat u andere activa zoals installatiekopieën dat toepassingsproxy tooaccess op hoogste niveau van de mapstructuur Hallo Hallo nodig hebt, u Hallo-app met publiceert *https://ExpenseApp* zoals Hallo interne URL.
- externe URL is standaard Hallo *https://ExpenseApp-contoso.msappproxy.net*, die uw gebruikers toohello aanmelding wordt pas op de pagina.  
- Stel *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* als startpagina URL toogive Hallo uw gebruikers een naadloze ervaring. 

>[!NOTE]
>Wanneer u gebruikerstoegang toopublished apps geeft, Hallo apps worden weergegeven in Hallo [Azure AD-Toegangsvenster](active-directory-saas-access-panel-introduction.md) en Hallo [Office 365 app linksboven](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).

## <a name="before-you-start"></a>Voordat u begint

Voordat u de URL van de startpagina Hallo instellen, houd er rekening mee Hallo volgens de vereisten:

* Zorg ervoor dat u opgeeft Hallo-pad is een subdomein pad van Hallo basis domein-URL.

  Als Hallo hoofddomein URL, bijvoorbeeld https://apps.contoso.com/app1/, Hallo startpagina URL die u configureert moet beginnen met https://apps.contoso.com/app1/.

* Als u een wijziging aanbrengt toohello-app gepubliceerd, Hallo wijziging mogelijk Hallo-waarde van de URL van de startpagina Hallo ingesteld. Wanneer u in toekomstige Hallo Hallo app bijwerkt, moet u controleren en, indien nodig werkt u de URL van de homepage Hallo.

## <a name="change-hello-home-page-in-hello-azure-portal"></a>Hallo-startpagina in hello Azure-portal wijzigen

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) als beheerder.
2. Navigeer te**Azure Active Directory** > **App registraties** en kiest u uw toepassing uit Hallo-lijst. 
3. Selecteer **eigenschappen** uit Hallo-instellingen.
4. Update Hallo **startpagina URL** veld met het nieuwe pad. 

   ![Nieuwe startpagina-URL opgeven](./media/application-proxy-office365-app-launcher/homepage.png)

5. Selecteer **opslaan**

## <a name="change-hello-home-page-with-powershell"></a>Hallo-startpagina met PowerShell wijzigen

### <a name="install-hello-azure-ad-powershell-module"></a>Hello Azure AD PowerShell-module installeren

Voordat u een aangepaste startpagina URL definiëren met behulp van PowerShell, installeer hello Azure AD PowerShell-module. U kunt Hallo pakket downloaden van Hallo [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), die gebruikt Hallo Graph API-eindpunt. 

tooinstall Hallo van het pakket, als volgt te werk:

1. Open een standaard PowerShell-venster en voer vervolgens Hallo volgende opdracht:

    ```
     Install-Module -Name AzureAD
    ```
    Als u Hallo-opdracht als een niet-beheerders uitvoert, gebruikt u Hallo `-scope currentuser` optie.
2. Selecteer tijdens de installatie Hallo **Y** tooinstall twee pakketten van Nuget.org. Beide pakketten zijn vereist. 

### <a name="find-hello-objectid-of-hello-app"></a>Hallo ObjectID van Hallo app zoeken

Hallo ObjectID van Hallo app verkrijgen en zoek vervolgens naar Hallo app door de startpagina.

1. Open PowerShell en hello Azure AD-module importeren.

    ```
    Import-Module AzureAD
    ```

2. Aanmelden toohello Azure AD-module als Hallo tenantbeheerder.

    ```
    Connect-AzureAD
    ```
3. Hallo-app op basis van de URL van de startpagina te zoeken. U vindt Hallo-URL in het Hallo-portal door te gaan**Azure Active Directory** > **bedrijfstoepassingen** > **alle toepassingen**. In dit voorbeeld wordt *sharepoint iddemo*.

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. Deze krijgt u een resultaat dat vergelijkbare toohello een hier weergegeven. Hallo ObjectID GUID toouse in de volgende sectie Hallo kopiëren.

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a>Hallo startpagina URL voor bijwerken

Dezelfde PowerShell-module die u hebt gebruikt voor stap 1: Voer in Hallo Hallo stappen te volgen:

1. Bevestigen dat u Hallo app corrigeren en vervang *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* Hello ObjectID die u in de voorgaande stap Hallo gekopieerd.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 Nu u Hallo app hebt bevestigd, bent u klaar tooupdate Hallo-startpagina, als volgt.

2. Maak een lege toepassing object toohold Hallo wijzigingen die u toomake wilt. Deze variabele bevat Hallo-waarden die u wilt dat tooupdate. Er is niets wordt in deze stap gemaakt.

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. Hallo startpagina URL toohello waarde die u wilt instellen. Hallo-waarde moet een pad van het subdomein van Hallo gepubliceerde app. Bijvoorbeeld, als u wijzigt de URL van de startpagina van Hallo *https://sharepoint-iddemo.msappproxy.net/* te*https://sharepoint-iddemo.msappproxy.net/hybrid/*, app-gebruikers gaan rechtstreeks toohello aangepast startpagina.

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. Zorg Hallo update met behulp van Hallo GUID (object-id) die u hebt genoteerd in ' stap 1: zoeken Hallo ObjectID van app Hallo. "

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. tooconfirm hello wijziging is geslaagd, opnieuw opstarten Hallo-app.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
>Eventuele wijzigingen die u toohello app mogelijk opnieuw ingesteld Hallo startpagina URL. Als de URL van uw startpagina wordt opnieuw ingesteld, herhaalt u stap 2.

## <a name="next-steps"></a>Volgende stappen

- [Externe toegang tooSharePoint met Azure AD-toepassingsproxy inschakelen](application-proxy-enable-remote-access-sharepoint.md)
- [Toepassingsproxy inschakelen in hello Azure-portal](active-directory-application-proxy-enable.md)
