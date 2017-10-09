---
title: aaaManage resources met hello Azure CLI | Microsoft Docs
description: Gebruik hello Azure-opdrachtregelinterface (CLI) toomanage Azure resources en groepen
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a>Gebruik hello Azure CLI toomanage Azure resources en resourcegroepen
> [!div class="op_single_selector"]
> * [Portal](resource-group-portal.md) 
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [REST API](resource-manager-rest-api.md)
> 
> 

Hello Azure-opdrachtregelinterface (Azure CLI) is een van verschillende hulpprogramma's kunt u toodeploy gebruiken en beheren van resources met Resource Manager. Dit artikel bevat algemene manieren toomanage Azure resources en resourcegroepen met behulp van Azure CLI Hallo in de modus Resource Manager. Zie voor meer informatie over het gebruik van Hallo CLI toodeploy resources [implementeren van resources met Resource Manager-sjablonen en Azure CLI](resource-group-template-deploy-cli.md). Voor achtergrondinformatie over Azure-resources en Resource Manager, gaat u naar Hallo [overzicht van Azure Resource Manager](resource-group-overview.md).

> [!NOTE]
> toomanage Azure resources Hello Azure CLI, hoeft te[hello Azure CLI installeren](../cli-install-nodejs.md), en [aanmelden tooAzure](../xplat-cli-connect.md) met behulp van Hallo `azure login` opdracht. Zorg ervoor dat Hallo CLI bevindt zich in de modus Resource Manager (uitvoeren `azure config mode arm`). Als u dit allemaal hebt gedaan, bent u klaar toogo.
> 
> 

## <a name="get-resource-groups-and-resources"></a>Get-resourcegroepen en resources
### <a name="resource-groups"></a>Resourcegroepen
een lijst met alle resourcegroepen in uw abonnement en de locaties tooget deze opdracht uitvoeren.

    azure group list


### <a name="resources"></a>Resources
 alle resources in een groep, zoals een met een naam toolist *testRG*, Hallo volgende opdracht gebruiken:

    azure resource list testRG

een afzonderlijke bron binnen Hallo-groep, zoals een virtuele machine met de naam tooview *MyUbuntuVM*, een opdracht zoals Hallo volgende gebruiken:

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

Kennisgeving Hallo **Microsoft.Compute/virtualMachines** parameter. Deze parameter geeft Hallo type Hallo resource aangevraagde informatie op.

> [!NOTE]
> Wanneer u Hallo **azure-resource** opdrachten dan Hallo **lijst** uitvoert, moet u Hallo API-versie van Hallo resource Hello **-o** parameter. Als u niet zeker weet over Hallo API-versie, raadpleegt u het sjabloonbestand Hallo en Hallo apiVersion veld vinden voor Hallo resource. Zie voor meer informatie over API-versies in Resource Manager [resourceproviders en typen](resource-manager-supported-services.md).
> 
> 

Wanneer ze informatie van een resource, is het vaak nuttig toouse hello `--json` parameter. Deze parameter maakt Hallo uitvoer beter leesbaar omdat sommige waarden geneste structuren of verzamelingen zijn. Hallo volgende voorbeeld toont terugkerende Hallo resultaten van Hallo **weergeven** opdracht als een JSON-document.

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> Als u wilt, sla Hallo JSON gegevens toofile met behulp van Hallo &gt; teken toodirect Hallo-uitvoerbestand tooa. Bijvoorbeeld:
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a>Tags
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a>Resources beheren
een resource, zoals een resourcegroep storage account tooa tooadd een vergelijkbaar met opdracht uitvoeren:

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

Bovendien toospecifying API-versie van de resource Hallo Hallo Hello **-o** parameter, gebruik Hallo **-p** parameter toopass JSON-indeling tekenreeks met de vereiste of aanvullende eigenschappen.

toodelete een bestaande resource, zoals de bron van een virtuele machine, een opdracht zoals Hallo volgende gebruiken:

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

toomove bestaande resources tooanother resourcegroep of abonnement, gebruikt u Hallo **azure-resource verplaatsen** opdracht. Hallo volgende voorbeeld wordt getoond hoe toomove een Redis-Cache tooa nieuwe resourcegroep. In Hallo **-i** parameter, Geef een door komma's gescheiden lijst met Hallo resource id toomove.

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a>Beheer toegang tooresources
U kunt gebruiken hello Azure CLI toocreate en beleidsregels toocontrol toegang tooAzure resources beheren. Zie voor achtergrondinformatie over beleidsdefinities en toewijzen beleid tooresources [beleid toomanage resources gebruiken en toegangsbeheer](resource-manager-policy.md).

Bijvoorbeeld Hallo beleid toodeny na alle aanvragen waar locatie niet VS-West of Noordelijk Centraal, VS is definiëren en sla het bestand policy.json van toohello beleid definitie:

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

Voer Hallo **beleidsdefinitie maken** opdracht:

    azure policy definition create MyPolicy -p c:\temp\policy.json

Deze opdracht geeft de vergelijkbare toohello volgende uitvoer:

    + Maken van de beleidsdefinitie MyPolicy gegevens: PolicyName: MyPolicy gegevens: PolicyDefinitionId: /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy

    gegevens: PolicyType: aangepaste gegevens: DisplayName: niet-gedefinieerde gegevens: Beschrijving: niet-gedefinieerde gegevens: PolicyRule: veld = locatie, in = [westus, northcentralus], effect = weigeren

 een beleid voor het Hallo bereik u wilt, gebruik Hallo tooassign **PolicyDefinitionId** geretourneerd van de vorige opdracht Hallo. In Hallo voorbeeld te volgen, is dit bereik Hallo abonnement, maar u kunt het bereik tooresource groepen of afzonderlijke resources:

    Azure beleidstoewijzing maken MyPolicyAssignment -p /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/###-###-###-###-### /

Ophalen, wijzigen of beleidsdefinities verwijderen met behulp van Hallo **beleid definitie weergeven**, **beleid definitieset**, en **beleidsdefinitie verwijderen** opdrachten.

Op dezelfde manier, u kunt ophalen, wijzigen of beleidstoewijzingen verwijderen met behulp van Hallo **beleid toewijzing weergeven**, **beleid toewijzing set**, en **beleidstoewijzing verwijderen** opdrachten .

## <a name="export-a-resource-group-as-a-template"></a>Een resourcegroep exporteren als een sjabloon
U kunt Hallo Resource Manager-sjabloon voor de resourcegroep Hallo weergeven voor een bestaande resourcegroep. Uitvoer Hallo sjabloon biedt twee voordelen:

1. Omdat alle Hallo-infrastructuur in Hallo-sjabloon is gedefinieerd, kunt u eenvoudig toekomstige implementaties van Hallo oplossing automatiseren.
2. U kunt meer vertrouwd raken met de sjabloonsyntaxis van de door te kijken Hallo JSON dat uw oplossing vertegenwoordigt.

Met behulp van hello Azure CLI, kunt u exporteren van een sjabloon waarmee de huidige status van de resourcegroep Hallo of Hallo-sjabloon die is gebruikt voor een bepaalde implementatie downloaden.

* **Exporteer de sjabloon voor een resourcegroep Hallo** -dit is handig wanneer u wijzigingen tooa resourcegroep hebt gemaakt en moet tooretrieve Hallo JSON-weergave van de huidige status. Deze gegenereerde sjabloon Hallo bevat echter alleen een minimum aantal parameters en geen variabelen. De meeste van waarden in de sjabloon Hallo Hallo zijn vastgelegd. Voordat u implementeert Hallo gegenereerd sjabloon, kunt u desgewenst tooconvert meer van de waarden Hallo parameters zodat u Hallo-implementatie voor verschillende omgevingen kan aanpassen.
  
    tooexport hello sjabloon voor een resource groep tooa lokale map uitvoeren Hallo `azure group export` zoals weergegeven in het volgende voorbeeld Hallo opdracht. (Vervangen door een lokale map voor uw omgeving van het besturingssysteem.)
  
        azure group export testRG ~/azure/templates/
* **Hallo-sjabloon voor een bepaalde implementatie downloaden** --dit is handig wanneer u tooview Hallo werkelijke sjabloon die gebruikt toodeploy bronnen is nodig. Hallo-sjabloon bevat alle parameters en variabelen die zijn gedefinieerd voor de oorspronkelijke implementatie Hallo. Als iemand in uw organisatie wijzigingen toohello resourcegroep buiten Hallo definitie in Hallo sjabloon hebt gemaakt, vertegenwoordigen niet met deze sjabloon echter Hallo huidige status van de resourcegroep Hallo.
  
    toodownload Hallo-sjabloon die wordt gebruikt voor een bepaalde implementatie tooa lokale map uitvoeren Hallo `azure group deployment template download` opdracht. Bijvoorbeeld:
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> Exporteren van de sjabloon is een Preview-versie en niet alle brontypen die momenteel ondersteuning voor het exporteren van een sjabloon. Wanneer u probeert een sjabloon tooexport, wordt er een fout die aangeeft dat sommige resources zijn niet geëxporteerd. Indien nodig, handmatig definiëren van deze resources in uw sjabloon nadat deze is gedownload.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* details van implementatiebewerkingen tooget en implementatiefouten Hello Azure CLI oplossen, raadpleegt [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).
* Als u toouse Hallo CLI tooset van een toepassing of script tooaccess bronnen wilt, Zie [gebruik Azure CLI toocreate een service-principal tooaccess resources](resource-group-authenticate-service-principal-cli.md).
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).

