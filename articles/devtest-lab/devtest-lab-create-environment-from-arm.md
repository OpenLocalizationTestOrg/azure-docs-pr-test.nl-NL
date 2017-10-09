---
title: aaaCreate multi-VM-omgevingen en PaaS-resources met Azure Resource Manager-sjablonen | Microsoft Docs
description: Meer informatie over hoe toocreate multi-VM-omgevingen en PaaS-resources in Azure DevTest Labs van een Azure Resource Manager-sjabloon
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: tarcher
ms.openlocfilehash: ab8628f6cb5a666435258efb93921ec69ad3a13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-multi-vm-environments-and-paas-resources-with-azure-resource-manager-templates"></a>Meerdere VM-omgevingen en PaaS-resources met Azure Resource Manager-sjablonen maken

Hallo [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) kunt u tooeasily [maken en toevoegen van een VM tooa lab](https://docs.microsoft.com/en-us/azure/devtest-lab/devtest-lab-add-vm). Dit werkt goed bij het maken van een virtuele machine tegelijk. Als Hallo omgeving meerdere virtuele machines bevat, heeft elke VM toobe afzonderlijk gemaakt. Voor scenario's zoals een meerlaagse Web-app of een SharePoint-farm is een mechanisme benodigde tooallow voor het maken van Hallo van meerdere virtuele machines in één stap. U kunt met behulp van Azure Resource Manager-sjablonen definiëren nu Hallo-infrastructuur en configuratie van uw Azure-oplossing en herhaaldelijk implementeren die meerdere virtuele machines in een consistente status. Deze functie biedt Hallo volgende voordelen:

- Azure Resource Manager-sjablonen zijn geladen rechtstreeks vanuit uw resourcebeheerbibliotheek (GitHub of Team Services Git).
- Na de configuratie, uw gebruikers een omgeving maken door het verzamelen van een Azure Resource Manager-sjabloon van hello Azure-portal als wat ze met andere typen doen kunnen [VM basissen](./devtest-lab-comparing-vm-base-image-types.md).
- Azure PaaS-resources kunnen worden ingericht in een omgeving van een Azure Resource Manager-sjabloon in toevoeging tooIaaS virtuele machines.
- Hallo kosten van omgevingen kan worden bijgehouden in de testomgeving Hallo in toevoeging tooindividual virtuele machines die zijn gemaakt door andere soorten basissen.
- PaaS-resources zijn gemaakt en wordt weergegeven in kosten bijhouden; virtuele machine automatisch afsluiten geldt echter niet tooPaaS resources.
- Gebruikers hebben dezelfde VM beleidscontrole voor omgevingen Hallo aangezien voor één lab virtuele machines.

Meer informatie over Hallo veel [voordelen van het gebruik van Resource Manager-sjablonen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#the-benefits-of-using-resource-manager) toodeploy, bijwerken of verwijderen van al uw lab-resources in één bewerking.

> [!NOTE]
> Wanneer u een Resource Manager-sjabloon als een basis-toocreate meer lab virtuele machines gebruikt, zijn er bepaalde verschillen tookeep rekening of meerdere virtuele machines of één voor virtuele machines te maken. Een virtuele machine gebruiken Azure Resource Manager-sjabloon wordt deze verschillen in meer detail uitgelegd.
>
>

## <a name="configure-azure-resource-manager-template-repositories"></a>Azure Resource Manager-sjabloon opslagplaatsen configureren

Als een best practices Hallo met infrastructuur als code en configuratie als code, omgeving sjablonen moet worden beheerd in broncodebeheer. Azure DevTest Labs volgt deze praktijk en laadt alle sjablonen voor Azure Resource Manager rechtstreeks vanuit GitHub of VSTS Git-opslagplaatsen. Als gevolg hiervan kunnen Resource Manager-sjablonen worden gebruikt over Hallo volledige releasecyclus van Hallo test toohello productieomgeving.

Er zijn een paar regels toofollow tooorganize uw Azure Resource Manager-sjablonen in een opslagplaats:

- Hallo master sjabloonbestand moet de naam `azuredeploy.json`. 

    ![De sjabloonbestanden sleutel Azure Resource Manager](./media/devtest-lab-create-environment-from-arm/master-template.png)

- Desgewenst kunt u parameterwaarden toouse gedefinieerd in een parameterbestand Hallo parameterbestand moet naam `azuredeploy.parameters.json`.
- U kunt de parameters hello gebruiken `_artifactsLocation` en `_artifactsLocationSasToken` tooconstruct hello parametersLink URI-waarde, waardoor DevTest Labs tooautomatically beheren geneste sjablonen. Zie [hoe Azure DevTest Labs gemakkelijker geneste Resource Manager sjabloonimplementaties te maken voor testomgevingen](https://blogs.msdn.microsoft.com/devtestlab/2017/05/23/how-azure-devtest-labs-makes-nested-arm-template-deployments-easier-for-testing-environments/) voor meer informatie.
- Metagegevens kunnen gedefinieerde toospecify Hallo sjabloon weergegeven naam en beschrijving zijn. Deze metagegevens moet zich in een bestand met de naam `metadata.json`. Hallo metagegevensbestand voor volgende voorbeeld ziet u hoe toospecify Hallo naam en beschrijving weergegeven: 

```json
{
 
"itemDisplayName": "<your template name>",
 
"description": "<description of hello template>"
 
}
```

Hallo volgende stappen begeleiden u bij het toevoegen van een opslagplaats tooyour lab met hello Azure-portal. 

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.
1. Selecteer de gewenste lab Hallo in lijst Hallo van labs.   
1. Selecteer op Hallo van labblade, **configuratie en het beleid**.

    ![Configuratie en het beleid](./media/devtest-lab-create-environment-from-arm/configuration-and-policies-menu.png)

1. Van Hallo **configuratie en het beleid** lijst met instellingen, selecteer **opslagplaatsen**. Hallo **opslagplaatsen** blade bevat Hallo-opslagplaatsen toohello lab zijn toegevoegd. Een opslagplaats met de naam `Public Repo` automatisch is gegenereerd voor alle labs en verbindt toohello [DevTest Labs GitHub-repo-](https://github.com/Azure/azure-devtestlab) die bevat verschillende VM artefacten voor het gebruik.

    ![Openbare opslagplaats](./media/devtest-lab-create-environment-from-arm/public-repo.png)

1. Selecteer **toevoegen +** tooadd uw opslagplaats Azure Resource Manager-sjabloon.
1. Wanneer Hallo tweede **opslagplaatsen** blade wordt geopend, voer de benodigde informatie Hallo als volgt:
    - **Naam** -Voer de naam van de Hallo-opslagplaats die wordt gebruikt in Hallo lab.
    - **GIT kloon-URL** -Hallo HTTPS GIT-kloon-URL invoeren in GitHub of Visual Studio Team Services.  
    - **Vertakking** -Hallo vertakking naam tooaccess Voer uw Azure Resource Manager-Sjabloondefinities. 
    - **Persoonlijke toegangstoken** -Hallo persoonlijke toegangstoken wordt gebruikt toosecurely toegang tot uw opslagplaats. uw token vanuit Visual Studio Team Services, selecteert u tooget  **&lt;uwnaam >> Mijn profiel > Beveiliging > openbare toegangstoken**. tooget uw token vanuit GitHub, selecteer uw avatar gevolgd door het selecteren van **instellingen > openbare toegangstoken**. 
    - **Paden voor mappen** - met behulp van een Hallo twee invoervelden, Voer Hallo mappad dat begint met een slash - / - en relatieve tooyour Git kloon-URI tooeither is uw artefactdefinities (eerste invoerveld) of de Azure Resource Manager-sjabloon definities.   
    
        ![Openbare opslagplaats](./media/devtest-lab-create-environment-from-arm/repo-values.png)

1. Wanneer alle vereiste Hallo velden worden ingevoerd en Hallo zijn gevalideerd, selecteren **opslaan**.

de volgende sectie Hallo begeleidt u stapsgewijs door omgevingen maken uit een Azure Resource Manager-sjabloon.

## <a name="create-an-environment-from-an-azure-resource-manager-template"></a>Een omgeving met een Azure Resource Manager-sjabloon maken

Als een opslagplaats Azure Resource Manager-sjabloon is geconfigureerd in de testomgeving hello, kunnen uw lab-gebruikers een omgeving met behulp van Azure portal met de volgende stappen uit Hallo maken:

1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.
1. Selecteer de gewenste lab Hallo in lijst Hallo van labs.   
1. Selecteer op Hallo van labblade, **toevoegen +**.
1. Hallo **kiezen een base** blade Hallo basisinstallatiekopieën kunt u met Azure Resource Manager-sjablonen Hallo bovenaan wordt weergegeven. Selecteer Hallo gewenste Azure Resource Manager-sjabloon.

    ![Kies een base](./media/devtest-lab-create-environment-from-arm/choose-a-base.png)
  
1. Op Hallo **toevoegen** blade Voer Hallo **omgevingsnaam** waarde. de naam van de omgeving Hallo is wat gebruikers in de testomgeving Hallo weergegeven tooyour is. de resterende invoervelden Hallo zijn gedefinieerd in hello Azure Resource Manager-sjabloon. Als de standaardwaarden zijn gedefinieerd in Hallo-sjabloon of Hallo `azuredeploy.parameter.json` bestand aanwezig is, de standaardwaarden worden weergegeven in de invoervelden. Voor de parameters van het type *tekenreeks secure*, kunt u Hallo geheimen die zijn opgeslagen in de Hallo lab [persoonlijke archief van de geheime](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store).

    ![Blade toevoegen](./media/devtest-lab-create-environment-from-arm/add.png)

    > [!NOTE]
    > Er zijn verschillende parameterwaarden die - zelfs als opgegeven - als lege waarden worden weergegeven. Dus als gebruikers die tooparameters waarden in een Azure Resource Manager-sjabloon toewijzen, worden DevTest Labs niet weergegeven Hallo waarden; in plaats daarvan leeg invoervelden waarbij Hallo lab gebruikers tooenter moeten een waarde weergeeft bij het maken van Hallo-omgeving.
    > 
    > - GEN UNIEKE
    > - -UNIEKE - GEN [N]
    > - GEN-SSH-PUB-KEY
    > - GEN-WACHTWOORD 
 
1. Selecteer **toevoegen** toocreate Hallo-omgeving. Hallo-omgeving wordt gestart onmiddellijk inrichten met de Hallo status weergeven in Hallo **mijn virtuele machines** lijst. Een nieuwe resourcegroep wordt automatisch gemaakt door Hallo lab tooprovision alle Hallo resources in hello Azure Resource Manager-sjabloon worden gedefinieerd.
1. Zodra Hallo-omgeving is gemaakt, selecteert u Hallo-omgeving in Hallo **mijn virtuele machines** lijst tooopen hello resourcegroepblade en blader alle Hallo-resources die zijn ingericht in Hallo-omgeving.
    
    ![De lijst met virtuele machines](./media/devtest-lab-create-environment-from-arm/all-environment-resources.png)
   
   U kunt ook uitbreiden Hallo omgeving tooview alleen Hallo lijst met virtuele machines die zijn ingericht op Hallo-omgeving.
    
    ![De lijst met virtuele machines](./media/devtest-lab-create-environment-from-arm/my-vm-list.png)

1. Klik op een Hallo omgevingen tooview Hallo beschikbare acties - zoals het toepassen van artefacten, gegevensschijven veranderende automatisch afsluiten en tijd meer koppelen.

    ![Omgeving acties](./media/devtest-lab-create-environment-from-arm/environment-actions.png)

## <a name="next-steps"></a>Volgende stappen
* Wanneer een virtuele machine is gemaakt, kunt u toohello VM door te selecteren **Connect** op Hallo van de virtuele machine-blade.
* Resources weergeven en beheren in een omgeving met de Hallo-omgeving in Hallo **mijn virtuele machines** lijst in uw testomgeving. 
* Hallo verkennen [Azure Resource Manager-sjablonen uit Azure sjabloon snelstartgalerie](https://github.com/Azure/azure-quickstart-templates)
