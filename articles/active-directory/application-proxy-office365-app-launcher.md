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
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="e3584-103">Een aangepaste startpagina van gepubliceerde apps instellen via Azure AD-toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="e3584-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="e3584-104">Dit artikel wordt beschreven hoe tooconfigure apps toodirect gebruikers tooa aangepaste startpagina.</span><span class="sxs-lookup"><span data-stu-id="e3584-104">This article discusses how tooconfigure apps toodirect users tooa custom home page.</span></span> <span data-ttu-id="e3584-105">Wanneer u een toepassing met toepassingsproxy publiceert, instellen van een interne URL maar soms die is geen Hallo pagina die uw gebruikers moeten eerst te zien.</span><span class="sxs-lookup"><span data-stu-id="e3584-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not hello page your users should see first.</span></span> <span data-ttu-id="e3584-106">De startpagina van een aangepaste zo instellen dat uw gebruikers gaan toohello rechts pagina wanneer ze toegang krijgen Hallo apps van Azure Active Directory-Toegangsvenster Hallo of Hallo Office 365-app starten tot.</span><span class="sxs-lookup"><span data-stu-id="e3584-106">Set a custom home page so that your users go toohello right page when they access hello apps from hello Azure Active Directory Access Panel or hello Office 365 app launcher.</span></span>

<span data-ttu-id="e3584-107">Wanneer gebruikers Hallo app openen, wordt ze omgeleid door standaard toohello hoofdmap domein-URL voor Hallo gepubliceerde app.</span><span class="sxs-lookup"><span data-stu-id="e3584-107">When users launch hello app, they're directed by default toohello root domain URL for hello published app.</span></span> <span data-ttu-id="e3584-108">Hallo-startpagina wordt meestal ingesteld als Hallo startpagina URL.</span><span class="sxs-lookup"><span data-stu-id="e3584-108">hello landing page is typically set as hello home page URL.</span></span> <span data-ttu-id="e3584-109">Hello Azure AD PowerShell-module toodefine aangepaste startpagina URL gebruiken als u wilt dat de app gebruikers tooland op een bepaalde pagina in Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="e3584-109">Use hello Azure AD PowerShell module toodefine custom home page URLs when you want app users tooland on a specific page within hello app.</span></span> 

<span data-ttu-id="e3584-110">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e3584-110">For example:</span></span>
- <span data-ttu-id="e3584-111">Binnen uw bedrijfsnetwerk gebruikers te gaan*https://ExpenseApp/login/login.aspx* toosign in en toegang tot uw app.</span><span class="sxs-lookup"><span data-stu-id="e3584-111">Inside your corporate network, users go too*https://ExpenseApp/login/login.aspx* toosign in and access your app.</span></span>
- <span data-ttu-id="e3584-112">Omdat u andere activa zoals installatiekopieën dat toepassingsproxy tooaccess op hoogste niveau van de mapstructuur Hallo Hallo nodig hebt, u Hallo-app met publiceert *https://ExpenseApp* zoals Hallo interne URL.</span><span class="sxs-lookup"><span data-stu-id="e3584-112">Because you have other assets like images that Application Proxy needs tooaccess at hello top level of hello folder structure, you publish hello app with *https://ExpenseApp* as hello internal URL.</span></span>
- <span data-ttu-id="e3584-113">externe URL is standaard Hallo *https://ExpenseApp-contoso.msappproxy.net*, die uw gebruikers toohello aanmelding wordt pas op de pagina.</span><span class="sxs-lookup"><span data-stu-id="e3584-113">hello default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users toohello sign in page.</span></span>  
- <span data-ttu-id="e3584-114">Stel *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* als startpagina URL toogive Hallo uw gebruikers een naadloze ervaring.</span><span class="sxs-lookup"><span data-stu-id="e3584-114">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as hello home page URL toogive your users a seamless experience.</span></span> 

>[!NOTE]
><span data-ttu-id="e3584-115">Wanneer u gebruikerstoegang toopublished apps geeft, Hallo apps worden weergegeven in Hallo [Azure AD-Toegangsvenster](active-directory-saas-access-panel-introduction.md) en Hallo [Office 365 app linksboven](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span><span class="sxs-lookup"><span data-stu-id="e3584-115">When you give users access toopublished apps, hello apps are displayed in hello [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and hello [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="e3584-116">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="e3584-116">Before you start</span></span>

<span data-ttu-id="e3584-117">Voordat u de URL van de startpagina Hallo instellen, houd er rekening mee Hallo volgens de vereisten:</span><span class="sxs-lookup"><span data-stu-id="e3584-117">Before you set hello home page URL, keep in mind hello following requirements:</span></span>

* <span data-ttu-id="e3584-118">Zorg ervoor dat u opgeeft Hallo-pad is een subdomein pad van Hallo basis domein-URL.</span><span class="sxs-lookup"><span data-stu-id="e3584-118">Ensure that hello path you specify is a subdomain path of hello root domain URL.</span></span>

  <span data-ttu-id="e3584-119">Als Hallo hoofddomein URL, bijvoorbeeld https://apps.contoso.com/app1/, Hallo startpagina URL die u configureert moet beginnen met https://apps.contoso.com/app1/.</span><span class="sxs-lookup"><span data-stu-id="e3584-119">If hello root-domain URL is, for example, https://apps.contoso.com/app1/, hello home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="e3584-120">Als u een wijziging aanbrengt toohello-app gepubliceerd, Hallo wijziging mogelijk Hallo-waarde van de URL van de startpagina Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="e3584-120">If you make a change toohello published app, hello change might reset hello value of hello home page URL.</span></span> <span data-ttu-id="e3584-121">Wanneer u in toekomstige Hallo Hallo app bijwerkt, moet u controleren en, indien nodig werkt u de URL van de homepage Hallo.</span><span class="sxs-lookup"><span data-stu-id="e3584-121">When you update hello app in hello future, you should recheck and, if necessary, update hello home page URL.</span></span>

## <a name="change-hello-home-page-in-hello-azure-portal"></a><span data-ttu-id="e3584-122">Hallo-startpagina in hello Azure-portal wijzigen</span><span class="sxs-lookup"><span data-stu-id="e3584-122">Change hello home page in hello Azure portal</span></span>

1. <span data-ttu-id="e3584-123">Meld u aan toohello [Azure-portal](https://portal.azure.com) als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e3584-123">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="e3584-124">Navigeer te**Azure Active Directory** > **App registraties** en kiest u uw toepassing uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="e3584-124">Navigate too**Azure Active Directory** > **App registrations** and choose your application from hello list.</span></span> 
3. <span data-ttu-id="e3584-125">Selecteer **eigenschappen** uit Hallo-instellingen.</span><span class="sxs-lookup"><span data-stu-id="e3584-125">Select **Properties** from hello settings.</span></span>
4. <span data-ttu-id="e3584-126">Update Hallo **startpagina URL** veld met het nieuwe pad.</span><span class="sxs-lookup"><span data-stu-id="e3584-126">Update hello **Home page URL** field with your new path.</span></span> 

   ![Nieuwe startpagina-URL opgeven](./media/application-proxy-office365-app-launcher/homepage.png)

5. <span data-ttu-id="e3584-128">Selecteer **opslaan**</span><span class="sxs-lookup"><span data-stu-id="e3584-128">Select **Save**</span></span>

## <a name="change-hello-home-page-with-powershell"></a><span data-ttu-id="e3584-129">Hallo-startpagina met PowerShell wijzigen</span><span class="sxs-lookup"><span data-stu-id="e3584-129">Change hello home page with PowerShell</span></span>

### <a name="install-hello-azure-ad-powershell-module"></a><span data-ttu-id="e3584-130">Hello Azure AD PowerShell-module installeren</span><span class="sxs-lookup"><span data-stu-id="e3584-130">Install hello Azure AD PowerShell module</span></span>

<span data-ttu-id="e3584-131">Voordat u een aangepaste startpagina URL definiëren met behulp van PowerShell, installeer hello Azure AD PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="e3584-131">Before you define a custom home page URL by using PowerShell, install hello Azure AD PowerShell module.</span></span> <span data-ttu-id="e3584-132">U kunt Hallo pakket downloaden van Hallo [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), die gebruikt Hallo Graph API-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="e3584-132">You can download hello package from hello [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses hello Graph API endpoint.</span></span> 

<span data-ttu-id="e3584-133">tooinstall Hallo van het pakket, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="e3584-133">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="e3584-134">Open een standaard PowerShell-venster en voer vervolgens Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e3584-134">Open a standard PowerShell window, and then run hello following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="e3584-135">Als u Hallo-opdracht als een niet-beheerders uitvoert, gebruikt u Hallo `-scope currentuser` optie.</span><span class="sxs-lookup"><span data-stu-id="e3584-135">If you're running hello command as a non-admin, use hello `-scope currentuser` option.</span></span>
2. <span data-ttu-id="e3584-136">Selecteer tijdens de installatie Hallo **Y** tooinstall twee pakketten van Nuget.org. Beide pakketten zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="e3584-136">During hello installation, select **Y** tooinstall two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-hello-objectid-of-hello-app"></a><span data-ttu-id="e3584-137">Hallo ObjectID van Hallo app zoeken</span><span class="sxs-lookup"><span data-stu-id="e3584-137">Find hello ObjectID of hello app</span></span>

<span data-ttu-id="e3584-138">Hallo ObjectID van Hallo app verkrijgen en zoek vervolgens naar Hallo app door de startpagina.</span><span class="sxs-lookup"><span data-stu-id="e3584-138">Obtain hello ObjectID of hello app, and then search for hello app by its home page.</span></span>

1. <span data-ttu-id="e3584-139">Open PowerShell en hello Azure AD-module importeren.</span><span class="sxs-lookup"><span data-stu-id="e3584-139">Open PowerShell and import hello Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="e3584-140">Aanmelden toohello Azure AD-module als Hallo tenantbeheerder.</span><span class="sxs-lookup"><span data-stu-id="e3584-140">Sign in toohello Azure AD module as hello tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="e3584-141">Hallo-app op basis van de URL van de startpagina te zoeken.</span><span class="sxs-lookup"><span data-stu-id="e3584-141">Find hello app based on its home page URL.</span></span> <span data-ttu-id="e3584-142">U vindt Hallo-URL in het Hallo-portal door te gaan**Azure Active Directory** > **bedrijfstoepassingen** > **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="e3584-142">You can find hello URL in hello portal by going too**Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="e3584-143">In dit voorbeeld wordt *sharepoint iddemo*.</span><span class="sxs-lookup"><span data-stu-id="e3584-143">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="e3584-144">Deze krijgt u een resultaat dat vergelijkbare toohello een hier weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e3584-144">You should get a result that's similar toohello one shown here.</span></span> <span data-ttu-id="e3584-145">Hallo ObjectID GUID toouse in de volgende sectie Hallo kopiëren.</span><span class="sxs-lookup"><span data-stu-id="e3584-145">Copy hello ObjectID GUID toouse in hello next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a><span data-ttu-id="e3584-146">Hallo startpagina URL voor bijwerken</span><span class="sxs-lookup"><span data-stu-id="e3584-146">Update hello home page URL</span></span>

<span data-ttu-id="e3584-147">Dezelfde PowerShell-module die u hebt gebruikt voor stap 1: Voer in Hallo Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e3584-147">In hello same PowerShell module that you used for step 1, perform hello following steps:</span></span>

1. <span data-ttu-id="e3584-148">Bevestigen dat u Hallo app corrigeren en vervang *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* Hello ObjectID die u in de voorgaande stap Hallo gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="e3584-148">Confirm that you have hello correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with hello ObjectID that you copied in hello preceding step.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="e3584-149">Nu u Hallo app hebt bevestigd, bent u klaar tooupdate Hallo-startpagina, als volgt.</span><span class="sxs-lookup"><span data-stu-id="e3584-149">Now that you've confirmed hello app, you're ready tooupdate hello home page, as follows.</span></span>

2. <span data-ttu-id="e3584-150">Maak een lege toepassing object toohold Hallo wijzigingen die u toomake wilt.</span><span class="sxs-lookup"><span data-stu-id="e3584-150">Create a blank application object toohold hello changes that you want toomake.</span></span> <span data-ttu-id="e3584-151">Deze variabele bevat Hallo-waarden die u wilt dat tooupdate.</span><span class="sxs-lookup"><span data-stu-id="e3584-151">This variable holds hello values that you want tooupdate.</span></span> <span data-ttu-id="e3584-152">Er is niets wordt in deze stap gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e3584-152">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="e3584-153">Hallo startpagina URL toohello waarde die u wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="e3584-153">Set hello home page URL toohello value that you want.</span></span> <span data-ttu-id="e3584-154">Hallo-waarde moet een pad van het subdomein van Hallo gepubliceerde app.</span><span class="sxs-lookup"><span data-stu-id="e3584-154">hello value must be a subdomain path of hello published app.</span></span> <span data-ttu-id="e3584-155">Bijvoorbeeld, als u wijzigt de URL van de startpagina van Hallo *https://sharepoint-iddemo.msappproxy.net/* te*https://sharepoint-iddemo.msappproxy.net/hybrid/*, app-gebruikers gaan rechtstreeks toohello aangepast startpagina.</span><span class="sxs-lookup"><span data-stu-id="e3584-155">For example, if you change hello home page URL from *https://sharepoint-iddemo.msappproxy.net/* too*https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly toohello custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="e3584-156">Zorg Hallo update met behulp van Hallo GUID (object-id) die u hebt genoteerd in ' stap 1: zoeken Hallo ObjectID van app Hallo. "</span><span class="sxs-lookup"><span data-stu-id="e3584-156">Make hello update by using hello GUID (ObjectID) that you copied in "Step 1: Find hello ObjectID of hello app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="e3584-157">tooconfirm hello wijziging is geslaagd, opnieuw opstarten Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="e3584-157">tooconfirm that hello change was successful, restart hello app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="e3584-158">Eventuele wijzigingen die u toohello app mogelijk opnieuw ingesteld Hallo startpagina URL.</span><span class="sxs-lookup"><span data-stu-id="e3584-158">Any changes that you make toohello app might reset hello home page URL.</span></span> <span data-ttu-id="e3584-159">Als de URL van uw startpagina wordt opnieuw ingesteld, herhaalt u stap 2.</span><span class="sxs-lookup"><span data-stu-id="e3584-159">If your home page URL resets, repeat step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3584-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e3584-160">Next steps</span></span>

- [<span data-ttu-id="e3584-161">Externe toegang tooSharePoint met Azure AD-toepassingsproxy inschakelen</span><span class="sxs-lookup"><span data-stu-id="e3584-161">Enable remote access tooSharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="e3584-162">Toepassingsproxy inschakelen in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e3584-162">Enable Application Proxy in hello Azure portal</span></span>](active-directory-application-proxy-enable.md)
