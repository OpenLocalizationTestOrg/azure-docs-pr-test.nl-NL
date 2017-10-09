---
title: aaaDiagnose artefact fouten in de virtuele machine in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot artefact fouten in DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 115e0086-3293-4adf-8738-9f639f31f918
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: tarcher
ms.openlocfilehash: 40b3cea72cf071cc5d9a6d002d309d923c3d3084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-artifact-failures-in-hello-lab"></a><span data-ttu-id="8a475-103">Artefacten mislukte diagnoses in Hallo lab</span><span class="sxs-lookup"><span data-stu-id="8a475-103">Diagnose artifact failures in hello lab</span></span> 
<span data-ttu-id="8a475-104">Nadat u een artefact hebt gemaakt, kunt u toosee kunt controleren als deze is geslaagd of mislukt.</span><span class="sxs-lookup"><span data-stu-id="8a475-104">After you have created an artifact, you can check toosee if it succeeded or failed.</span></span> <span data-ttu-id="8a475-105">Artefacten Logboeken in DevTest Labs bevatten informatie kunt u toodiagnose een artefact-fout.</span><span class="sxs-lookup"><span data-stu-id="8a475-105">Artifact logs in DevTest Labs provide information you can use toodiagnose an artifact failure.</span></span> <span data-ttu-id="8a475-106">Er zijn een aantal verschillende manieren vindt u Hallo artefact-logboekgegevens voor een virtuele machine van Windows.</span><span class="sxs-lookup"><span data-stu-id="8a475-106">There are a couple different ways you can view hello artifact log information for a Windows VM.</span></span>

> [!NOTE]
> <span data-ttu-id="8a475-107">tooensure dat fouten correct worden geïdentificeerd en beschreven, is het belangrijk dat Hallo artefact is goed gestructureerd.</span><span class="sxs-lookup"><span data-stu-id="8a475-107">tooensure that failures are correctly identified and explained, it is important that hello artifact is properly structured.</span></span> <span data-ttu-id="8a475-108">Zie voor meer informatie over de manier waarop toocorrectly een artefact samenstelt [aangepaste artefacten maken](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="8a475-108">For information about how toocorrectly construct an artifact, see [Create custom artifacts](devtest-lab-artifact-author.md).</span></span> <span data-ttu-id="8a475-109">En toosee een voorbeeld van een goed gestructureerd artefact Bekijk dit [Test parametertypen](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artefacten.</span><span class="sxs-lookup"><span data-stu-id="8a475-109">And toosee an example of a properly structured artifact, check out this [Test Parameter Types](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artifact.</span></span>

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a><span data-ttu-id="8a475-110">Problemen met het artefact met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="8a475-110">Troubleshoot artifact failures using hello Azure portal</span></span>
<span data-ttu-id="8a475-111">toouse hello Azure portal toodiagnose fouten tijdens het maken van een artefact als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="8a475-111">toouse hello Azure portal toodiagnose failures during artifact creation, follow these steps:</span></span>

1. <span data-ttu-id="8a475-112">Selecteer uw lab in Hallo lijst met resources.</span><span class="sxs-lookup"><span data-stu-id="8a475-112">From hello list of resources, select your lab.</span></span>

2. <span data-ttu-id="8a475-113">Kies Hallo virtuele machine van Windows met de gewenste tooinvestigate Hallo-artefacten.</span><span class="sxs-lookup"><span data-stu-id="8a475-113">Choose hello Windows VM that includes hello artifact you want tooinvestigate.</span></span>

3. <span data-ttu-id="8a475-114">In het linkerdeelvenster onder Hallo **algemene**, kies **artefacten**.</span><span class="sxs-lookup"><span data-stu-id="8a475-114">In hello left panel under **GENERAL**, choose **Artifacts**.</span></span> <span data-ttu-id="8a475-115">Een lijst met artefacten die zijn gekoppeld aan die VM wordt weergegeven, hetgeen betekent dat Hallo-naam van het Hallo-artefacten en de status ervan.</span><span class="sxs-lookup"><span data-stu-id="8a475-115">A list of artifacts associated with that VM appears, indicating hello name of hello artifact and its status.</span></span>

   ![Voorbeeld van artefacten git-opslagplaats](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. <span data-ttu-id="8a475-117">Kies een artefact waarin de status van **mislukt**.</span><span class="sxs-lookup"><span data-stu-id="8a475-117">Choose an artifact that shows a status of **Failed**.</span></span> <span data-ttu-id="8a475-118">Hallo artefact wordt geopend en ziet u een extensie-bericht met meer informatie over de fout Hallo Hallo artefact.</span><span class="sxs-lookup"><span data-stu-id="8a475-118">hello artifact opens and shows an extension message that includes details about hello failure of hello artifact.</span></span>

   ![Voorbeeld van artefacten git-opslagplaats](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a><span data-ttu-id="8a475-120">Problemen met artefacten uit binnen Hallo VM</span><span class="sxs-lookup"><span data-stu-id="8a475-120">Troubleshoot artifact failures from within hello VM</span></span>
<span data-ttu-id="8a475-121">tooview hello artefact logboeken van binnen Hallo virtuele machine, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="8a475-121">tooview hello artifact logs from within hello virtual machine, follow these steps:</span></span>

1. <span data-ttu-id="8a475-122">Meld u bij toohello VM die Hallo artefact gewenste toodiagnose bevat.</span><span class="sxs-lookup"><span data-stu-id="8a475-122">Log in toohello VM that contains hello artifact you want toodiagnose.</span></span>

2. <span data-ttu-id="8a475-123">Navigeer tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status waarbij '1,9 Hallo Clientextensie versienummer staat.</span><span class="sxs-lookup"><span data-stu-id="8a475-123">Navigate tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status where "1.9 is hello CSE version number.</span></span>

   ![Voorbeeld van artefacten git-opslagplaats](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. <span data-ttu-id="8a475-125">Open Hallo **status** tooview bestandsgegevens dat helpt bij het artefact mislukte diagnoses voor die VM.</span><span class="sxs-lookup"><span data-stu-id="8a475-125">Open hello **status** file tooview information that helps diagnose artifact failures for that VM.</span></span>




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="8a475-126">Verwante blogberichten</span><span class="sxs-lookup"><span data-stu-id="8a475-126">Related blog posts</span></span>
* [<span data-ttu-id="8a475-127">Deelnemen aan een VM-tooexisting AD-domein met een resource manager-sjabloon in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8a475-127">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="8a475-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8a475-128">Next steps</span></span>
* <span data-ttu-id="8a475-129">Meer informatie over hoe te[een Git-opslagplaats tooa lab toevoegen](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="8a475-129">Learn how too[add a Git repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

