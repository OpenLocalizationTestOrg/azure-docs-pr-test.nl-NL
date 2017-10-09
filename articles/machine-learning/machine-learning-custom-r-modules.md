---
title: aaaAuthor aangepaste R-Modules in Azure Machine Learning | Microsoft Docs
description: Snel starten voor het schrijven van aangepaste R-modules in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 8007c2abe20a4ab990f38b6d09bc4e6834ad2082
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a><span data-ttu-id="c1d97-103">Aangepaste R-modules maken in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c1d97-103">Author custom R modules in Azure Machine Learning</span></span>
<span data-ttu-id="c1d97-104">Dit onderwerp wordt beschreven hoe tooauthor en implementeren van een aangepaste R-module in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c1d97-104">This topic describes how tooauthor and deploy a custom R module in Azure Machine Learning.</span></span> <span data-ttu-id="c1d97-105">Hierin wordt uitgelegd wat aangepaste R-modules zijn en welke bestanden zijn gebruikte toodefine ze.</span><span class="sxs-lookup"><span data-stu-id="c1d97-105">It explains what custom R modules are and what files are used toodefine them.</span></span> <span data-ttu-id="c1d97-106">Dit wordt geïllustreerd hoe tooconstruct Hallo voor bestanden die een module te definiëren en hoe tooregister Hallo-module voor implementatie in een Machine Learning-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="c1d97-106">It illustrates how tooconstruct hello files that define a module and how tooregister hello module for deployment in a Machine Learning workspace.</span></span> <span data-ttu-id="c1d97-107">Hallo zijn-elementen en kenmerken die worden gebruikt in Hallo definitie van de aangepaste module Hallo vervolgens uitvoeriger beschreven.</span><span class="sxs-lookup"><span data-stu-id="c1d97-107">hello elements and attributes used in hello definition of hello custom module are then described in more detail.</span></span> <span data-ttu-id="c1d97-108">Hoe toouse aanvullende functionaliteit, bestanden en meerdere uitgangen wordt ook beschreven.</span><span class="sxs-lookup"><span data-stu-id="c1d97-108">How toouse auxiliary functionality and files and multiple outputs is also discussed.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a><span data-ttu-id="c1d97-109">Wat is een aangepaste R-module?</span><span class="sxs-lookup"><span data-stu-id="c1d97-109">What is a custom R module?</span></span>
<span data-ttu-id="c1d97-110">Een **aangepaste module** is een door de gebruiker gedefinieerde module die kan worden geüpload tooyour werkruimte en uitgevoerd als onderdeel van een Azure Machine Learning-experiment.</span><span class="sxs-lookup"><span data-stu-id="c1d97-110">A **custom module** is a user-defined module that can be uploaded tooyour workspace and executed as part of an Azure Machine Learning experiment.</span></span> <span data-ttu-id="c1d97-111">Een **aangepaste R-module** is een aangepaste module die wordt uitgevoerd een R door de gebruiker gedefinieerde functie.</span><span class="sxs-lookup"><span data-stu-id="c1d97-111">A **custom R module** is a custom module that executes a user-defined R function.</span></span> <span data-ttu-id="c1d97-112">**R** is een programmeertaal voor statistische computing en afbeeldingen die veel door statistici en gegevens verzameld gebruikt wordt voor het implementeren van de algoritmen.</span><span class="sxs-lookup"><span data-stu-id="c1d97-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span></span> <span data-ttu-id="c1d97-113">R is momenteel de enige Hallo-taal ondersteund in aangepaste modules, maar ondersteuning voor extra talen is gepland voor toekomstige releases.</span><span class="sxs-lookup"><span data-stu-id="c1d97-113">Currently, R is hello only language supported in custom modules, but support for additional languages is scheduled for future releases.</span></span>

<span data-ttu-id="c1d97-114">Aangepaste modules hebben **eersteklas status** in Azure Machine Learning in Hallo zin dat ze net als elke andere module kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c1d97-114">Custom modules have **first-class status** in Azure Machine Learning in hello sense that they can be used just like any other module.</span></span> <span data-ttu-id="c1d97-115">Ze kunnen worden uitgevoerd met andere modules, opgenomen in gepubliceerde experimenten of visualisaties.</span><span class="sxs-lookup"><span data-stu-id="c1d97-115">They can be executed with other modules, included in published experiments or in visualizations.</span></span> <span data-ttu-id="c1d97-116">U hebben controle over Hallo algoritme geïmplementeerd door de module hello, Hallo invoer en uitvoer poorten toobe gebruikt, Hallo modellering parameters en andere verschillende runtime-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="c1d97-116">You have control over hello algorithm implemented by hello module, hello input and output ports toobe used, hello modeling parameters, and other various runtime behaviors.</span></span> <span data-ttu-id="c1d97-117">Een experiment met aangepaste modules kan ook worden gepubliceerd in Hallo Cortana Intelligence Gallery delen.</span><span class="sxs-lookup"><span data-stu-id="c1d97-117">An experiment that contains custom modules can also be published into hello Cortana Intelligence Gallery for easy sharing.</span></span>

## <a name="files-in-a-custom-r-module"></a><span data-ttu-id="c1d97-118">Bestanden in een aangepaste R-module</span><span class="sxs-lookup"><span data-stu-id="c1d97-118">Files in a custom R module</span></span>
<span data-ttu-id="c1d97-119">Een aangepaste R-module is gedefinieerd door een ZIP-bestand met ten minste twee bestanden:</span><span class="sxs-lookup"><span data-stu-id="c1d97-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span></span>

* <span data-ttu-id="c1d97-120">Een **bronbestand** die beschikbaar is gemaakt door de module Hallo Hallo R-functie wordt geïmplementeerd</span><span class="sxs-lookup"><span data-stu-id="c1d97-120">A **source file** that implements hello R function exposed by hello module</span></span>
* <span data-ttu-id="c1d97-121">Een **definitie XML-bestand** die beschrijft Hallo aangepaste module-interface</span><span class="sxs-lookup"><span data-stu-id="c1d97-121">An **XML definition file** that describes hello custom module interface</span></span>

<span data-ttu-id="c1d97-122">Aanvullende hulpbestanden kunnen ook worden opgenomen in Hallo ZIP-bestand dat wordt functionaliteit geboden die toegankelijk zijn vanuit Hallo aangepaste module.</span><span class="sxs-lookup"><span data-stu-id="c1d97-122">Additional auxiliary files can also be included in hello .zip file that provides functionality that can be accessed from hello custom module.</span></span> <span data-ttu-id="c1d97-123">Deze optie wordt besproken in Hallo **argumenten** deel uit van Hallo verwijzing sectie **elementen in de definitie van Hallo XML-bestand** Hallo Quick Start-voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="c1d97-123">This option is discussed in hello **Arguments** part of hello reference section **Elements in hello XML definition file** following hello quickstart example.</span></span>

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a><span data-ttu-id="c1d97-124">Quick Start-voorbeeld: definiëren, verpakken en registreren van een aangepaste R-module</span><span class="sxs-lookup"><span data-stu-id="c1d97-124">Quickstart example: define, package, and register a custom R module</span></span>
<span data-ttu-id="c1d97-125">In dit voorbeeld ziet u hoe tooconstruct Hallo voor bestanden die vereist zijn door een aangepaste R-module, verpakken in een zip-bestand en registreren Hallo-module in Machine Learning-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="c1d97-125">This example illustrates how tooconstruct hello files required by a custom R module, package them into a zip file, and then register hello module in your Machine Learning workspace.</span></span> <span data-ttu-id="c1d97-126">Hallo voorbeeld zip-pakket en voorbeeld-bestanden kunnen worden gedownload vanuit [CustomAddRows.zip downloaden bestand](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="c1d97-126">hello example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span></span>

## <a name="hello-source-file"></a><span data-ttu-id="c1d97-127">Hallo-bronbestand</span><span class="sxs-lookup"><span data-stu-id="c1d97-127">hello source file</span></span>
<span data-ttu-id="c1d97-128">Bekijk Hallo voorbeeld van een **rijen toevoegen van aangepaste** module die u de standaardimplementatie Hallo Hallo wijzigt **rijen toevoegen** module tooconcatenate rijen (opmerkingen) van twee gegevenssets (gegevensframes) gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c1d97-128">Consider hello example of a **Custom Add Rows** module that modifies hello standard implementation of hello **Add Rows** module used tooconcatenate rows (observations) from two datasets (data frames).</span></span> <span data-ttu-id="c1d97-129">Hallo standaard **rijen toevoegen** module voegt Hallo rijen van Hallo tweede invoergegevensset toohello einde van Hallo eerste invoergegevensset met Hallo `rbind` algoritme.</span><span class="sxs-lookup"><span data-stu-id="c1d97-129">hello standard **Add Rows** module appends hello rows of hello second input dataset toohello end of hello first input dataset using hello `rbind` algorithm.</span></span> <span data-ttu-id="c1d97-130">Hallo aangepast `CustomAddRows` functie op dezelfde manier accepteert twee gegevenssets, maar ook een parameter Booleaanse wisselen als extra invoer.</span><span class="sxs-lookup"><span data-stu-id="c1d97-130">hello customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span></span> <span data-ttu-id="c1d97-131">Als Hallo swap-parameter is ingesteld, te**FALSE**, het retourneert Hallo dezelfde gegevensset zoals Hallo standaardimplementatie.</span><span class="sxs-lookup"><span data-stu-id="c1d97-131">If hello swap parameter is set too**FALSE**, it returns hello same data set as hello standard implementation.</span></span> <span data-ttu-id="c1d97-132">Maar als Hallo wisselen parameter **TRUE**, Hallo functie voegt rijen van de eerste invoergegevensset toohello einde van de tweede gegevensset Hallo in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="c1d97-132">But if hello swap parameter is **TRUE**, hello function appends rows of first input dataset toohello end of hello second dataset instead.</span></span> <span data-ttu-id="c1d97-133">Hallo CustomAddRows.R-bestand met de Hallo-implementatie van Hallo R `CustomAddRows` functie die worden weergegeven door Hallo **rijen toevoegen van aangepaste** module heeft Hallo R code te volgen.</span><span class="sxs-lookup"><span data-stu-id="c1d97-133">hello CustomAddRows.R file that contains hello implementation of hello R `CustomAddRows` function exposed by hello **Custom Add Rows** module has hello following R code.</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="hello-xml-definition-file"></a><span data-ttu-id="c1d97-134">Hallo definitie XML-bestand</span><span class="sxs-lookup"><span data-stu-id="c1d97-134">hello XML definition file</span></span>
<span data-ttu-id="c1d97-135">tooexpose dit `CustomAddRows` functie als een Azure Machine Learning-module, een XML-definitie-bestand moet worden gemaakt toospecify hoe Hallo **rijen toevoegen van aangepaste** module dient uiterlijk en gedrag.</span><span class="sxs-lookup"><span data-stu-id="c1d97-135">tooexpose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created toospecify how hello **Custom Add Rows** module should look and behave.</span></span> 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother. Dataset 2 is concatenated tooDataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify hello base language, script file and R function toouse for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: hello values of hello id attributes in hello Input and Arg elements must match hello parameter names in hello R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>hello combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


<span data-ttu-id="c1d97-136">Het is essentieel toonote die waarde van Hallo Hallo **id** kenmerken van Hallo **invoer** en **Arg** elementen in de XML-bestand Hallo moeten overeenkomen met de Hallo functie parameternamen Hallo R code in Hallo CustomAddRows.R bestand exact: (*dataset1*, *dataset2*, en *wisselen* in Hallo voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="c1d97-136">It is critical toonote that hello value of hello **id** attributes of hello **Input** and **Arg** elements in hello XML file must match hello function parameter names of hello R code in hello CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in hello example).</span></span> <span data-ttu-id="c1d97-137">Op deze manier Hallo waarde Hallo **entryPoint** kenmerk Hallo **taal** element moet exact Hallo-naam van Hallo-functie in Hallo R-script: (*CustomAddRows* in Hallo voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="c1d97-137">Similarly, hello value of hello **entryPoint** attribute of hello **Language** element must match hello name of hello function in hello R script EXACTLY: (*CustomAddRows* in hello example).</span></span> 

<span data-ttu-id="c1d97-138">Daarentegen Hallo **id** kenmerk voor Hallo **uitvoer** element komt niet overeen met tooany variabelen in Hallo R-script.</span><span class="sxs-lookup"><span data-stu-id="c1d97-138">In contrast, hello **id** attribute for hello **Output** element does not correspond tooany variables in hello R script.</span></span> <span data-ttu-id="c1d97-139">Als meer dan één uitvoer vereist is, gewoon retourneren een lijst van Hallo R-functie met resultaten geplaatst *in Hallo dezelfde volgorde* als **uitvoer** elementen zijn gedeclareerd in Hallo XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="c1d97-139">When more than one output is required, simply return a list from hello R function with results placed *in hello same order* as **Outputs** elements are declared in hello XML file.</span></span>

### <a name="package-and-register-hello-module"></a><span data-ttu-id="c1d97-140">Hallo-module voor pakket- en registreren</span><span class="sxs-lookup"><span data-stu-id="c1d97-140">Package and register hello module</span></span>
<span data-ttu-id="c1d97-141">Deze twee bestanden opslaan als *CustomAddRows.R* en *CustomAddRows.xml* en vervolgens zip Hallo twee bestanden samen in een *CustomAddRows.zip* bestand.</span><span class="sxs-lookup"><span data-stu-id="c1d97-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip hello two files together into a *CustomAddRows.zip* file.</span></span>

<span data-ttu-id="c1d97-142">ze op in uw Machine Learning-werkruimte, Ga tooyour werkruimte in Hallo Machine Learning Studio, klikt u op Hallo tooregister **+ nieuw** knop op Hallo onder en kies **MODULE -> van ZIP-pakket** tooupload Hallo nieuwe **rijen toevoegen van aangepaste** module.</span><span class="sxs-lookup"><span data-stu-id="c1d97-142">tooregister them in your Machine Learning workspace, go tooyour workspace in hello Machine Learning Studio, click hello **+NEW** button on hello bottom and choose **MODULE -> FROM ZIP PACKAGE** tooupload hello new **Custom Add Rows** module.</span></span>

![Zip uploaden](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

<span data-ttu-id="c1d97-144">Hallo **rijen toevoegen van aangepaste** -module is nu gereed toobe toegankelijk is voor uw Machine Learning-experimenten.</span><span class="sxs-lookup"><span data-stu-id="c1d97-144">hello **Custom Add Rows** module is now ready toobe accessed by your Machine Learning experiments.</span></span>

## <a name="elements-in-hello-xml-definition-file"></a><span data-ttu-id="c1d97-145">Elementen in de definitie van Hallo XML-bestand</span><span class="sxs-lookup"><span data-stu-id="c1d97-145">Elements in hello XML definition file</span></span>
### <a name="module-elements"></a><span data-ttu-id="c1d97-146">Module-elementen</span><span class="sxs-lookup"><span data-stu-id="c1d97-146">Module elements</span></span>
<span data-ttu-id="c1d97-147">Hallo **Module** element heeft de gebruikte toodefine een aangepaste module in Hallo XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="c1d97-147">hello **Module** element is used toodefine a custom module in hello XML file.</span></span> <span data-ttu-id="c1d97-148">Meerdere modules kunnen worden gedefinieerd in een XML-bestand meerdere **module** elementen.</span><span class="sxs-lookup"><span data-stu-id="c1d97-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span></span> <span data-ttu-id="c1d97-149">Elke module in uw werkruimte moet een unieke naam hebben.</span><span class="sxs-lookup"><span data-stu-id="c1d97-149">Each module in your workspace must have a unique name.</span></span> <span data-ttu-id="c1d97-150">Een aangepaste module hebt geregistreerd met dezelfde naam als een bestaande aangepaste module Hallo en vervangt bestaande module Hallo Hello nieuwe.</span><span class="sxs-lookup"><span data-stu-id="c1d97-150">Register a custom module with hello same name as an existing custom module and it replaces hello existing module with hello new one.</span></span> <span data-ttu-id="c1d97-151">Aangepaste modules kunnen echter worden geregistreerd met dezelfde naam als een bestaande Azure Machine Learning module Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1d97-151">Custom modules can, however, be registered with hello same name as an existing Azure Machine Learning module.</span></span> <span data-ttu-id="c1d97-152">Als u dus ze worden weergegeven in Hallo **aangepaste** categorie van het modulepalet Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1d97-152">If so, they appear in hello **Custom** category of hello module palette.</span></span>

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


<span data-ttu-id="c1d97-153">Binnen Hallo **Module** element, kunt u twee extra optionele elementen:</span><span class="sxs-lookup"><span data-stu-id="c1d97-153">Within hello **Module** element, you can specify two additional optional elements:</span></span>

* <span data-ttu-id="c1d97-154">een **eigenaar** element dat is ingesloten in het Hallo-module</span><span class="sxs-lookup"><span data-stu-id="c1d97-154">an **Owner** element that is embedded into hello module</span></span>  
* <span data-ttu-id="c1d97-155">een **beschrijving** element bevat tekst die wordt weergegeven in de help voor Hallo-module van snelle en wanneer u de muisaanwijzer op Hallo-module in Machine Learning UI Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1d97-155">a **Description** element that contains text that is displayed in quick help for hello module and when you hover over hello module in hello Machine Learning UI.</span></span>

<span data-ttu-id="c1d97-156">Regels voor de limieten van de tekens in Hallo Module elementen:</span><span class="sxs-lookup"><span data-stu-id="c1d97-156">Rules for characters limits in hello Module elements:</span></span>

* <span data-ttu-id="c1d97-157">waarde van Hallo Hallo **naam** kenmerk in Hallo **Module** element mag niet groter zijn dan 64 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="c1d97-157">hello value of hello **name** attribute in hello **Module** element must not exceed 64 characters in length.</span></span> 
* <span data-ttu-id="c1d97-158">inhoud van het Hallo Hallo **beschrijving** element mag niet groter zijn dan 128 tekens.</span><span class="sxs-lookup"><span data-stu-id="c1d97-158">hello content of hello **Description** element must not exceed 128 characters in length.</span></span>
* <span data-ttu-id="c1d97-159">inhoud van het Hallo Hallo **eigenaar** element mag niet groter zijn dan 32 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="c1d97-159">hello content of hello **Owner** element must not exceed 32 characters in length.</span></span>

<span data-ttu-id="c1d97-160">De resultaten van de module kunnen deterministische of nondeterministic.* * standaard, alle modules worden beschouwd als toobe deterministisch.</span><span class="sxs-lookup"><span data-stu-id="c1d97-160">A module's results can be deterministic or nondeterministic.** By default, all modules are considered toobe deterministic.</span></span> <span data-ttu-id="c1d97-161">Dat wil zeggen, gezien een onveranderlijke reeks invoerparameters en gegevens, Hallo module moet worden geretourneerd Hallo dezelfde resulteert eacRAND of een functionh terwijl die deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c1d97-161">That is, given an unchanging set of input parameters and data, hello module should return hello same results eacRAND or a functionh time it is run.</span></span> <span data-ttu-id="c1d97-162">Dit gedrag, Azure Machine Learning Studio wordt alleen opnieuw uitgevoerd modules die zijn gemarkeerd als deterministisch als een parameter of de invoergegevens Hallo is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c1d97-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or hello input data has changed.</span></span> <span data-ttu-id="c1d97-163">Retourneren van resultaten in de cache opgeslagen Hallo biedt ook veel experimenten sneller wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c1d97-163">Returning hello cached results also provides much faster execution of experiments.</span></span>

<span data-ttu-id="c1d97-164">Er zijn functies die niet-deterministisch, zoals RNG of een functie die Hallo huidige datum of tijd retourneert.</span><span class="sxs-lookup"><span data-stu-id="c1d97-164">There are functions that are nondeterministic, such as RAND or a function that returns hello current date or time.</span></span> <span data-ttu-id="c1d97-165">Als uw module heeft een niet-deterministische functie gebruikt, kunt u opgeven dat Hallo-module is niet-deterministische door Hallo instelling optioneel **isDeterministic** te kenmerk**FALSE**.</span><span class="sxs-lookup"><span data-stu-id="c1d97-165">If your module uses a nondeterministic function, you can specify that hello module is non-deterministic by setting hello optional **isDeterministic** attribute too**FALSE**.</span></span> <span data-ttu-id="c1d97-166">Hierdoor weet u zeker dat Hallo-module is opnieuw uitgevoerd wanneer Hallo experiment wordt uitgevoerd, zelfs als hello module-invoer en parameters zijn niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c1d97-166">This insures that hello module is rerun whenever hello experiment is run, even if hello module input and parameters have not changed.</span></span> 

### <a name="language-definition"></a><span data-ttu-id="c1d97-167">Definitie van de taal</span><span class="sxs-lookup"><span data-stu-id="c1d97-167">Language Definition</span></span>
<span data-ttu-id="c1d97-168">Hallo **taal** -element in het XML-definitie-bestand is gebruikte toospecify Hallo aangepaste module taal.</span><span class="sxs-lookup"><span data-stu-id="c1d97-168">hello **Language** element in your XML definition file is used toospecify hello custom module language.</span></span> <span data-ttu-id="c1d97-169">R is momenteel alleen ondersteund taal Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1d97-169">Currently, R is hello only supported language.</span></span> <span data-ttu-id="c1d97-170">waarde van Hallo Hallo **bronbestand** kenmerk moet Hallo-naam van Hallo R-bestand met Hallo functie toocall Hallo module wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c1d97-170">hello value of hello **sourceFile** attribute must be hello name of hello R file that contains hello function toocall when hello module is run.</span></span> <span data-ttu-id="c1d97-171">Dit bestand moet deel uitmaken van Hallo zip-pakket.</span><span class="sxs-lookup"><span data-stu-id="c1d97-171">This file must be part of hello zip package.</span></span> <span data-ttu-id="c1d97-172">waarde van Hallo Hallo **entryPoint** kenmerk Hallo-naam van Hallo-functie wordt aangeroepen en moet overeenkomen met een geldige functie gedefinieerd met in Hallo-bronbestand.</span><span class="sxs-lookup"><span data-stu-id="c1d97-172">hello value of hello **entryPoint** attribute is hello name of hello function being called and must match a valid function defined with in hello source file.</span></span>

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a><span data-ttu-id="c1d97-173">Poorten</span><span class="sxs-lookup"><span data-stu-id="c1d97-173">Ports</span></span>
<span data-ttu-id="c1d97-174">Hallo invoer en uitvoer poorten voor een aangepaste module worden opgegeven in de onderliggende elementen van Hallo **poorten** sectie van definitie Hallo XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="c1d97-174">hello input and output ports for a custom module are specified in child elements of hello **Ports** section of hello XML definition file.</span></span> <span data-ttu-id="c1d97-175">Hallo-volgorde van deze elementen bepaalt Hallo layout ervaren (UX) door gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c1d97-175">hello order of these elements determines hello layout experienced (UX) by users.</span></span> <span data-ttu-id="c1d97-176">het eerste onderliggende Hello **invoer** of **uitvoer** die worden vermeld in Hallo **poorten** element van Hallo XML-bestand wordt Hallo meest linkse invoerpoort in Machine Learning UX Hallo</span><span class="sxs-lookup"><span data-stu-id="c1d97-176">hello first child **input** or **output** listed in hello **Ports** element of hello XML file becomes hello left-most input port in hello Machine Learning UX.</span></span>
<span data-ttu-id="c1d97-177">Elk invoer en uitvoerpoort heeft misschien een optionele **beschrijving** onderliggend element waarmee Hallo-tekst die wordt weergegeven wanneer u de muisaanwijzer muisaanwijzer Hallo Hallo-poort in Hallo Machine Learning-gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="c1d97-177">Each input and output port may have an optional **Description** child element that specifies hello text shown when you hover hello mouse cursor over hello port in hello Machine Learning UI.</span></span>

<span data-ttu-id="c1d97-178">**Regels poorten**:</span><span class="sxs-lookup"><span data-stu-id="c1d97-178">**Ports Rules**:</span></span>

* <span data-ttu-id="c1d97-179">Maximum aantal **invoer en uitvoer poorten** is 8 voor elk.</span><span class="sxs-lookup"><span data-stu-id="c1d97-179">Maximum number of **input and output ports** is 8 for each.</span></span>

### <a name="input-elements"></a><span data-ttu-id="c1d97-180">Invoer-elementen</span><span class="sxs-lookup"><span data-stu-id="c1d97-180">Input elements</span></span>
<span data-ttu-id="c1d97-181">Ingangspoorten kunnen u toopass gegevens tooyour R-functie en de werkruimte.</span><span class="sxs-lookup"><span data-stu-id="c1d97-181">Input ports allow you toopass data tooyour R function and workspace.</span></span> <span data-ttu-id="c1d97-182">Hallo **gegevenstypen** die worden ondersteund voor ingangspoorten als volgt zijn:</span><span class="sxs-lookup"><span data-stu-id="c1d97-182">hello **data types** that are supported for input ports are as follows:</span></span> 

<span data-ttu-id="c1d97-183">**DataTable:** dit type functie tooyour R is doorgegeven als een data.frame.</span><span class="sxs-lookup"><span data-stu-id="c1d97-183">**DataTable:** This type is passed tooyour R function as a data.frame.</span></span> <span data-ttu-id="c1d97-184">In feite geen typen (bijvoorbeeld CSV-bestanden of bestanden ARFF) die worden ondersteund door Machine Learning en die compatibel zijn met **DataTable** geconverteerde tooa data.frame automatisch zijn.</span><span class="sxs-lookup"><span data-stu-id="c1d97-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted tooa data.frame automatically.</span></span> 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

<span data-ttu-id="c1d97-185">Hallo **id** die zijn gekoppeld aan elk kenmerk **DataTable** invoerpoort moet een unieke waarde hebben en deze waarde moet overeenkomen met de bijbehorende parameter in uw R-functie met de naam.</span><span class="sxs-lookup"><span data-stu-id="c1d97-185">hello **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span></span>
<span data-ttu-id="c1d97-186">Optionele **DataTable** poorten die niet worden doorgegeven als invoer in een experiment Hallo waarde hebben **NULL** doorgegeven toohello R-functie en optioneel zip-poorten worden genegeerd als Hallo-invoer is niet verbonden.</span><span class="sxs-lookup"><span data-stu-id="c1d97-186">Optional **DataTable** ports that are not passed as input in an experiment have hello value **NULL** passed toohello R function and optional zip ports are ignored if hello input is not connected.</span></span> <span data-ttu-id="c1d97-187">Hallo **isOptional** kenmerk is optioneel voor beide Hallo **DataTable** en **Zip** en afkomstig is *false* standaard.</span><span class="sxs-lookup"><span data-stu-id="c1d97-187">hello **isOptional** attribute is optional for both hello **DataTable** and **Zip** types and is *false* by default.</span></span>

<span data-ttu-id="c1d97-188">**Postcode:** aangepaste modules kunnen een zip-bestand als invoer worden geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="c1d97-188">**Zip:** Custom modules can accept a zip file as input.</span></span> <span data-ttu-id="c1d97-189">Deze invoer is uitgepakt in de werkmap Hallo R van de functie</span><span class="sxs-lookup"><span data-stu-id="c1d97-189">This input is unpacked into hello R working directory of your function</span></span>

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

<span data-ttu-id="c1d97-190">Voor aangepaste R-modules heeft Hallo-id voor een Zip-poort geen toomatch parameters van functie Hallo R.</span><span class="sxs-lookup"><span data-stu-id="c1d97-190">For custom R modules, hello id for a Zip port does not have toomatch any parameters of hello R function.</span></span> <span data-ttu-id="c1d97-191">Dit komt omdat Hallo zip-bestand automatisch uitgepakte toohello R-werkmap.</span><span class="sxs-lookup"><span data-stu-id="c1d97-191">This is because hello zip file is automatically extracted toohello R working directory.</span></span>

<span data-ttu-id="c1d97-192">**Invoer regels:**</span><span class="sxs-lookup"><span data-stu-id="c1d97-192">**Input Rules:**</span></span>

* <span data-ttu-id="c1d97-193">waarde van Hallo Hallo **id** kenmerk Hallo **invoer** element moet een geldige R variabelenaam in.</span><span class="sxs-lookup"><span data-stu-id="c1d97-193">hello value of hello **id** attribute of hello **Input** element must be a valid R variable name.</span></span>
* <span data-ttu-id="c1d97-194">waarde van Hallo Hallo **id** kenmerk Hallo **invoer** element mag niet langer zijn dan 64 tekens zijn.</span><span class="sxs-lookup"><span data-stu-id="c1d97-194">hello value of hello **id** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="c1d97-195">waarde van Hallo Hallo **naam** kenmerk Hallo **invoer** element mag niet langer zijn dan 64 tekens zijn.</span><span class="sxs-lookup"><span data-stu-id="c1d97-195">hello value of hello **name** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="c1d97-196">inhoud van het Hallo Hallo **beschrijving** element mag niet langer zijn dan 128 tekens zijn</span><span class="sxs-lookup"><span data-stu-id="c1d97-196">hello content of hello **Description** element must not be longer than 128 characters</span></span>
* <span data-ttu-id="c1d97-197">waarde van Hallo Hallo **type** kenmerk Hallo **invoer** element moet *Zip* of *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="c1d97-197">hello value of hello **type** attribute of hello **Input** element must be *Zip* or *DataTable*.</span></span>
* <span data-ttu-id="c1d97-198">waarde van Hallo Hallo **isOptional** kenmerk Hallo **invoer** element is niet vereist (en *false* standaard als niet is opgegeven); maar als deze is opgegeven, moet dit *true* of *false*.</span><span class="sxs-lookup"><span data-stu-id="c1d97-198">hello value of hello **isOptional** attribute of hello **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span></span>

### <a name="output-elements"></a><span data-ttu-id="c1d97-199">Elementen van de uitvoer</span><span class="sxs-lookup"><span data-stu-id="c1d97-199">Output elements</span></span>
<span data-ttu-id="c1d97-200">**Standaard uitvoer poorten:** uitvoerpoorten zijn toegewezen toohello retourwaarden van uw R-functie, die vervolgens kunnen worden gebruikt door de volgende modules.</span><span class="sxs-lookup"><span data-stu-id="c1d97-200">**Standard output ports:** Output ports are mapped toohello return values from your R function, which can then be used by subsequent modules.</span></span> <span data-ttu-id="c1d97-201">*DataTable* Hallo alleen standaarduitvoer poort type op dit moment ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c1d97-201">*DataTable* is hello only standard output port type supported currently.</span></span> <span data-ttu-id="c1d97-202">(Ondersteuning voor *overbrengen* en *transformeert* ontbreekt.) Een *DataTable* uitvoer is gedefinieerd als:</span><span class="sxs-lookup"><span data-stu-id="c1d97-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span></span>

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

<span data-ttu-id="c1d97-203">Voor de uitvoer in aangepaste R-modules Hallo waarde Hallo **id** kenmerk heeft geen toocorrespond met iets in Hallo R-script, maar deze moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="c1d97-203">For outputs in custom R modules, hello value of hello **id** attribute does not have toocorrespond with anything in hello R script, but it must be unique.</span></span> <span data-ttu-id="c1d97-204">Voor een uitvoer één module Hallo geretourneerde waarde van Hallo R-functie moet een *data.frame*.</span><span class="sxs-lookup"><span data-stu-id="c1d97-204">For a single module output, hello return value from hello R function must be a *data.frame*.</span></span> <span data-ttu-id="c1d97-205">In volgorde toooutput meer dan een object van een ondersteund gegevenstype, Hallo juiste output poorten moeten toobe opgegeven in de definitie van Hallo XML-bestand en Hallo objecten moeten toobe geretourneerd als een lijst.</span><span class="sxs-lookup"><span data-stu-id="c1d97-205">In order toooutput more than one object of a supported data type, hello appropriate output ports need toobe specified in hello XML definition file and hello objects need toobe returned as a list.</span></span> <span data-ttu-id="c1d97-206">Hallo uitvoer objecten toegewezen toooutput poorten uit de linker tooright, opgetreden bij het Hallo-volgorde waarin Hallo objecten worden geplaatst in de lijst geretourneerd Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="c1d97-206">hello output objects are assigned toooutput ports from left tooright, reflecting hello order in which hello objects are placed in hello returned list.</span></span>

<span data-ttu-id="c1d97-207">Bijvoorbeeld, als u wilt dat toomodify hello **rijen toevoegen van aangepaste** module toooutput Hallo oorspronkelijke twee gegevenssets, *dataset1* en *dataset2*, Daarnaast toohello nieuw lid DataSet *gegevensset*, (in volgorde, van links tooright als: *gegevensset*, *dataset1*, *dataset2*), vervolgens Hallo definiëren poorten in Hallo CustomAddRows.xml bestand als volgt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c1d97-207">For example, if you want toomodify hello **Custom Add Rows** module toooutput hello original two datasets, *dataset1* and *dataset2*, in addition toohello new joined dataset, *dataset*, (in an order, from left tooright, as: *dataset*, *dataset1*, *dataset2*), then define hello output ports in hello CustomAddRows.xml file as follows:</span></span>

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


<span data-ttu-id="c1d97-208">En retourneren een lijst Hallo-lijst van objecten in de juiste volgorde Hallo in 'CustomAddRows.R':</span><span class="sxs-lookup"><span data-stu-id="c1d97-208">And return hello list of objects in a list in hello correct order in ‘CustomAddRows.R’:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

<span data-ttu-id="c1d97-209">**Visualisatie uitvoer:** kunt u ook een uitvoerpoort van het type opgeven *visualisatie*, die Hallo-uitvoer van Hallo R grafische apparaat en de console-uitvoer wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c1d97-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays hello output from hello R graphics device and console output.</span></span> <span data-ttu-id="c1d97-210">Deze poort maakt geen deel uit van de uitvoer van de functie Hallo R en niet van invloed op volgorde Hallo Hallo andere poorttypen uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c1d97-210">This port is not part of hello R function output and does not interfere with hello order of hello other output port types.</span></span> <span data-ttu-id="c1d97-211">tooadd toevoegen van een visualisatie poort toohello aangepaste modules die een **uitvoer** element met een waarde van *visualisatie* voor de **type** kenmerk:</span><span class="sxs-lookup"><span data-stu-id="c1d97-211">tooadd a visualization port toohello custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span></span>

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

<span data-ttu-id="c1d97-212">**Regels voor uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="c1d97-212">**Output Rules:**</span></span>

* <span data-ttu-id="c1d97-213">waarde van Hallo Hallo **id** kenmerk Hallo **uitvoer** element moet een geldige R variabelenaam in.</span><span class="sxs-lookup"><span data-stu-id="c1d97-213">hello value of hello **id** attribute of hello **Output** element must be a valid R variable name.</span></span>
* <span data-ttu-id="c1d97-214">waarde van Hallo Hallo **id** kenmerk Hallo **uitvoer** element mag niet langer zijn dan 32 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="c1d97-214">hello value of hello **id** attribute of hello **Output** element must not be longer than 32 characters.</span></span>
* <span data-ttu-id="c1d97-215">waarde van Hallo Hallo **naam** kenmerk Hallo **uitvoer** element mag niet langer zijn dan 64 tekens zijn.</span><span class="sxs-lookup"><span data-stu-id="c1d97-215">hello value of hello **name** attribute of hello **Output** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="c1d97-216">waarde van Hallo Hallo **type** kenmerk Hallo **uitvoer** element moet *visualisatie*.</span><span class="sxs-lookup"><span data-stu-id="c1d97-216">hello value of hello **type** attribute of hello **Output** element must be *Visualization*.</span></span>

### <a name="arguments"></a><span data-ttu-id="c1d97-217">Argumenten</span><span class="sxs-lookup"><span data-stu-id="c1d97-217">Arguments</span></span>
<span data-ttu-id="c1d97-218">Aanvullende gegevens kan toohello R-functie worden doorgegeven via de moduleparameters die zijn gedefinieerd in Hallo **argumenten** element.</span><span class="sxs-lookup"><span data-stu-id="c1d97-218">Additional data can be passed toohello R function via module parameters which are defined in hello **Arguments** element.</span></span> <span data-ttu-id="c1d97-219">Deze parameters worden weergegeven in de meest rechtse eigenschappendeelvenster Hallo Hallo Machine Learning UI wanneer Hallo-module is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="c1d97-219">These parameters appear in hello rightmost properties pane of hello Machine Learning UI when hello module is selected.</span></span> <span data-ttu-id="c1d97-220">Argumenten kunnen worden ondersteund Hallo typen of kunt u een aangepaste opsomming wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="c1d97-220">Arguments can be any of hello supported types or you can create a custom enumeration when needed.</span></span> <span data-ttu-id="c1d97-221">Vergelijkbare toohello **poorten** elementen, **argumenten** elementen kunnen hebben een optioneel **beschrijving** element waarmee wordt aangegeven Hallo-tekst die wordt weergegeven wanneer u de Hallo muisaanwijzer via Hallo parameternaam.</span><span class="sxs-lookup"><span data-stu-id="c1d97-221">Similar toohello **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies hello text that appears when you hover hello mouse over hello parameter name.</span></span>
<span data-ttu-id="c1d97-222">Optionele eigenschappen voor een module, zoals defaultValue minValue en maxValue tooany argument zoals tooa kenmerken kunnen worden toegevoegd **eigenschappen** element.</span><span class="sxs-lookup"><span data-stu-id="c1d97-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added tooany argument as attributes tooa **Properties** element.</span></span> <span data-ttu-id="c1d97-223">Geldige eigenschappen voor Hallo **eigenschappen** element afhankelijk zijn van Hallo argumenttype en met de argumenttypen hello wordt ondersteund in de volgende sectie Hallo worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="c1d97-223">Valid properties for hello **Properties** element depend on hello argument type and are described with hello supported argument types in hello next section.</span></span> <span data-ttu-id="c1d97-224">Argumenten Hello **isOptional** eigenschappenset te**'true'** vereisen geen Hallo gebruiker tooenter een waarde.</span><span class="sxs-lookup"><span data-stu-id="c1d97-224">Arguments with hello **isOptional** property set too**"true"** do not require hello user tooenter a value.</span></span> <span data-ttu-id="c1d97-225">Als een waarde toohello argument niet is opgegeven, is klikt u vervolgens Hallo-argument niet doorgegeven functie vermeldingspunt toohello.</span><span class="sxs-lookup"><span data-stu-id="c1d97-225">If a value is not provided toohello argument, then hello argument is not passed toohello entry point function.</span></span> <span data-ttu-id="c1d97-226">Argumenten van de functie vermeldingspunt Hallo die optionele nodig toobe expliciet verwerkt door de functie Hallo toegewezen bijvoorbeeld een standaardwaarde van NULL in Hallo vermelding punt functiedefinitie.</span><span class="sxs-lookup"><span data-stu-id="c1d97-226">Arguments of hello entry point function that are optional need toobe explicitly handled by hello function, e.g. assigned a default value of NULL in hello entry point function definition.</span></span> <span data-ttu-id="c1d97-227">Een optioneel argument wordt alleen afgedwongen Hallo andere beperkingen argument, dat wil zeggen min of max, als een waarde is opgegeven door de gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1d97-227">An optional argument will only enforce hello other argument constraints, i.e. min or max, if a value is provided by hello user.</span></span>
<span data-ttu-id="c1d97-228">Met in- en uitgangen is het cruciaal dat elk Hallo parameters unieke id-waarden die zijn gekoppeld hebben.</span><span class="sxs-lookup"><span data-stu-id="c1d97-228">As with inputs and outputs, it is critical that each of hello parameters have unique id values associated with them.</span></span> <span data-ttu-id="c1d97-229">In onze snel starten voorbeeld Hallo gekoppeld id-parameter is *wisselen*.</span><span class="sxs-lookup"><span data-stu-id="c1d97-229">In our quick start example hello associated id/parameter was *swap*.</span></span>

### <a name="arg-element"></a><span data-ttu-id="c1d97-230">Arg element</span><span class="sxs-lookup"><span data-stu-id="c1d97-230">Arg element</span></span>
<span data-ttu-id="c1d97-231">Een module-parameter is gedefinieerd met behulp van Hallo **Arg** onderliggend element van Hallo **argumenten** sectie van definitie Hallo XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="c1d97-231">A module parameter is defined using hello **Arg** child element of hello **Arguments** section of hello XML definition file.</span></span> <span data-ttu-id="c1d97-232">Net als bij Hallo onderliggende elementen in Hallo **poorten** sectie, Hallo ordening van parameters in Hallo **argumenten** sectie Hallo lay-out aangetroffen in Hallo UX worden gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="c1d97-232">As with hello child elements in hello **Ports** section, hello ordering of parameters in hello **Arguments** section defines hello layout encountered in hello UX.</span></span> <span data-ttu-id="c1d97-233">Hallo parameters staan van boven naar beneden in Hallo UI in dezelfde volgorde in die ze gedefinieerd Hallo in Hallo XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="c1d97-233">hello parameters appear from top down in hello UI in hello same order in which they are defined in hello XML file.</span></span> <span data-ttu-id="c1d97-234">Hallo die worden ondersteund door Machine Learning voor parameters worden hier weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c1d97-234">hello types supported by Machine Learning for parameters are listed here.</span></span> 

<span data-ttu-id="c1d97-235">**int** – een typeparameter van geheel getal (32-bits).</span><span class="sxs-lookup"><span data-stu-id="c1d97-235">**int** – an Integer (32-bit) type parameter.</span></span>

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* <span data-ttu-id="c1d97-236">*Optionele eigenschappen*: **min**, **max**, **standaard** en **isOptional**</span><span class="sxs-lookup"><span data-stu-id="c1d97-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="c1d97-237">**dubbele** – een double-type-parameter.</span><span class="sxs-lookup"><span data-stu-id="c1d97-237">**double** – a double type parameter.</span></span>

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* <span data-ttu-id="c1d97-238">*Optionele eigenschappen*: **min**, **max**, **standaard** en **isOptional**</span><span class="sxs-lookup"><span data-stu-id="c1d97-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="c1d97-239">**BOOL** – een Boole-parameter die wordt vertegenwoordigd door een selectievakje in UX</span><span class="sxs-lookup"><span data-stu-id="c1d97-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span></span>

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* <span data-ttu-id="c1d97-240">*Optionele eigenschappen*: **standaard** -false als dat niet is ingesteld</span><span class="sxs-lookup"><span data-stu-id="c1d97-240">*Optional Properties*: **default** - false if not set</span></span>

<span data-ttu-id="c1d97-241">**tekenreeks**: een standaardtekenreeks</span><span class="sxs-lookup"><span data-stu-id="c1d97-241">**string**: a standard string</span></span>

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* <span data-ttu-id="c1d97-242">*Optionele eigenschappen*: **standaard** en **isOptional**</span><span class="sxs-lookup"><span data-stu-id="c1d97-242">*Optional Properties*: **default** and **isOptional**</span></span>

<span data-ttu-id="c1d97-243">**ColumnPicker**: een parameter van de selectie kolom.</span><span class="sxs-lookup"><span data-stu-id="c1d97-243">**ColumnPicker**: a column selection parameter.</span></span> <span data-ttu-id="c1d97-244">Dit type wordt gerenderd in Hallo UX als het kiezen van een kolom.</span><span class="sxs-lookup"><span data-stu-id="c1d97-244">This type renders in hello UX as a column chooser.</span></span> <span data-ttu-id="c1d97-245">Hallo **eigenschap** element is gebruikte hier toospecify Hallo-id van Hallo-poort van waaruit de kolommen worden geselecteerd, waarop Hallo poort doeltype moet *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="c1d97-245">hello **Property** element is used here toospecify hello id of hello port from which columns are selected, where hello target port type must be *DataTable*.</span></span> <span data-ttu-id="c1d97-246">Hallo-resultaat van Hallo kolomselectie wordt toohello R functie doorgegeven als een lijst met tekenreeksen met de kolomnamen Hallo geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="c1d97-246">hello result of hello column selection is passed toohello R function as a list of strings containing hello selected column names.</span></span> 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* <span data-ttu-id="c1d97-247">*Vereiste eigenschappen*: **portId** -komt overeen met de id van een invoer-element met type Hallo *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="c1d97-247">*Required Properties*: **portId** - matches hello id of an Input element with type *DataTable*.</span></span>
* <span data-ttu-id="c1d97-248">*Optionele eigenschappen*:</span><span class="sxs-lookup"><span data-stu-id="c1d97-248">*Optional Properties*:</span></span>
  
  * <span data-ttu-id="c1d97-249">**allowedTypes** -Filters Hallo kolom typen uit die u kunt kiezen.</span><span class="sxs-lookup"><span data-stu-id="c1d97-249">**allowedTypes** - Filters hello column types from which you can pick.</span></span> <span data-ttu-id="c1d97-250">Geldige waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="c1d97-250">Valid values include:</span></span> 
    
    * <span data-ttu-id="c1d97-251">numerieke</span><span class="sxs-lookup"><span data-stu-id="c1d97-251">Numeric</span></span>
    * <span data-ttu-id="c1d97-252">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="c1d97-252">Boolean</span></span>
    * <span data-ttu-id="c1d97-253">Categorische gegevens</span><span class="sxs-lookup"><span data-stu-id="c1d97-253">Categorical</span></span>
    * <span data-ttu-id="c1d97-254">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c1d97-254">String</span></span>
    * <span data-ttu-id="c1d97-255">Label</span><span class="sxs-lookup"><span data-stu-id="c1d97-255">Label</span></span>
    * <span data-ttu-id="c1d97-256">Functie</span><span class="sxs-lookup"><span data-stu-id="c1d97-256">Feature</span></span>
    * <span data-ttu-id="c1d97-257">Score</span><span class="sxs-lookup"><span data-stu-id="c1d97-257">Score</span></span>
    * <span data-ttu-id="c1d97-258">Alle</span><span class="sxs-lookup"><span data-stu-id="c1d97-258">All</span></span>
  * <span data-ttu-id="c1d97-259">**standaard** -geldig standaardselecties voor Hallo kolomkiezer omvatten:</span><span class="sxs-lookup"><span data-stu-id="c1d97-259">**default** - Valid default selections for hello column picker include:</span></span> 
    
    * <span data-ttu-id="c1d97-260">Geen</span><span class="sxs-lookup"><span data-stu-id="c1d97-260">None</span></span>
    * <span data-ttu-id="c1d97-261">NumericFeature</span><span class="sxs-lookup"><span data-stu-id="c1d97-261">NumericFeature</span></span>
    * <span data-ttu-id="c1d97-262">NumericLabel</span><span class="sxs-lookup"><span data-stu-id="c1d97-262">NumericLabel</span></span>
    * <span data-ttu-id="c1d97-263">NumericScore</span><span class="sxs-lookup"><span data-stu-id="c1d97-263">NumericScore</span></span>
    * <span data-ttu-id="c1d97-264">NumericAll</span><span class="sxs-lookup"><span data-stu-id="c1d97-264">NumericAll</span></span>
    * <span data-ttu-id="c1d97-265">BooleanFeature</span><span class="sxs-lookup"><span data-stu-id="c1d97-265">BooleanFeature</span></span>
    * <span data-ttu-id="c1d97-266">BooleanLabel</span><span class="sxs-lookup"><span data-stu-id="c1d97-266">BooleanLabel</span></span>
    * <span data-ttu-id="c1d97-267">BooleanScore</span><span class="sxs-lookup"><span data-stu-id="c1d97-267">BooleanScore</span></span>
    * <span data-ttu-id="c1d97-268">BooleanAll</span><span class="sxs-lookup"><span data-stu-id="c1d97-268">BooleanAll</span></span>
    * <span data-ttu-id="c1d97-269">CategoricalFeature</span><span class="sxs-lookup"><span data-stu-id="c1d97-269">CategoricalFeature</span></span>
    * <span data-ttu-id="c1d97-270">CategoricalLabel</span><span class="sxs-lookup"><span data-stu-id="c1d97-270">CategoricalLabel</span></span>
    * <span data-ttu-id="c1d97-271">CategoricalScore</span><span class="sxs-lookup"><span data-stu-id="c1d97-271">CategoricalScore</span></span>
    * <span data-ttu-id="c1d97-272">CategoricalAll</span><span class="sxs-lookup"><span data-stu-id="c1d97-272">CategoricalAll</span></span>
    * <span data-ttu-id="c1d97-273">StringFeature</span><span class="sxs-lookup"><span data-stu-id="c1d97-273">StringFeature</span></span>
    * <span data-ttu-id="c1d97-274">StringLabel</span><span class="sxs-lookup"><span data-stu-id="c1d97-274">StringLabel</span></span>
    * <span data-ttu-id="c1d97-275">StringScore</span><span class="sxs-lookup"><span data-stu-id="c1d97-275">StringScore</span></span>
    * <span data-ttu-id="c1d97-276">StringAll</span><span class="sxs-lookup"><span data-stu-id="c1d97-276">StringAll</span></span>
    * <span data-ttu-id="c1d97-277">AllLabel</span><span class="sxs-lookup"><span data-stu-id="c1d97-277">AllLabel</span></span>
    * <span data-ttu-id="c1d97-278">AllFeature</span><span class="sxs-lookup"><span data-stu-id="c1d97-278">AllFeature</span></span>
    * <span data-ttu-id="c1d97-279">AllScore</span><span class="sxs-lookup"><span data-stu-id="c1d97-279">AllScore</span></span>
    * <span data-ttu-id="c1d97-280">Alle</span><span class="sxs-lookup"><span data-stu-id="c1d97-280">All</span></span>

<span data-ttu-id="c1d97-281">**Vervolgkeuzelijst**: een gebruiker opgegeven opgesomde (vervolgkeuzelijst) wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c1d97-281">**DropDown**: a user-specified enumerated (dropdown) list.</span></span> <span data-ttu-id="c1d97-282">Hallo dropdown artikelen zijn opgegeven in Hallo **eigenschappen** met behulp van element een **Item** element.</span><span class="sxs-lookup"><span data-stu-id="c1d97-282">hello dropdown items are specified within hello **Properties** element using an **Item** element.</span></span> <span data-ttu-id="c1d97-283">Hallo **id** voor elk **Item** moeten uniek zijn en een geldige R-variabele.</span><span class="sxs-lookup"><span data-stu-id="c1d97-283">hello **id** for each **Item** must be unique and a valid R variable.</span></span> <span data-ttu-id="c1d97-284">waarde van Hallo Hallo **naam** van een **Item** fungeert als zowel Hallo-tekst die wordt weergegeven als Hallo-waarde die wordt doorgegeven toohello R-functie.</span><span class="sxs-lookup"><span data-stu-id="c1d97-284">hello value of hello **name** of an **Item** serves as both hello text that you see and hello value that is passed toohello R function.</span></span>

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* <span data-ttu-id="c1d97-285">*Optionele eigenschappen*:</span><span class="sxs-lookup"><span data-stu-id="c1d97-285">*Optional Properties*:</span></span>
  * <span data-ttu-id="c1d97-286">**standaard** - hello waarde voor de standaardeigenschap Hallo met een id-waarde van een Hallo overeenkomen moet **Item** elementen.</span><span class="sxs-lookup"><span data-stu-id="c1d97-286">**default** - hello value for hello default property must correspond with an id value from one of hello **Item** elements.</span></span>

### <a name="auxiliary-files"></a><span data-ttu-id="c1d97-287">Hulpbestanden</span><span class="sxs-lookup"><span data-stu-id="c1d97-287">Auxiliary Files</span></span>
<span data-ttu-id="c1d97-288">Elk bestand dat wordt geplaatst in uw aangepaste module-ZIP-bestand is momenteel toobe beschikbaar voor gebruik tijdens uitvoeringstijd.</span><span class="sxs-lookup"><span data-stu-id="c1d97-288">Any file that is placed in your custom module ZIP file is going toobe available for use during execution time.</span></span> <span data-ttu-id="c1d97-289">Eventuele mapstructuren aanwezig blijven behouden.</span><span class="sxs-lookup"><span data-stu-id="c1d97-289">Any directory structures present are preserved.</span></span> <span data-ttu-id="c1d97-290">Dit betekent dat bestand sourcing works dezelfde Hallo lokaal en in Azure Machine Learning worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c1d97-290">This means that file sourcing works hello same locally and in Azure Machine Learning execution.</span></span> 

> [!NOTE]
> <span data-ttu-id="c1d97-291">Merk op dat alle bestanden uitgepakt too'src zijn ' directory zodat alle paden moet ' src /' voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="c1d97-291">Notice that all files are extracted too‘src’ directory so all paths should have ‘src/’ prefix.</span></span>
> 
> 

<span data-ttu-id="c1d97-292">Stel dat u wilt tooremove rijen met NAs uit Hallo gegevensset en ook eventuele dubbele rijen verwijderen voordat deze worden uitgevoerd in CustomAddRows als u al een R functie die in een bestand RemoveDupNARows.R hebt geschreven:</span><span class="sxs-lookup"><span data-stu-id="c1d97-292">For example, say you want tooremove any rows with NAs from hello dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span></span>

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
<span data-ttu-id="c1d97-293">U kunt bronbestand Hallo reserve RemoveDupNARows.R in Hallo CustomAddRows functie:</span><span class="sxs-lookup"><span data-stu-id="c1d97-293">You can source hello auxiliary file RemoveDupNARows.R in hello CustomAddRows function:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

<span data-ttu-id="c1d97-294">Vervolgens uploaden een zip-bestand met 'CustomAddRows.R', 'CustomAddRows.xml' en 'RemoveDupNARows.R' als een aangepaste R-module.</span><span class="sxs-lookup"><span data-stu-id="c1d97-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span></span>

## <a name="execution-environment"></a><span data-ttu-id="c1d97-295">Uitvoeringsomgeving</span><span class="sxs-lookup"><span data-stu-id="c1d97-295">Execution Environment</span></span>
<span data-ttu-id="c1d97-296">Hallo uitvoeringsomgeving voor Hallo R-script maakt gebruik van dezelfde versie van R als Hallo Hallo **R-Script uitvoeren** module en gebruik kunt Hallo dezelfde standaard pakketten.</span><span class="sxs-lookup"><span data-stu-id="c1d97-296">hello execution environment for hello R script uses hello same version of R as hello **Execute R Script** module and can use hello same default packages.</span></span> <span data-ttu-id="c1d97-297">U kunt ook aanvullende R-pakketten tooyour aangepaste module toevoegen door ze in Hallo aangepaste module-zip-pakket.</span><span class="sxs-lookup"><span data-stu-id="c1d97-297">You can also add additional R packages tooyour custom module by including them in hello custom module zip package.</span></span> <span data-ttu-id="c1d97-298">Zojuist geladen in het R-script zoals u zou in uw eigen omgeving voor R doen.</span><span class="sxs-lookup"><span data-stu-id="c1d97-298">Just load them in your R script as you would in your own R environment.</span></span> 

<span data-ttu-id="c1d97-299">**Beperkingen van de uitvoeringsomgeving Hallo** omvatten:</span><span class="sxs-lookup"><span data-stu-id="c1d97-299">**Limitations of hello execution environment** include:</span></span>

* <span data-ttu-id="c1d97-300">Niet-permanente bestandssysteem: bestanden die zijn geschreven wanneer Hallo aangepaste module wordt uitgevoerd, blijven niet bestaan voor meerdere uitvoert Hallo dezelfde module.</span><span class="sxs-lookup"><span data-stu-id="c1d97-300">Non-persistent file system: Files written when hello custom module is run are not persisted across multiple runs of hello same module.</span></span>
* <span data-ttu-id="c1d97-301">Er is geen toegang tot het netwerk</span><span class="sxs-lookup"><span data-stu-id="c1d97-301">No network access</span></span>

