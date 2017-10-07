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
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a>Aangepaste artefacten maken voor uw DevTest Labs VM
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a>Overzicht
**Artefacten** gebruikte toodeploy zijn en uw toepassing configureren nadat een virtuele machine is ingericht. Een artefact bestaat uit een definitiebestand van artefacten en andere scriptbestanden die zijn opgeslagen in een map in een git-opslagplaats. Artefacten definitiebestanden bestaan uit JSON en uitdrukkingen die u kunt gebruiken toospecify wat u wilt tooinstall op een virtuele machine. U kunt bijvoorbeeld definiëren Hallo-naam van een artefact opdracht toorun parameters, en die beschikbaar worden gesteld wanneer het Hallo-opdracht wordt uitgevoerd. U kunt tooother scriptbestanden binnen Hallo artefact definitiebestand verwijzen met de naam.

## <a name="artifact-definition-file-format"></a>Bestandsindeling van pakketdefinities artefact
Hallo toont volgende voorbeeld Hallo secties die gezamenlijk Hallo basisstructuur van een definitiebestand van:

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

| Elementnaam | Vereist? | Beschrijving |
| --- | --- | --- |
| $schema |Nee |Locatie van Hallo JSON-schema-bestand waarmee tests Hallo geldigheid van Hallo definitiebestand. |
| titel |Ja |Naam van de weergegeven in de testomgeving Hallo Hallo-artefacten. |
| description |Ja |Beschrijving van de weergegeven in de testomgeving Hallo Hallo-artefacten. |
| iconUri |Nee |De URI van Hallo pictogram dat wordt weergegeven in de testomgeving Hallo. |
| targetOsType |Ja |Besturingssysteem van Hallo VM waarop artefact is geïnstalleerd. Ondersteunde opties zijn: Windows- en Linux. |
| parameters |Nee |De waarden die worden opgegeven wanneer de installatieopdracht artefact wordt uitgevoerd op een machine. Dit helpt bij het aanpassen van uw artefacten. |
| OpdrachtUitvoeren |Ja |Artefacten installeren de opdracht die wordt uitgevoerd op een virtuele machine. |

### <a name="artifact-parameters"></a>Parameters van artefacten
U opgeven welke waarden van een gebruiker kan invoer bij het installeren van een artefact in Hallo gedeelte parameters van Hallo definitiebestand van. U kunt toothese waarden in Hallo artefact installatieopdracht verwijzen.

U kunt parameters definiëren Hello structuur te volgen:

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| Elementnaam | Vereist? | Beschrijving |
| --- | --- | --- |
| type |Ja |Type van parameterwaarde. Zie Hallo lijst met toegestane typen hello te volgen: |
| Weergavenaam |Ja |Naam van het Hallo-parameter die de gebruiker weergegeven tooa in Hallo lab is. | |
| description |Ja |Beschrijving van het Hallo-parameter die wordt weergegeven in de testomgeving Hallo. |

Hallo toegestane typen zijn:

* tekenreeks – een willekeurige geldige JSON-tekenreeks
* int – een geldige JSON geheel getal
* BOOL – geldige JSON Boole
* matrix – een geldig JSON-matrix

## <a name="artifact-expressions-and-functions"></a>Artefacten expressies en functies
U kunt een expressie en functies tooconstruct Hallo artefact installatieopdracht.
Expressies tussen haakjes ([en]), en worden geëvalueerd wanneer Hallo artefact is geïnstalleerd. Expressies kunnen overal voorkomen in een string-waarde van JSON en altijd een andere JSON-waarde retourneren. Als u moet een letterlijke tekenreeks die met een haakje begint toouse [, moet u twee haken [[.
Normaal gesproken gebruikt u expressies met functies tooconstruct een waarde. Net als in JavaScript zijn-functieaanroepen die opgemaakt als functionName(arg1,arg2,arg3).

Hallo bevat volgende lijst algemene functies:

* parameters(parameterName) - retourneert een waarde van parameter die is opgegeven als Hallo artefact-opdracht wordt uitgevoerd.
* concat (arg1, arg2, arg3,...) - combineert meerdere tekenreekswaarden. Deze functie kan duren voordat een willekeurig aantal argumenten.

Hallo volgende voorbeeld wordt getoond hoe toouse expressie en functies tooconstruct een waarde:

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a>Een aangepaste artefacten maken
Uw aangepaste artefacten maken met de volgende stappen:

1. Installeer een JSON-editor - moet u een JSON-editor toowork met artefacten definitiebestanden. Wordt u aangeraden [Visual Studio Code](https://code.visualstudio.com/), die beschikbaar is voor Windows, Linux en OS X.
2. Een voorbeeld artifactfile.json - uitchecken Hallo artefacten gemaakt door het team van Azure DevTest Labs op Get onze [GitHub-opslagplaats](https://github.com/Azure/azure-devtestlab), waarbij er een uitgebreide bibliotheek met gemaakt artefacten die u helpen uw eigen artefacten maken. Download een definitiebestand van artefacten en wijzigingen tooit toocreate uw eigen artefacten maken.
3. Maakt gebruik van IntelliSense - hefboomwerking IntelliSense toosee geldige elementen die gebruikt tooconstruct worden kunnen een definitiebestand van artefacten. U ziet ook Hallo verschillende opties voor waarden van een element. Bijvoorbeeld: IntelliSense weergeven u twee mogelijkheden van Windows of Linux Hallo bij het bewerken van Hallo **targetOsType** element.
4. Store Hallo artefacten in een [git-opslagplaats](devtest-lab-add-artifact-repo.md).
   
   1. Maak een afzonderlijke map voor elke artefact waar Hallo mapnaam is Hallo dezelfde als de naam van de artefacten Hallo.
   2. Hallo artefact-definitiebestand (artifactfile.json) opslaan in Hallo-directory die u hebt gemaakt.
   3. Installatieopdracht Store Hallo scripts waarnaar wordt verwezen vanaf Hallo artefacten.
      
      Hier volgt een voorbeeld van een map artefact kan als volgt uitzien:
      
      ![Voorbeeld van artefacten git-opslagplaats](./media/devtest-lab-artifact-author/git-repo.png)
5. Hallo artefacten opslagplaats toohello lab Add - toohello artikel, Raadpleeg [een Git-opslagplaats voor artefacten en sjablonen toevoegen](devtest-lab-add-artifact-repo.md).

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a>Verwante artikelen:
* [Hoe toodiagnose artefact fouten in DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md)
* [Deelnemen aan een VM-tooexisting AD-domein met een resource manager-sjabloon in Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[een Git artefact opslagplaats tooa lab toevoegen](devtest-lab-add-artifact-repo.md).

