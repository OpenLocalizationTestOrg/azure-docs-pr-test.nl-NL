---
title: De extensie van de toegang tot Azure-Configuratiescherm probleemoplossing voor IE | Microsoft Docs
description: Het gebruik van Groepsbeleid voor het implementeren van de invoegtoepassing Internet Explorer voor de portal mijn Apps.
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
ms.openlocfilehash: 938d0b4046afa8c80eabe542f4541d0554948f5d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-the-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="d8b8a-103">De uitbreiding van het deelvenster toegang tot het oplossen van problemen voor Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="d8b8a-103">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="d8b8a-104">In dit artikel helpt u de volgende problemen:</span><span class="sxs-lookup"><span data-stu-id="d8b8a-104">This article helps you troubleshoot the following problems:</span></span>

* <span data-ttu-id="d8b8a-105">U kunt geen toegang krijgt tot uw apps via de portal mijn Apps tijdens het gebruik van Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-105">You're unable to access your apps through the My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="d8b8a-106">U ziet het bericht 'Software installeren' zelfs als u de software al hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-106">You see the "Install Software" message even though you've already installed the software.</span></span>

<span data-ttu-id="d8b8a-107">Als u een beheerder bent, Zie ook: [het implementeren van de uitbreiding van het Configuratiescherm toegang voor Internet Explorer met behulp van Groepsbeleid](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="d8b8a-107">If you are an admin, see also: [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-the-diagnostic-tool"></a><span data-ttu-id="d8b8a-108">Het diagnostische hulpprogramma uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d8b8a-108">Run the Diagnostic Tool</span></span>
<span data-ttu-id="d8b8a-109">U kunt problemen installatie met de extensie van het Configuratiescherm toegang door te downloaden en uitvoeren van het toegangsvenster diagnostische hulpprogramma:</span><span class="sxs-lookup"><span data-stu-id="d8b8a-109">You can diagnose installation problems with the Access Panel Extension by downloading and running the Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="d8b8a-110">Klik hier om het diagnostisch hulpprogramma voor downloaden.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-110">Click here to download the diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="d8b8a-111">Open het bestand en druk op **alle uitpakken** knop.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-111">Open the file, and press **Extract all** button.</span></span>
   
    ![Druk op alle uitpakken](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="d8b8a-113">Druk op de **extraheren** om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-113">Then press the **Extract** button to continue.</span></span>
   
    ![Druk op uitpakken](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="d8b8a-115">Als u wilt het hulpprogramma uitvoert, met de rechtermuisknop op het bestand met de naam **AccessPanelExtensionDiagnosticTool**, selecteer daarna **openen met > Microsoft Windows Script Host die is gebaseerd**.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-115">To run the tool, right-click the file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![Open met > Microsoft Windows scripthost gebaseerd](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="d8b8a-117">Vervolgens ziet u de volgende diagnostische venster waarin wordt beschreven wat mis zijn met de installatie.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-117">You will then see the following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![Een voorbeeld van het venster diagnostische](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="d8b8a-119">Klik op '**Ja**' zodat het programma los de problemen die zijn gevonden.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-119">Click "**YES**" to let the program fix the issues that have been found.</span></span>
7. <span data-ttu-id="d8b8a-120">Om deze wijzigingen opslaat, elke Internet Explorer-venster sluiten en open Internet Explorer opnieuw.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-120">To save these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="d8b8a-121">Als u nog steeds geen toegang uw apps tot, probeert u de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-121">If you still can't access your apps, try the steps below.</span></span>

## <a name="check-that-the-access-panel-extension-is-enabled"></a><span data-ttu-id="d8b8a-122">Controleer of de uitbreiding van het Configuratiescherm toegang is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="d8b8a-122">Check that the Access Panel Extension is enabled</span></span>
<span data-ttu-id="d8b8a-123">Controleren dat de uitbreiding van het Configuratiescherm toegang is ingeschakeld in Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="d8b8a-123">To verify that the Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="d8b8a-124">Klik in Internet Explorer op de **Tandwielpictogram pictogram** in de rechterbovenhoek van het venster.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-124">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="d8b8a-125">Selecteer vervolgens **Internetopties**.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="d8b8a-126">(In oudere versies van Internet Explorer kunt u dit onder vinden **Extra > Internetopties**.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Ga naar Extra > Internetopties](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="d8b8a-128">Klik op de **programma's** tabblad en klik vervolgens op de **invoegtoepassingen beheren** knop.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-128">Click the **Programs** tab, then click the **Manage add-ons** button.</span></span>
   
    ![Klik op Invoegtoepassingen beheren](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="d8b8a-130">Selecteer in dit dialoogvenster **Configuratiescherm-uitbreiding voor toegang tot** en klik vervolgens op de **inschakelen** knop.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-130">In this dialog, select **Access Panel Extension** and then click the **Enable** button.</span></span>
   
    ![Klik op inschakelen](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="d8b8a-132">Om deze wijzigingen opslaat, elke Internet Explorer-venster sluiten en open Internet Explorer opnieuw.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-132">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="d8b8a-133">Uitbreidingen inschakelen voor InPrivate-navigatie</span><span class="sxs-lookup"><span data-stu-id="d8b8a-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="d8b8a-134">Als u de modus InPrivate-navigatie:</span><span class="sxs-lookup"><span data-stu-id="d8b8a-134">If you are using the InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="d8b8a-135">Klik in Internet Explorer op de **Tandwielpictogram pictogram** in de rechterbovenhoek van het venster.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-135">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="d8b8a-136">Selecteer vervolgens **Internetopties**.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="d8b8a-137">(In oudere versies van Internet Explorer kunt u dit onder vinden **Extra > Internetopties**.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Een voorbeeld van het venster diagnostische](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="d8b8a-139">Ga naar de **Privacy** tabblad vervolgens **schakelt** het selectievakje **werkbalken en extensies uitschakelen wanneer InPrivate-navigatie wordt gestart**</span><span class="sxs-lookup"><span data-stu-id="d8b8a-139">Go to the **Privacy** tab, then **uncheck** the checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![Schakel het selectievakje uitschakelen werkbalken en extensies wanneer InPrivate-navigatie wordt gestart](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="d8b8a-141">Om deze wijzigingen opslaat, elke Internet Explorer-venster sluiten en open Internet Explorer opnieuw.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-141">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-the-access-panel-extension"></a><span data-ttu-id="d8b8a-142">De extensie van het Configuratiescherm toegang verwijderen</span><span class="sxs-lookup"><span data-stu-id="d8b8a-142">Uninstall the Access Panel Extension</span></span>
<span data-ttu-id="d8b8a-143">De extensie Toegangspaneel van uw computer verwijderen:</span><span class="sxs-lookup"><span data-stu-id="d8b8a-143">To uninstall the Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="d8b8a-144">Op het toetsenbord, drukt u op de **Windows-toets** het menu Start openen.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-144">On your keyboard, press the **Windows key** to open the Start menu.</span></span> <span data-ttu-id="d8b8a-145">Wanneer het menu geopend is, typt u iets als u wilt zoeken.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-145">When the menu is open, you can type anything to do a search.</span></span> <span data-ttu-id="d8b8a-146">Typ 'Configuratiescherm' en open vervolgens de **Configuratiescherm** wanneer deze wordt weergegeven in de zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-146">Type "Control Panel" and then open the **Control Panel** when it appears in the search results.</span></span>
   
    ![Zoeken naar het Configuratiescherm](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="d8b8a-148">Wijzig in de rechterbovenhoek van het Configuratiescherm de **weergeven door** optie naar **grote pictogrammen**.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-148">In the top right corner of the Control Panel, change the **View by** option to **Large icons**.</span></span> <span data-ttu-id="d8b8a-149">Vervolgens zoeken en klik op de **programma's en onderdelen** knop.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-149">Then find and click the **Programs and Features** button.</span></span>
   
    ![Chang de weergave grote pictogrammen weer te geven](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="d8b8a-151">Selecteer in de lijst **Configuratiescherm-uitbreiding voor toegang tot**, en klik op de **verwijderen** knop.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-151">From the list, select **Access Panel Extension**, and the click the **Uninstall** button.</span></span>
   
    ![Klik op verwijderen](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="d8b8a-153">U kunt vervolgens voor het installeren van de uitbreiding opnieuw uit om te zien als het probleem is opgelost.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-153">You can then try to install the extension again to see if the problem has been resolved.</span></span>

<span data-ttu-id="d8b8a-154">Als u de uitbreiding verwijderen problemen ondervindt, kunt u ook verwijderen met behulp van de [Microsoft los It](https://go.microsoft.com/?linkid=9779673) hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="d8b8a-154">If you encounter issues uninstalling the extension, you can also remove it using the [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="d8b8a-155">Verwante artikelen</span><span class="sxs-lookup"><span data-stu-id="d8b8a-155">Related Articles</span></span>
* <span data-ttu-id="d8b8a-156">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="d8b8a-156">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* [<span data-ttu-id="d8b8a-157">Toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8b8a-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="d8b8a-158">De extensie van het Configuratiescherm toegang voor Internet Explorer met behulp van Groepsbeleid implementeren</span><span class="sxs-lookup"><span data-stu-id="d8b8a-158">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)

