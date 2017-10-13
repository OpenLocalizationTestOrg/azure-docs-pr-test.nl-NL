---
title: Aan de slag met Azure CLI voor Batch | Microsoft Docs
description: Een korte inleiding in de Batch-opdrachten in Azure CLI voor het beheren van Azure Batch-serviceresources
services: batch
documentationcenter: 
author: v-dotren
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 09/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 68a5493282fa4a0b54ba551c48ae963a42b94dca
ms.sourcegitcommit: 51ea178c8205726e8772f8c6f53637b0d43259c6
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/11/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a>Batch-resources beheren met Azure CLI

De Azure CLI 2.0 is de nieuwe opdrachtregelervaring van Azure voor het beheer van Azure-resources. Deze kan worden gebruikt in Mac OS, Linux en Windows. Azure CLI 2.0 is geoptimaliseerd voor het beheren van Azure-resources vanaf de opdrachtregel. U kunt de Azure CLI gebruiken om uw Azure Batch-accounts te beheren en om resources zoals pools, functies en taken te beheren. Met de Azure CLI kunt u scripts maken om veel van dezelfde taken uit te voeren die u ook uitvoert met de Batch-API's, Azure Portal en Batch PowerShell-cmdlets.

Dit artikel biedt een overzicht van het gebruik van [Azure CLI versie 2.0](https://docs.microsoft.com/cli/azure/overview) met Batch. Zie [Aan de slag met Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) voor een overzicht van het gebruik van CLI met Azure.

Microsoft adviseert om de nieuwste versie van Azure CLI te gebruiken, versie 2.0. Meer informatie over versie 2.0 kunt u lezen in [Azure Command Line 2.0 now generally available](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/) (Azure Command Line 2.0 nu algemeen beschikbaar).

## <a name="set-up-the-azure-cli"></a>De Azure CLI instellen

Volg de stappen in [Azure CLI installeren](https://docs.microsoft.com/cli/azure/install-azure-cli) voor het installeren van de Azure CLI.

> [!TIP]
> Het wordt aangeraden de Azure CLI-installatie regelmatig bij te werken om te profiteren van service-updates en verbeteringen.
> 
> 

## <a name="command-help"></a>Opdracht Help

U kunt voor elke opdracht in de Azure CLI Help-tekst weergeven door `-h` toe te voegen aan de opdracht. Laat alle andere opties weg. Bijvoorbeeld:

* Als u hulp nodig hebt bij de opdracht `az`, voert u in: `az -h`
* Voor een lijst met alle Batch-opdrachten in de opdrachtregelinterface, gebruikt u: `az batch -h`
* Als u hulp nodig hebt bij het maken van een Batch-account, voert u in: `az batch account create -h`

Gebruik bij twijfel de opdrachtregeloptie `-h` voor hulp bij een willekeurige Azure CLI-opdracht.

> [!NOTE]
> In eerdere versies van de Azure CLI werd `azure` gebruikt vóór een CLI-opdracht. In versie 2.0 worden alle opdrachten nu voorafgegaan door `az`. Vergeet niet om uw scripts bij te werken met de nieuwe syntaxis van versie 2.0.
>
>  

Raadpleeg de naslagdocumentatie van Azure CLI voor informatie over [Azure CLI-opdrachten voor Batch](https://docs.microsoft.com/cli/azure/batch). 

## <a name="log-in-and-authenticate"></a>Aanmelden en verifiëren

Als u de Azure CLI wilt gebruiken met Batch, moet u zich aanmelden en verifiëren. Dit kan via twee eenvoudige stappen:

1. **Aanmelden bij Azure.** Als u bent aangemeld bij Azure, hebt u toegang tot opdrachten van Azure Resource Manager, inclusief opdrachten van de [Batch Management-service](batch-management-dotnet.md).  
2. **Aanmelden bij uw Batch-account.** Als u bent aangemeld bij uw Batch-account, hebt u toegang tot opdrachten van de Batch-service.   

### <a name="log-in-to-azure"></a>Meld u aan bij Azure.

Er zijn een aantal manieren om u aan te melden bij Azure, zoals u kunt lezen in [Aanmelden met de Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):

1. [Interactief aanmelden](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#az_authenticate_azure_cli_interactive_log_in). Meld u interactief aan wanneer u zelf Azure CLI-opdrachten uitvoert vanaf de opdrachtregel.
2. [Aanmelden met een service-principal](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#az_authenticate_azure_cli_logging_in_with_a_service_principal). Meld u aan met een service-principal wanneer u Azure CLI-opdrachten uitvoert vanuit een script of een toepassing.

Ten behoeve van dit artikel laten we zien hoe u zich interactief aanmeldt bij Azure. Typ [az login](https://docs.microsoft.com/cli/azure/#login) op de opdrachtregel:

```azurecli
# Log in to Azure and authenticate interactively.
az login
```

De opdracht `az login` retourneert een token dat u kunt gebruiken om u te verifiëren, zoals hier wordt weergegeven. Volg de weergegeven instructies om een webpagina te openen en het token naar Azure te verzenden:

![Meld u aan bij Azure.](./media/batch-cli-get-started/az-login.png)

De voorbeelden in de sectie [Voorbeelden van shell-scripts](#sample-shell-scripts) laten ook zien hoe u een Azure CLI-sessie start door u interactief aan te melden bij Azure. Wanneer u bent aangemeld, kunt u opdrachten aanroepen voor gebruik met resources van Batch Management, met inbegrip van Batch-accounts, sleutels, toepassingspakketten en quota's.  

### <a name="log-in-to-your-batch-account"></a>Aanmelden bij uw Batch-account

Als u de Azure CLI wilt gebruiken voor het beheren van Batch-resources, zoals pools, functies en taken, moet u zich aanmelden bij uw Batch-account en u vervolgens verifiëren. U kunt zich aanmelden bij de Batch-service met de opdracht [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#az_batch_account_login). 

Er zijn twee mogelijkheden voor verificatie van uw Batch-account:

- **Met behulp van Azure AD-verificatie (Azure Active Directory).** 

    Verificatie met Azure AD is de standaardinstelling als u de Azure CLI gebruikt met Batch en wordt aanbevolen voor de meeste scenario's. 
    
    Wanneer u zich interactief aanmeldt bij Azure, zoals beschreven in de vorige sectie, worden uw referenties in de cache opgeslagen, zodat de Azure CLI u met behulp van deze zelfde referenties kan aanmelden bij uw Batch-account. Als u zich aanmeldt bij Azure met behulp van een service-principal, worden deze referenties ook gebruikt voor aanmelding bij uw Batch-account.

    Een voordeel van Azure AD is de ondersteuning voor toegangsbeheer op basis van rollen (RBAC). Met RBAC is de toegang van gebruikers afhankelijk van hun rol, in plaats van of ze wel of niet over de accountsleutels beschikken. U hoeft dus geen accountsleutels te beheren, maar RBAC-rollen, waarna Azure AD de toegang en verificatie afhandelt.  

        To log in to your Batch account using Azure AD, call the [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#az_batch_account_login) command: 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- **Met behulp van gedeelde sleutelverificatie.**

    Bij [gedeelde sleutelverificatie](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) worden de toegangssleutels van uw account gebruikt om Azure CLI-opdrachten te verifiëren voor de Batch-service.

    Als u Azure CLI-scripts maakt om het aanroepen van Batch-opdrachten te automatiseren, kunt u gebruikmaken van gedeelde sleutelverificatie of van een service-principal van Azure AD. In sommige scenario's kan gedeelde sleutelverificatie een eenvoudigere oplossing zijn dan het maken van een service-principal.  

    Als u zich wilt aanmelden met behulp van gedeelde sleutelverificatie, gebruikt u de optie `--shared-key-auth` op de opdrachtregel:

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

De voorbeelden in de sectie [Voorbeelden van shell-scripts](#sample-shell-scripts) laten zien hoe u zich met de Azure CLI aanmeldt bij uw Batch-account met zowel Azure AD als een gedeelde sleutel.

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Azure Batch CLI-sjablonen en -bestandsoverdracht gebruiken (preview)

U kunt de Azure CLI gebruiken om Batch-taken end-to-end uit te voeren zonder code te schrijven. Batch-sjabloonbestanden ondersteunen het maken van pools, jobs en taken met de Azure CLI. U kunt de Azure CLI ook gebruiken om jobinvoerbestanden te uploaden naar het Azure Storage-account dat is gekoppeld aan het Batch-account en de jobuitvoerbestanden ervan downloaden. Zie [Azure Batch CLI sjablonen en -bestandsoverdracht gebruiken (preview)](batch-cli-templates.md) voor meer informatie.

## <a name="sample-shell-scripts"></a>Voorbeelden van shell-scripts

De voorbeeldscripts in de volgende tabel laten zien hoe u Azure CLI-opdrachten gebruikt met de Batch-service en de Batch-Management-service om veelvoorkomende taken uit te voeren. In deze voorbeeldscripts worden veel van de opdrachten behandeld die beschikbaar zijn in de Azure CLI voor Batch. 

| Script | Opmerkingen |
|---|---|
| [Een Batch-account maken](./scripts/batch-cli-sample-create-account.md) | Hiermee maakt u een Batch-account en wordt dit gekoppeld aan een opslagaccount. |
| [Een toepassing toevoegen](./scripts/batch-cli-sample-add-application.md) | Hiermee voegt u een toepassing toe en worden pakketten met binaire bestanden geüpload.|
| [Batch-pools beheren](./scripts/batch-cli-sample-manage-pool.md) | In dit script ziet u hoe u pools maakt, deze groter of kleiner maakt en beheert. |
| [Een functie en taken uitvoeren met Batch](./scripts/batch-cli-sample-run-job.md) | In dit script ziet u hoe u een functie uitvoert en taken toevoegt. |

## <a name="json-files-for-resource-creation"></a>JSON-bestanden voor het maken van resources

Als u Batch-resources maakt, zoals groepen en taken, kunt u een JSON-bestand opgeven dat de configuratie van de nieuwe resource bevat, in plaats van de bijbehorende parameters op te geven als opdrachtregelopties. Bijvoorbeeld:

```azurecli
az batch pool create my_batch_pool.json
```

Hoewel u de meeste resources kunt maken met alleen opdrachtregelopties, is voor sommige functies vereist dat u een bestand met de JSON-indeling opgeeft met daarin details van de resource. U moet bijvoorbeeld een JSON-bestand gebruiken als u resourcebestanden wilt opgeven voor een starttaak.

Informatie over de juiste JSON-syntaxis voor het maken van een resource vindt u in de Engelstalige [Azure Batch REST API Reference][rest_api]. De onderwerpen voor het toevoegen van een *resourcetype* in de Azure Batch REST API Reference bevat JSON-voorbeeldscripts voor het maken van die resource. U kunt deze JSON-voorbeeldscripts als sjablonen gebruiken voor JSON-bestanden die u met de Azure CLI wilt gebruiken. Als u bijvoorbeeld de JSON-syntaxis wilt zien voor het maken van een pool, raadpleegt u [Add a pool to an account][rest_add_pool] (Een pool toevoegen aan een account).

Zie [Running jobs on Azure Batch with Azure CLI](./scripts/batch-cli-sample-run-job.md) (Taken uitvoeren in Azure Batch met Azure CLI) voor een voorbeeld van een script waarin een JSON-bestand is opgegeven.

> [!NOTE]
> Als u een JSON-bestand opgeeft bij het maken van een resource, worden alle andere parameters die u opgeeft op de opdrachtregel, genegeerd.
> 
> 

## <a name="efficient-queries-for-batch-resources"></a>Efficiënte query's voor Batch-resources

Elk Batch-resourcetype ondersteunt een `list`-opdracht die een query uitvoert voor het Batch-account, en vermeldt een lijst met resources van dit type. U kunt bijvoorbeeld de groepen in uw account vermelden en de taken in een taak:

```azurecli
az batch pool list
az batch task list --job-id job001
```

Wanneer u op de Batch-service een query uitvoert met daarin een `list`-bewerking, kunt u een OData-component opgeven om de hoeveelheid geretourneerde gegevens te beperken. Omdat de filteracties op de server plaatsvinden, worden alleen de gegevens geretourneerd waarin u bent geïnteresseerd. Gebruik deze componenten om bandbreedte (en dus tijd) te besparen tijdens het uitvoeren van lijstbewerkingen.

De volgende tabel beschrijft de OData-componenten die worden ondersteund door de Batch-service:

| Component | Beschrijving |
|---|---|
| `--select-clause [select-clause]` | Retourneert een subset met eigenschappen voor elke entiteit. |
| `--filter-clause [filter-clause]` | Retourneert alleen entiteiten die overeenkomen met de opgegeven OData-expressie. |
| `--expand-clause [expand-clause]` | Vraagt de entiteitgegevens op in één onderliggende REST-aanroep. De component expand ondersteunt momenteel alleen de eigenschap `stats`. |

Zie [Een functie en taken uitvoeren met Batch](./scripts/batch-cli-sample-run-job.md) voor een voorbeeld van een script dat laat zien hoe u een OData-component gebruikt.

Zie [Create queries to list Batch resources efficiently](batch-efficient-list-queries.md) (Query's maken om efficiënt Batch-resources op te vragen) voor meer informatie over het uitvoeren van efficiënte lijstquery's met OData-componenten.

## <a name="troubleshooting-tips"></a>Tips voor probleemoplossing

De volgende tips kunnen helpen bij het oplossen van problemen met Azure CLI:

* Gebruik `-h` om **Help-tekst** weer te geven voor elke willekeurige CLI-opdracht
* Gebruik `-v` en `-vv` om **uitgebreide** opdrachtuitvoer weer te geven. Als u de vlag `-vv` toevoegt, toont de Azure CLI de werkelijke REST-aanvragen en -antwoorden. Deze schakelopties zijn handig voor het weergeven van de volledige foutuitvoer.
* U kunt **opdrachtuitvoer weergeven als JSON** met de `--json`-optie. `az batch pool show pool001 --json` wordt bijvoorbeeld weergegeven als eigenschappen van pool001 in de JSON-indeling. Vervolgens kunt u deze uitvoer kopiëren en aanpassen om te worden gebruikt in een `--json-file` (zie [JSON-bestanden](#json-files) eerder in dit artikel).
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting to any location.--->
* Het [Batch-forum][batch_forum] wordt gecontroleerd door leden van het Batch-team. U kunt hier vragen posten als u problemen hebt of hulp nodig hebt met een bepaalde bewerking.

## <a name="next-steps"></a>Volgende stappen

* Raadpleeg de [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview) voor meer informatie over de Azure CLI.
* Meer informatie over Batch-resources vindt u in dit Engelstalige [overzicht van Azure Batch voor ontwikkelaars](batch-api-basics.md).
* Zie [Azure Batch CLI-sjablonen en -bestandsoverdracht gebruiken (preview)](batch-cli-templates.md) voor meer informatie over het gebruik van Batch-sjablonen voor het maken van pools, jobs en taken zonder code te schrijven.

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
