---
title: aaaAzure SDK voor .NET 2.9 Release-opmerkingen
description: Azure SDK voor .NET 2.9 Release-opmerkingen
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a>Azure SDK voor .NET 2.9 release-opmerkingen

Dit onderwerp bevat opmerkingen bij de release voor versies 2.9 en 2.9.6 van Azure SDK voor .NET.

##<a name="azure-sdk-for-net-296-release-summary"></a>Azure SDK voor .NET 2.9.6 release samenvatting

Releasedatum: 16-11-2016
 
Er zijn geen recente wijzigingen toohello Azure SDK 2.9 zijn geïntroduceerd in deze release. Er is ook geen tooleverage upgradeproces nodig deze SDK met bestaande Cloud Service-projecten.

### <a name="visual-studio-2017-release-candidate"></a>Visual Studio 2017 Release Candidate

- In Visual Studio 2017 RC, wordt deze versie van hello Azure SDK voor .NET ingebouwd in hello Azure werkbelasting. Alle Hallo-hulpprogramma's, moet u toodo ontwikkelen van Azure zal onderdeel zijn van Visual Studio 2017 RC voortaan. Voor Visual Studio 2015 en Visual Studio 2013 steeds Hallo SDK nog beschikbaar is via WebPI. We zullen worden beëindigde Azure SDK voor .NET-versies voor Visual Studio 2013 wanneer Visual Studio 2017 als laatste product loslaat. Volg deze link toodownload Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/

### <a name="azure-diagnostics"></a>Azure Diagnostics

- Een gedeeltelijke verbindingsreeks gewijzigde Hallo gedrag tooonly opslaan met Hallo sleutel vervangen door een token voor de verbindingsreeks voor opslag van Cloud Services-diagnostische gegevens. de werkelijke opslagsleutel Hallo worden nu opgeslagen in de map gebruikersprofiel Hallo zodat de toegang kan worden beheerd. Visual Studio wordt Hallo-opslagsleutel lezen uit de map voor lokale foutopsporing en publicatieproces gebruikersprofiel. 
- In het antwoord toohello wijziging die hierboven worden beschreven, team Visual Studio Online verbeterde hello Azure Cloud Services-implementatiesjabloon taak zodat gebruikers Hallo-opslagsleutel voor het instellen van de extensie voor diagnostische gegevens bij het publiceren van tooAzure in continue integratie kunnen opgeven en implementatie.
- We hebben het mogelijke toostore beveiligde verbindingsreeks en tokeniseren voor Azure Diagnostics (af), het oplossen van problemen met configuratie over environements toohelp aangebracht.
 
### <a name="windows-server-2016-virtual-machines"></a>Windows Server 2016 virtuele machines

- Visual Studio ondersteunt nu implementeren Cloudservices tooOS familie 5 (Windows Server 2016) virtuele machines. Voor bestaande cloudservices, kunt u uw instellingen tootarget Hallo van nieuwe OS-familie. Bij het maken van nieuwe cloudservices als u ervoor kiest toocreate Hallo service met .net 4.6 of hoger, wordt standaard Hallo service toouse OS-familie 5.  Voor meer informatie kunt u bekijken Hallo [Gastbesturingssysteemgroep ondersteunen tabel](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).

#### <a name="known-issues"></a>Bekende problemen

- Azure .NET SDK 2.9.6 geïntroduceerd een beperking die blokkeert de implementatie van niet-ondersteunde .NET frameworks (zoals .NET 4.6) tooany OS-familie met projecten < 5. Een tijdelijke oplossing wordt aangeboden [hier](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).

 
### <a name="azure-in-role-cache"></a>Azure In-Role Cache 

- Ondersteuning voor Azure In-Role Cache eindigt op 30 November 2016. Klik voor meer informatie [hier](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).

### <a name="azure-resource-manager-templates-for-azure-stack"></a>Azure Resource Manager-sjablonen voor Azure Stack

- Hebben wij de Stack Azure als het implementatiedoel van een voor uw Azure Resource Manager-sjablonen.


## <a name="azure-sdk-for-net-29-summary"></a>Azure SDK voor .NET 2.9 samenvatting

## <a name="overview"></a>Overzicht
Dit document bevat Hallo release-opmerkingen voor hello Azure SDK voor .NET 2.9 release. 

Zie voor gedetailleerde informatie over de updates in deze release Hallo [Azure SDK 2.9 aankondiging post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a>Azure SDK 2.9 voor Visual Studio 2015 Update 2 en Visual Studio "15" Preview
Deze update omvat Hallo oplossingen voor problemen te volgen:

* Verwante tooREST API Client generatie uitgeven in in welke tekenreeks Hallo 'Onbekend Type' wordt weergegeven als Hallo-naam van Hallo code gen map en/of Hallo-naam van het Hallo-naamruimte neergezet in Hallo gegenereerde code.
* Verwante tooScheduled WebJobs in welke Hallo verificatiegegevens toobe toohello Scheduler-inrichtingsproces doorgegeven vertoonde uitgeven.

Deze update bevat de volgende nieuwe functie Hallo:

* Ondersteuning voor secundaire App Services Hallo 'Services' tabblad Hallo inrichting dialoogvenster App Service. 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a>Azure Data Lake Tools voor Visual Studio 2015 Update 2
Deze update omvat Hallo volgende:

* **Azure Data Lake Tools** voor Visual Studio nu samengevoegd met hello Azure SDK voor .NET versie. Hallo-hulpprogramma wordt automatisch geïnstalleerd wanneer u Azure SDK installeert. 
  
    Hallo hulpprogramma vaak wordt bijgewerkt, gaat u [hier](http://aka.ms/datalaketool) tooget Hallo updates.
* **Server Explorer** nu kunt u alle tooview en sommige U-SQL-metagegevens-entiteiten maken. Zie voor meer informatie [dit](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.

## <a name="hdinsight-tools"></a>HDInsight-hulpprogramma 's
**HDInsight Tools** voor Visual Studio nu ondersteunt HDInsight versie 3.3, inclusief met Tez-grafieken en andere taal worden opgelost.

## <a name="azure-resource-manager"></a>Azure Resource Manager
Deze release voegt [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) ondersteuning voor Resource Manager-sjablonen.

## <a name="see-also"></a>Zie ook
[Azure SDK 2.9 aankondiging post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

