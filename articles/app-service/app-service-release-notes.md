---
title: aaaAzure SDK voor .NET 2.5.1 Release-opmerkingen
description: Azure SDK voor .NET 2.5.1 Release-opmerkingen
services: app-service
documentationcenter: .net,nodejs,java
author: Juliako
manager: erikre
editor: 
ms.assetid: 8d3d815f-bb58-447e-8ff0-f9b9603c7b00
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/10/2016
ms.author: juliako
ms.openlocfilehash: 5ee7688617c966baa409045881c172bbbc55ff63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-251-release-notes"></a>Azure SDK voor .NET 2.5.1 Release-opmerkingen
Dit document bevat de releaseopmerkingen Hallo voor hello Azure SDK voor .NET 2.5.1 release. 

## <a name="azure-sdk-for-net-251-release-notes"></a>Azure SDK voor .NET 2.5.1 release-opmerkingen
Hallo volgen nieuwe functies en -updates in hello Azure SDK voor .NET 2.5.1.

* Nieuwe features\scenarios te gerelateerde**Web extra Extensions**. 
  
  * Azure Websites is hernoemde tooAzure App Service. Zie voor meer informatie, [Azure App Service en de bestaande Azure Services](../app-service-web/app-service-changes-existing-services.md).
  * Ondersteuning van Azure API-Apps (Preview) is toegevoegd zodat klanten ASP.NET-projecten als API-Apps publiceren en gebruik vervolgens Hallo toevoegen > gebaar van de Azure-API-App-Client in C#-projecten toogenerate-code op basis van de structuur Hallo Hallo API-App geïmplementeerd. 
  * Hallo Websites knooppunt in Server Explorer is afgeschaft in plaats van hello Azure App Service knooppunt met ondersteuning voor Resource groepering van Azure API-Apps, Mobile Apps en Web-Apps op basis van groep.
  * Ondersteuning van Azure Mobile Apps (Preview) is toegevoegd zodat klanten kunnen maken van nieuwe Mobile Apps-projecten, Mobile Apps-domeincontrollers toevoegt, Hallo projecten publiceren en op afstand fouten opsporen in toepassingen.
  * Toevoegen > gebaar van de Azure-API-App-Client biedt nu ondersteuning voor lokale Swagger JSON-bestanden, zodat ontwikkelaars van Web-API kunt NuGets van derden zoals toogenerate Swashbuckle Swagger of handmatig maken. Op deze manier client ontwikkelaars kunnen gebruiken Hallo genereren van code functies tooconsume een willekeurig eindpunt Swagger in C#-projecten. 
  * Web-App en het API-App publiceren dialoogvensters zijn verbeterde toosupport hello Azure Portal-concept van bron groeperen en selectie/maken van Azure-resourcegroepen en de App Service-abonnementen worden in Hallo nieuwe Web-Apps en API-App inrichten dialoogvenster weergegeven. 
  * Azure API-App Server Explorer-knooppunten bieden koppelingen toohello die grondige API-Apps in Azure Portal hello, evenals andere functies zoals logboek Streaming en foutopsporing op afstand koppelen.
    
    Voor bekende problemen en de huidige beperkingen in Azure SDK .NET 2.5.1 [dit](app-service-release-notes.md#known_issues_2_5_1) hieronder.
* Nieuwe features\scenarios te gerelateerde**HDInsight Tools** in Visual Studio zijn ingeschakeld in deze release. 
  
  * Lokale validatie van hive-scripts. Klik op Hallo valideren script in Hallo werkbalk toosee als er fouten in uw script zijn. 
  * Verbeterd foutopsporing van Hive-taken. U kunt nu fouten opsporen Hive-taken via Yarn-Logboeken in Visual Studio. Als uw toepassing prestatieproblemen heeft, biedt onderzoekt YARN-logboeken nuttige informatie...
  * (Openbare Preview) Sleutelwoord automatisch aanvullen en IntelliSense ondersteuning voor Hive. schrijven van scripts Hive, HDInsight Tools voor Visual Studio toohelp toegevoegd sleutelwoord automatisch aanvullen en IntelliSense-ondersteuning voor Hive.
  * Storm-ondersteuning. U kunt nu HDInsight Tools voor Visual Studio toodevelop Storm-topologieën/Spouts/Bolts in C#. U kunt vervolgens verzenden Hallo ontwikkeld topologie tooa Storm-cluster en Hallo bolt-topologie/spout status zien. U kunt het systeemlogboek in Logboeken en klant registreert tootroubleshoot uw Storm-topologieën/Bolts/Spouts. U kunt ook bestaande JAVA-elementen in Storm op HDInsight.
    
    Zie voor meer informatie [aan de slag met HDInsight Hadoop-hulpprogramma's voor Visual Studio](../hdinsight/hdinsight-hadoop-visual-studio-tools-get-started.md).

## <a id="known_issues_2_5_1"></a>Azure SDK voor .NET 2.5.1 bekende problemen en beperkingen
* Azure API-Apps wordt weergegeven als een implementatiedoel voor mobiele Apps. Web Apps moet Hallo enige doel voor Mobile Apps tot en met een latere release. 
* Azure API-App inrichten kan leiden tot succes maar afwisselend mislukken tooupdate Hallo voortgang in hello Azure App Service-activiteit venster. Tijdelijke oplossing is toocheck status van Hallo nieuwe Azure API App in hello Azure-Portal. 
* Bestand > Nieuw Project > API-App > F5 ervaring resulteert in een HTTP-fout, omdat er geen default/index.html. Tijdelijke oplossing is toomanually bladeren toohello/api/waarden-URL. 
* Server Explorer pictogrammen weergegeven en met tussenpozen platte. Dit probleem wordt opgelost tegenover opnieuw te starten. 
* Als een uitzondering is opgetreden tijdens het inrichten van Web-App of API-App (zoals quotum overschreden fouten of dubbele naam van de Azure API-App-gateway), wordt in Hallo fouten sommige onbewerkte JSON-tekst weergeven. 
* Maken van onregelmatige projecten problemen bij het Application Insights is ingeschakeld tijdens het project maken.
* In sommige gevallen kan gegenereerd hello Azure API-App clientcode ontbreekt naamruimten, moeten deze toobe handmatig opgenomen (of automatisch geïmporteerd via Visual Studio-hints) voor de code toocompile. 
* Mobiele App projecten moet tooweb gepubliceerde apps, maar u moet een site die u hebt gemaakt als een mobiele App in Azure Portal Hallo omdat mobiele App-projecten is vereist voor een database kiezen. 
* Hallo-startpagina voor mobiele Apps gebruikt Hallo term 'mobiele service' in plaats van 'mobiele apps' 
* Mobiele App-project maken kan duren voordat de minuut toocreate tooa. 
* Tijdens de API-App weer inrichten (in sommige gevallen) een fout van hello Azure API opgetreden bij het weergeven dat Hallo machtigingen kunnen niet worden ingesteld naar behoren tijdens het Hallo API-App juist is ingericht en is klaar voor gebruik. U kunt handmatig hello Azure-Portal met machtigingen instellen.
* Application Insights wordt niet ondersteund voor sjablonen van de API-App en sjablonen van de mobiele App.
* API-App-projecten kunnen niet worden gebruikt in combinatie met Cloud Service-projecten.
* API-App-projectsjablonen zijn alleen beschikbaar in C#.
* API-App-verbruik via contextmenu van Hallo 'Azure API-App-Client toevoegen' wordt alleen ondersteund in C#.

