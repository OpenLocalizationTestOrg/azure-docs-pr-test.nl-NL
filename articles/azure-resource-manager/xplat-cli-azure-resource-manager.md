---
title: Resources beheren met de Azure CLI | Microsoft Docs
description: De Azure-opdrachtregelinterface (CLI) gebruiken voor het beheren van Azure-resources en groepen
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
ms.openlocfilehash: 3ad4e68b90979fd7f9d3ddf5278e65e19cb07152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-cli-to-manage-azure-resources-and-resource-groups"></a>De Azure CLI gebruiken voor het beheren van Azure-resources en resourcegroepen
> [!div class="op_single_selector"]
> * [Portal](resource-group-portal.md) 
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [REST API](resource-manager-rest-api.md)
> 
> 

De Azure-opdrachtregelinterface (Azure CLI) is een van de verschillende hulpprogramma's die u gebruiken kunt om te implementeren en beheren van resources met Resource Manager. Dit artikel bevat algemene manieren voor het beheren van Azure-resources en resourcegroepen met behulp van de Azure CLI in de modus Resource Manager. Zie voor meer informatie over het implementeren van resources met de CLI [implementeren van resources met Resource Manager-sjablonen en Azure CLI](resource-group-template-deploy-cli.md). Voor achtergrondinformatie over Azure-resources en Resource Manager, gaat u naar de [overzicht van Azure Resource Manager](resource-group-overview.md).

> [!NOTE]
> Voor het beheren van Azure-resources met de Azure CLI, moet u [Azure CLI installeren](../cli-install-nodejs.md), en [aanmelden bij Azure](../xplat-cli-connect.md) met behulp van de `azure login` opdracht. Controleer of de CLI in de modus Resource Manager (uitvoeren `azure config mode arm`). Als u dit allemaal hebt gedaan, bent u klaar voor gebruik.
> 
> 

## <a name="get-resource-groups-and-resources"></a>Get-resourcegroepen en resources
### <a name="resource-groups"></a>Resourcegroepen
Als u een lijst met alle resourcegroepen in uw abonnement en de locaties, moet u deze opdracht uitvoeren.

    azure group list


### <a name="resources"></a>Resources
 Voor een lijst met alle bronnen in een groep, zoals een met de naam *testRG*, gebruik de volgende opdracht:

    azure resource list testRG

Om weer te geven van een afzonderlijke resource binnen de groep, zoals een virtuele machine met de naam *MyUbuntuVM*, een opdracht als volgt gebruiken:

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

U ziet de **Microsoft.Compute/virtualMachines** parameter. Deze parameter geeft het type van de resource die u aanvraagt informatie op.

> [!NOTE]
> Wanneer u de **azure-resource** opdrachten anders dan de **lijst** opdracht, moet u de API-versie van de resource met de **-o** parameter. Als u niet zeker weet over de API-versie, raadpleegt u het sjabloonbestand en het veld apiVersion voor de resource niet vinden. Zie voor meer informatie over API-versies in Resource Manager [resourceproviders en typen](resource-manager-supported-services.md).
> 
> 

Wanneer u details weergeven van een resource, is het vaak handig om te gebruiken de `--json` parameter. Deze parameter wordt de uitvoer beter leesbaar omdat sommige waarden geneste structuren of verzamelingen zijn. Het volgende voorbeeld toont de resultaten van de **weergeven** opdracht als een JSON-document.

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> Als u wilt, slaat u de JSON-gegevens naar bestand met behulp van de &gt; teken de uitvoer naar een bestand. Bijvoorbeeld:
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a>Tags
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a>Resources beheren
Als u wilt een resource zoals een opslagaccount toevoegen aan een resourcegroep, een vergelijkbaar met opdracht wordt uitgevoerd:

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

Naast het opgeven van de API-versie van de resource met de **-o** parameter, gebruik de **-p** parameter tekenreeks met de vereiste JSON-indeling of extra eigenschappen moeten worden doorgegeven.

Voor het verwijderen van een bestaande resource, zoals de bron van een virtuele machine, moet u een opdracht als volgt gebruiken:

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

U kunt bestaande resources verplaatsen naar een andere resourcegroep of abonnement met de **azure-resource verplaatsen** opdracht. Het volgende voorbeeld laat zien hoe een Redis-Cache verplaatsen naar een nieuwe resourcegroep. In de **-i** parameter, Geef een door komma's gescheiden lijst van de resource-id's te verplaatsen.

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-to-resources"></a>Toegang tot resources beheren
De Azure CLI kunt u beleidsregels voor het beheren van toegang tot Azure-resources maken en beheren. Zie voor achtergrondinformatie over beleidsregels en beleidsregels toewijzen aan resources [beleid gebruiken voor het beheren van resources en toegangsbeheer](resource-manager-policy.md).

Bijvoorbeeld het volgende beleid voor het weigeren van alle aanvragen waar locatie niet VS-West of Noordelijk Centraal, VS is definiëren en opslaan in het beleid definitie bestand policy.json:

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

Voer vervolgens de **beleidsdefinitie maken** opdracht:

    azure policy definition create MyPolicy -p c:\temp\policy.json

Deze opdracht geeft u de uitvoer ziet er als volgt:

    + Maken van de beleidsdefinitie MyPolicy gegevens: PolicyName: MyPolicy gegevens: PolicyDefinitionId: /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy

    gegevens: PolicyType: aangepaste gegevens: DisplayName: niet-gedefinieerde gegevens: Beschrijving: niet-gedefinieerde gegevens: PolicyRule: veld = locatie, in = [westus, northcentralus], effect = weigeren

 Als u een beleid voor het bereik dat u wilt toewijzen, gebruikt u de **PolicyDefinitionId** geretourneerd van de vorige opdracht. Dit bereik is het abonnement in het volgende voorbeeld, maar u kunt het bereik aan resourcegroepen of afzonderlijke resources:

    Azure beleidstoewijzing maken MyPolicyAssignment -p /subscriptions/###-###-###-###-###/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/###-###-###-###-### /

U kunt ophalen, wijzigen of beleidsdefinities verwijderen met behulp van de **beleid definitie weergeven**, **beleid definitieset**, en **beleidsdefinitie verwijderen** opdrachten.

Op dezelfde manier, u kunt ophalen, wijzigen of beleidstoewijzingen verwijderen met behulp van de **beleid toewijzing weergeven**, **beleid toewijzing set**, en **beleidstoewijzing verwijderen** opdrachten.

## <a name="export-a-resource-group-as-a-template"></a>Een resourcegroep exporteren als een sjabloon
U kunt de Resource Manager-sjabloon voor de resourcegroep weergeven voor een bestaande resourcegroep. De sjabloon exporteren biedt twee voordelen:

1. Omdat de infrastructuur in de sjabloon is gedefinieerd, kunt u eenvoudig toekomstige implementaties van de oplossing automatiseren.
2. U kunt meer vertrouwd raken met de sjabloonsyntaxis van de door te kijken in de JSON die uw oplossing vertegenwoordigt.

Met de Azure CLI, kunt u een sjabloon met de huidige status van de resourcegroep exporteren of downloaden van de sjabloon die is gebruikt voor een bepaalde implementatie.

* **De sjabloon voor een resourcegroep exporteren** -dit is handig wanneer u wijzigingen aan een resourcegroep aangebracht en moet de JSON-weergave van de huidige status ophalen. De gegenereerde sjabloon bevat echter alleen een minimum aantal parameters en geen variabelen. De meeste van de waarden in de sjabloon zijn vastgelegd. Voordat u de gegenereerde sjabloon implementeert, wilt u mogelijk meer van de waarden converteren naar parameters, zodat u de implementatie voor verschillende omgevingen kan aanpassen.
  
    Uitvoeren als u wilt de sjabloon voor een resourcegroep exporteren naar een lokale map, de `azure group export` opdracht zoals weergegeven in het volgende voorbeeld. (Vervangen door een lokale map voor uw omgeving van het besturingssysteem.)
  
        azure group export testRG ~/azure/templates/
* **Download de sjabloon voor een bepaalde implementatie** --dit is handig als u weergeven van de werkelijke sjabloon die is gebruikt wilt voor het implementeren van resources. De sjabloon bevat alle parameters en variabelen die zijn gedefinieerd voor de oorspronkelijke implementatie. Als iemand zich in uw organisatie wijzigingen in de resourcegroep buiten de definitie van de sjabloon aangebracht, vertegenwoordigen niet met deze sjabloon echter in de huidige status van de resourcegroep.
  
    Voor het downloaden van de sjabloon voor een bepaalde implementatie naar een lokale map gebruikt, voer de `azure group deployment template download` opdracht. Bijvoorbeeld:
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> Exporteren van de sjabloon is een Preview-versie en niet alle brontypen die momenteel ondersteuning voor het exporteren van een sjabloon. Wanneer u probeert om een sjabloon te exporteren, wordt er een fout die aangeeft dat sommige resources zijn niet geëxporteerd. Indien nodig, handmatig definiëren van deze resources in uw sjabloon nadat deze is gedownload.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* U kunt details van implementatiebewerkingen ophalen en implementatie fouten met de Azure CLI, Zie [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).
* Als u de CLI gebruik wilt voor het instellen van een toepassing of het script voor toegang tot bronnen, Zie [Azure CLI gebruiken voor het maken van een service-principal voor toegang tot bronnen](resource-group-authenticate-service-principal-cli.md).
* Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).

