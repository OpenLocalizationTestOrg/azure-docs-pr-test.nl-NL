---
title: aaaTroubleshooting hello Azure Access Configuratiescherm-extensie voor IE | Microsoft Docs
description: Hoe groepeert toouse beleid toodeploy Hallo Internet Explorer-invoegtoepassing voor Hallo mijn Apps portal.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56b3230-26fd-42ec-9e3d-2c12daf15479
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23cbb6117f34759330206de3a26f1397486acedb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="9a2fd-103">Hallo Configuratiescherm-uitbreiding voor toegang tot het oplossen van problemen voor Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="9a2fd-103">Troubleshooting hello Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="9a2fd-104">In dit artikel helpt u Hallo na de problemen oplossen:</span><span class="sxs-lookup"><span data-stu-id="9a2fd-104">This article helps you troubleshoot hello following problems:</span></span>

* <span data-ttu-id="9a2fd-105">U bent tooaccess uw apps via Hallo mijn Apps portal tijdens het gebruik van Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-105">You're unable tooaccess your apps through hello My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="9a2fd-106">U ziet Hallo 'Software installeren' bericht zelfs als u al Hallo software hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-106">You see hello "Install Software" message even though you've already installed hello software.</span></span>

<span data-ttu-id="9a2fd-107">Als u een beheerder bent, Zie ook: [hoe tooDeploy uitbreiding voor toegang tot Configuratiescherm Hallo voor Internet Explorer met behulp van Groepsbeleid](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="9a2fd-107">If you are an admin, see also: [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-hello-diagnostic-tool"></a><span data-ttu-id="9a2fd-108">Hallo diagnostisch hulpprogramma uitvoeren</span><span class="sxs-lookup"><span data-stu-id="9a2fd-108">Run hello Diagnostic Tool</span></span>
<span data-ttu-id="9a2fd-109">U kunt problemen installatie Hello Configuratiescherm-uitbreiding voor toegang door te downloaden en uitvoeren van Hallo Toegangsvenster diagnostische hulpprogramma:</span><span class="sxs-lookup"><span data-stu-id="9a2fd-109">You can diagnose installation problems with hello Access Panel Extension by downloading and running hello Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="9a2fd-110">Klik hier toodownload Hallo diagnostische hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-110">Click here toodownload hello diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="9a2fd-111">Open Hallo bestands- en druk op **alle uitpakken** knop.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-111">Open hello file, and press **Extract all** button.</span></span>
   
    ![Druk op alle uitpakken](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="9a2fd-113">Druk op Hallo **extraheren** knop toocontinue.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-113">Then press hello **Extract** button toocontinue.</span></span>
   
    ![Druk op uitpakken](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="9a2fd-115">hulpprogramma voor toorun hello, klik met de rechtermuisknop Hallo-bestand met de naam **AccessPanelExtensionDiagnosticTool**, selecteer daarna **openen met > Microsoft Windows Script Host die is gebaseerd**.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-115">toorun hello tool, right-click hello file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![Open met > Microsoft Windows scripthost gebaseerd](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="9a2fd-117">Vervolgens ziet u Hallo na diagnostische venster waarin wordt beschreven wat mis zijn met de installatie.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-117">You will then see hello following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![Een voorbeeld van diagnostische Hallo-venster](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="9a2fd-119">Klik op '**Ja**' toolet Hallo programma fix Hallo problemen zijn gevonden.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-119">Click "**YES**" toolet hello program fix hello issues that have been found.</span></span>
7. <span data-ttu-id="9a2fd-120">Deze wijzigingen, toosave elke Internet Explorer-venster sluiten en open Internet Explorer opnieuw.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-120">toosave these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="9a2fd-121">Als u nog steeds geen toegang uw apps tot, probeert u Hallo onderstaande stappen.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-121">If you still can't access your apps, try hello steps below.</span></span>

## <a name="check-that-hello-access-panel-extension-is-enabled"></a><span data-ttu-id="9a2fd-122">Controleer dat Hallo die toegang Configuratiescherm-extensie is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="9a2fd-122">Check that hello Access Panel Extension is enabled</span></span>
<span data-ttu-id="9a2fd-123">tooverify die Hallo uitbreiding van het Configuratiescherm toegang is ingeschakeld in Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="9a2fd-123">tooverify that hello Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="9a2fd-124">Klik in Internet Explorer op Hallo **Tandwielpictogram pictogram** op Hallo rechtsboven Hallo-venster.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-124">In Internet Explorer, click hello **Gear icon** on hello top right corner of hello window.</span></span> <span data-ttu-id="9a2fd-125">Selecteer vervolgens **Internetopties**.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="9a2fd-126">(In oudere versies van Internet Explorer kunt u dit onder vinden **Extra > Internetopties**.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Ga tooTools > Internetopties](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="9a2fd-128">Klik op Hallo **programma's** tabblad en klik op Hallo **invoegtoepassingen beheren** knop.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-128">Click hello **Programs** tab, then click hello **Manage add-ons** button.</span></span>
   
    ![Klik op Invoegtoepassingen beheren](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="9a2fd-130">Selecteer in dit dialoogvenster **Configuratiescherm-uitbreiding voor toegang tot** en klik vervolgens op Hallo **inschakelen** knop.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-130">In this dialog, select **Access Panel Extension** and then click hello **Enable** button.</span></span>
   
    ![Klik op inschakelen](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="9a2fd-132">Deze wijzigingen, toosave elke Internet Explorer-venster sluiten en open Internet Explorer opnieuw.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-132">toosave these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="9a2fd-133">Uitbreidingen inschakelen voor InPrivate-navigatie</span><span class="sxs-lookup"><span data-stu-id="9a2fd-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="9a2fd-134">Als u Hallo InPrivate-navigatie-modus met:</span><span class="sxs-lookup"><span data-stu-id="9a2fd-134">If you are using hello InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="9a2fd-135">Klik in Internet Explorer op Hallo **Tandwielpictogram pictogram** op Hallo rechtsboven Hallo-venster.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-135">In Internet Explorer, click hello **Gear icon** on hello top right corner of hello window.</span></span> <span data-ttu-id="9a2fd-136">Selecteer vervolgens **Internetopties**.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="9a2fd-137">(In oudere versies van Internet Explorer kunt u dit onder vinden **Extra > Internetopties**.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Een voorbeeld van diagnostische Hallo-venster](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="9a2fd-139">Ga toohello **Privacy** tabblad vervolgens **schakelt** Hallo selectievakje **werkbalken en extensies uitschakelen wanneer InPrivate-navigatie wordt gestart**</span><span class="sxs-lookup"><span data-stu-id="9a2fd-139">Go toohello **Privacy** tab, then **uncheck** hello checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![Schakel het selectievakje uitschakelen werkbalken en extensies wanneer InPrivate-navigatie wordt gestart](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="9a2fd-141">Deze wijzigingen, toosave elke Internet Explorer-venster sluiten en open Internet Explorer opnieuw.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-141">toosave these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-hello-access-panel-extension"></a><span data-ttu-id="9a2fd-142">Hallo uitbreiding van het Configuratiescherm toegang verwijderen</span><span class="sxs-lookup"><span data-stu-id="9a2fd-142">Uninstall hello Access Panel Extension</span></span>
<span data-ttu-id="9a2fd-143">toouninstall hello Toegangspaneel uitbreiding van uw computer:</span><span class="sxs-lookup"><span data-stu-id="9a2fd-143">toouninstall hello Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="9a2fd-144">Op het toetsenbord, drukt u op Hallo **Windows-toets** tooopen Hallo startmenu.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-144">On your keyboard, press hello **Windows key** tooopen hello Start menu.</span></span> <span data-ttu-id="9a2fd-145">Wanneer het Hallo-menu is geopend, kunt u alles typen toodo een zoekopdracht.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-145">When hello menu is open, you can type anything toodo a search.</span></span> <span data-ttu-id="9a2fd-146">Typ 'Configuratiescherm' en open vervolgens Hallo **Configuratiescherm** wanneer deze wordt weergegeven in zoekresultaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-146">Type "Control Panel" and then open hello **Control Panel** when it appears in hello search results.</span></span>
   
    ![Zoeken naar het Configuratiescherm](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="9a2fd-148">Wijzig in Hallo rechterbovenhoek van het Configuratiescherm hello, Hallo **weergeven door** te optie**grote pictogrammen**.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-148">In hello top right corner of hello Control Panel, change hello **View by** option too**Large icons**.</span></span> <span data-ttu-id="9a2fd-149">Vervolgens zoeken en klik op Hallo **programma's en onderdelen** knop.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-149">Then find and click hello **Programs and Features** button.</span></span>
   
    ![Chang Hallo weergave tooshow grote pictogrammen](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="9a2fd-151">Selecteer in de lijst Hallo **Configuratiescherm-uitbreiding voor toegang tot**, en klikt u op Hallo Hallo **verwijderen** knop.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-151">From hello list, select **Access Panel Extension**, and hello click hello **Uninstall** button.</span></span>
   
    ![Klik op verwijderen](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="9a2fd-153">U kunt vervolgens tooinstall Hallo-uitbreiding opnieuw toosee als Hallo probleem opgelost is.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-153">You can then try tooinstall hello extension again toosee if hello problem has been resolved.</span></span>

<span data-ttu-id="9a2fd-154">Als u problemen hebt met het Hallo-uitbreiding te verwijderen, kunt u ook verwijderen met behulp van Hallo [Microsoft los It](https://go.microsoft.com/?linkid=9779673) hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="9a2fd-154">If you encounter issues uninstalling hello extension, you can also remove it using hello [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="9a2fd-155">Verwante artikelen</span><span class="sxs-lookup"><span data-stu-id="9a2fd-155">Related Articles</span></span>
* <span data-ttu-id="9a2fd-156">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="9a2fd-156">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* [<span data-ttu-id="9a2fd-157">Toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a2fd-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="9a2fd-158">Hoe tooDeploy uitbreiding voor toegang tot Configuratiescherm Hallo voor Internet Explorer met behulp van Groepsbeleid</span><span class="sxs-lookup"><span data-stu-id="9a2fd-158">How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)

