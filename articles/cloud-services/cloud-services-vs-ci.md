---
title: aaaContinuous leveringsmethode voor cloud services met Visual Studio Online | Microsoft Docs
description: Meer informatie over hoe tooset up continue leveringsmethode voor Azure cloud-apps zonder op te slaan diagnostics opslagbestanden sleutel toohello service configuration
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
ms.openlocfilehash: dc87d049e46daf8b8a26ee4450ebd9b7910f287b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a><span data-ttu-id="4ad0b-103">Securely Cloud Services Diagnostics opslagsleutel opslaan en Setup continue integratie en implementatie tooAzure met behulp van Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="4ad0b-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment tooAzure using Visual Studio Online</span></span>
 <span data-ttu-id="4ad0b-104">Een algemene practice tooopen bronprojecten is tegenwoordig.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-104">It is a common practice tooopen source projects nowadays.</span></span> <span data-ttu-id="4ad0b-105">Opslaan van de toepassing geheimen in configuratiebestanden is niet meer veilig practice als beveiligingsrisico's beschikbaar worden gesteld van geheimen van besturingselementen voor openbare gegevensbronnen wordt gelekt.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="4ad0b-106">Geheim opslaan als tekst zonder opmaak in een bestand in een pijplijn continue integratie niet beveiligd is gedeelde ofwel omdat buildservers kunnen bronnen op Hallo cloudomgeving.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on hello Cloud environment.</span></span> <span data-ttu-id="4ad0b-107">Dit artikel wordt uitgelegd hoe Visual Studio en Visual Studio Online vermindert Hallo beveiligingskwesties weergegeven tijdens het ontwikkelen en continue integratie-proces.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-107">This article explains how Visual Studio and Visual Studio Online mitigates hello security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="4ad0b-108">Diagnostische gegevens opslag sleutel geheim verwijderen in het configuratiebestand van Project</span><span class="sxs-lookup"><span data-stu-id="4ad0b-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="4ad0b-109">Extensie voor diagnostische gegevens van cloud-Services vereist Azure-opslag voor het opslaan van resultaten van de diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="4ad0b-110">Voorheen Hallo-verbindingsreeks voor opslag is opgegeven in Hallo Cloudservices (.cscfg) configuratiebestanden en toosource controle kan worden gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-110">Formerly hello storage connection string is specified in hello Cloud Services configuration (.cscfg) files and could be checked in toosource control.</span></span> <span data-ttu-id="4ad0b-111">In de nieuwste Azure SDK versie Hallo gewijzigd we Hallo gedrag tooonly store een gedeeltelijke connection string met Hallo sleutel vervangen door een token.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-111">In hello latest Azure SDK release we changed hello behavior tooonly store a partial connection string with hello key replaced by a token.</span></span> <span data-ttu-id="4ad0b-112">Hallo stappen wordt beschreven hoe Hallo nieuwe Cloudservices tooling werkt:</span><span class="sxs-lookup"><span data-stu-id="4ad0b-112">hello following steps describe how hello new Cloud Services tooling works:</span></span>

### <a name="1-open-hello-role-designer"></a><span data-ttu-id="4ad0b-113">1. Hallo rol designer openen</span><span class="sxs-lookup"><span data-stu-id="4ad0b-113">1. Open hello Role designer</span></span>
* <span data-ttu-id="4ad0b-114">Dubbelklik op of klik met de rechtermuisknop op een Cloud Services-rol tooopen rol designer</span><span class="sxs-lookup"><span data-stu-id="4ad0b-114">Double click or right click on a Cloud Services role tooopen Role designer</span></span>

![Rol openen designer][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="4ad0b-116">2. Onder de sectie diagnostische gegevens, het selectievakje nieuwe 'niet verwijderen geheim project-opslagsleutel' is toegevoegd</span><span class="sxs-lookup"><span data-stu-id="4ad0b-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="4ad0b-117">Als u van de lokale opslagemulator Hallo gebruikmaakt, dit selectievakje is uitgeschakeld omdat er geen geheime toomanage Hallo lokale verbindingsreeks, namelijk UseDevelopmentStorage = true.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-117">If you are using hello local storage emulator, this checkbox is disabled because there is no secret toomanage for hello local connection string, which is UseDevelopmentStorage=true.</span></span>

![Lokale opslag emulator-verbindingstekenreeks is geen geheime][1]

* <span data-ttu-id="4ad0b-119">Als u een nieuw project maakt, zijn is dit selectievakje standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="4ad0b-120">Dit resulteert in Hallo opslag sleutel sectie van de verbindingsreeks voor opslag van Hallo geselecteerd wordt vervangen door een token.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-120">This results in hello storage key section of hello selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="4ad0b-121">Hallo waarde Hallo-token worden gevonden onder Hallo van de huidige gebruiker AppData Roaming map, bijvoorbeeld: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span><span class="sxs-lookup"><span data-stu-id="4ad0b-121">hello value of hello token will be found under hello current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="4ad0b-122">Houd er rekening mee Hallo user\AppData map toegang beheerd is door de gebruiker zich aanmelden en wordt beschouwd als een veilige plaats toostore ontwikkeling geheimen.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-122">Note that hello user\AppData folder is Access Controlled by user sign-in and is considered a secure place toostore development secrets.</span></span>
> 
> 

![Opslagsleutel wordt opgeslagen in de gebruikersprofielmap][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="4ad0b-124">3. Selecteer een opslagaccount voor diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="4ad0b-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="4ad0b-125">Selecteer een opslagaccount van Hallo dialoogvenster gestart door te klikken op '...' Hallo</span><span class="sxs-lookup"><span data-stu-id="4ad0b-125">Select a storage account from hello dialog launched by clicking hello “…”</span></span> <span data-ttu-id="4ad0b-126">te klikken.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-126">button.</span></span> <span data-ttu-id="4ad0b-127">U ziet hoe Hallo opslagverbindingsreeks gegenereerd geen sleutel Hallo opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-127">Notice how hello storage connection string generated will not have hello storage account key.</span></span>
* <span data-ttu-id="4ad0b-128">Bijvoorbeeld: DefaultEndpointsProtocol = https; AccountName = contosostorage; AccountKey = $(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="4ad0b-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-hello-project"></a><span data-ttu-id="4ad0b-129">4.    Foutopsporing Hallo-project</span><span class="sxs-lookup"><span data-stu-id="4ad0b-129">4.    Debugging hello project</span></span>
* <span data-ttu-id="4ad0b-130">F5 toostart foutopsporing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-130">F5 toostart debugging in Visual Studio.</span></span> <span data-ttu-id="4ad0b-131">Alles wat u moet werken in Hallo dezelfde manier als voorheen.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-131">Everything should work in hello same way as before.</span></span>
  <span data-ttu-id="4ad0b-132">![Lokaal foutopsporing starten][3]</span><span class="sxs-lookup"><span data-stu-id="4ad0b-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="4ad0b-133">5. Visual Studio-project publiceren</span><span class="sxs-lookup"><span data-stu-id="4ad0b-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="4ad0b-134">Start Hallo dialoogvenster publiceren en verdergaan met het aanmelden instructies toopublish hello applicaion tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-134">Launch hello publish dialog and proceed with sign-in instructions toopublish hello applicaion tooAzure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="4ad0b-135">6. Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="4ad0b-135">6. Additional information</span></span>
> <span data-ttu-id="4ad0b-136">Opmerking: paneel met toepassingsinstellingen Hallo in Hallo rol designer blijven omdat deze nu.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-136">Note: hello Settings panel in hello role designer will stay as it is for now.</span></span> <span data-ttu-id="4ad0b-137">Als u wilt dat toouse Hallo geheime beheerfunctie voor diagnostische gegevens, gaat u toohello configuraties tabblad.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-137">If you want toouse hello secret management feature for diagnostics, go toohello Configurations tab.</span></span>
> 
> 

![Instellingen toevoegen][4]

> <span data-ttu-id="4ad0b-139">Opmerking: Als ingeschakeld, Hallo Application Insights sleutel wordt opgeslagen als tekst zonder opmaak.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-139">Note: If enabled, hello Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="4ad0b-140">Hallo-sleutel wordt alleen gebruikt voor het uploaden van inhoud dus geen gevoelige gegevens risico wordt aangetast.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-140">hello key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="4ad0b-141">Maken en publiceren van een Cloud Services-Project met behulp van Visual Studio online taaksjablonen</span><span class="sxs-lookup"><span data-stu-id="4ad0b-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="4ad0b-142">Hallo stappen ziet u hoe toosetup continue integratie voor Cloud Services-project met behulp van Visual Studio online taken:</span><span class="sxs-lookup"><span data-stu-id="4ad0b-142">hello following steps illustrates how toosetup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="4ad0b-143">1.    Een account VSO verkrijgen</span><span class="sxs-lookup"><span data-stu-id="4ad0b-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="4ad0b-144">[Visual Studio Online-account maken] [ Create Visual Studio Online account] als u nog niet hebt</span><span class="sxs-lookup"><span data-stu-id="4ad0b-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="4ad0b-145">[Maken van teamproject] [ Create team project] in uw Visual Studio online-account</span><span class="sxs-lookup"><span data-stu-id="4ad0b-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="4ad0b-146">2.    Setup van broncodebeheer in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4ad0b-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="4ad0b-147">Verbinding maken met tooa teamproject</span><span class="sxs-lookup"><span data-stu-id="4ad0b-147">Connect tooa team project</span></span>

![Verbinding maken met tooteam project][5]

![Team project tooconnect te selecteren][6]

* <span data-ttu-id="4ad0b-150">Uw project toosource besturingselement toevoegen</span><span class="sxs-lookup"><span data-stu-id="4ad0b-150">Add your project toosource control</span></span>

![Project toosource besturingselement toevoegen][7]

![Project tooa bronmap besturingselement toewijzen][8]

* <span data-ttu-id="4ad0b-153">Controleer in uw project vanuit de Explorer-Team</span><span class="sxs-lookup"><span data-stu-id="4ad0b-153">Check in your project from Team Explorer</span></span>

![Controleer in het project toosource besturingselement][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="4ad0b-155">3.    Buildproces configureren</span><span class="sxs-lookup"><span data-stu-id="4ad0b-155">3.    Configure Build process</span></span>
* <span data-ttu-id="4ad0b-156">Blader tooyour teamproject en voegt u een nieuwe buildproces sjablonen</span><span class="sxs-lookup"><span data-stu-id="4ad0b-156">Browse tooyour team project and add a new build process Templates</span></span>

![Een nieuwe build toevoegen][10]

* <span data-ttu-id="4ad0b-158">Selecteer opbouwtaak</span><span class="sxs-lookup"><span data-stu-id="4ad0b-158">Select build task</span></span>

![Een taak build toevoegen][11]

![Visual Studio bouwen taak sjabloon selecteren][12]

* <span data-ttu-id="4ad0b-161">Build taak invoer bewerken.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-161">Edit build task input.</span></span> <span data-ttu-id="4ad0b-162">Hallo-build parameters volgens tooyour moeten aanpassen</span><span class="sxs-lookup"><span data-stu-id="4ad0b-162">Please customize hello build parameters according tooyour need</span></span>

![Opbouwtaak configureren][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="4ad0b-164">Build variabelen configureren</span><span class="sxs-lookup"><span data-stu-id="4ad0b-164">Configure build variables</span></span>

![Build variabelen configureren][14]

* <span data-ttu-id="4ad0b-166">Een taak tooupload build afname toevoegen</span><span class="sxs-lookup"><span data-stu-id="4ad0b-166">Add a task tooupload build drop</span></span>

![Kies neerzetten opbouwtaak publiceren][15]

![Configureer neerzetten opbouwtaak publiceren][16]

* <span data-ttu-id="4ad0b-169">Hallo build uitvoeren</span><span class="sxs-lookup"><span data-stu-id="4ad0b-169">Run hello build</span></span>

![Nieuwe Wachtrijvorming][17]

![Overzicht van de build weergeven][18]

* <span data-ttu-id="4ad0b-172">Als Hallo build geslaagd is ziet u een vergelijkbare toobelow resultaat</span><span class="sxs-lookup"><span data-stu-id="4ad0b-172">if hello build is successful you will see a result similar toobelow</span></span>

![Resultaat bouwen][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="4ad0b-174">4.    Release-proces configureren</span><span class="sxs-lookup"><span data-stu-id="4ad0b-174">4.    Configure Release process</span></span>
* <span data-ttu-id="4ad0b-175">Een nieuwe release gemaakt</span><span class="sxs-lookup"><span data-stu-id="4ad0b-175">Create a new release</span></span>

![Nieuwe release gemaakt][20]

* <span data-ttu-id="4ad0b-177">Selecteer hello Azure Cloud Services-implementatie taak</span><span class="sxs-lookup"><span data-stu-id="4ad0b-177">Select hello Azure Cloud Services Deployment task</span></span>

![Selecteer taak voor Azure Cloud Services-implementatie][21]

* <span data-ttu-id="4ad0b-179">Naarmate de opslagaccountsleutel Hallo niet toosource controle is ingeschakeld, moeten we toospecify Hallo geheime sleutel voor het instellen van extensies van diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-179">As hello storage account key is not checked in toosource control, we need toospecify hello secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="4ad0b-180">Vouw Hallo **geavanceerde opties voor nieuwe Service maken** sectie en Hallo bewerken **Opslagaccountsleutels Diagnostics** parameter invoer.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-180">Expand hello **Advanced Options for Creating New Service** section and edit hello **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="4ad0b-181">Deze invoer nodig is op meerdere regels van sleutel-waardepaar Hallo indeling **[RoleName]:$(StorageAccountKey)**</span><span class="sxs-lookup"><span data-stu-id="4ad0b-181">This input takes in multiple lines of key value pair in hello format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="4ad0b-182">Opmerking: als uw opslagaccount onder de ligt diagnostics hello hetzelfde abonnement als waar u Hallo Cloud Services-toepassing wilt publiceren, hebt u niet tooenter Hallo sleutel in de invoer voor Hallo implementatie taak; Hallo-implementatie wordt programmatisch Hallo storage-gegevens ophalen uit uw abonnement</span><span class="sxs-lookup"><span data-stu-id="4ad0b-182">Note: if your diagnostics storage account is under hello same subscription as where you will publish hello Cloud Services application, you don't have tooenter hello key in hello deployment task input; hello deployment will programmatically obtain hello storage information from your subscription</span></span>
> 
> 

![Taak voor Cloud Services-implementatie configureren][22]

* <span data-ttu-id="4ad0b-184">Gebruik geheim bouwen variabelen toosave Opslagsleutels.</span><span class="sxs-lookup"><span data-stu-id="4ad0b-184">Use secret build variables toosave storage Keys.</span></span> <span data-ttu-id="4ad0b-185">een variabele als geheim klikt u op Hallo vergrendelingspictogram aan de rechterkant Hallo Hallo toomask variabelen invoer</span><span class="sxs-lookup"><span data-stu-id="4ad0b-185">toomask a variable as secret click on hello lock icon on hello right side of hello Variables input</span></span>

![Opslagsleutels opslaan in geheime build variabelen][23]

* <span data-ttu-id="4ad0b-187">Een releaserecord maken en implementeren van uw project tooAzure</span><span class="sxs-lookup"><span data-stu-id="4ad0b-187">Create a release and deploy your project tooAzure</span></span>

![Nieuwe release gemaakt][24]

## <a name="next-steps"></a><span data-ttu-id="4ad0b-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4ad0b-189">Next steps</span></span>
<span data-ttu-id="4ad0b-190">Zie de toolearn meer informatie over het instellen van extensies van diagnostische gegevens voor Azure Cloud Services [diagnostische gegevens in Azure Cloud Services met behulp van PowerShell inschakelen][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="4ad0b-190">toolearn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

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
