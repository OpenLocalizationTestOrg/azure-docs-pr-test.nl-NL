---
title: Continue leveringsmethode voor cloud services met Visual Studio Online | Microsoft Docs
description: Meer informatie over het instellen van continue leveringsmethode voor Azure cloud-apps zonder opslagsleutel diagnostische gegevens opslaan in de configuratiebestanden van de service
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 7e70f92d4d1333ca6cbac5876e5ccbc763bd915c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-to-azure-using-visual-studio-online"></a><span data-ttu-id="11fd8-103">Securely Cloud Services Diagnostics opslagsleutel opslaan en Setup continue integratie en implementatie naar Azure met Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="11fd8-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment to Azure using Visual Studio Online</span></span>
 <span data-ttu-id="11fd8-104">Het is een gebruikelijk om bronprojecten te openen tegenwoordig.</span><span class="sxs-lookup"><span data-stu-id="11fd8-104">It is a common practice to open source projects nowadays.</span></span> <span data-ttu-id="11fd8-105">Opslaan van de toepassing geheimen in configuratiebestanden is niet meer veilig practice als beveiligingsrisico's beschikbaar worden gesteld van geheimen van besturingselementen voor openbare gegevensbronnen wordt gelekt.</span><span class="sxs-lookup"><span data-stu-id="11fd8-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="11fd8-106">Geheim opslaan als tekst zonder opmaak in een bestand in een pijplijn continue integratie niet beveiligd is ofwel omdat buildservers kunnen worden gedeeld met resources op de cloudomgeving.</span><span class="sxs-lookup"><span data-stu-id="11fd8-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on the Cloud environment.</span></span> <span data-ttu-id="11fd8-107">Dit artikel wordt uitgelegd hoe Visual Studio en Visual Studio Online vermindert de beveiligingsproblemen tijdens ontwikkeling en het proces voor continue integratie.</span><span class="sxs-lookup"><span data-stu-id="11fd8-107">This article explains how Visual Studio and Visual Studio Online mitigates the security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="11fd8-108">Diagnostische gegevens opslag sleutel geheim verwijderen in het configuratiebestand van Project</span><span class="sxs-lookup"><span data-stu-id="11fd8-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="11fd8-109">Extensie voor diagnostische gegevens van cloud-Services vereist Azure-opslag voor het opslaan van resultaten van de diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="11fd8-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="11fd8-110">Voorheen de verbindingsreeks voor opslag is opgegeven in de Cloud Services-configuratiebestanden (.cscfg) en kan worden ingecheckt met resourcebeheer.</span><span class="sxs-lookup"><span data-stu-id="11fd8-110">Formerly the storage connection string is specified in the Cloud Services configuration (.cscfg) files and could be checked in to source control.</span></span> <span data-ttu-id="11fd8-111">In de nieuwste Azure SDK-versie gewijzigd we het gedrag voor het opslaan van slechts een gedeeltelijke verbindingsreeks met de sleutel vervangen door een token.</span><span class="sxs-lookup"><span data-stu-id="11fd8-111">In the latest Azure SDK release we changed the behavior to only store a partial connection string with the key replaced by a token.</span></span> <span data-ttu-id="11fd8-112">De volgende stappen wordt beschreven hoe de nieuwe Cloudservices tooling werkt:</span><span class="sxs-lookup"><span data-stu-id="11fd8-112">The following steps describe how the new Cloud Services tooling works:</span></span>

### <a name="1-open-the-role-designer"></a><span data-ttu-id="11fd8-113">1. Open de rol designer</span><span class="sxs-lookup"><span data-stu-id="11fd8-113">1. Open the Role designer</span></span>
* <span data-ttu-id="11fd8-114">Dubbelklik op of klik met de rechtermuisknop op een Cloud Services-rol rol designer openen</span><span class="sxs-lookup"><span data-stu-id="11fd8-114">Double click or right click on a Cloud Services role to open Role designer</span></span>

![Rol openen designer][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="11fd8-116">2. Onder de sectie diagnostische gegevens, het selectievakje nieuwe 'niet verwijderen geheim project-opslagsleutel' is toegevoegd</span><span class="sxs-lookup"><span data-stu-id="11fd8-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="11fd8-117">Als u van de emulator van de lokale opslag gebruikmaakt, dit selectievakje is uitgeschakeld omdat er geen geheim beheren voor de lokale verbindingsreeks, UseDevelopmentStorage = true.</span><span class="sxs-lookup"><span data-stu-id="11fd8-117">If you are using the local storage emulator, this checkbox is disabled because there is no secret to manage for the local connection string, which is UseDevelopmentStorage=true.</span></span>

![Lokale opslag emulator-verbindingstekenreeks is geen geheime][1]

* <span data-ttu-id="11fd8-119">Als u een nieuw project maakt, zijn is dit selectievakje standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="11fd8-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="11fd8-120">Dit resulteert in de belangrijkste sectie van de opslag van de geselecteerde opslagverbindingsreeks wordt vervangen door een token.</span><span class="sxs-lookup"><span data-stu-id="11fd8-120">This results in the storage key section of the selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="11fd8-121">De waarde van het token worden gevonden in de huidige gebruiker AppData Roaming map, bijvoorbeeld: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span><span class="sxs-lookup"><span data-stu-id="11fd8-121">The value of the token will be found under the current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="11fd8-122">Houd er rekening mee dat de map user\AppData toegang beheerd door de gebruiker zich aanmelden en wordt beschouwd als een veilige plaats voor het opslaan van ontwikkeling geheimen.</span><span class="sxs-lookup"><span data-stu-id="11fd8-122">Note that the user\AppData folder is Access Controlled by user sign-in and is considered a secure place to store development secrets.</span></span>
> 
> 

![Opslagsleutel wordt opgeslagen in de gebruikersprofielmap][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="11fd8-124">3. Selecteer een opslagaccount voor diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="11fd8-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="11fd8-125">Selecteer een opslagaccount van het dialoogvenster gestart door te klikken op de '...'</span><span class="sxs-lookup"><span data-stu-id="11fd8-125">Select a storage account from the dialog launched by clicking the “…”</span></span> <span data-ttu-id="11fd8-126">te klikken.</span><span class="sxs-lookup"><span data-stu-id="11fd8-126">button.</span></span> <span data-ttu-id="11fd8-127">U ziet hoe de verbindingsreeks voor de opslag gegenereerde geen sleutel van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="11fd8-127">Notice how the storage connection string generated will not have the storage account key.</span></span>
* <span data-ttu-id="11fd8-128">Bijvoorbeeld: DefaultEndpointsProtocol = https; AccountName = contosostorage; AccountKey = $(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="11fd8-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-the-project"></a><span data-ttu-id="11fd8-129">4.    Foutopsporing voor het project</span><span class="sxs-lookup"><span data-stu-id="11fd8-129">4.    Debugging the project</span></span>
* <span data-ttu-id="11fd8-130">F5 in Visual Studio foutopsporing te starten.</span><span class="sxs-lookup"><span data-stu-id="11fd8-130">F5 to start debugging in Visual Studio.</span></span> <span data-ttu-id="11fd8-131">Alles wat u moet werken op dezelfde manier als voor.</span><span class="sxs-lookup"><span data-stu-id="11fd8-131">Everything should work in the same way as before.</span></span>
  <span data-ttu-id="11fd8-132">![Lokaal foutopsporing starten][3]</span><span class="sxs-lookup"><span data-stu-id="11fd8-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="11fd8-133">5. Visual Studio-project publiceren</span><span class="sxs-lookup"><span data-stu-id="11fd8-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="11fd8-134">Start het dialoogvenster publiceren en verdergaan met het aanmelden instructies voor het publiceren van de applicaion naar Azure.</span><span class="sxs-lookup"><span data-stu-id="11fd8-134">Launch the publish dialog and proceed with sign-in instructions to publish the applicaion to Azure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="11fd8-135">6. Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="11fd8-135">6. Additional information</span></span>
> <span data-ttu-id="11fd8-136">Opmerking: Het paneel met toepassingsinstellingen in de ontwerpfunctie voor rol blijven omdat deze nu.</span><span class="sxs-lookup"><span data-stu-id="11fd8-136">Note: The Settings panel in the role designer will stay as it is for now.</span></span> <span data-ttu-id="11fd8-137">Als u gebruiken van de geheime beheerfunctie voor diagnostische gegevens wilt, gaat u naar het tabblad configuraties.</span><span class="sxs-lookup"><span data-stu-id="11fd8-137">If you want to use the secret management feature for diagnostics, go to the Configurations tab.</span></span>
> 
> 

![Instellingen toevoegen][4]

> <span data-ttu-id="11fd8-139">Opmerking: Als ingeschakeld, de Application Insights-sleutel wordt opgeslagen als tekst zonder opmaak.</span><span class="sxs-lookup"><span data-stu-id="11fd8-139">Note: If enabled, the Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="11fd8-140">De sleutel wordt alleen gebruikt voor het uploaden van inhoud, dus geen gevoelige gegevens risico wordt aangetast.</span><span class="sxs-lookup"><span data-stu-id="11fd8-140">The key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="11fd8-141">Maken en publiceren van een Cloud Services-Project met behulp van Visual Studio online taaksjablonen</span><span class="sxs-lookup"><span data-stu-id="11fd8-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="11fd8-142">De volgende stappen ziet u hoe continue integratie instellen voor Cloud Services-project met behulp van Visual Studio online taken:</span><span class="sxs-lookup"><span data-stu-id="11fd8-142">The following steps illustrates how to setup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="11fd8-143">1.    Een account VSO verkrijgen</span><span class="sxs-lookup"><span data-stu-id="11fd8-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="11fd8-144">[Visual Studio Online-account maken] [ Create Visual Studio Online account] als u nog niet hebt</span><span class="sxs-lookup"><span data-stu-id="11fd8-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="11fd8-145">[Maken van teamproject] [ Create team project] in uw Visual Studio online-account</span><span class="sxs-lookup"><span data-stu-id="11fd8-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="11fd8-146">2.    Setup van broncodebeheer in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="11fd8-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="11fd8-147">Verbinding maken met een teamproject</span><span class="sxs-lookup"><span data-stu-id="11fd8-147">Connect to a team project</span></span>

![Verbinding maken met teamproject][5]

![Selecteer teamproject verbinding maken met][6]

* <span data-ttu-id="11fd8-150">Uw project toevoegen aan bronbeheer</span><span class="sxs-lookup"><span data-stu-id="11fd8-150">Add your project to source control</span></span>

![Project toevoegen aan bronbeheer][7]

![Project worden toegewezen aan een besturingselement bronmap][8]

* <span data-ttu-id="11fd8-153">Controleer in uw project vanuit de Explorer-Team</span><span class="sxs-lookup"><span data-stu-id="11fd8-153">Check in your project from Team Explorer</span></span>

![Controleer in het project met resourcebeheer][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="11fd8-155">3.    Buildproces configureren</span><span class="sxs-lookup"><span data-stu-id="11fd8-155">3.    Configure Build process</span></span>
* <span data-ttu-id="11fd8-156">Blader naar uw teamproject en voegt u een nieuwe buildproces sjablonen</span><span class="sxs-lookup"><span data-stu-id="11fd8-156">Browse to your team project and add a new build process Templates</span></span>

![Een nieuwe build toevoegen][10]

* <span data-ttu-id="11fd8-158">Selecteer opbouwtaak</span><span class="sxs-lookup"><span data-stu-id="11fd8-158">Select build task</span></span>

![Een taak build toevoegen][11]

![Visual Studio bouwen taak sjabloon selecteren][12]

* <span data-ttu-id="11fd8-161">Build taak invoer bewerken.</span><span class="sxs-lookup"><span data-stu-id="11fd8-161">Edit build task input.</span></span> <span data-ttu-id="11fd8-162">Controleer de parameters build volgens uw behoeften aanpassen</span><span class="sxs-lookup"><span data-stu-id="11fd8-162">Please customize the build parameters according to your need</span></span>

![Opbouwtaak configureren][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="11fd8-164">Build variabelen configureren</span><span class="sxs-lookup"><span data-stu-id="11fd8-164">Configure build variables</span></span>

![Build variabelen configureren][14]

* <span data-ttu-id="11fd8-166">Toevoegen van een taak voor het uploaden van build neerzetten</span><span class="sxs-lookup"><span data-stu-id="11fd8-166">Add a task to upload build drop</span></span>

![Kies neerzetten opbouwtaak publiceren][15]

![Configureer neerzetten opbouwtaak publiceren][16]

* <span data-ttu-id="11fd8-169">De build uitvoeren</span><span class="sxs-lookup"><span data-stu-id="11fd8-169">Run the build</span></span>

![Nieuwe Wachtrijvorming][17]

![Overzicht van de build weergeven][18]

* <span data-ttu-id="11fd8-172">Als de build geslaagd is ziet u een resultaat vergelijkbaar met hieronder</span><span class="sxs-lookup"><span data-stu-id="11fd8-172">if the build is successful you will see a result similar to below</span></span>

![Resultaat bouwen][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="11fd8-174">4.    Release-proces configureren</span><span class="sxs-lookup"><span data-stu-id="11fd8-174">4.    Configure Release process</span></span>
* <span data-ttu-id="11fd8-175">Een nieuwe release gemaakt</span><span class="sxs-lookup"><span data-stu-id="11fd8-175">Create a new release</span></span>

![Nieuwe release gemaakt][20]

* <span data-ttu-id="11fd8-177">Selecteer de implementatie van Azure Cloud Services-taak</span><span class="sxs-lookup"><span data-stu-id="11fd8-177">Select the Azure Cloud Services Deployment task</span></span>

![Selecteer taak voor Azure Cloud Services-implementatie][21]

* <span data-ttu-id="11fd8-179">Als de sleutel van het opslagaccount met resourcebeheer niet is ingeschakeld, moeten we de geheime sleutel voor het instellen van extensies van diagnostische gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="11fd8-179">As the storage account key is not checked in to source control, we need to specify the secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="11fd8-180">Vouw de **geavanceerde opties voor nieuwe Service maken** sectie en bewerkt u de **toegangscodes voor opslag van diagnostische gegevens** parameter invoer.</span><span class="sxs-lookup"><span data-stu-id="11fd8-180">Expand the **Advanced Options for Creating New Service** section and edit the **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="11fd8-181">Deze invoer nodig is op meerdere regels van sleutel-waardepaar in de indeling van **[RoleName]:$(StorageAccountKey)**</span><span class="sxs-lookup"><span data-stu-id="11fd8-181">This input takes in multiple lines of key value pair in the format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="11fd8-182">Opmerking: als uw opslagaccount voor diagnostische gegevens onder hetzelfde abonnement is als waar u de Cloud Services-toepassing wilt publiceren, hebt u niet in te voeren van de sleutel in de invoer van de implementatie taak; de implementatie wordt programmatisch de storage-gegevens ophalen uit uw abonnement</span><span class="sxs-lookup"><span data-stu-id="11fd8-182">Note: if your diagnostics storage account is under the same subscription as where you will publish the Cloud Services application, you don't have to enter the key in the deployment task input; the deployment will programmatically obtain the storage information from your subscription</span></span>
> 
> 

![Taak voor Cloud Services-implementatie configureren][22]

* <span data-ttu-id="11fd8-184">Gebruik geheim bouwen variabelen Opslagsleutels opslaan.</span><span class="sxs-lookup"><span data-stu-id="11fd8-184">Use secret build variables to save storage Keys.</span></span> <span data-ttu-id="11fd8-185">Voor het maskeren van een variabele als geheim klikt u op het vergrendelingspictogram aan de rechterkant van de invoer-variabelen</span><span class="sxs-lookup"><span data-stu-id="11fd8-185">To mask a variable as secret click on the lock icon on the right side of the Variables input</span></span>

![Opslagsleutels opslaan in geheime build variabelen][23]

* <span data-ttu-id="11fd8-187">Een releaserecord maken en implementeren van uw project naar Azure</span><span class="sxs-lookup"><span data-stu-id="11fd8-187">Create a release and deploy your project to Azure</span></span>

![Nieuwe release gemaakt][24]

## <a name="next-steps"></a><span data-ttu-id="11fd8-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="11fd8-189">Next steps</span></span>
<span data-ttu-id="11fd8-190">Raadpleeg voor meer informatie over het instellen van extensies van diagnostische gegevens voor Azure Cloud Services, [diagnostische gegevens in Azure Cloud Services met behulp van PowerShell inschakelen][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="11fd8-190">To learn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
