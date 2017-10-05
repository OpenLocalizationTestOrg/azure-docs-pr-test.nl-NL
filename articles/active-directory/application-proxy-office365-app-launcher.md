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
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="2791f-103">Een aangepaste startpagina van gepubliceerde apps instellen via Azure AD-toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="2791f-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="2791f-104">In dit artikel wordt beschreven hoe gebruikers verwijzen naar de startpagina van een aangepaste apps configureren.</span><span class="sxs-lookup"><span data-stu-id="2791f-104">This article discusses how to configure apps to direct users to a custom home page.</span></span> <span data-ttu-id="2791f-105">Wanneer u een toepassing met toepassingsproxy publiceert, kunt u een interne URL maar soms die niet de pagina die uw gebruikers moeten eerst zien instellen.</span><span class="sxs-lookup"><span data-stu-id="2791f-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not the page your users should see first.</span></span> <span data-ttu-id="2791f-106">De startpagina van een aangepaste zo instellen dat uw gebruikers gaat u naar de juiste pagina wanneer ze toegang krijgen de apps van het toegangsvenster Azure Active Directory of het startprogramma voor Office 365-app tot.</span><span class="sxs-lookup"><span data-stu-id="2791f-106">Set a custom home page so that your users go to the right page when they access the apps from the Azure Active Directory Access Panel or the Office 365 app launcher.</span></span>

<span data-ttu-id="2791f-107">Wanneer gebruikers de app openen, wordt ze omgeleid naar de hoofdmap domein-URL voor de gepubliceerde app standaard.</span><span class="sxs-lookup"><span data-stu-id="2791f-107">When users launch the app, they're directed by default to the root domain URL for the published app.</span></span> <span data-ttu-id="2791f-108">De startpagina is standaard ingesteld als de URL van de startpagina.</span><span class="sxs-lookup"><span data-stu-id="2791f-108">The landing page is typically set as the home page URL.</span></span> <span data-ttu-id="2791f-109">Gebruik de Azure AD PowerShell-module voor het definiëren van aangepaste startpagina URL's wanneer u wilt dat gebruikers van de app op een bepaalde pagina in de app.</span><span class="sxs-lookup"><span data-stu-id="2791f-109">Use the Azure AD PowerShell module to define custom home page URLs when you want app users to land on a specific page within the app.</span></span> 

<span data-ttu-id="2791f-110">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2791f-110">For example:</span></span>
- <span data-ttu-id="2791f-111">Binnen uw bedrijfsnetwerk gebruikers gaat u naar *https://ExpenseApp/login/login.aspx* aanmelden en toegang tot uw app.</span><span class="sxs-lookup"><span data-stu-id="2791f-111">Inside your corporate network, users go to *https://ExpenseApp/login/login.aspx* to sign in and access your app.</span></span>
- <span data-ttu-id="2791f-112">Aangezien u andere activa zoals afbeeldingen die Application Proxy nodig heeft voor toegang tot op het hoogste niveau van de mapstructuur hebt, kunt u de app met publiceren *https://ExpenseApp* als de interne URL.</span><span class="sxs-lookup"><span data-stu-id="2791f-112">Because you have other assets like images that Application Proxy needs to access at the top level of the folder structure, you publish the app with *https://ExpenseApp* as the internal URL.</span></span>
- <span data-ttu-id="2791f-113">De externe URL van de standaardwaarde is *https://ExpenseApp-contoso.msappproxy.net*, die uw gebruikers de aanmelding wordt pas op de pagina.</span><span class="sxs-lookup"><span data-stu-id="2791f-113">The default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users to the sign in page.</span></span>  
- <span data-ttu-id="2791f-114">Stel *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* als de URL van de startpagina om uw gebruikers een naadloze ervaring.</span><span class="sxs-lookup"><span data-stu-id="2791f-114">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as the home page URL to give your users a seamless experience.</span></span> 

>[!NOTE]
><span data-ttu-id="2791f-115">Wanneer u gebruikers toegang tot gepubliceerde apps geven, de apps worden weergegeven in de [Azure AD-Toegangsvenster](active-directory-saas-access-panel-introduction.md) en de [Office 365 app linksboven](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span><span class="sxs-lookup"><span data-stu-id="2791f-115">When you give users access to published apps, the apps are displayed in the [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and the [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="2791f-116">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="2791f-116">Before you start</span></span>

<span data-ttu-id="2791f-117">Voordat u de URL van de startpagina instellen, houd de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="2791f-117">Before you set the home page URL, keep in mind the following requirements:</span></span>

* <span data-ttu-id="2791f-118">Zorg ervoor dat het opgegeven pad een subdomein-pad voor de hoofd-domein-URL is.</span><span class="sxs-lookup"><span data-stu-id="2791f-118">Ensure that the path you specify is a subdomain path of the root domain URL.</span></span>

  <span data-ttu-id="2791f-119">Als de URL hoofddomein is, bijvoorbeeld https://apps.contoso.com/app1/, de startpagina-URL die u configureert moet beginnen met https://apps.contoso.com/app1/.</span><span class="sxs-lookup"><span data-stu-id="2791f-119">If the root-domain URL is, for example, https://apps.contoso.com/app1/, the home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="2791f-120">Als u een wijziging in de gepubliceerde app aanbrengt, kan de wijziging van de waarde van de URL van de opnieuw.</span><span class="sxs-lookup"><span data-stu-id="2791f-120">If you make a change to the published app, the change might reset the value of the home page URL.</span></span> <span data-ttu-id="2791f-121">Wanneer u de app in de toekomst bijwerkt, moet u controleren en, indien nodig werkt u de URL van de startpagina.</span><span class="sxs-lookup"><span data-stu-id="2791f-121">When you update the app in the future, you should recheck and, if necessary, update the home page URL.</span></span>

## <a name="change-the-home-page-in-the-azure-portal"></a><span data-ttu-id="2791f-122">Wijzigen van de startpagina in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="2791f-122">Change the home page in the Azure portal</span></span>

1. <span data-ttu-id="2791f-123">Meld u als beheerder aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2791f-123">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="2791f-124">Navigeer naar **Azure Active Directory** > **App registraties** en kiest u uw toepassing in de lijst.</span><span class="sxs-lookup"><span data-stu-id="2791f-124">Navigate to **Azure Active Directory** > **App registrations** and choose your application from the list.</span></span> 
3. <span data-ttu-id="2791f-125">Selecteer **eigenschappen** uit de instellingen.</span><span class="sxs-lookup"><span data-stu-id="2791f-125">Select **Properties** from the settings.</span></span>
4. <span data-ttu-id="2791f-126">Update de **startpagina URL** veld met het nieuwe pad.</span><span class="sxs-lookup"><span data-stu-id="2791f-126">Update the **Home page URL** field with your new path.</span></span> 

   ![Nieuwe startpagina-URL opgeven](./media/application-proxy-office365-app-launcher/homepage.png)

5. <span data-ttu-id="2791f-128">Selecteer **opslaan**</span><span class="sxs-lookup"><span data-stu-id="2791f-128">Select **Save**</span></span>

## <a name="change-the-home-page-with-powershell"></a><span data-ttu-id="2791f-129">Wijzigen van de startpagina met PowerShell</span><span class="sxs-lookup"><span data-stu-id="2791f-129">Change the home page with PowerShell</span></span>

### <a name="install-the-azure-ad-powershell-module"></a><span data-ttu-id="2791f-130">Installeer de Azure AD PowerShell-module</span><span class="sxs-lookup"><span data-stu-id="2791f-130">Install the Azure AD PowerShell module</span></span>

<span data-ttu-id="2791f-131">Voordat u een aangepaste startpagina URL definiëren met behulp van PowerShell, moet u de Azure AD PowerShell-module installeren.</span><span class="sxs-lookup"><span data-stu-id="2791f-131">Before you define a custom home page URL by using PowerShell, install the Azure AD PowerShell module.</span></span> <span data-ttu-id="2791f-132">U kunt het downloaden van de [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), waarbij het Graph API-eindpunt wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2791f-132">You can download the package from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses the Graph API endpoint.</span></span> 

<span data-ttu-id="2791f-133">Volg deze stappen voor het installeren van het pakket:</span><span class="sxs-lookup"><span data-stu-id="2791f-133">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="2791f-134">Open een standaard PowerShell-venster en voer vervolgens de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2791f-134">Open a standard PowerShell window, and then run the following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="2791f-135">Als u de opdracht als een niet-beheerders uitvoert, gebruikt u de `-scope currentuser` optie.</span><span class="sxs-lookup"><span data-stu-id="2791f-135">If you're running the command as a non-admin, use the `-scope currentuser` option.</span></span>
2. <span data-ttu-id="2791f-136">Tijdens de installatie selecteert **Y** twee pakketten installeren via Nuget.org. Beide pakketten zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="2791f-136">During the installation, select **Y** to install two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-the-objectid-of-the-app"></a><span data-ttu-id="2791f-137">De object-id van de app zoeken</span><span class="sxs-lookup"><span data-stu-id="2791f-137">Find the ObjectID of the app</span></span>

<span data-ttu-id="2791f-138">De object-id van de app verkrijgen en zoek vervolgens naar de app door de startpagina.</span><span class="sxs-lookup"><span data-stu-id="2791f-138">Obtain the ObjectID of the app, and then search for the app by its home page.</span></span>

1. <span data-ttu-id="2791f-139">Open PowerShell en de Azure AD-module importeren.</span><span class="sxs-lookup"><span data-stu-id="2791f-139">Open PowerShell and import the Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="2791f-140">Meld u aan de Azure AD-module als de tenantbeheerder.</span><span class="sxs-lookup"><span data-stu-id="2791f-140">Sign in to the Azure AD module as the tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="2791f-141">De app op basis van de URL van de startpagina te zoeken.</span><span class="sxs-lookup"><span data-stu-id="2791f-141">Find the app based on its home page URL.</span></span> <span data-ttu-id="2791f-142">U vindt de URL in de portal door te gaan naar **Azure Active Directory** > **bedrijfstoepassingen** > **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2791f-142">You can find the URL in the portal by going to **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="2791f-143">In dit voorbeeld wordt *sharepoint iddemo*.</span><span class="sxs-lookup"><span data-stu-id="2791f-143">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="2791f-144">Deze krijgt u een resultaat die vergelijkbaar is met hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2791f-144">You should get a result that's similar to the one shown here.</span></span> <span data-ttu-id="2791f-145">Kopieer de ObjectID GUID moet worden gebruikt in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="2791f-145">Copy the ObjectID GUID to use in the next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-the-home-page-url"></a><span data-ttu-id="2791f-146">De URL van de startpagina bijwerken</span><span class="sxs-lookup"><span data-stu-id="2791f-146">Update the home page URL</span></span>

<span data-ttu-id="2791f-147">In dezelfde PowerShell-module die u hebt gebruikt voor stap 1, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="2791f-147">In the same PowerShell module that you used for step 1, perform the following steps:</span></span>

1. <span data-ttu-id="2791f-148">Bevestigen dat u de juiste app hebt en vervang *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* met de object-id die u in de vorige stap hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="2791f-148">Confirm that you have the correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with the ObjectID that you copied in the preceding step.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="2791f-149">Nu dat u de app hebt bevestigd, kunt u als volgt bijwerken van de startpagina.</span><span class="sxs-lookup"><span data-stu-id="2791f-149">Now that you've confirmed the app, you're ready to update the home page, as follows.</span></span>

2. <span data-ttu-id="2791f-150">Maak een lege application-object voor het opslaan van de wijzigingen die u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="2791f-150">Create a blank application object to hold the changes that you want to make.</span></span> <span data-ttu-id="2791f-151">Deze variabele bevat de waarden die u wilt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="2791f-151">This variable holds the values that you want to update.</span></span> <span data-ttu-id="2791f-152">Er is niets wordt in deze stap gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2791f-152">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="2791f-153">De URL voor de startpagina in de waarde die u wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="2791f-153">Set the home page URL to the value that you want.</span></span> <span data-ttu-id="2791f-154">De waarde moet een pad van het subdomein van de gepubliceerde app.</span><span class="sxs-lookup"><span data-stu-id="2791f-154">The value must be a subdomain path of the published app.</span></span> <span data-ttu-id="2791f-155">Bijvoorbeeld, als u de URL van de startpagina van wijzigen *https://sharepoint-iddemo.msappproxy.net/* naar *https://sharepoint-iddemo.msappproxy.net/hybrid/*, app-gebruikers rechtstreeks naar de aangepaste startpagina gaan.</span><span class="sxs-lookup"><span data-stu-id="2791f-155">For example, if you change the home page URL from *https://sharepoint-iddemo.msappproxy.net/* to *https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly to the custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="2791f-156">Bij te werken met behulp van de GUID (object-id) die u hebt genoteerd in ' stap 1: de object-id van de app te vinden. '</span><span class="sxs-lookup"><span data-stu-id="2791f-156">Make the update by using the GUID (ObjectID) that you copied in "Step 1: Find the ObjectID of the app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="2791f-157">Om te bevestigen dat de wijziging voltooid is, start u de app opnieuw.</span><span class="sxs-lookup"><span data-stu-id="2791f-157">To confirm that the change was successful, restart the app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="2791f-158">Alle wijzigingen die u in de app aanbrengt mogelijk opnieuw instellen van de URL van de startpagina.</span><span class="sxs-lookup"><span data-stu-id="2791f-158">Any changes that you make to the app might reset the home page URL.</span></span> <span data-ttu-id="2791f-159">Als de URL van uw startpagina wordt opnieuw ingesteld, herhaalt u stap 2.</span><span class="sxs-lookup"><span data-stu-id="2791f-159">If your home page URL resets, repeat step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2791f-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2791f-160">Next steps</span></span>

- [<span data-ttu-id="2791f-161">Externe toegang voor SharePoint met Azure AD-toepassingsproxy inschakelen</span><span class="sxs-lookup"><span data-stu-id="2791f-161">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="2791f-162">Toepassingsproxy inschakelen in de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="2791f-162">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)
