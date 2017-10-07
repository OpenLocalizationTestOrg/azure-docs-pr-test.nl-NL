---
title: aaaGuidance voor het ontwikkelen van Azure Functions | Microsoft Docs
description: Informatie over hello Azure Functions concepten en technieken, moet u toodevelop functies in Azure, voor alle programmeertalen en bindingen.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: Developer guide, azure-functies, functies, gebeurtenisverwerking webhooks, dynamische compute, zonder server-architectuur
ms.assetid: d8efe41a-bef8-4167-ba97-f3e016fcd39e
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: chrande
ms.openlocfilehash: 86d37dae5333f615faafc966e9da6e08e0a6354e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-developers-guide"></a>Azure Functions-handleiding voor ontwikkelaars
Specifieke functies delen in Azure Functions enkele core technische concepten en -onderdelen, ongeacht het Hallo-taal of de binding die u gebruikt. Voordat u gaan in de details van de specifieke tooa gegeven taal of binding leren, moet u ervoor tooread via dit overzicht die van toepassing tooall hiervan is.

In dit artikel wordt ervan uitgegaan dat u hebt al Hallo gelezen [overzicht van Azure Functions](functions-overview.md) en bekend bent met [WebJobs SDK concepten zoals triggers en bindingen Hallo JobHost runtime](../app-service-web/websites-dotnet-webjobs-sdk.md). Azure Functions is gebaseerd op Hallo WebJobs SDK. 

## <a name="function-code"></a>Functiecode
Een *functie* Hallo primaire concept in Azure Functions. U code schrijven voor een functie in een andere taal van uw keuze en slaat Hallo code en de configuratiebestanden in dezelfde map Hallo. Hallo configuratie heet `function.json`, die de JSON-configuratiegegevens bevat. Diverse talen worden ondersteund, en elke service heeft een iets andere ervaring geoptimaliseerd toowork aanbevolen voor die taal. 

Hallo function.json bestand definieert het Hallo-functiebindingen en andere configuratie-instellingen. Hallo runtime maakt gebruik van dit bestand toodetermine Hallo gebeurtenissen toomonitor en hoe werken uitvoering toopass gegevens in en gegevens uit. Hallo Hieronder volgt een voorbeeld function.json-bestand.

```json
{
    "disabled":false,
    "bindings":[
        // ... bindings here
        {
            "type": "bindingType",
            "direction": "in",
            "name": "myParamName",
            // ... more depending on binding
        }
    ]
}
```

Set Hallo `disabled` eigenschap te`true` tooprevent Hallo functie uit te voeren.

Hallo `bindings` eigenschap is waar u zowel triggers en bindingen configureren. Elke binding deelt enkele algemene instellingen en bepaalde instellingen die specifieke tooa bepaald type binding zijn. Elke binding moet Hallo volgende instellingen:

| Eigenschap | Waarden/typen | Opmerkingen |
| --- | --- | --- |
| `type` |Tekenreeks |Bindingstype. Bijvoorbeeld `queueTrigger`. |
| `direction` |'in', 'out' |Hiermee wordt aangegeven of Hallo binding voor ontvangst van gegevens in de functie Hallo of verzenden van gegevens uit de Hallo-functie. |
| `name` |Tekenreeks |Hallo-naam die wordt gebruikt voor Hallo gebonden gegevens in de Hallo-functie. Voor C# is dit de naam van een argument; Als u JavaScript 's het Hallo-sleutel in een sleutel/waarde-lijst. |

## <a name="function-app"></a>Functie-app
Een functie-app bestaat uit een of meer afzonderlijke functies die samen worden beheerd door Azure App Service. Alle functies in een share van de functie app Hallo Hallo dezelfde prijzen plan, continue implementatie en runtime-versie. Functies die zijn geschreven in meerdere talen kunnen dat alle Hallo delen functie dezelfde-app. Denk van een functie-app als een manier tooorganize en gezamenlijk beheren van uw functies. 

## <a name="runtime-script-host-and-web-host"></a>Runtime (scripthost en webhost)
Hallo runtime of scripthost, is het onderliggende WebJobs SDK host hello, die luistert naar gebeurtenissen, verzamelt en verzendt gegevens en uiteindelijk uw code wordt uitgevoerd. 

triggers toofacilitate HTTP, er is ook een host die is ontworpen toosit voor de scripthost Hallo in productiescenario's. Met twee hosts helpt tooisolate Hallo scripthost worden Hallo beheerd door de webhost Hallo front-end-verkeer.

## <a name="folder-structure"></a>Mapstructuur
[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

Bij het instellen van een project voor het implementeren van functies tooa functie-app in Azure App Service, kunt u deze mapstructuur behandelen als de code van uw site. U kunt bestaande hulpprogramma's zoals continue integratie en implementatie of aangepaste implementatie scripts hiervoor pakketinstallatie implementeren of transpilation code.

> [!NOTE]
> Zorg ervoor dat toodeploy uw `host.json` bestands- en -mappen rechtstreeks toohello `wwwroot` map. Neem geen Hallo `wwwroot` map in uw implementaties. Anders u uiteindelijk `wwwroot\wwwroot` mappen. 
> 
> 

## <a id="fileupdate"></a>Hoe de app-bestanden voor het functioneren van tooupdate
Hallo functie editor is ingebouwd in hello Azure-portal kunt u bijwerken Hallo *function.json* Hallo code-bestand voor een functie en het bestand. tooupload of update andere bestanden zoals *package.json* of *project.json* of afhankelijkheden, hebt u toouse andere methoden voor het implementeren.

Functie apps zijn gebouwd op App Service, zodat alle Hallo [implementatieopties beschikbaar toostandard web-apps](../app-service-web/web-sites-deploy.md) zijn ook beschikbaar voor de functie apps. Hier volgen enkele methoden die u kunt gebruiken tooupload of bijwerken van de functie app-bestanden. 

#### <a name="toouse-app-service-editor"></a>toouse App Service-Editor
1. Klik in de Azure Functions-portal Hallo **werken app-instellingen**.
2. In Hallo **geavanceerde instellingen** sectie, klikt u op **Ga tooApp Service-instellingen**.
3. Klik op **App Service-Editor** in App-Menu Nav onder **ONTWIKKELINGSPROGRAMMA's**.
4. Klik op **gaat**.
   
   Nadat de App Service-Editor wordt geladen, ziet u Hallo *host.json* bestands- en mappen onder *wwwroot*. 
5. Geopende bestanden tooedit, of slepen en neerzetten van uw ontwikkeling machine tooupload bestanden.

#### <a name="toouse-hello-function-apps-scm-kudu-endpoint"></a>toouse hello functie-app van SCM (Kudu) eindpunt
1. Ga naar: `https://<function_app_name>.scm.azurewebsites.net`.
2. Klik op **Console voor foutopsporing > CMD**.
3. Navigeer te`D:\home\site\wwwroot\` tooupdate *host.json* of `D:\home\site\wwwroot\<function_name>` tooupdate bestanden van een functie.
4. Slepen en neerzetten een bestand dat u wilt dat tooupload in de juiste map Hallo in Hallo bestand raster. Er zijn twee gebieden in Hallo bestand raster waar u een bestand kunt neerzetten. Voor *.zip* bestanden, ziet u een vak met Hallo label 'tooupload hier naartoe slepen en pak.' Voor andere bestandstypen verwijderen in Hallo bestand raster maar buiten Hallo 'uitpakken van' vak.

<!--NOTE: I've removed documentation on FTP, because it does not sync triggers on hello consumption plan --DonnaM -->

#### <a name="toouse-continuous-deployment"></a>doorlopende implementatie toouse
Volg de instructies Hallo in Hallo onderwerp [continue implementatie voor Azure Functions](functions-continuous-deployment.md).

## <a name="parallel-execution"></a>Parallelle uitvoering
Wanneer meerdere activerende gebeurtenissen sneller plaatsvinden dan een functie single thread-runtime kan verwerken, kan Hallo functie meerdere keren parallel Hallo runtime worden aangeroepen.  Als een functie-app van Hallo gebruikmaakt [verbruik die als host fungeert voor plan](functions-scale.md#how-the-consumption-plan-works), Hallo functie-app kan automatisch geschaald uitbreiden.  Elk exemplaar van Hallo functie-app, of het Hallo-app wordt uitgevoerd op Hallo verbruik hosting-abonnement of een gewone [App Service-plan hostingplan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), gelijktijdige functie aanroepen parallel met meerdere threads mogelijk verwerkt.  maximum aantal gelijktijdige functie aanroepen in de app-exemplaar van elke functie Hallo varieert op basis van Hallo-type van de trigger en Hallo-bronnen worden gebruikt door andere functies binnen Hallo functie-app wordt gebruikt.

## <a name="functions-runtime-versioning"></a>Functies runtime versiebeheer

U kunt configureren Hallo versie van de runtime van Functions Hallo Hallo met `FUNCTIONS_EXTENSION_VERSION` app-instelling. Hallo-waarde '~ 1' geeft bijvoorbeeld aan uw App in de functie wordt gebruik 1 als de primaire versie. Functie Apps zijn nieuwe secundaire versie van de bijgewerkte tooeach zodra ze worden vrijgegeven. U kunt exacte versie van uw App functie Hallo weergeven in Hallo **instellingen** tabblad in hello Azure-Portal.

## <a name="repositories"></a>Opslagplaatsen
Hallo-code voor Azure Functions is open source en opgeslagen in de GitHub-opslagplaatsen:

* [Azure Functions-runtime](https://github.com/Azure/azure-webjobs-sdk-script/)
* [Azure Functions-portal](https://github.com/projectkudu/AzureFunctionsPortal)
* [Azure Functions-sjablonen](https://github.com/Azure/azure-webjobs-sdk-templates/)
* [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/)
* [Azure WebJobs SDK-extensies](https://github.com/Azure/azure-webjobs-sdk-extensions/)

## <a name="bindings"></a>Bindingen
Hier volgt een lijst met alle ondersteunde bindingen.

[!INCLUDE [dynamic compute](../../includes/functions-bindings.md)]

## <a name="reporting-issues"></a>Melden van problemen
[!INCLUDE [Reporting Issues](../../includes/functions-reporting-issues.md)]

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie Hallo resources te volgen:

* [Aanbevolen procedures voor Azure Functions](functions-best-practices.md)
* [Azure Functions C# referentie voor ontwikkelaars](functions-reference-csharp.md)
* [Azure Functions F # referentie voor ontwikkelaars](functions-reference-fsharp.md)
* [Azure Functions NodeJS-referentie voor ontwikkelaars](functions-reference-node.md)
* [Azure Functions-triggers en bindingen](functions-triggers-bindings.md)
* [Azure Functions: Hallo reis](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) op Hallo Azure App Service-teamblog. Een overzicht van hoe Azure Functions is ontwikkeld.

