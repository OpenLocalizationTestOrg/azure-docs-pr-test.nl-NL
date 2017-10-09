---
title: aaaDevelop Azure Functions met Visual Studio | Microsoft Docs
description: Meer informatie over hoe Azure-functies voor toodevelop en testen met behulp van Azure Functions-hulpprogramma's voor Visual Studio 2017.
services: functions
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: glenga
ms.openlocfilehash: c9baf882bf58068cb9a8930bea337fe51b2a77ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a>Azure Functions-Tools voor Visual Studio  

Azure Functions-hulpprogramma's voor Visual Studio 2017 is een uitbreiding voor Visual Studio waarmee u ontwikkelen, testen en implementeren van tooAzure van C#-functies. Als dit de eerste ervaring met Azure Functions, kunt u meer informatie op [fungeert voor een inleiding tooAzure](functions-overview.md).

Hallo hulpprogramma's van Azure Functions biedt Hallo volgende voordelen: 

* Bewerken, bouwen en uitvoeren van functies op de lokale computer. 
* Publiceren van uw Azure Functions project rechtstreeks tooAzure. 
* Gebruik WebJobs kenmerken toodeclare functiebindingen rechtstreeks in Hallo C#-code in plaats van het onderhouden van een afzonderlijke function.json voor het binden van definities.
* Ontwikkelen en implementeren van vooraf gecompileerde C#-functies. Vooraf gecompileerde functies bieden een betere koude start prestaties dan C# script gebaseerde functies. 
* Terwijl alle Hallo voordelen van Visual Studio-ontwikkeling van uw functies in C#-code. 

Dit onderwerp leest u hoe toouse hello Azure Functions-Tools voor Visual Studio 2017 toodevelop uw functies in C#. U leert ook hoe toopublish uw project tooAzure als een .NET-assembly.

## <a name="prerequisites"></a>Vereisten

Azure Functions-hulpprogramma's is opgenomen in hello Azure ontwikkeling werkbelasting van [Visual Studio 2017 versie 15,3](https://www.visualstudio.com/vs/), of een latere versie. Zorg ervoor dat u Hallo **ontwikkelen van Azure** werkbelasting in uw Visual Studio 2017 versie 15,3 installatie:

![Installeer Visual Studio 2017 met hello Azure ontwikkeling werkbelasting](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

toocreate en implementeren van functies, moet u ook:

* Een actief Azure-abonnement. Als u een Azure-abonnement geen [gratis accounts](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) beschikbaar zijn.

* Een Azure Storage-account. een opslagaccount toocreate Zie [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account).  
## <a name="create-an-azure-functions-project"></a>Een Azure Functions-project maken 

[!INCLUDE [Create a project using hello Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-hello-project-for-local-development"></a>Hallo-project voor lokale ontwikkeling configureren

Wanneer u een nieuw project met hello Azure Functions-sjabloon maakt, kunt u een leeg C#-project met de volgende bestanden Hallo krijgen:

* **host.JSON**: Hiermee kunt u configureren Hallo functies host. Deze instellingen gelden beide wanneer lokaal en in Azure wordt uitgevoerd. Zie voor meer informatie [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) artikel.
    
* **Local.Settings.JSON**: onderhoudt instellingen bij lokale uitvoering van de functies die worden gebruikt. Deze instellingen worden niet gebruikt door Azure, ze worden gebruikt door Hallo [kernonderdelen van Azure Functions](functions-run-local.md). Gebruik deze instellingen toospecify, zoals verbinding tekenreeksen tooother Azure services. Voeg een nieuwe sleutel toohello **waarden** matrix voor elke verbinding vereist voor functies in uw project. Zie voor meer informatie [lokale instellingenbestand](functions-run-local.md#local-settings-file) in Hallo kernonderdelen van Azure Functions onderwerp.

Hallo functies runtime wordt intern gebruikt een Azure Storage-account. Voor alle typen dan HTTP en webhooks activeert, moet u instellen Hallo **Values.AzureWebJobsStorage** sleutel tooa geldige Azure Storage-account-verbindingsreeks.

[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

 tooset hello account opslagverbindingsreeks:

1. Open in Visual Studio **Cloud Explorer**, vouw **Opslagaccount** > **uw Opslagaccount**, selecteer daarna **eigenschappen**en kopiëren Hallo **primaire verbindingsreeks** waarde.   

2. In uw project Hallo local.settings.json projectbestand openen en stel de waarde Hallo Hallo **AzureWebJobsStorage** sleutel toohello-verbindingsreeks die u hebt gekopieerd.

3. Herhaal Hallo vorige stap tooadd unieke sleutels toohello **waarden** matrix voor eventuele andere verbindingen die vereist zijn voor uw functies.  

## <a name="create-a-function"></a>Een functie maken

Hallo bindingen die wordt gebruikt door de functie Hallo worden in de vooraf gecompileerde functies gedefinieerd door de kenmerken in het Hallo-code toepassen. Wanneer u uw functies van Hallo opgegeven sjablonen hello Azure Functions Tools toocreate opgeeft, wordt deze kenmerken worden toegepast voor u. 

1. Klik in **Solution Explorer** met de rechtermuisknop op het projectknooppunt en selecteer  > **Nieuw item****Toevoegen**. Selecteer **Azure-functie**, typ een **naam** voor Hallo klasse en klik op **toevoegen**.

2. Kies de trigger en klikt u op Hallo bindingeigenschappen instellen **maken**. Hallo volgende voorbeeld ziet Hallo instellingen wanneer de functie voor het maken van een Queue storage geactiveerd. 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    Een sleutelreeks voor verbinding met de naam **QueueStorage** wordt geleverd, die is gedefinieerd in Hallo local.settings.json bestand. 
 
3. Bekijk Hallo toegevoegde klasse. U ziet een statische **uitvoeren** methode, dat is toegewezen met Hallo **functienaam** kenmerk. Dit kenmerk geeft aan dat Hallo methode Hallo toegangspunt voor Hallo-functie. 

    Hallo volgende C#-klasse vertegenwoordigt bijvoorbeeld een eenvoudige wachtrij geactiveerd opslagfunctie:

    ````csharp
    using System;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Host;
    
    namespace FunctionApp1
    {
        public static class Function1
        {
            [FunctionName("QueueTriggerCSharp")]        
            public static void Run([QueueTrigger("myqueue-items", Connection = "QueueStorage")]string myQueueItem, TraceWriter log)
            {
                log.Info($"C# Queue trigger function processed: {myQueueItem}");
            }
        }
    } 
    ````
 
    Een binding-specifieke kenmerk is toegepaste tooeach binding geleverde parameter toohello entry point-methode. Hallo-kenmerk heeft Hallo bindingsgegevens als parameters. In het vorige voorbeeld Hallo Hallo eerste parameter heeft een **QueueTrigger** kenmerk dat wordt toegepast, die wachtrij geactiveerd functie aangeeft. Hallo wachtrijnaam en de naam van instelling verbindingsreeks worden als parameters doorgegeven.  

## <a name="testing-functions"></a>Functies testen

Met Azure Functions Core-hulpprogramma's kunt u Azure Functions-projecten uitvoeren op uw lokale ontwikkelcomputer. U bent na vragen aan gebruiker tooinstall deze hulpprogramma's Hallo eerste keer dat u een functie vanuit Visual Studio start.  

tootest uw functie druk op F5. Als u wordt gevraagd, Hallo verzoek van Visual Studio toodownload accepteert en hulpprogramma's voor Azure Functions Core (CLI) installeren.  U moet mogelijk ook een firewall-uitzondering tooenable zodat Hallo hulpprogramma's voor HTTP-aanvragen kunnen verwerken.

Hallo-project is uitgevoerd, kunt u uw code testen zoals u zou geïmplementeerde functie testen. Zie voor meer informatie [strategieën voor het testen van uw code in Azure Functions](functions-test-a-function.md). Wanneer in de foutopsporingsmodus wordt uitgevoerd, worden de onderbrekingspunten druk in Visual Studio zoals verwacht. 

Zie voor een voorbeeld van hoe een wachtrij tootest functie geactiveerd, Hallo [wachtrij geactiveerd functie Quick Start-zelfstudie](functions-create-storage-queue-triggered-function.md#test-the-function).  

toolearn meer over het gebruik van de kernonderdelen van hello Azure Functions, Zie [Code en testen van Azure functions lokaal](functions-run-local.md).

## <a name="publish-tooazure"></a>TooAzure publiceren

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
>Alle instellingen die u hebt toegevoegd in Hallo local.settings.json moeten ook toevoegen toohello functie-app in Azure. Deze instellingen worden niet automatisch toegevoegd. U kunt de vereiste instellingen tooyour functie-app in een van de volgende manieren toevoegen:
>
>* [Azure-portal met behulp van Hallo](functions-how-to-use-azure-function-app-settings.md#settings).
>* [Met behulp van Hallo `--publish-local-settings` optie publiceren in Hallo kernonderdelen van Azure Functions](functions-run-local.md#publish).
>* [Met behulp van Azure CLI Hallo](/cli/azure/functionapp/config/appsettings#set). 

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hulpprogramma's van Azure-functies, de sectie Algemene vragen Hallo Hallo [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blogbericht.

toolearn meer informatie over de kernonderdelen van hello Azure Functions, Zie [Code en testen van Azure functions lokaal](functions-run-local.md).  
toolearn meer informatie over het ontwikkelen van functies als .NET-klassebibliotheken, Zie [met behulp van .NET-klassebibliotheken met Azure Functions](functions-dotnet-class-library.md). Dit onderwerp bevat ook voorbeelden van hoe toouse kenmerken toodeclare Hallo voor verschillende soorten bindingen die worden ondersteund door Azure Functions.    
