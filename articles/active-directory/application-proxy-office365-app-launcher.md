---
title: Een aangepaste startpagina van gepubliceerde apps instellen via Azure AD-toepassingsproxy | Microsoft Docs
description: Bevat informatie over de basisbeginselen van Azure AD-toepassingsproxy connectors
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
ms.openlocfilehash: 9069166259265f5d2b43043b75039e239f397f6c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a>Een aangepaste startpagina van gepubliceerde apps instellen via Azure AD-toepassingsproxy

In dit artikel wordt beschreven hoe gebruikers verwijzen naar de startpagina van een aangepaste apps configureren. Wanneer u een toepassing met toepassingsproxy publiceert, kunt u een interne URL maar soms die niet de pagina die uw gebruikers moeten eerst zien instellen. De startpagina van een aangepaste zo instellen dat uw gebruikers gaat u naar de juiste pagina wanneer ze toegang krijgen de apps van het toegangsvenster Azure Active Directory of het startprogramma voor Office 365-app tot.

Wanneer gebruikers de app openen, wordt ze omgeleid naar de hoofdmap domein-URL voor de gepubliceerde app standaard. De startpagina is standaard ingesteld als de URL van de startpagina. Gebruik de Azure AD PowerShell-module voor het definiëren van aangepaste startpagina URL's wanneer u wilt dat gebruikers van de app op een bepaalde pagina in de app. 

Bijvoorbeeld:
- Binnen uw bedrijfsnetwerk gebruikers gaat u naar *https://ExpenseApp/login/login.aspx* aanmelden en toegang tot uw app.
- Aangezien u andere activa zoals afbeeldingen die Application Proxy nodig heeft voor toegang tot op het hoogste niveau van de mapstructuur hebt, kunt u de app met publiceren *https://ExpenseApp* als de interne URL.
- De externe URL van de standaardwaarde is *https://ExpenseApp-contoso.msappproxy.net*, die uw gebruikers de aanmelding wordt pas op de pagina.  
- Stel *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* als de URL van de startpagina om uw gebruikers een naadloze ervaring. 

>[!NOTE]
>Wanneer u gebruikers toegang tot gepubliceerde apps geven, de apps worden weergegeven in de [Azure AD-Toegangsvenster](active-directory-saas-access-panel-introduction.md) en de [Office 365 app linksboven](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).

## <a name="before-you-start"></a>Voordat u begint

Voordat u de URL van de startpagina instellen, houd de volgende vereisten:

* Zorg ervoor dat het opgegeven pad een subdomein-pad voor de hoofd-domein-URL is.

  Als de URL hoofddomein is, bijvoorbeeld https://apps.contoso.com/app1/, de startpagina-URL die u configureert moet beginnen met https://apps.contoso.com/app1/.

* Als u een wijziging in de gepubliceerde app aanbrengt, kan de wijziging van de waarde van de URL van de opnieuw. Wanneer u de app in de toekomst bijwerkt, moet u controleren en, indien nodig werkt u de URL van de startpagina.

## <a name="change-the-home-page-in-the-azure-portal"></a>Wijzigen van de startpagina in de Azure portal

1. Meld u als beheerder aan bij [Azure Portal](https://portal.azure.com).
2. Navigeer naar **Azure Active Directory** > **App registraties** en kiest u uw toepassing in de lijst. 
3. Selecteer **eigenschappen** uit de instellingen.
4. Update de **startpagina URL** veld met het nieuwe pad. 

   ![Nieuwe startpagina-URL opgeven](./media/application-proxy-office365-app-launcher/homepage.png)

5. Selecteer **opslaan**

## <a name="change-the-home-page-with-powershell"></a>Wijzigen van de startpagina met PowerShell

### <a name="install-the-azure-ad-powershell-module"></a>Installeer de Azure AD PowerShell-module

Voordat u een aangepaste startpagina URL definiëren met behulp van PowerShell, moet u de Azure AD PowerShell-module installeren. U kunt het downloaden van de [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), waarbij het Graph API-eindpunt wordt gebruikt. 

Volg deze stappen voor het installeren van het pakket:

1. Open een standaard PowerShell-venster en voer vervolgens de volgende opdracht:

    ```
     Install-Module -Name AzureAD
    ```
    Als u de opdracht als een niet-beheerders uitvoert, gebruikt u de `-scope currentuser` optie.
2. Tijdens de installatie selecteert **Y** twee pakketten installeren via Nuget.org. Beide pakketten zijn vereist. 

### <a name="find-the-objectid-of-the-app"></a>De object-id van de app zoeken

De object-id van de app verkrijgen en zoek vervolgens naar de app door de startpagina.

1. Open PowerShell en de Azure AD-module importeren.

    ```
    Import-Module AzureAD
    ```

2. Meld u aan de Azure AD-module als de tenantbeheerder.

    ```
    Connect-AzureAD
    ```
3. De app op basis van de URL van de startpagina te zoeken. U vindt de URL in de portal door te gaan naar **Azure Active Directory** > **bedrijfstoepassingen** > **alle toepassingen**. In dit voorbeeld wordt *sharepoint iddemo*.

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. Deze krijgt u een resultaat die vergelijkbaar is met hieronder wordt weergegeven. Kopieer de ObjectID GUID moet worden gebruikt in de volgende sectie.

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-the-home-page-url"></a>De URL van de startpagina bijwerken

In dezelfde PowerShell-module die u hebt gebruikt voor stap 1, moet u de volgende stappen uitvoeren:

1. Bevestigen dat u de juiste app hebt en vervang *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* met de object-id die u in de vorige stap hebt gekopieerd.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 Nu dat u de app hebt bevestigd, kunt u als volgt bijwerken van de startpagina.

2. Maak een lege application-object voor het opslaan van de wijzigingen die u wilt maken. Deze variabele bevat de waarden die u wilt bijwerken. Er is niets wordt in deze stap gemaakt.

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. De URL voor de startpagina in de waarde die u wilt instellen. De waarde moet een pad van het subdomein van de gepubliceerde app. Bijvoorbeeld, als u de URL van de startpagina van wijzigen *https://sharepoint-iddemo.msappproxy.net/* naar *https://sharepoint-iddemo.msappproxy.net/hybrid/*, app-gebruikers rechtstreeks naar de aangepaste startpagina gaan.

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. Bij te werken met behulp van de GUID (object-id) die u hebt genoteerd in ' stap 1: de object-id van de app te vinden. '

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. Om te bevestigen dat de wijziging voltooid is, start u de app opnieuw.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
>Alle wijzigingen die u in de app aanbrengt mogelijk opnieuw instellen van de URL van de startpagina. Als de URL van uw startpagina wordt opnieuw ingesteld, herhaalt u stap 2.

## <a name="next-steps"></a>Volgende stappen

- [Externe toegang voor SharePoint met Azure AD-toepassingsproxy inschakelen](application-proxy-enable-remote-access-sharepoint.md)
- [Toepassingsproxy inschakelen in de Azure-portal](active-directory-application-proxy-enable.md)
