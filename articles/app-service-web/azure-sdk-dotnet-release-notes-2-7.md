---
title: aaaAzure SDK voor .NET 2.7 en .NET 2.7.1 Release-opmerkingen
description: Azure SDK voor .NET 2.7 en .NET 2.7.1 Release-opmerkingen
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: 877d070a-9bd5-49b3-8fac-6bb5f65c3554
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 8ec72b0f18702e6d811f0cbe4790685be7881d96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-27-and-net-271-release-notes"></a>Azure SDK voor .NET 2.7 en .NET 2.7.1 Release-opmerkingen
## <a name="overview"></a>Overzicht
Dit document bevat Hallo release-opmerkingen voor hello Azure SDK voor .NET 2.7 release. 

Hallo-document bevat ook Hallo release-opmerkingen voor hello Azure SDK voor .NET 2.7.1 release.

Azure SDK 2.7 wordt alleen ondersteund in Visual Studio 2015 en Visual Studio 2013. [Azure SDK 2.6](https://azure.microsoft.com/downloads/) is Hallo ondersteund laatste SDK voor Visual Studio 2012.

Zie voor gedetailleerde informatie over deze release [Azure SDK 2.7 aankondiging post](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/) en [Azure SDK 2.7.1 aankondiging post](http://go.microsoft.com/fwlink/?LinkId=623850).

## <a name="azure-sdk-for-net-27"></a>Azure SDK voor .NET 2.7
### <a name="sign-in-improvements-for-visual-studio-2015"></a>Meld u aan de verbeteringen voor Visual Studio 2015
2.7 van Azure SDK voor Visual Studio 2015 ondersteunt Hallo nieuwe identiteit functies in Visual Studio 2015.  Dit biedt ondersteuning voor de accounts toegang krijgen tot Azure via op rollen gebaseerd toegangsbeheer, Cloud Solution Providers, DreamSpark en andere typen account en abonnement.

Hallo aanmelden verbeteringen die deel uitmaakt van de Azure SDK 2.7 zijn alleen beschikbaar in Visual Studio 2015. Ondersteuning voor Visual Studio 2013 is opgenomen in de Azure SDK 2.7.1.

### <a name="mobile-sdk"></a>Mobiele SDK
Bijgewerkt **Mobile Apps** sjablonen tooreflect nieuwste [NuGet-pakket](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) en -instellingen te openen.

### <a name="service-bus"></a>Service Bus
Algemene oplossingen voor problemen en verbeteringen. Raadpleeg voor informatie over updates en functies, toohello release-opmerkingen van de meest recente Hallo [Service Bus NuGet](http://www.nuget.org/packages/WindowsAzure.ServiceBus/).

### <a name="hdinsight-tools"></a>HDInsight-hulpprogramma 's
In deze release Hallo zijn volgende updates aangebracht. Deze updates zijn in preview. Zie voor meer informatie [deze blog](http://go.microsoft.com/fwlink/?LinkId=619108).

* Hive-grafieken voor Hive op Tez-taken
* Volledige Hive DML IntelliSense-ondersteuning
* Ondersteuning voor pig-sjabloon
* Storm-sjablonen voor Azure-services

#### <a name="breaking-changes"></a>Wijzigingen op te splitsen
* Oude **Storm** project moet worden bijgewerkt wanneer u deze versie van het Hallo-hulpprogramma's. Zie voor meer informatie [deze blog](http://go.microsoft.com/fwlink/?LinkId=619108).
* Web Visual Studio Express is niet langer ondersteund. Zie voor meer informatie [deze blog](http://go.microsoft.com/fwlink/?LinkId=619108).

### <a name="azure-app-service-tools"></a>Hulpprogramma's van Azure App Service
In deze release Hallo zijn volgende updates aangebracht in tooWeb extra extensies. Zie voor meer informatie [dit](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/) blog. 

* Ondersteuning voor DreamSpark-accounts die zijn toegevoegd
* Volledige wijzigen tooAzure hulpprogramma's die zijn aangebracht toosupport Hallo van nieuwe Azure Resource Management API 's
* Ondersteuning voor Azure App Service te toegevoegd[Cloud Explorer](#cloud_explorer)

#### <a name="known-issues"></a>Bekende problemen
Web-App-implementatiesleuf knooppunten worden niet weergegeven onder het knooppunt van de Hallo sleuven in Server Explorer en Web-App-implementatiesleuf onderliggende knooppunten onder Cloud Explorer niet laden. Dit probleem is opgelost en voorbereid op Hallo volgende SDK-versie. 

### <a name="cloud_explorer"></a>Cloud Explorer voor Visual Studio 2015
Azure SDK 2.7 omvat Cloud Explorer voor Visual Studio 2015 waarmee u tooview uw Azure-resources, inspecteren van de eigenschappen en uitvoeren van acties van de belangrijkste ontwikkelaars uit vanuit Visual Studio. 

Cloud explorer ondersteunt Hallo volgende:

* Resourcegroep en het resourcetype weergaven van uw Azure-resources 
* Resources zoeken op naam (beschikbaar in de weergave van brontype)
* Ondersteuning voor abonnementen en -resources met rol gebaseerd toegangsbeheer (RBAC een) toegepast 
* Geïntegreerde actie Configuratiescherm waarmee ontwikkelaars gerichte acties specifieke tooselected resources weergegeven. Bijvoorbeeld: externe foutopsporingsprogramma koppelen voor virtuele Machines die zijn gemaakt met behulp van Hallo Resource Manager-Stack diagnostische gegevens weergeven voor virtuele Machines, enzovoort.
* Geïntegreerde eigenschappen Configuratiescherm waarin ontwikkelaars gerichte eigenschappen vaak nodig tijdens ontwikkelen en testen 
* Snelle overschakelen van Hallo account toouse bij het opsommen van de resources (opdracht instellingen op de werkbalk gebruiken) 
* Filteren van abonnementen toouse bij het opsommen van de resources (opdracht instellingen op de werkbalk gebruiken) 
* Dieptekoppelingen toohello Azure-Portal voor het beheren van resources en resourcegroepen 

### <a name="azure-resource-manager-tools"></a>Azure Resource Manager-hulpprogramma 's
Hello Azure Resource Manager-hulpprogramma's zijn bijgewerkt toowork met rollen gebaseerd toegangsbeheer (RBAC) en het nieuwe abonnement typen.  Bij deze wijzigingen is inbegrepen Hallo mogelijkheid toouse nieuwe opslagaccounts, Daarnaast tooclassic opslag, toostore artefacten tijdens de implementatie.  

Als u een Azure-resourcegroepproject van een eerdere versie van Hallo SDK Hello SDK 2.7 gebruikt, is het script voor een nieuwe implementatie benodigde toodeploy met een nieuw opslagaccount in plaats van klassieke opslag.  U wordt gevraagd voordat wijzigingen worden aangebracht tooyour project tooadd Hallo nieuwe script.  Hallo oude script worden gewijzigd en moet u toomanually Breng eventuele wijzigingen toohello nieuwe script.

### <a name="storage-explorer-tools"></a>Hulpprogramma's voor Storage Explorer
* Ondersteuning voor het weergeven van toevoeg-Blobs. Meer informatie over de in [dit blogbericht](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/04/13/introducing-azure-storage-append-blob.aspx). 
* Ondersteuning voor het weergeven van Premium Storage-accounts via Server Explorer. Server Explorer worden alleen weergegeven voor pagina-blobs voor premium storage-accounts als type Hallo alleen ondersteund voor premium storage-accounts.

### <a name="azure-data-factory-tools-for-visual-studio"></a>Azure Data Factory-hulpprogramma's voor Visual Studio
Inleiding tot **Azure Data Factory-hulpprogramma's** voor Visual Studio. Hieronder vindt u functies Hallo ingeschakeld. Zie [deze blog](http://go.microsoft.com/fwlink/?LinkId=617530) voor meer informatie.

* **Sjabloon gebaseerd ontwerpen**: Selecteer gebaseerde sjablonen gebruik geïntegreerd, data movement sjablonen of gegevensverwerking sjablonen toodeploy een oplossing end-to-end-integratie en aan de slag met Data Factory snel. 
* **Integratie met Solution Explorer voor het ontwerpen en implementeren van de Data Factory-entiteiten**: maken en implementeren van de pijplijnen en gerelateerde entiteiten als Visual Studio-projecten. 
* **Integratie met de diagramweergave voor visual interactie bij het ontwerpen van**: pijplijnen en gegevenssets met hulp van Hallo diagramweergave visueel te ontwerpen. 
* **Integratie met Server explorer voor het bekijken en interactie met de reeds geïmplementeerde entiteiten**: hefboomwerking Hallo Server Explorer toobrowse al geïmplementeerd gegevensfactory's en bijbehorende entiteiten. Een geïmplementeerde gegevensfactory of een entiteit (gegevenssets Pipeline, de gekoppelde Service) in uw project importeren. 
* **JSON bewerken met schema-validatie en geavanceerde intellisense**: efficiënt te configureren en bewerken van JSON-documenten van de Data Factory-entiteiten met uitgebreide intellisense en schema-validatie 
* **Publicatie van een omgeving met meerdere**: opgestelde pijplijnen toodev, test- of Prod omgeving publiceren door afzonderlijke configuratiebestanden voor elke omgeving te maken.
* **Pig, Hive en .net op basis van gegevensverwerking ondersteuning**: ondersteuning voor Pig en Hive-Scripts in Data Factory-project. Ondersteuning voor C#-Project voor het beheren van .net verwijzende activiteit.

## <a name="azure-sdk-for-net-271"></a>Azure SDK voor .NET 2.7.1
Hallo volgende sectie bevat updates die zijn geïntroduceerd in hello Azure SDK voor .NET 2.7.1 release.

### <a name="hdinsight-tools"></a>HDInsight-hulpprogramma 's
Zie voor meer uitleg over updates van HDInsight-hulpprogramma's gedetailleerde, [deze blog](http://go.microsoft.com/fwlink/?LinkId=623831).

* Hive-weergave van de Operator taak (een nieuwe functie)
  
    toohelp u inzicht in uw Hive-query betere, Hallo Operator weergave Hive-functie is toegevoegd. toosee alle Hallo operators in een hoekpunt, dubbelklikt u op de hoekpunten van de taakgrafiek Hallo Hallo. tooview meer details van een bepaalde operator Beweeg de muisaanwijzer over die operator.
* Hive-fout-markering (een nieuwe functie)
  
    tooenable die u tooview Hallo grammaticafouten onmiddellijk Hallo fout markering Hive-functie is toegevoegd. Ook foutberichten zijn uitgebreid en u ziet nu gedetailleerde grammaticafouten onmiddellijk (totdat deze release, moest u toosubmit een Hive-script toohello cluster en wacht enige tijd voordat u meer informatie over het foutbericht).  
* Storm-topologie grafiek (een nieuwe functie)
  
    Visualiseren is erg belangrijk als u wilt dat toosee als uw topologie werkt zoals verwacht. In deze release toegevoegd we visualisatie voor Storm-grafieken. U kunt Hallo belangrijke metrische gegevens voor uw topologie visualiseren (bijvoorbeeld een kleur geeft weer een bepaalde Bolt 'bezet' is of niet). U kunt ook Dubbelklik Hallo Bolt/Spout tooview meer informatie.
* Ondersteuning voor HDInsight-clusters die zijn gemaakt in hello Azure-Portal (een bug fix)
  
    U kunt nu gebruik van Visual Studio tooview en het verzenden van taken tooall uw HDInsight-clusters ongeacht waar Hallo cluster zijn gemaakt.
* Meer ondersteuning voor IntelliSense & sneller Hive-metagegevens bij het laden van (een verbetering)
  
    We hebben Hallo IntelliSense verbeterd door meer gebruikersvriendelijker suggesties toe te voegen. Bijvoorbeeld, kan tabelalias nu ook worden voorgesteld in IntelliSense zodat u kunt eenvoudig uw query schrijven. We hebben ook een Hallo Hive-metagegevens verbeterde laden zodat het duurt slechts enkele seconden toolist Hallo databases, tabellen en kolommen van uw Hive-metastore.

Zie voor meer uitleg over updates van HDInsight-hulpprogramma's gedetailleerde, [deze blog](http://go.microsoft.com/fwlink/?LinkId=623831).

### <a name="improvements-in-visual-studio-2013"></a>Verbeteringen in Visual Studio 2013
* Azure SDK 2.7.1 kunt Visual Studio 2013 tooaccess Azure-accounts en -abonnementen via op rollen gebaseerd toegangsbeheer, Cloud Solution Providers en Dreamspark.
* Met Azure SDK 2.7.1 is nieuw venster van Cloud Explorer hulpprogramma Hallo nu ook beschikbaar in Visual Studio 2013.

### <a name="known-issues"></a>Bekende problemen
Een waarschuwing die Engels Hallo installatie hello Azure SDK 2.6 of 2.7.1 voor Visual Studio Community 2013 op een niet - Engelse OS wordt weergegeven en niet-Engelse resources van Visual Studio misschien overeen. Deze waarschuwing kan veilig worden genegeerd. Dit gebeurt alleen als Hallo machine niet een eerdere installatie van Visual Studio Community 2013 bevat en u Hallo SDK op een niet - Engelse OS installeert. Hallo-waarschuwing wordt weergegeven nadat Hallo taalpakket van de toepassing hello RTM resources tooVisual Studio, maar voordat deze Update 4 is van toepassing. Hallo waarschuwing genegeerd toegestaan Hallo language pack toocontinue en volledige toepassen Hallo Update 4-versie van Hallo taalpakket inhoud.

LightSwitch-projecten zijn niet compatibile met deze release. Dit probleem wordt opgelost met Hallo volgende SDK release.

## <a name="also-see"></a>Zie ook
[Azure SDK 2.7.1 aankondiging post](http://go.microsoft.com/fwlink/?LinkId=623850)

[Azure SDK 2.7 aankondiging post](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/)

[Ondersteuning en buiten gebruik stellen informatie voor hello Azure SDK voor .NET- en API 's](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

