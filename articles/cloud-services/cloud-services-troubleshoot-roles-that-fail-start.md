---
title: Functies die niet worden gestart oplossen | Microsoft Docs
description: Hier volgen enkele veelvoorkomende redenen waarom een Service in de Cloud-rol kan niet worden gestart. Oplossingen voor deze problemen worden ook gegeven.
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
ms.openlocfilehash: 7d956192e8b9c3688b8b6f0108bd9296f66fbd62
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-to-start"></a><span data-ttu-id="c437c-104">Problemen met Cloud Service-functies die niet worden gestart</span><span class="sxs-lookup"><span data-stu-id="c437c-104">Troubleshoot Cloud Service roles that fail to start</span></span>
<span data-ttu-id="c437c-105">Hier volgen enkele veelvoorkomende problemen en oplossingen die zijn gerelateerd aan Azure Cloud Services functies die niet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="c437c-105">Here are some common problems and solutions related to Azure Cloud Services roles that fail to start.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="c437c-106">Ontbrekende dll's of afhankelijkheden</span><span class="sxs-lookup"><span data-stu-id="c437c-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="c437c-107">Niet-reagerende rollen en functies die zijn functioneert tussen **Bezig met initialiseren**, **bezet**, en **stoppen** statussen kunnen zijn veroorzaakt door ontbrekende dll-bestanden of assembly's.</span><span class="sxs-lookup"><span data-stu-id="c437c-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="c437c-108">Problemen met ontbrekende dll's of assembly's zijn:</span><span class="sxs-lookup"><span data-stu-id="c437c-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="c437c-109">De rolinstantie is doorlopen **Bezig met initialiseren**, **bezet**, en **stoppen** statussen.</span><span class="sxs-lookup"><span data-stu-id="c437c-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="c437c-110">Uw rolexemplaar is verplaatst naar **gereed** maar als u uw webtoepassing navigeert, wordt de pagina wordt niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c437c-110">Your role instance has moved to **Ready** but if you navigate to your web application, the page does not appear.</span></span>

<span data-ttu-id="c437c-111">Er zijn verschillende aanbevolen methoden om deze problemen te onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="c437c-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="c437c-112">Vaststellen van problemen met ontbrekende dll-bestand in een Webrol</span><span class="sxs-lookup"><span data-stu-id="c437c-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="c437c-113">Wanneer u navigeren naar een website die wordt geïmplementeerd in een web-rol en de browser een vergelijkbaar met de volgende serverfout wordt weergegeven, kan dit wijzen op een DLL-bestand ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="c437c-113">When you navigate to a website that is deployed in a web role, and the browser displays a server error similar to the following, it may indicate that a DLL is missing.</span></span>

![Serverfout in '/' toepassing.](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="c437c-115">Problemen vaststellen door het uitschakelen van aangepaste fouten</span><span class="sxs-lookup"><span data-stu-id="c437c-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="c437c-116">Gedetailleerde foutinformatie kan worden weergegeven door het configureren van het bestand web.config voor de Webrol in de aangepaste fout-modus instellen op uitgeschakeld en opnieuw distribueren van de service.</span><span class="sxs-lookup"><span data-stu-id="c437c-116">More complete error information can be viewed by configuring the web.config for the web role to set the custom error mode to Off and redeploying the service.</span></span>

<span data-ttu-id="c437c-117">Gedetailleerde fouten zonder gebruik van extern bureaublad weergeven:</span><span class="sxs-lookup"><span data-stu-id="c437c-117">To view more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="c437c-118">Open de oplossing in Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c437c-118">Open the solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="c437c-119">In de **Solution Explorer**en zoek het bestand web.config en open deze.</span><span class="sxs-lookup"><span data-stu-id="c437c-119">In the **Solution Explorer**, locate the web.config file and open it.</span></span>
3. <span data-ttu-id="c437c-120">In het bestand web.config, zoek naar de sectie system.web en voeg de volgende regel:</span><span class="sxs-lookup"><span data-stu-id="c437c-120">In the web.config file, locate the system.web section and add the following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="c437c-121">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="c437c-121">Save the file.</span></span>
5. <span data-ttu-id="c437c-122">Opnieuw verpakken en implementeer de service opnieuw.</span><span class="sxs-lookup"><span data-stu-id="c437c-122">Repackage and redeploy the service.</span></span>

<span data-ttu-id="c437c-123">Wanneer de service is geïmplementeerd, ziet u een foutbericht met de naam van de ontbrekende assembly- of DLL-bestand.</span><span class="sxs-lookup"><span data-stu-id="c437c-123">Once the service is redeployed, you will see an error message with the name of the missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-the-error-remotely"></a><span data-ttu-id="c437c-124">Problemen vaststellen door het bekijken van de fout op afstand</span><span class="sxs-lookup"><span data-stu-id="c437c-124">Diagnose issues by viewing the error remotely</span></span>
<span data-ttu-id="c437c-125">U kunt Extern bureaublad gebruiken voor toegang tot de rol en gedetailleerde foutinformatie extern weergeven.</span><span class="sxs-lookup"><span data-stu-id="c437c-125">You can use Remote Desktop to access the role and view more complete error information remotely.</span></span> <span data-ttu-id="c437c-126">Gebruik de volgende stappen om de fouten met behulp van extern bureaublad weer te geven:</span><span class="sxs-lookup"><span data-stu-id="c437c-126">Use the following steps to view the errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="c437c-127">Zorg ervoor dat de Azure SDK 1.3 of hoger is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="c437c-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="c437c-128">Tijdens de implementatie van de oplossing met behulp van Visual Studio, ervoor kiezen om 'Configureren extern-bureaubladverbindingen...'.</span><span class="sxs-lookup"><span data-stu-id="c437c-128">During the deployment of the solution by using Visual Studio, choose to “Configure Remote Desktop connections…”.</span></span> <span data-ttu-id="c437c-129">Zie voor meer informatie over het configureren van de verbinding met extern bureaublad [met behulp van extern bureaublad met de Azure-rollen](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="c437c-129">For more information on configuring the Remote Desktop connection, see [Using Remote Desktop with Azure Roles](../vs-azure-tools-remote-desktop-roles.md).</span></span>
3. <span data-ttu-id="c437c-130">In de Microsoft Azure klassieke portal, zodra het exemplaar de status van wordt **gereed**, klikt u op een van de rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="c437c-130">In the Microsoft Azure classic portal, once the instance shows a status of **Ready**, click one of the role instances.</span></span>
4. <span data-ttu-id="c437c-131">Klik op de **Connect** pictogram in de **RAS** gebied van het lint.</span><span class="sxs-lookup"><span data-stu-id="c437c-131">Click the **Connect** icon in the **Remote Access** area of the ribbon.</span></span>
5. <span data-ttu-id="c437c-132">Meld u aan de virtuele machine met de referenties die zijn opgegeven tijdens de configuratie van extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="c437c-132">Sign in to the virtual machine by using the credentials that were specified during the Remote Desktop configuration.</span></span>
6. <span data-ttu-id="c437c-133">Open een opdrachtvenster.</span><span class="sxs-lookup"><span data-stu-id="c437c-133">Open a command window.</span></span>
7. <span data-ttu-id="c437c-134">Typ `IPconfig`.</span><span class="sxs-lookup"><span data-stu-id="c437c-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="c437c-135">Noteer de waarde van de IPV4-adres.</span><span class="sxs-lookup"><span data-stu-id="c437c-135">Note the IPV4 Address value.</span></span>
9. <span data-ttu-id="c437c-136">Open Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="c437c-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="c437c-137">Typ het adres en de naam van de webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="c437c-137">Type the address and the name of the web application.</span></span> <span data-ttu-id="c437c-138">Bijvoorbeeld `http://<IPV4 Address>/default.aspx`.</span><span class="sxs-lookup"><span data-stu-id="c437c-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="c437c-139">Navigeren naar de website, wordt er nu meer uitgebreide foutberichten geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="c437c-139">Navigating to the website will now return more explicit error messages:</span></span>

* <span data-ttu-id="c437c-140">Serverfout in '/' toepassing.</span><span class="sxs-lookup"><span data-stu-id="c437c-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="c437c-141">Beschrijving: Er is een onverwerkte uitzondering opgetreden tijdens het uitvoeren van de huidige webaanvraag.</span><span class="sxs-lookup"><span data-stu-id="c437c-141">Description: An unhandled exception occurred during the execution of the current web request.</span></span> <span data-ttu-id="c437c-142">Raadpleeg de stacktracering voor meer informatie over de fout en de oorsprong ervan in de code.</span><span class="sxs-lookup"><span data-stu-id="c437c-142">Please review the stack trace for more information about the error and where it originated in the code.</span></span>
* <span data-ttu-id="c437c-143">Details van uitzondering: System.IO.FIleNotFoundException: kan niet worden geladen, bestand of assembly ' Microsoft.WindowsAzure.StorageClient, versie 1.1.0.0, Culture = neutral, PublicKeyToken = 31bf856ad364e35 =' of een van de afhankelijkheden ervan.</span><span class="sxs-lookup"><span data-stu-id="c437c-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="c437c-144">Het systeem kan het opgegeven bestand niet vinden.</span><span class="sxs-lookup"><span data-stu-id="c437c-144">The system cannot find the file specified.</span></span>

<span data-ttu-id="c437c-145">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c437c-145">For example:</span></span>

![Expliciete Serverfout in '/' toepassing](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-the-compute-emulator"></a><span data-ttu-id="c437c-147">Problemen met behulp van de rekenemulator vaststellen</span><span class="sxs-lookup"><span data-stu-id="c437c-147">Diagnose issues by using the compute emulator</span></span>
<span data-ttu-id="c437c-148">De Microsoft Azure-rekenemulator kunt u vaststellen en oplossen van problemen met ontbrekende afhankelijkheden en fouten van web.config.</span><span class="sxs-lookup"><span data-stu-id="c437c-148">You can use the Microsoft Azure compute emulator to diagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="c437c-149">Voor de beste resultaten bij het gebruik van deze methode van de diagnose van, moet u een computer of virtuele machine waarop een schone installatie van Windows is.</span><span class="sxs-lookup"><span data-stu-id="c437c-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="c437c-150">Gebruik voor het beste de Azure-omgeving nabootsen, Windows Server 2008 R2 x64.</span><span class="sxs-lookup"><span data-stu-id="c437c-150">To best simulate the Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="c437c-151">Installeer de zelfstandige versie van de [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c437c-151">Install the standalone version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="c437c-152">Bouw het cloudserviceproject op de ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="c437c-152">On the development machine, build the cloud service project.</span></span>
3. <span data-ttu-id="c437c-153">Navigeer in Windows Verkenner naar de map bin\debug van het cloudserviceproject.</span><span class="sxs-lookup"><span data-stu-id="c437c-153">In Windows Explorer, navigate to the bin\debug folder of the cloud service project.</span></span>
4. <span data-ttu-id="c437c-154">Kopieer het .csx map- en .cscfg-bestand op de computer die u gebruikt voor fouten opsporen in de problemen.</span><span class="sxs-lookup"><span data-stu-id="c437c-154">Copy the .csx folder and .cscfg file to the computer that you are using to debug the issues.</span></span>
5. <span data-ttu-id="c437c-155">Open een venster van de Azure SDK-opdrachtprompt en typ op de computer schoon `csrun.exe /devstore:start`.</span><span class="sxs-lookup"><span data-stu-id="c437c-155">On the clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="c437c-156">Typ het volgende achter de opdrachtprompt `run csrun <path to .csx folder> <path to .cscfg file> /launchBrowser`.</span><span class="sxs-lookup"><span data-stu-id="c437c-156">At the command prompt, type `run csrun <path to .csx folder> <path to .cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="c437c-157">Wanneer de functie wordt gestart, ziet u de gedetailleerde foutinformatie in Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="c437c-157">When the role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="c437c-158">U kunt ook de standaard-Windows-hulpprogramma's voor probleemoplossing gebruiken voor verdere diagnose van het probleem.</span><span class="sxs-lookup"><span data-stu-id="c437c-158">You can also use standard Windows troubleshooting tools to further diagnose the problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="c437c-159">Problemen met behulp van IntelliTrace vaststellen</span><span class="sxs-lookup"><span data-stu-id="c437c-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="c437c-160">Voor worker en webservice-functies die er gebruik van .NET Framework 4, kunt u [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), die beschikbaar is in Microsoft Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="c437c-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="c437c-161">Volg deze stappen voor het implementeren van de service met IntelliTrace ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="c437c-161">Follow these steps to deploy the service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="c437c-162">Controleer of de Azure SDK 1.3 of hoger is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="c437c-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="c437c-163">De oplossing implementeren met behulp van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c437c-163">Deploy the solution by using Visual Studio.</span></span> <span data-ttu-id="c437c-164">Controleer tijdens de implementatie van de **IntelliTrace inschakelen voor .NET 4 rollen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="c437c-164">During deployment, check the **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="c437c-165">Zodra het exemplaar wordt gestart, opent u de **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="c437c-165">Once the instance starts, open the **Server Explorer**.</span></span>
4. <span data-ttu-id="c437c-166">Vouw de **Azure\\Cloudservices** knooppunt en zoek de implementatie.</span><span class="sxs-lookup"><span data-stu-id="c437c-166">Expand the **Azure\\Cloud Services** node and locate the deployment.</span></span>
5. <span data-ttu-id="c437c-167">Vouw de implementatie uit totdat u de rolexemplaren ziet.</span><span class="sxs-lookup"><span data-stu-id="c437c-167">Expand the deployment until you see the role instances.</span></span> <span data-ttu-id="c437c-168">Met de rechtermuisknop op een van de exemplaren.</span><span class="sxs-lookup"><span data-stu-id="c437c-168">Right-click on one of the instances.</span></span>
6. <span data-ttu-id="c437c-169">Kies **weergave IntelliTrace-logboeken**.</span><span class="sxs-lookup"><span data-stu-id="c437c-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="c437c-170">De **IntelliTrace samenvatting** wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c437c-170">The **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="c437c-171">Zoek de sectie uitzonderingen van de samenvatting.</span><span class="sxs-lookup"><span data-stu-id="c437c-171">Locate the exceptions section of the summary.</span></span> <span data-ttu-id="c437c-172">Als er uitzonderingen zijn, de sectie heet **uitzonderingsgegevens**.</span><span class="sxs-lookup"><span data-stu-id="c437c-172">If there are exceptions, the section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="c437c-173">Vouw de **uitzonderingsgegevens** en zoekt u **System.IO.FileNotFoundException** vergelijkbaar met de volgende fouten:</span><span class="sxs-lookup"><span data-stu-id="c437c-173">Expand the **Exception Data** and look for **System.IO.FileNotFoundException** errors similar to the following:</span></span>

![Uitzonderingsgegevens, ontbreekt een bestand of assembly](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="c437c-175">Adres van de ontbrekende dll's en verzamelingen</span><span class="sxs-lookup"><span data-stu-id="c437c-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="c437c-176">Ontbrekende dll-bestand en assembly fouten oplossen, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c437c-176">To address missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="c437c-177">Open de oplossing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c437c-177">Open the solution in Visual Studio.</span></span>
2. <span data-ttu-id="c437c-178">In **Solution Explorer**, open de **verwijzingen** map.</span><span class="sxs-lookup"><span data-stu-id="c437c-178">In **Solution Explorer**, open the **References** folder.</span></span>
3. <span data-ttu-id="c437c-179">Klik op de assembly die is geïdentificeerd in de fout.</span><span class="sxs-lookup"><span data-stu-id="c437c-179">Click the assembly identified in the error.</span></span>
4. <span data-ttu-id="c437c-180">In de **eigenschappen** deelvenster, zoek **lokale kopie van de eigenschap** en stel de waarde op **True**.</span><span class="sxs-lookup"><span data-stu-id="c437c-180">In the **Properties** pane, locate **Copy Local property** and set the value to **True**.</span></span>
5. <span data-ttu-id="c437c-181">Implementeer de cloudservice opnieuw.</span><span class="sxs-lookup"><span data-stu-id="c437c-181">Redeploy the cloud service.</span></span>

<span data-ttu-id="c437c-182">Zodra u hebt gecontroleerd dat alle fouten hebt gecorrigeerd, kunt u de service implementeren zonder te controleren of de **IntelliTrace inschakelen voor .NET 4 rollen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="c437c-182">Once you have verified that all errors have been corrected, you can deploy the service without checking the **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c437c-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c437c-183">Next steps</span></span>
<span data-ttu-id="c437c-184">Meer [probleemoplossing artikelen](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) voor cloudservices.</span><span class="sxs-lookup"><span data-stu-id="c437c-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="c437c-185">Zie voor meer informatie over het oplossen van problemen met de rol van de cloud service met behulp van Azure PaaS computer diagnostics-gegevens, [blogreeks van Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="c437c-185">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
