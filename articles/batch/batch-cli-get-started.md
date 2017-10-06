---
title: aaaGet de slag met Azure CLI voor Batch | Microsoft Docs
description: Get-een korte inleiding toohello batchopdrachten in de Azure CLI voor het beheren van bronnen van Azure Batch-service
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14f28311ecb16c8097d0d304a4ad89de282a2e9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a>Batch-resources beheren met Azure CLI

Hello Azure CLI 2.0 is een nieuwe Azure opdrachtregelprogramma ervaring voor het beheren van Azure-resources. Deze kan worden gebruikt in Mac OS, Linux en Windows. Azure CLI 2.0 is geoptimaliseerd voor het beheren en Azure-resources beheren vanaf Hallo-opdrachtregel. U kunt hello Azure CLI toomanage uw Azure Batch-accounts en toomanage resources zoals pools, jobs en taken. Hello Azure CLI, kunt u veel van Hallo script dezelfde taken die u met uitvoert Hallo Batch-API's, Azure-portal en Batch PowerShell-cmdlets.

Dit artikel biedt een overzicht van het gebruik van [Azure CLI versie 2.0](https://docs.microsoft.com/cli/azure/overview) met Batch. Zie [aan de slag met Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) voor een overzicht van het gebruik van Hallo CLI met Azure.

Microsoft raadt u aan met de nieuwste versie Hallo van hello Azure CLI versie 2.0. Meer informatie over versie 2.0 kunt u lezen in [Azure Command Line 2.0 now generally available](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/) (Azure Command Line 2.0 nu algemeen beschikbaar).

## <a name="set-up-hello-azure-cli"></a>Hello Azure CLI instellen

tooinstall hello Azure CLI stappen Hallo die worden beschreven in [installeren hello Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).

> [!TIP]
> We bevelen aan dat u de installatie van Azure CLI vaak tootake profiteren van de service-updates en verbeteringen.
> 
> 

## <a name="command-help"></a>Opdracht Help

U kunt voor elke opdracht help-tekst weergeven in hello Azure CLI door toe te voegen `-h` toohello opdracht. Laat alle andere opties weg. Bijvoorbeeld:

* help voor Hallo tooget `az` opdracht, invoeren:`az -h`
* een lijst met alle Batch-opdrachten in Hallo CLI tooget gebruiken:`az batch -h`
* Voer in tooget informatie over het maken van een Batch-account:`az batch account create -h`

Bij twijfel gebruiken Hallo `-h` opdrachtregeloptie tooget help bij de Azure CLI-opdrachten.

> [!NOTE]
> Eerdere versies van hello Azure CLI gebruikt `azure` toopreface een CLI-opdracht. In versie 2.0 worden alle opdrachten nu voorafgegaan door `az`. Worden tooupdate ervoor dat uw scripts toouse Hallo nieuwe syntaxis met versie 2.0.
>
>  

Raadpleeg daarnaast toohello Azure CLI-naslagdocumentatie voor informatie over [Azure CLI-opdrachten voor Batch](https://docs.microsoft.com/cli/azure/batch). 

## <a name="log-in-and-authenticate"></a>Aanmelden en verifiëren

toouse hello Azure CLI met Batch, u moet toolog in en te verifiëren. Er zijn twee eenvoudige stappen toofollow:

1. **Aanmelden bij Azure.** Aanmelden bij Azure biedt u tooAzure Resource Manager-opdrachten, inclusief toegang tot [Batch Management-service](batch-management-dotnet.md) opdrachten.  
2. **Aanmelden bij uw Batch-account.** Aan te melden bij uw Batch-account biedt openen u de opdrachten tooBatch service.   

### <a name="log-in-tooazure"></a>Meld u bij tooAzure

Er zijn een aantal verschillende manieren toolog in Azure, gedetailleerd beschreven in [aanmelden met Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):

1. [Interactief aanmelden](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in). Interactief aanmelden wanneer u Azure CLI-opdrachten zelf worden uitgevoerd vanaf de opdrachtregel Hallo.
2. [Aanmelden met een service-principal](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal). Meld u aan met een service-principal wanneer u Azure CLI-opdrachten uitvoert vanuit een script of een toepassing.

Voor de toepassing hello van dit artikel, laten we zien hoe toolog in Azure interactief. Type [az aanmelding](https://docs.microsoft.com/cli/azure/#login) op Hallo-opdrachtregel:

```azurecli
# Log in tooAzure and authenticate interactively.
az login
```

Hallo `az login` opdracht retourneert een token dat u tooauthenticate, kunt zoals hier wordt weergegeven. Ga als volgt Hallo instructies tooopen webpagina's en het verzenden van Hallo token tooAzure:

![Meld u bij tooAzure](./media/batch-cli-get-started/az-login.png)

Hallo-voorbeelden die worden vermeld in Hallo [steekproef shell-scripts](#sample-shell-scripts) sectie ook tonen hoe toostart uw Azure CLI-sessie door interactief aanmelden bij Azure. Wanneer u zich hebt aangemeld, kunt u opdrachten toowork met Batch Management bronnen, met inbegrip van Batch-accounts, sleutels toepassingspakketten en quota's aanroepen.  

### <a name="log-in-tooyour-batch-account"></a>Meld u bij tooyour Batch-account

toouse hello Azure CLI toomanage Batch-resources, zoals groepen, taken en taken, u moet toolog in uw Batch-account en verifiëren. toolog in toohello Batch-service gebruiken Hallo [az batch-account aanmelding](https://docs.microsoft.com/cli/azure/batch/account#login) opdracht. 

Er zijn twee mogelijkheden voor verificatie van uw Batch-account:

- **Met behulp van Azure AD-verificatie (Azure Active Directory).** 

    Verificatie met Azure AD is Hallo standaardwaarde als u hello Azure CLI met Batch gebruiken en aanbevolen voor de meeste scenario's. 
    
    Wanneer u in tooAzure interactief aanmelden, zoals beschreven in de vorige sectie hello, uw referenties in cache zijn opgeslagen, zodat hello Azure CLI kunt u kunt zich aanmelden tooyour Batch-account met behulp van deze dezelfde referenties. Als u zich aanmeldt met een service-principal tooAzure, wordt deze referenties worden ook gebruikt toolog in tooyour Batch-account.

    Een voordeel van Azure AD is de ondersteuning voor toegangsbeheer op basis van rollen (RBAC). Met RBAC, van een gebruiker toegang is afhankelijk van hun rol, in plaats van of ze Hallo toegangscodes bezitten. U hoeft dus geen accountsleutels te beheren, maar RBAC-rollen, waarna Azure AD de toegang en verificatie afhandelt.  

    Verificatie met Azure AD is vereist als u hebt gemaakt uw Azure Batch-account met de modus van de toewijzing van toepassingen instellen too'User abonnement '. 

    toolog in tooyour Batch-account met behulp van Azure AD, neemt u contact Hallo [az batch-account aanmelding](https://docs.microsoft.com/cli/azure/batch/account#login) opdracht: 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- **Met behulp van gedeelde sleutelverificatie.**

    [Verificatie met een gedeelde sleutel](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) maakt gebruik van uw account toegangstoetsen tooauthenticate Azure CLI-opdrachten voor Hallo Batch-service.

    Als u Azure CLI-scripts tooautomate aanroepen Batch-opdrachten maakt, kunt u verificatie met gedeelde sleutel of een Azure AD-service principal. In sommige scenario's kan gedeelde sleutelverificatie een eenvoudigere oplossing zijn dan het maken van een service-principal.  

    toolog bij het gebruik van verificatie met een gedeelde sleutel opnemen Hallo `--shared-key-auth` optie op Hallo-opdrachtregel:

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

Hallo-voorbeelden die worden vermeld in Hallo [steekproef shell-scripts](#sample-shell-scripts) sectie laten zien hoe toolog in uw Batch-account met Azure CLI met zowel hello Azure AD en gedeelde sleutel.

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Azure Batch CLI-sjablonen en -bestandsoverdracht gebruiken (preview)

U kunt hello Azure CLI toorun Batch taken end-to-end-code te schrijven. Batch-sjabloonbestanden ondersteuning maken pools, jobs en taken Hello Azure CLI. U kunt ook hello Azure CLI tooupload taak invoerbestanden toohello Azure Storage-account gekoppeld Hallo Batch-account en uitvoerbestanden taak downloaden. Zie [Azure Batch CLI sjablonen en -bestandsoverdracht gebruiken (preview)](batch-cli-templates.md) voor meer informatie.

## <a name="sample-shell-scripts"></a>Voorbeelden van shell-scripts

Hallo-voorbeeldscripts vermeld in Hallo tabel weergeven na hoe toouse Azure CLI-opdrachten met Hallo Batch-service en algemene taken voor tooaccomplish Batch Management-service. Deze voorbeeldscripts betrekking hebben op veel van Hallo-opdrachten die beschikbaar zijn in hello Azure CLI voor Batch. 

| Script | Opmerkingen |
|---|---|
| [Een Batch-account maken](./scripts/batch-cli-sample-create-account.md) | Hiermee maakt u een Batch-account en wordt dit gekoppeld aan een opslagaccount. |
| [Een toepassing toevoegen](./scripts/batch-cli-sample-add-application.md) | Hiermee voegt u een toepassing toe en worden pakketten met binaire bestanden geüpload.|
| [Batch-pools beheren](./scripts/batch-cli-sample-manage-pool.md) | In dit script ziet u hoe u pools maakt, deze groter of kleiner maakt en beheert. |
| [Een functie en taken uitvoeren met Batch](./scripts/batch-cli-sample-run-job.md) | In dit script ziet u hoe u een functie uitvoert en taken toevoegt. |

## <a name="json-files-for-resource-creation"></a>JSON-bestanden voor het maken van resources

Wanneer u Batch-resources zoals pools en jobs maakt, kunt u een JSON-bestand met Hallo nieuwe resource-configuratie in plaats van de parameters doorgeven als opdrachtregelopties opgeven. Bijvoorbeeld:

```azurecli
az batch pool create my_batch_pool.json
```

U kunt de meeste Batch-resources met behulp van alleen opdrachtregelopties voor het maken, worden sommige functies vereisen dat u een bestand JSON-indeling met details van de resource Hallo opgeeft. U moet bijvoorbeeld een JSON-bestand gebruiken als u wilt dat de bronbestanden toospecify voor een begintaak.

toosee hello JSON syntaxis toocreate vereist een resource, raadpleeg dan toohello [Batch REST-API-verwijzing] [ rest_api] documentatie. Elke ' Add *brontype*' onderwerp in Hallo naslaginformatie over REST API bevat JSON-voorbeeldscripts voor het maken van die bron. U kunt deze JSON-voorbeeldscripts als sjabloon gebruiken voor JSON-bestanden toouse Hello Azure CLI. Bijvoorbeeld toosee Hallo JSON-syntaxis voor het maken van de groep van toepassingen te verwijzen[toevoegen van een account voor toepassingsgroep tooan][rest_add_pool].

Zie [Running jobs on Azure Batch with Azure CLI](./scripts/batch-cli-sample-run-job.md) (Taken uitvoeren in Azure Batch met Azure CLI) voor een voorbeeld van een script waarin een JSON-bestand is opgegeven.

> [!NOTE]
> Als u een JSON-bestand opgeeft wanneer u een resource maakt, worden andere parameters die u op de opdrachtregel Hallo voor die bron opgeeft worden genegeerd.
> 
> 

## <a name="efficient-queries-for-batch-resources"></a>Efficiënte query's voor Batch-resources

Elk Batch-resourcetype ondersteunt een `list`-opdracht die een query uitvoert voor het Batch-account, en vermeldt een lijst met resources van dit type. U kunt bijvoorbeeld Hallo toepassingen weergeven in uw account en het Hallo-taken in een job:

```azurecli
az batch pool list
az batch task list --job-id job001
```

Wanneer u een query Hallo Batch-service met een `list` bewerking, kunt u een OData-component toolimit Hallo hoeveelheid gegevens die worden geretourneerd. Omdat alle filteren serverzijde plaatsvindt, bestrijkt alleen Hallo gegevens die u aanvragen Hallo-kabel. Deze componenten toosave bandbreedte gebruiken (en dus time) wanneer u een lijst met bewerkingen uitvoert.

Hallo staan volgende tabel Hallo OData-componenten ondersteund door Hallo Batch-service:

| Component | Beschrijving |
|---|---|
| `--select-clause [select-clause]` | Retourneert een subset met eigenschappen voor elke entiteit. |
| `--filter-clause [filter-clause]` | Retourneert alleen entiteiten die overeenkomen met de Hallo opgegeven OData-expressie. |
| `--expand-clause [expand-clause]` | Verkrijgt Hallo entiteit in één onderliggende REST-aanroep. Hallo Vouw Component momenteel ondersteunt alleen Hallo `stats` eigenschap. |

Voor een voorbeeld van een script dat toont hoe een OData-component toouse zien [een job en taken uitvoeren met Batch](./scripts/batch-cli-sample-run-job.md).

Zie voor meer informatie over het uitvoeren van query's efficiënt lijst met OData-componenten [hello Azure Batch-service efficiënt Query](batch-efficient-list-queries.md).

## <a name="troubleshooting-tips"></a>Tips voor probleemoplossing

Hallo kunt volgende tips u Azure CLI-problemen oplossen:

* Gebruik `-h` tooget **help-tekst** voor elke opdracht CLI
* Gebruik `-v` en `-vv` toodisplay **uitgebreide** opdracht uitvoer. Wanneer Hallo `-vv` vlag is opgenomen, hello Azure CLI geeft Hallo werkelijke REST-aanvragen en antwoorden. Deze schakelopties zijn handig voor het weergeven van de volledige foutuitvoer.
* U kunt bekijken **opdracht uitvoer als JSON** Hello `--json` optie. `az batch pool show pool001 --json` wordt bijvoorbeeld weergegeven als eigenschappen van pool001 in de JSON-indeling. U kunt vervolgens kopiëren en wijzigen van deze toouse uitvoer in een `--json-file` (Zie [JSON-bestanden](#json-files) eerder in dit artikel).
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting tooany location.--->
* Hallo [Batch-forum] [ batch_forum] wordt bewaakt door de teamleden Batch. U kunt hier vragen posten als u problemen hebt of hulp nodig hebt met een bepaalde bewerking.

## <a name="next-steps"></a>Volgende stappen

* Zie voor meer informatie over hello Azure CLI Hallo [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).
* Meer informatie over Batch-resources vindt u in dit Engelstalige [overzicht van Azure Batch voor ontwikkelaars](batch-api-basics.md).
* Zie voor meer informatie over het gebruik van Batch sjablonen toocreate pools, jobs en taken zonder code te schrijven [gebruik Azure Batch CLI sjablonen en File Transfer (Preview)](batch-cli-templates.md).

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
