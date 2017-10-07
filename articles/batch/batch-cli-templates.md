---
title: Azure Batch aaaRun taken end-to-end-code (Preview) te schrijven | Microsoft Docs
description: Maak sjabloonbestanden hello Azure CLI toocreate Batch-pools, jobs en taken.
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: c0434d09766451f6ba516efbad949834711ee819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Azure Batch CLI-sjablonen en -bestandsoverdracht gebruiken (preview)

Met hello Azure CLI is het mogelijk toorun batchtaken zonder code te schrijven.

Sjabloonbestanden worden gemaakt en gebruikt met hello Azure CLI waarmee Batch-pools, jobs en taken toobe gemaakt. Taak invoerbestanden kunnen eenvoudig worden geüpload naar Hallo storage-account gekoppeld Hallo Batch-account en taak uitvoerbestanden gedownload.

## <a name="overview"></a>Overzicht

Een uitbreiding toohello Azure CLI kunt Batch toobe gebruikt end-to-end door gebruikers die geen ontwikkelaars. Een groep kan worden gemaakt, invoergegevens geüpload, taken en de bijbehorende taken die zijn gemaakt, en Hallo resulterende uitvoergegevens gedownload – geen code vereist, Hallo CLI wordt geïntegreerd in scripts of rechtstreeks worden gebruikt.

Batch-sjablonen samenstellen op Hallo [bestaande Batch-ondersteuning in hello Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) waarmee JSON-bestanden toospecify eigenschapswaarden voor Hallo maken van groepen, taken, taken en andere items. Met Batch-sjablonen worden hello volgende mogelijkheden toegevoegd via wat is er mogelijk met Hallo JSON-bestanden:

-   Parameters kunnen worden gedefinieerd. Wanneer het Hallo-sjabloon gebruikt, zijn alleen Hallo parameterwaarden opgegeven toocreate Hallo artikel, met andere item eigenschapswaarden worden opgegeven in de hoofdtekst van de Hallo-sjabloon. Een gebruiker die werkt met dat batch- en de toobe toepassingen worden uitgevoerd door de Batch kunt sjablonen maken pool, Jobs en taak eigenschapswaarden opgeven. Een gebruiker minder bekend bent met de Batch-en/of de toepassingen hoeft slechts toospecify Hallo waarden voor parameters Hallo gedefinieerd.

-   Taak taak fabrieken maken van een of meer taken die zijn gekoppeld aan een taak, waardoor het Hallo voorkomen moeten voor veel taak definities toobe gemaakt en aanzienlijk vereenvoudigen verzending van de taak.


Invoergegevensbestanden moeten worden opgegeven voor taken toobe en uitvoerbestanden gegevens vaak worden geproduceerd. Een opslagaccount is gekoppeld, standaard, bij elke Batch-account en bestanden eenvoudig overgebrachte tooand van dit opslagaccount met behulp van de CLI met geen coderingen kunnen worden en geen referenties opslag vereist.

Bijvoorbeeld: [ffmpeg](http://ffmpeg.org/) is een populaire toepassing die audio en video-bestanden worden verwerkt. Hello Azure Batch CLI kan gebruikte tooinvoke ffmpeg tootranscode bron videobestanden toodifferent oplossingen zijn.

-   Een pool-sjabloon is gemaakt. Hallo-gebruiker maken Hallo sjabloon weet hoe toocall Hallo ffmpeg toepassing en de vereisten; Deze Hallo opgeven juiste OS, VM grootte, hoe ffmpeg is geïnstalleerd (van een toepassingspakket of met behulp van een Pakketbeheer bijvoorbeeld), en andere eigenschapswaarden-groep. Parameters worden gemaakt wanneer het Hallo-sjabloon gebruikt, alleen Hallo verzameling-id en het aantal virtuele machines moet toobe opgegeven.

-   Een sjabloon wordt gemaakt. Hallo maken Hallo gebruikerssjabloon weet hoe ffmpeg behoeften toobe aangeroepen tootranscode bron video tooa andere resolutie en geeft Hallo taak opdrachtregel; ze ook weten dat er een map met de Hallo bron videobestanden, met een taak vereist per bestand voor invoer.

-   Een eindgebruiker met een reeks videobestanden tootranscode maakt eerst een groep Hallo groep sjabloon gebruikt, geven alleen Hallo verzameling-id en het aantal virtuele machines die zijn vereist. Ze kunnen vervolgens Hallo bron bestanden tootranscode uploaden. Een taak kan vervolgens worden verzonden met behulp van Hallo-taaksjabloon opgeven alleen Hallo pool-id en de locatie van bronbestanden Hallo geüpload. Hallo Batch-job is gemaakt met één taak per bestand voor invoer wordt gegenereerd. Ten slotte kunnen Hallo getranscodeerd uitvoerbestanden worden gedownload.

## <a name="installation"></a>Installeren

Hallo-sjabloon en de bestandsnaam overdrachtmogelijkheden vereisen een extensie toobe geïnstalleerd.

Voor instructies over hoe tooinstall hello Azure CLI zien [2.0 voor Azure CLI installeren](https://docs.microsoft.com/cli/azure/install-azure-cli).

Eenmaal hello die Azure CLI is geïnstalleerd, Hallo Batch-extensie kan worden geïnstalleerd met de volgende CLI-opdracht:

```azurecli
az component update --add batch-extensions --allow-third-party
```

Zie voor meer informatie over Hallo Batch extensie [Microsoft Azure Batch CLI uitbreidingen voor Windows, Mac en Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).

## <a name="templates"></a>Sjablonen

Hello Azure Batch CLI kunt items zoals pools, jobs en taken toobe gemaakt door te geven van een JSON-bestand met de namen van eigenschappen en waarden. Bijvoorbeeld:

```azurecli
az batch pool create –-json-file AppPool.json
```

Azure Batch-sjablonen zijn vergelijkbaar tooAzure Resource Manager-sjablonen, in de functionaliteit en syntaxis. Ze zijn JSON-bestanden die itemnamen en waarden bevatten, maar na de belangrijkste concepten Hallo toevoegen:

-   **Parameters**

    -   Toestaan dat de eigenschap waarden toobe is opgegeven in een sectie hoofdtekst met alleen parameterwaarden hoeven toobe wanneer Hallo sjabloon wordt opgegeven. Hallo volledige definitie voor een groep kan bijvoorbeeld worden geplaatst in Hallo-instantie en slechts één parameter gedefinieerd voor groep-id; alleen een tekenreeks in de pool-id moet daarom toobe opgegeven toocreate een pool.
        
    -   Hallo sjabloon instantie worden geschreven door iemand met kennis van Batch en Hallo toepassingen toobe uitvoeren door de Batch; alleen waarden voor Hallo auteur gedefinieerde parameters moeten worden opgegeven als Hallo-sjabloon gebruikt. Een gebruiker zonder Hallo diepgaande Batch en/of kennis van de toepassing gebruik daarom de sjablonen.

-   **Variabelen**

    -   Eenvoudige of complexe parameter waarden toobe opgegeven in één locatie en gebruikt op een of meer plaatsen in de hoofdtekst van de sjabloon Hallo toestaan. Variabelen kunnen vereenvoudigen en verkleinen Hallo Hallo-sjabloon, evenals meer bruikbaar maken door er één locatie toochange eigenschappen waarvan de waarde mag wijzigen.

-   **Een hoger niveau constructies**

    -   Sommige op een hoger niveau constructies zijn beschikbaar in het Hallo-sjabloon die nog niet beschikbaar in Hallo Batch-API's. Een taak factory kan bijvoorbeeld worden gedefinieerd in een sjabloon die wordt gemaakt van meerdere taken voor het Hallo-taak met een gemeenschappelijke taakdefinitie. Deze gegevens te voorkomen dat Hallo nodig toocode om dynamisch meerdere JSON-bestanden, zoals één bestand per taak te maken, evenals een script bijvoorbeeld bestanden tooinstall toepassingen via een Pakketbeheer maken.

    -   Op sommige punt, waar van toepassing, dat deze gegevens kunnen worden toegevoegd toothe Batch-service en is beschikbaar in Hallo Batch-API's, UI, enzovoort.

### <a name="pool-templates"></a>Pool-sjablonen

Bovendien worden toohello standaardsjabloon mogelijkheden van de parameters en variabelen, Hallo na een hoger niveau constructies ondersteund door Hallo groep sjabloon:

-   **Pakket met verwijzingen**

    -   Desgewenst kunnen software toobe gekopieerd toopool knooppunten met behulp van pakket managers. Hallo Pakketbeheer en pakket-id worden opgegeven. Kan toodeclare worden een of meer pakketten voorkomt Hallo nodig toocreate een script dat vereist hello-pakketten opgehaald, Hallo script installeren en Hallo-script uitvoeren op elk knooppunt van de groep van toepassingen.

Hallo Hier volgt een voorbeeld van een sjabloon die u een pool van Linux virtuele machines met ffmpeg geïnstalleerd en alleen maakt een pool-id tekenreeks en Hallo aantal virtuele machines toobe opgegeven toouse vereist:

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "hello number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

Als de naam van het sjabloonbestand Hallo _groep ffmpeg.json_, en vervolgens de sjabloon Hallo zou als volgt worden aangeroepen:

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a>Taaksjablonen

Bovendien worden toohello standaardsjabloon mogelijkheden van de parameters en variabelen, Hallo na een hoger niveau constructies ondersteund door Hallo taaksjabloon:

-   **Taak factory**

    -   Meerdere taken voor een taak maakt van de definitie van één taak. Drie soorten taak factory worden ondersteund: parametrische sweep, taak per bestand, en verzameling van de taak.

Hallo Hieronder volgt een voorbeeld van een sjabloon die u maakt een taak die gebruikmaakt van ffmpeg te transcoderen MP4 videobestanden tooone van twee lagere resolutie, met één taak per video bronbestand gemaakt:

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch pool which runs hello job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

Als de naam van het sjabloonbestand Hallo _taak ffmpeg.json_, en vervolgens de sjabloon Hallo zou als volgt worden aangeroepen:

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a>Bestandsgroepen en bestandsoverdracht

De meeste jobs en taken vereisen invoerbestanden en uitvoerbestanden wordt geproduceerd. Beide bestanden invoer- en uitvoerbestanden moeten doorgaans toobe worden overgedragen, van Hallo client toohello knooppunt of Hallo node toohello-client. Hello Azure Batch CLI extensie isoleert opslag bestandsoverdracht en maakt gebruik van Hallo storage-account dat door de standaardwaarde voor elk Batch-account wordt gemaakt.

Een bestandsgroep gelijkstaat tooa-container die in hello Azure storage-account is gemaakt. Hallo-bestandsgroep misschien submappen.

Hallo Batch CLI-uitbreiding bevat opdrachten voor het uploaden van bestanden uit clientgroep tooa opgegeven bestand en downloaden van bestanden van Hallo opgegeven bestand groep tooa client.

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

Groep van toepassingen en -taak sjablonen kunnen bestanden die zijn opgeslagen in bestand groepen toobe opgegeven voor kopiëren naar de knooppunten van de groep van toepassingen of uit de groep knooppunten tooa bestandsgroep terug. Bijvoorbeeld, in de taaksjabloon eerder hebt opgegeven, is Hallo bestand groep 'ffmpeg-invoer' opgegeven voor Hallo taak factory als Hallo locatie Hallo video van bronbestanden voor gekopieerd naar beneden op Hallo knooppunt voor transcodering; Hallo bestand groep 'ffmpeg-uitvoer' wordt gebruikt als hello locatie waar de uitvoerbestanden van Hallo getranscodeerd gekopieerd toofrom Hallo knooppunt uitgevoerd elke taak.

## <a name="summary"></a>Samenvatting

Sjabloon en een bestand overdracht hebt op dit moment is ondersteuning toegevoegd alleen toohello Azure CLI. Hallo-doel is tooexpand Hallo doelgroep die Batch toousers hoeven niet toodevelop code met Hallo Batch-API's, zoals onderzoekers en IT-gebruikers kan gebruiken. Zonder codering, kunnen gebruikers met kennis van Azure Batch en Hallo toepassingen toobe uitvoeren door de Batch sjablonen voor het maken van toepassingen en -taak maken. Met Sjabloonparameters, kunnen gebruikers zonder grondige kennis van de Batch- en Hallo toepassingen Hallo sjablonen gebruikt.

Hallo Batch-extensie voor hello Azure CLI uitproberen en moet u alle feedback of suggesties, ofwel in Hallo opmerkingen voor dit artikel of via Hallo [Azure Batch-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).

## <a name="next-steps"></a>Volgende stappen

- Zie Hallo Batch sjablonen blogbericht: [uitgevoerd op Azure Batch-taken met behulp van Azure CLI – geen code vereist Hallo](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).
- Gedetailleerde documentatie voor installatie en het gebruik, voorbeelden en broncode zijn beschikbaar in Hallo [Azure GitHub-opslagplaats](https://github.com/Azure/azure-batch-cli-extensions).
