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
# <a name="diagnose-artifact-failures-in-hello-lab"></a>Artefacten mislukte diagnoses in Hallo lab 
Nadat u een artefact hebt gemaakt, kunt u toosee kunt controleren als deze is geslaagd of mislukt. Artefacten Logboeken in DevTest Labs bevatten informatie kunt u toodiagnose een artefact-fout. Er zijn een aantal verschillende manieren vindt u Hallo artefact-logboekgegevens voor een virtuele machine van Windows.

> [!NOTE]
> tooensure dat fouten correct worden geïdentificeerd en beschreven, is het belangrijk dat Hallo artefact is goed gestructureerd. Zie voor meer informatie over de manier waarop toocorrectly een artefact samenstelt [aangepaste artefacten maken](devtest-lab-artifact-author.md). En toosee een voorbeeld van een goed gestructureerd artefact Bekijk dit [Test parametertypen](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artefacten.

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a>Problemen met het artefact met hello Azure-portal
toouse hello Azure portal toodiagnose fouten tijdens het maken van een artefact als volgt te werk:

1. Selecteer uw lab in Hallo lijst met resources.

2. Kies Hallo virtuele machine van Windows met de gewenste tooinvestigate Hallo-artefacten.

3. In het linkerdeelvenster onder Hallo **algemene**, kies **artefacten**. Een lijst met artefacten die zijn gekoppeld aan die VM wordt weergegeven, hetgeen betekent dat Hallo-naam van het Hallo-artefacten en de status ervan.

   ![Voorbeeld van artefacten git-opslagplaats](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. Kies een artefact waarin de status van **mislukt**. Hallo artefact wordt geopend en ziet u een extensie-bericht met meer informatie over de fout Hallo Hallo artefact.

   ![Voorbeeld van artefacten git-opslagplaats](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a>Problemen met artefacten uit binnen Hallo VM
tooview hello artefact logboeken van binnen Hallo virtuele machine, als volgt te werk:

1. Meld u bij toohello VM die Hallo artefact gewenste toodiagnose bevat.

2. Navigeer tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status waarbij '1,9 Hallo Clientextensie versienummer staat.

   ![Voorbeeld van artefacten git-opslagplaats](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. Open Hallo **status** tooview bestandsgegevens dat helpt bij het artefact mislukte diagnoses voor die VM.




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Verwante blogberichten
* [Deelnemen aan een VM-tooexisting AD-domein met een resource manager-sjabloon in Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[een Git-opslagplaats tooa lab toevoegen](devtest-lab-add-artifact-repo.md).

