---
title: aangepaste artefacten aaaCreate voor uw VM van DevTest Labs | Microsoft Docs
description: Meer informatie over hoe tooauthor uw eigen artefacten voor gebruiken met DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 32dcdc61-ec23-4a01-b731-78c029ea5316
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 2bd603bc1241ca6b669a3a276a677729514f0df2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="6e4a6-103">Aangepaste artefacten maken voor uw DevTest Labs VM</span><span class="sxs-lookup"><span data-stu-id="6e4a6-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="6e4a6-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="6e4a6-104">Overview</span></span>
<span data-ttu-id="6e4a6-105">**Artefacten** gebruikte toodeploy zijn en uw toepassing configureren nadat een virtuele machine is ingericht.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-105">**Artifacts** are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="6e4a6-106">Een artefact bestaat uit een definitiebestand van artefacten en andere scriptbestanden die zijn opgeslagen in een map in een git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="6e4a6-107">Artefacten definitiebestanden bestaan uit JSON en uitdrukkingen die u kunt gebruiken toospecify wat u wilt tooinstall op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-107">Artifact definition files consist of JSON and expressions that you can use toospecify what you want tooinstall on a VM.</span></span> <span data-ttu-id="6e4a6-108">U kunt bijvoorbeeld definiëren Hallo-naam van een artefact opdracht toorun parameters, en die beschikbaar worden gesteld wanneer het Hallo-opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-108">For example, you can define hello name of an artifact, command toorun, and parameters that are made available when hello command is run.</span></span> <span data-ttu-id="6e4a6-109">U kunt tooother scriptbestanden binnen Hallo artefact definitiebestand verwijzen met de naam.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-109">You can refer tooother script files within hello artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="6e4a6-110">Bestandsindeling van pakketdefinities artefact</span><span class="sxs-lookup"><span data-stu-id="6e4a6-110">Artifact definition file format</span></span>
<span data-ttu-id="6e4a6-111">Hallo toont volgende voorbeeld Hallo secties die gezamenlijk Hallo basisstructuur van een definitiebestand van:</span><span class="sxs-lookup"><span data-stu-id="6e4a6-111">hello following example shows hello sections that make up hello basic structure of a definition file:</span></span>

    {
      "$schema": "https://raw.githubusercontent.com/Azure/azure-devtestlab/master/schemas/2016-11-28/dtlArtifacts.json",
      "title": "",
      "description": "",
      "iconUri": "",
      "targetOsType": "",
      "parameters": {
        "<parameterName>": {
          "type": "",
          "displayName": "",
          "description": ""
        }
      },
      "runCommand": {
        "commandToExecute": ""
      }
    }

| <span data-ttu-id="6e4a6-112">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="6e4a6-112">Element name</span></span> | <span data-ttu-id="6e4a6-113">Vereist?</span><span class="sxs-lookup"><span data-stu-id="6e4a6-113">Required?</span></span> | <span data-ttu-id="6e4a6-114">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6e4a6-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6e4a6-115">$schema</span><span class="sxs-lookup"><span data-stu-id="6e4a6-115">$schema</span></span> |<span data-ttu-id="6e4a6-116">Nee</span><span class="sxs-lookup"><span data-stu-id="6e4a6-116">No</span></span> |<span data-ttu-id="6e4a6-117">Locatie van Hallo JSON-schema-bestand waarmee tests Hallo geldigheid van Hallo definitiebestand.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-117">Location of hello JSON schema file that helps in testing hello validity of hello definition file.</span></span> |
| <span data-ttu-id="6e4a6-118">titel</span><span class="sxs-lookup"><span data-stu-id="6e4a6-118">title</span></span> |<span data-ttu-id="6e4a6-119">Ja</span><span class="sxs-lookup"><span data-stu-id="6e4a6-119">Yes</span></span> |<span data-ttu-id="6e4a6-120">Naam van de weergegeven in de testomgeving Hallo Hallo-artefacten.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-120">Name of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="6e4a6-121">description</span><span class="sxs-lookup"><span data-stu-id="6e4a6-121">description</span></span> |<span data-ttu-id="6e4a6-122">Ja</span><span class="sxs-lookup"><span data-stu-id="6e4a6-122">Yes</span></span> |<span data-ttu-id="6e4a6-123">Beschrijving van de weergegeven in de testomgeving Hallo Hallo-artefacten.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-123">Description of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="6e4a6-124">iconUri</span><span class="sxs-lookup"><span data-stu-id="6e4a6-124">iconUri</span></span> |<span data-ttu-id="6e4a6-125">Nee</span><span class="sxs-lookup"><span data-stu-id="6e4a6-125">No</span></span> |<span data-ttu-id="6e4a6-126">De URI van Hallo pictogram dat wordt weergegeven in de testomgeving Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-126">Uri of hello icon displayed in hello lab.</span></span> |
| <span data-ttu-id="6e4a6-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="6e4a6-127">targetOsType</span></span> |<span data-ttu-id="6e4a6-128">Ja</span><span class="sxs-lookup"><span data-stu-id="6e4a6-128">Yes</span></span> |<span data-ttu-id="6e4a6-129">Besturingssysteem van Hallo VM waarop artefact is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-129">Operating system of hello VM where artifact is installed.</span></span> <span data-ttu-id="6e4a6-130">Ondersteunde opties zijn: Windows- en Linux.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="6e4a6-131">parameters</span><span class="sxs-lookup"><span data-stu-id="6e4a6-131">parameters</span></span> |<span data-ttu-id="6e4a6-132">Nee</span><span class="sxs-lookup"><span data-stu-id="6e4a6-132">No</span></span> |<span data-ttu-id="6e4a6-133">De waarden die worden opgegeven wanneer de installatieopdracht artefact wordt uitgevoerd op een machine.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="6e4a6-134">Dit helpt bij het aanpassen van uw artefacten.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="6e4a6-135">OpdrachtUitvoeren</span><span class="sxs-lookup"><span data-stu-id="6e4a6-135">runCommand</span></span> |<span data-ttu-id="6e4a6-136">Ja</span><span class="sxs-lookup"><span data-stu-id="6e4a6-136">Yes</span></span> |<span data-ttu-id="6e4a6-137">Artefacten installeren de opdracht die wordt uitgevoerd op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="6e4a6-138">Parameters van artefacten</span><span class="sxs-lookup"><span data-stu-id="6e4a6-138">Artifact parameters</span></span>
<span data-ttu-id="6e4a6-139">U opgeven welke waarden van een gebruiker kan invoer bij het installeren van een artefact in Hallo gedeelte parameters van Hallo definitiebestand van.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-139">In hello parameters section of hello definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="6e4a6-140">U kunt toothese waarden in Hallo artefact installatieopdracht verwijzen.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-140">You can refer toothese values in hello artifact install command.</span></span>

<span data-ttu-id="6e4a6-141">U kunt parameters definiëren Hello structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e4a6-141">You define parameters with hello following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="6e4a6-142">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="6e4a6-142">Element name</span></span> | <span data-ttu-id="6e4a6-143">Vereist?</span><span class="sxs-lookup"><span data-stu-id="6e4a6-143">Required?</span></span> | <span data-ttu-id="6e4a6-144">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6e4a6-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6e4a6-145">type</span><span class="sxs-lookup"><span data-stu-id="6e4a6-145">type</span></span> |<span data-ttu-id="6e4a6-146">Ja</span><span class="sxs-lookup"><span data-stu-id="6e4a6-146">Yes</span></span> |<span data-ttu-id="6e4a6-147">Type van parameterwaarde.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-147">Type of parameter value.</span></span> <span data-ttu-id="6e4a6-148">Zie Hallo lijst met toegestane typen hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="6e4a6-148">See hello following list for hello allowed types:</span></span> |
| <span data-ttu-id="6e4a6-149">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="6e4a6-149">displayName</span></span> |<span data-ttu-id="6e4a6-150">Ja</span><span class="sxs-lookup"><span data-stu-id="6e4a6-150">Yes</span></span> |<span data-ttu-id="6e4a6-151">Naam van het Hallo-parameter die de gebruiker weergegeven tooa in Hallo lab is.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-151">Name of hello parameter that is displayed tooa user in hello lab.</span></span> | |
| <span data-ttu-id="6e4a6-152">description</span><span class="sxs-lookup"><span data-stu-id="6e4a6-152">description</span></span> |<span data-ttu-id="6e4a6-153">Ja</span><span class="sxs-lookup"><span data-stu-id="6e4a6-153">Yes</span></span> |<span data-ttu-id="6e4a6-154">Beschrijving van het Hallo-parameter die wordt weergegeven in de testomgeving Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-154">Description of hello parameter that is displayed in hello lab.</span></span> |

<span data-ttu-id="6e4a6-155">Hallo toegestane typen zijn:</span><span class="sxs-lookup"><span data-stu-id="6e4a6-155">hello allowed types are:</span></span>

* <span data-ttu-id="6e4a6-156">tekenreeks – een willekeurige geldige JSON-tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e4a6-156">string – any valid JSON string</span></span>
* <span data-ttu-id="6e4a6-157">int – een geldige JSON geheel getal</span><span class="sxs-lookup"><span data-stu-id="6e4a6-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="6e4a6-158">BOOL – geldige JSON Boole</span><span class="sxs-lookup"><span data-stu-id="6e4a6-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="6e4a6-159">matrix – een geldig JSON-matrix</span><span class="sxs-lookup"><span data-stu-id="6e4a6-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="6e4a6-160">Artefacten expressies en functies</span><span class="sxs-lookup"><span data-stu-id="6e4a6-160">Artifact expressions and functions</span></span>
<span data-ttu-id="6e4a6-161">U kunt een expressie en functies tooconstruct Hallo artefact installatieopdracht.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-161">You can use expression and functions tooconstruct hello artifact install command.</span></span>
<span data-ttu-id="6e4a6-162">Expressies tussen haakjes ([en]), en worden geëvalueerd wanneer Hallo artefact is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when hello artifact is installed.</span></span> <span data-ttu-id="6e4a6-163">Expressies kunnen overal voorkomen in een string-waarde van JSON en altijd een andere JSON-waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="6e4a6-164">Als u moet een letterlijke tekenreeks die met een haakje begint toouse [, moet u twee haken [[.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-164">If you need toouse a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="6e4a6-165">Normaal gesproken gebruikt u expressies met functies tooconstruct een waarde.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-165">Typically, you use expressions with functions tooconstruct a value.</span></span> <span data-ttu-id="6e4a6-166">Net als in JavaScript zijn-functieaanroepen die opgemaakt als functionName(arg1,arg2,arg3).</span><span class="sxs-lookup"><span data-stu-id="6e4a6-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3).</span></span>

<span data-ttu-id="6e4a6-167">Hallo bevat volgende lijst algemene functies:</span><span class="sxs-lookup"><span data-stu-id="6e4a6-167">hello following list shows common functions:</span></span>

* <span data-ttu-id="6e4a6-168">parameters(parameterName) - retourneert een waarde van parameter die is opgegeven als Hallo artefact-opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-168">parameters(parameterName) - Returns a parameter value that is provided when hello artifact command is run.</span></span>
* <span data-ttu-id="6e4a6-169">concat (arg1, arg2, arg3,...) - combineert meerdere tekenreekswaarden.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="6e4a6-170">Deze functie kan duren voordat een willekeurig aantal argumenten.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="6e4a6-171">Hallo volgende voorbeeld wordt getoond hoe toouse expressie en functies tooconstruct een waarde:</span><span class="sxs-lookup"><span data-stu-id="6e4a6-171">hello following example shows how toouse expression and functions tooconstruct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="6e4a6-172">Een aangepaste artefacten maken</span><span class="sxs-lookup"><span data-stu-id="6e4a6-172">Create a custom artifact</span></span>
<span data-ttu-id="6e4a6-173">Uw aangepaste artefacten maken met de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="6e4a6-173">Create your custom artifact by following these steps:</span></span>

1. <span data-ttu-id="6e4a6-174">Installeer een JSON-editor - moet u een JSON-editor toowork met artefacten definitiebestanden.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-174">Install a JSON editor - You need a JSON editor toowork with artifact definition files.</span></span> <span data-ttu-id="6e4a6-175">Wordt u aangeraden [Visual Studio Code](https://code.visualstudio.com/), die beschikbaar is voor Windows, Linux en OS X.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="6e4a6-176">Een voorbeeld artifactfile.json - uitchecken Hallo artefacten gemaakt door het team van Azure DevTest Labs op Get onze [GitHub-opslagplaats](https://github.com/Azure/azure-devtestlab), waarbij er een uitgebreide bibliotheek met gemaakt artefacten die u helpen uw eigen artefacten maken.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-176">Get a sample artifactfile.json - Check out hello artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab), where we have created a rich library of artifacts that help you create your own artifacts.</span></span> <span data-ttu-id="6e4a6-177">Download een definitiebestand van artefacten en wijzigingen tooit toocreate uw eigen artefacten maken.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-177">Download an artifact definition file and make changes tooit toocreate your own artifacts.</span></span>
3. <span data-ttu-id="6e4a6-178">Maakt gebruik van IntelliSense - hefboomwerking IntelliSense toosee geldige elementen die gebruikt tooconstruct worden kunnen een definitiebestand van artefacten.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-178">Make use of IntelliSense - Leverage IntelliSense toosee valid elements that can be used tooconstruct an artifact definition file.</span></span> <span data-ttu-id="6e4a6-179">U ziet ook Hallo verschillende opties voor waarden van een element.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-179">You can also see hello different options for values of an element.</span></span> <span data-ttu-id="6e4a6-180">Bijvoorbeeld: IntelliSense weergeven u twee mogelijkheden van Windows of Linux Hallo bij het bewerken van Hallo **targetOsType** element.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-180">For example, IntelliSense show you hello two choices of Windows or Linux when editing hello **targetOsType** element.</span></span>
4. <span data-ttu-id="6e4a6-181">Store Hallo artefacten in een [git-opslagplaats](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="6e4a6-181">Store hello artifact in a [git repository](devtest-lab-add-artifact-repo.md).</span></span>
   
   1. <span data-ttu-id="6e4a6-182">Maak een afzonderlijke map voor elke artefact waar Hallo mapnaam is Hallo dezelfde als de naam van de artefacten Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-182">Create a separate directory for each artifact where hello directory name is hello same as hello artifact name.</span></span>
   2. <span data-ttu-id="6e4a6-183">Hallo artefact-definitiebestand (artifactfile.json) opslaan in Hallo-directory die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-183">Store hello artifact definition file (artifactfile.json) in hello directory you created.</span></span>
   3. <span data-ttu-id="6e4a6-184">Installatieopdracht Store Hallo scripts waarnaar wordt verwezen vanaf Hallo artefacten.</span><span class="sxs-lookup"><span data-stu-id="6e4a6-184">Store hello scripts that are referenced from hello artifact install command.</span></span>
      
      <span data-ttu-id="6e4a6-185">Hier volgt een voorbeeld van een map artefact kan als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="6e4a6-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![Voorbeeld van artefacten git-opslagplaats](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="6e4a6-187">Hallo artefacten opslagplaats toohello lab Add - toohello artikel, Raadpleeg [een Git-opslagplaats voor artefacten en sjablonen toevoegen](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="6e4a6-187">Add hello artifacts repository toohello lab - Refer toohello article, [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a><span data-ttu-id="6e4a6-188">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="6e4a6-188">Related articles</span></span>
* [<span data-ttu-id="6e4a6-189">Hoe toodiagnose artefact fouten in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="6e4a6-189">How toodiagnose artifact failures in DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="6e4a6-190">Deelnemen aan een VM-tooexisting AD-domein met een resource manager-sjabloon in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="6e4a6-190">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="6e4a6-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6e4a6-191">Next steps</span></span>
* <span data-ttu-id="6e4a6-192">Meer informatie over hoe te[een Git artefact opslagplaats tooa lab toevoegen](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="6e4a6-192">Learn how too[add a Git artifact repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

