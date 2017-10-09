---
title: aaaTroubleshoot-functies die niet voldoen aan toostart | Microsoft Docs
description: Hier volgen enkele veelvoorkomende redenen waarom een Service in de Cloud-rol toostart kan mislukken. Oplossingen voor problemen toothese worden ook gegeven.
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a><span data-ttu-id="db3b5-104">Cloudservice-functies die niet voldoen aan toostart oplossen</span><span class="sxs-lookup"><span data-stu-id="db3b5-104">Troubleshoot Cloud Service roles that fail toostart</span></span>
<span data-ttu-id="db3b5-105">Hier volgen enkele veelvoorkomende problemen en oplossingen gerelateerde tooAzure Cloud Services-functies die niet voldoen aan toostart.</span><span class="sxs-lookup"><span data-stu-id="db3b5-105">Here are some common problems and solutions related tooAzure Cloud Services roles that fail toostart.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="db3b5-106">Ontbrekende dll's of afhankelijkheden</span><span class="sxs-lookup"><span data-stu-id="db3b5-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="db3b5-107">Niet-reagerende rollen en functies die zijn functioneert tussen **Bezig met initialiseren**, **bezet**, en **stoppen** statussen kunnen zijn veroorzaakt door ontbrekende dll-bestanden of assembly's.</span><span class="sxs-lookup"><span data-stu-id="db3b5-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="db3b5-108">Problemen met ontbrekende dll's of assembly's zijn:</span><span class="sxs-lookup"><span data-stu-id="db3b5-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="db3b5-109">De rolinstantie is doorlopen **Bezig met initialiseren**, **bezet**, en **stoppen** statussen.</span><span class="sxs-lookup"><span data-stu-id="db3b5-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="db3b5-110">Uw rolexemplaar is verplaatst, te**gereed** , maar als u de webtoepassing tooyour navigeert, Hallo pagina wordt niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="db3b5-110">Your role instance has moved too**Ready** but if you navigate tooyour web application, hello page does not appear.</span></span>

<span data-ttu-id="db3b5-111">Er zijn verschillende aanbevolen methoden om deze problemen te onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="db3b5-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="db3b5-112">Vaststellen van problemen met ontbrekende dll-bestand in een Webrol</span><span class="sxs-lookup"><span data-stu-id="db3b5-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="db3b5-113">Wanneer u tooa-website die wordt geïmplementeerd in een Webrol navigeren en een server fout vergelijkbare toohello volgende wordt weergegeven in Hallo browser, kan dit wijzen op een DLL-bestand ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="db3b5-113">When you navigate tooa website that is deployed in a web role, and hello browser displays a server error similar toohello following, it may indicate that a DLL is missing.</span></span>

![Serverfout in '/' toepassing.](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="db3b5-115">Problemen vaststellen door het uitschakelen van aangepaste fouten</span><span class="sxs-lookup"><span data-stu-id="db3b5-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="db3b5-116">Gedetailleerde foutinformatie kan worden bekeken door Hallo web.config voor Hallo web rol tooset Hallo aangepaste fout modus tooOff configureren en het Hallo-service opnieuw te implementeren.</span><span class="sxs-lookup"><span data-stu-id="db3b5-116">More complete error information can be viewed by configuring hello web.config for hello web role tooset hello custom error mode tooOff and redeploying hello service.</span></span>

<span data-ttu-id="db3b5-117">fouten tooview meer voltooid zonder te maken met extern bureaublad:</span><span class="sxs-lookup"><span data-stu-id="db3b5-117">tooview more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="db3b5-118">Hallo-oplossing in Microsoft Visual Studio openen.</span><span class="sxs-lookup"><span data-stu-id="db3b5-118">Open hello solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="db3b5-119">In Hallo **Solution Explorer**, Hallo web.config-bestand vinden en te openen.</span><span class="sxs-lookup"><span data-stu-id="db3b5-119">In hello **Solution Explorer**, locate hello web.config file and open it.</span></span>
3. <span data-ttu-id="db3b5-120">Zoek de sectie system.web Hallo in Hallo web.config-bestand en Hallo volgt regel toevoegen:</span><span class="sxs-lookup"><span data-stu-id="db3b5-120">In hello web.config file, locate hello system.web section and add hello following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="db3b5-121">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="db3b5-121">Save hello file.</span></span>
5. <span data-ttu-id="db3b5-122">Opnieuw verpakken en implementeer Hallo-service opnieuw.</span><span class="sxs-lookup"><span data-stu-id="db3b5-122">Repackage and redeploy hello service.</span></span>

<span data-ttu-id="db3b5-123">Wanneer het Hallo-service is geïmplementeerd, ziet u een foutbericht met de naam van de Hallo Hallo assembly- of DLL-bestand ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="db3b5-123">Once hello service is redeployed, you will see an error message with hello name of hello missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a><span data-ttu-id="db3b5-124">Problemen vaststellen door op afstand Hallo fout weer te geven</span><span class="sxs-lookup"><span data-stu-id="db3b5-124">Diagnose issues by viewing hello error remotely</span></span>
<span data-ttu-id="db3b5-125">U kunt Extern bureaublad tooaccess Hallo rol gebruiken en gedetailleerde foutinformatie extern weergeven.</span><span class="sxs-lookup"><span data-stu-id="db3b5-125">You can use Remote Desktop tooaccess hello role and view more complete error information remotely.</span></span> <span data-ttu-id="db3b5-126">Volgende stappen tooview Hallo fouten met behulp van extern bureaublad hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="db3b5-126">Use hello following steps tooview hello errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="db3b5-127">Zorg ervoor dat de Azure SDK 1.3 of hoger is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="db3b5-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="db3b5-128">Tijdens de implementatie van Hallo-oplossing met behulp van Visual Studio hello te kiezen '... verbindingen met extern bureaublad configureren'.</span><span class="sxs-lookup"><span data-stu-id="db3b5-128">During hello deployment of hello solution by using Visual Studio, choose too“Configure Remote Desktop connections…”.</span></span> <span data-ttu-id="db3b5-129">Zie voor meer informatie over het configureren van extern bureaublad-verbinding Hallo [met behulp van extern bureaublad met de Azure-rollen](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="db3b5-129">For more information on configuring hello Remote Desktop connection, see [Using Remote Desktop with Azure Roles](../vs-azure-tools-remote-desktop-roles.md).</span></span>
3. <span data-ttu-id="db3b5-130">In Hallo Microsoft klassieke Azure portal, zodra het Hallo-exemplaar wordt de status van **gereed**, klikt u op een Hallo rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="db3b5-130">In hello Microsoft Azure classic portal, once hello instance shows a status of **Ready**, click one of hello role instances.</span></span>
4. <span data-ttu-id="db3b5-131">Klikt u op Hallo **Connect** pictogram in Hallo **RAS** gebied van Hallo-lint.</span><span class="sxs-lookup"><span data-stu-id="db3b5-131">Click hello **Connect** icon in hello **Remote Access** area of hello ribbon.</span></span>
5. <span data-ttu-id="db3b5-132">Meld u toohello virtuele machine met behulp van Hallo-referenties die zijn opgegeven bij de configuratie van extern bureaublad Hallo.</span><span class="sxs-lookup"><span data-stu-id="db3b5-132">Sign in toohello virtual machine by using hello credentials that were specified during hello Remote Desktop configuration.</span></span>
6. <span data-ttu-id="db3b5-133">Open een opdrachtvenster.</span><span class="sxs-lookup"><span data-stu-id="db3b5-133">Open a command window.</span></span>
7. <span data-ttu-id="db3b5-134">Typ `IPconfig`.</span><span class="sxs-lookup"><span data-stu-id="db3b5-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="db3b5-135">Noteer de waarde van het Hallo IPV4-adres.</span><span class="sxs-lookup"><span data-stu-id="db3b5-135">Note hello IPV4 Address value.</span></span>
9. <span data-ttu-id="db3b5-136">Open Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="db3b5-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="db3b5-137">Typ Hallo-adres en de naam van de Hallo van Hallo-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="db3b5-137">Type hello address and hello name of hello web application.</span></span> <span data-ttu-id="db3b5-138">Bijvoorbeeld `http://<IPV4 Address>/default.aspx`.</span><span class="sxs-lookup"><span data-stu-id="db3b5-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="db3b5-139">Navigeren toohello retourneert website nu gedetailleerde foutberichten:</span><span class="sxs-lookup"><span data-stu-id="db3b5-139">Navigating toohello website will now return more explicit error messages:</span></span>

* <span data-ttu-id="db3b5-140">Serverfout in '/' toepassing.</span><span class="sxs-lookup"><span data-stu-id="db3b5-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="db3b5-141">Beschrijving: Er is een onverwerkte uitzondering opgetreden tijdens het uitvoeren van de huidige webaanvraag Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="db3b5-141">Description: An unhandled exception occurred during hello execution of hello current web request.</span></span> <span data-ttu-id="db3b5-142">Bekijk Hallo stacktracering voor meer informatie over de fout Hallo en oorsprong ervan in Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="db3b5-142">Please review hello stack trace for more information about hello error and where it originated in hello code.</span></span>
* <span data-ttu-id="db3b5-143">Details van uitzondering: System.IO.FIleNotFoundException: kan niet worden geladen, bestand of assembly ' Microsoft.WindowsAzure.StorageClient, versie 1.1.0.0, Culture = neutral, PublicKeyToken = 31bf856ad364e35 =' of een van de afhankelijkheden ervan.</span><span class="sxs-lookup"><span data-stu-id="db3b5-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="db3b5-144">Hallo vinden bestand niet Hallo opgegeven.</span><span class="sxs-lookup"><span data-stu-id="db3b5-144">hello system cannot find hello file specified.</span></span>

<span data-ttu-id="db3b5-145">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="db3b5-145">For example:</span></span>

![Expliciete Serverfout in '/' toepassing](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a><span data-ttu-id="db3b5-147">Problemen met behulp van de rekenemulator Hallo vaststellen</span><span class="sxs-lookup"><span data-stu-id="db3b5-147">Diagnose issues by using hello compute emulator</span></span>
<span data-ttu-id="db3b5-148">U kunt gebruiken Hallo Microsoft Azure compute-emulator toodiagnose en oplossen van problemen met ontbrekende afhankelijkheden en fouten van web.config.</span><span class="sxs-lookup"><span data-stu-id="db3b5-148">You can use hello Microsoft Azure compute emulator toodiagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="db3b5-149">Voor de beste resultaten bij het gebruik van deze methode van de diagnose van, moet u een computer of virtuele machine waarop een schone installatie van Windows is.</span><span class="sxs-lookup"><span data-stu-id="db3b5-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="db3b5-150">toobest hello Azure-omgeving te simuleren, gebruikt u Windows Server 2008 R2 x64.</span><span class="sxs-lookup"><span data-stu-id="db3b5-150">toobest simulate hello Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="db3b5-151">Installeer Hallo zelfstandige versie van Hallo [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="db3b5-151">Install hello standalone version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="db3b5-152">Op de ontwikkelcomputer hello, Hallo cloudserviceproject te bouwen.</span><span class="sxs-lookup"><span data-stu-id="db3b5-152">On hello development machine, build hello cloud service project.</span></span>
3. <span data-ttu-id="db3b5-153">Navigeer in Windows Verkenner toohello bin\debug map van Hallo cloudserviceproject.</span><span class="sxs-lookup"><span data-stu-id="db3b5-153">In Windows Explorer, navigate toohello bin\debug folder of hello cloud service project.</span></span>
4. <span data-ttu-id="db3b5-154">Hallo .csx map- en .cscfg-bestand toohello computer dat u van toodebug Hallo problemen gebruikmaakt kopiëren.</span><span class="sxs-lookup"><span data-stu-id="db3b5-154">Copy hello .csx folder and .cscfg file toohello computer that you are using toodebug hello issues.</span></span>
5. <span data-ttu-id="db3b5-155">Open op Hallo schone computer, een Azure SDK-opdrachtpromptvenster en typ `csrun.exe /devstore:start`.</span><span class="sxs-lookup"><span data-stu-id="db3b5-155">On hello clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="db3b5-156">Typ het volgende achter de opdrachtprompt Hallo `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.</span><span class="sxs-lookup"><span data-stu-id="db3b5-156">At hello command prompt, type `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="db3b5-157">Wanneer de rol Hallo wordt gestart, ziet u de gedetailleerde foutinformatie in Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="db3b5-157">When hello role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="db3b5-158">U kunt ook de standaard-Windows-hulpprogramma's voor probleemoplossing toofurther diagnose Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="db3b5-158">You can also use standard Windows troubleshooting tools toofurther diagnose hello problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="db3b5-159">Problemen met behulp van IntelliTrace vaststellen</span><span class="sxs-lookup"><span data-stu-id="db3b5-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="db3b5-160">Voor worker en webservice-functies die er gebruik van .NET Framework 4, kunt u [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), die beschikbaar is in Microsoft Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="db3b5-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="db3b5-161">Volg deze stappen toodeploy Hallo-service met IntelliTrace ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="db3b5-161">Follow these steps toodeploy hello service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="db3b5-162">Controleer of de Azure SDK 1.3 of hoger is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="db3b5-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="db3b5-163">Hallo-oplossing implementeren met behulp van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db3b5-163">Deploy hello solution by using Visual Studio.</span></span> <span data-ttu-id="db3b5-164">Tijdens de implementatie controleren Hallo **IntelliTrace inschakelen voor .NET 4 rollen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="db3b5-164">During deployment, check hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="db3b5-165">Zodra het Hallo-exemplaar wordt gestart, opent u Hallo **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="db3b5-165">Once hello instance starts, open hello **Server Explorer**.</span></span>
4. <span data-ttu-id="db3b5-166">Vouw Hallo **Azure\\Cloudservices** knooppunt en zoek Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="db3b5-166">Expand hello **Azure\\Cloud Services** node and locate hello deployment.</span></span>
5. <span data-ttu-id="db3b5-167">Vouw Hallo implementatie totdat er Hallo rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="db3b5-167">Expand hello deployment until you see hello role instances.</span></span> <span data-ttu-id="db3b5-168">Met de rechtermuisknop op een van de Hallo-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="db3b5-168">Right-click on one of hello instances.</span></span>
6. <span data-ttu-id="db3b5-169">Kies **weergave IntelliTrace-logboeken**.</span><span class="sxs-lookup"><span data-stu-id="db3b5-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="db3b5-170">Hallo **IntelliTrace samenvatting** wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="db3b5-170">hello **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="db3b5-171">Ga naar Hallo uitzonderingen sectie Hallo samenvatting.</span><span class="sxs-lookup"><span data-stu-id="db3b5-171">Locate hello exceptions section of hello summary.</span></span> <span data-ttu-id="db3b5-172">Als er uitzonderingen, Hallo sectie heet **uitzonderingsgegevens**.</span><span class="sxs-lookup"><span data-stu-id="db3b5-172">If there are exceptions, hello section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="db3b5-173">Vouw Hallo **uitzonderingsgegevens** en zoekt u **System.IO.FileNotFoundException** fouten vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="db3b5-173">Expand hello **Exception Data** and look for **System.IO.FileNotFoundException** errors similar toohello following:</span></span>

![Uitzonderingsgegevens, ontbreekt een bestand of assembly](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="db3b5-175">Adres van de ontbrekende dll's en verzamelingen</span><span class="sxs-lookup"><span data-stu-id="db3b5-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="db3b5-176">DLL-bestand en de assembly-fouten, ontbrekende tooaddress als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="db3b5-176">tooaddress missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="db3b5-177">Hallo-oplossing in Visual Studio openen.</span><span class="sxs-lookup"><span data-stu-id="db3b5-177">Open hello solution in Visual Studio.</span></span>
2. <span data-ttu-id="db3b5-178">In **Solution Explorer**Open Hallo **verwijzingen** map.</span><span class="sxs-lookup"><span data-stu-id="db3b5-178">In **Solution Explorer**, open hello **References** folder.</span></span>
3. <span data-ttu-id="db3b5-179">Klik op Hallo assembly in Hallo fout geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="db3b5-179">Click hello assembly identified in hello error.</span></span>
4. <span data-ttu-id="db3b5-180">In Hallo **eigenschappen** deelvenster, zoek **lokale kopie van de eigenschap** en stelt u Hallo waarde te**True**.</span><span class="sxs-lookup"><span data-stu-id="db3b5-180">In hello **Properties** pane, locate **Copy Local property** and set hello value too**True**.</span></span>
5. <span data-ttu-id="db3b5-181">Implementeer Hallo cloud-service opnieuw in.</span><span class="sxs-lookup"><span data-stu-id="db3b5-181">Redeploy hello cloud service.</span></span>

<span data-ttu-id="db3b5-182">Zodra u hebt gecontroleerd dat alle fouten hebt gecorrigeerd, kunt u Hallo service implementeren zonder te controleren of Hallo **IntelliTrace inschakelen voor .NET 4 rollen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="db3b5-182">Once you have verified that all errors have been corrected, you can deploy hello service without checking hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db3b5-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="db3b5-183">Next steps</span></span>
<span data-ttu-id="db3b5-184">Meer [probleemoplossing artikelen](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) voor cloudservices.</span><span class="sxs-lookup"><span data-stu-id="db3b5-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="db3b5-185">Zie hoe tootroubleshoot cloud service rol problemen met behulp van Azure PaaS computer diagnostische gegevens toolearn [blogreeks van Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="db3b5-185">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
