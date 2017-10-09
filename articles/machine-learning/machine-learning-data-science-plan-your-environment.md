---
title: aaaIdentify scenario's en plan uw proces analytics - Azure | Microsoft Docs
description: Abonnement voor geavanceerde analyses op basis van een reeks van belangrijke vragen.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 421520dd-7728-4d29-889c-ebe6a0a6fb07
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: e445973be0d020a4f9949e5c9d8554fbbd4b515f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooidentify-scenarios-and-plan-for-advanced-analytics-data-processing"></a>Hoe advanced analytics gegevensverwerking tooidentify scenario's en plannen
Welke bronnen moet u van plan tooinclude bij het instellen van een omgeving toodo geavanceerde analyses verwerken van een gegevensset? In dit artikel stelt een reeks vragen tooask waarmee identificeren Hallo taken en bronnen die relevant zijn voor uw scenario. Hallo-volgorde van stappen op hoog niveau voor predictive analytics wordt beschreven in [wat is er Hallo Team gegevens wetenschap proces (TDSP)?](data-science-process-overview.md). Elk van deze stappen nodig specifieke bronnen voor Hallo taken relevante tooyour bepaald scenario. Hallo belangrijke vragen tooidentify uw scenario problematisch gegevens logistiek, kenmerken, kwaliteit Hallo Hallo-gegevenssets en Hallo-hulpprogramma's en talen die u liever toodo Hallo analyse.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="logistic-questions-data-locations-and-movement"></a>Logistic vragen: gegevenslocaties en verkeer
Hallo logistic vragen hebben betrekking op locatie Hallo Hallo **gegevensbron**, Hallo **doellocatie** in Azure, en de vereisten voor bewegende Hallo-gegevens, inclusief Hallo planning, het bedrag en resources betrokken. Hallo gegevens moet mogelijk verschillende keren verplaatst tijdens Hallo analytics toobe. Een gebruikelijk scenario is toomove lokale gegevens in een vorm van opslag in Azure en vervolgens in Machine Learning Studio.

1. **Wat is uw gegevensbron?** Is het lokaal of in de cloud Hallo? Bijvoorbeeld:
   
   * Hallo gegevens is openbaar beschikbaar is op een HTTP-adres.
   * Hallo gegevens bevindt zich op een LAN/bestandslocatie.
   * Hallo-gegevens zijn in een SQL Server-database.
   * Hallo-gegevens worden opgeslagen in een Azure storage-container
2. **Wat is Azure bestemming Hallo?** Waar heeft het toobe voor verwerking of modelleren nodig? Bijvoorbeeld:
   
   * Azure Blob Storage
   * Azure SQL-databases
   * SQL Server op virtuele Azure-machine
   * HDInsight (Hadoop op Azure) of Hive-tabellen
   * Azure Machine Learning
   * Koppelbaar Azure virtuele harde schijven.
3. **Hoe gaat u toomove Hallo gegevens?**  hello procedures en bronnen beschikbaar tooingest gegevens of laden in tal van andere opslag en verwerking van omgevingen worden beschreven in de volgende onderwerpen Hallo.
   
   * [Gegevens laden in omgevingen met opslag voor analyses](machine-learning-data-science-ingest-data.md)
   * [Uw trainingsgegevens importeren in Azure Machine Learning Studio van verschillende gegevensbronnen](machine-learning-data-science-import-data.md).
4. **Hoeft Hallo gegevens toobe regelmatig verplaatst of gewijzigd tijdens de migratie** Overweeg het gebruik van Azure Data Factory (ADF) gegevens behoeften toobe voortdurend worden gemigreerd, met name als een hybride scenario die toegang heeft tot zowel on-premises en cloudresources betrokken is, of gegevens Hallo is transactionele of toobe gewijzigd moet of bedrijfslogica tooit toegevoegd in de loop van de Hallo wordt gemigreerd. Zie voor meer informatie [verplaatsen van gegevens uit een lokale SQL server tooSQL Azure met Azure Data Factory](machine-learning-data-science-move-sql-azure-adf.md)
5. **Hoeveel gegevens Hallo is verplaatst toobe tooAzure?** Zeer grote gegevenssets overschrijdt misschien de opslagcapaciteit Hallo van bepaalde omgevingen. Zie voor een voorbeeld Hallo bespreking van de maximale grootte voor Machine Learning Studio in de volgende sectie Hallo. In dergelijke gevallen kan een voorbeeld van Hallo gegevens tijdens de analyse hello worden gebruikt. Zie voor meer informatie over hoe toodown-sample gegevensset in verschillende Azure-omgevingen, [voorbeeldgegevens in Hallo Team gegevens wetenschap proces](machine-learning-data-science-sample-data.md).

## <a name="data-characteristics-questions-type-format-and-size"></a>Vragen over de kenmerken van gegevens: type, indeling en grootte
Deze vragen zijn belangrijke tooplanning uw opslag en omgevingen, die zijn juiste toovarious verwerken typen gegevens en elk hebben bepaalde beperkingen.

1. **Wat zijn de gegevenstypen Hallo?** Bijvoorbeeld:
   
   * Numerieke
   * Categorische gegevens
   * Tekenreeksen
   * Binaire
2. **Hoe wordt uw gegevens opgemaakt?** Bijvoorbeeld:
   
   * Door komma's gescheiden (CSV) of door tabs gescheiden (TSV) platte bestanden
   * Wel of niet gecomprimeerd
   * Azure blobs
   * Hadoop Hive-tabellen
   * SQL Server-tabellen
3. **Hoe groot is uw gegevens?**
   
   * Kleine: minder dan 2GB
   * Gemiddeld: Groter is dan 2GB en minder dan 10GB
   * Grote: Groter zijn dan 10GB

Neem bijvoorbeeld hello Azure Machine Learning Studio omgeving:

* Zie voor een lijst van Hallo Gegevensopmaak en die worden ondersteund door Azure Machine Learning Studio [gegevensindelingen en de ondersteunde gegevenstypen](machine-learning-data-science-import-data.md#data-formats-and-data-types-supported) sectie.
* Zie voor informatie over gegevens beperkingen voor Azure Machine Learning Studio, Hallo **hoe groot mag Hallo gegevensset zijn voor mijn modules?** sectie van [importeren en exporteren van gegevens voor Machine Learning](machine-learning-faq.md#machine-learning-studio-questions)

Zie voor informatie over Hallo beperkingen van andere Azure-services gebruikt tijdens Hallo analytics, [Azure-abonnement en Service-limieten, quota's en beperkingen](../azure-subscription-service-limits.md).

## <a name="data-quality-questions-exploration-and-pre-processing"></a>Vragen over de kwaliteit van de gegevens: exploratie en vooraf verwerken
1. **Wat u weten over uw gegevens** Verken gegevens wanneer u een understand toogain moet de basiskenmerken. Wat patronen of trends deze voorwerpen, wat uitschieters heeft of hoeveel waarden ontbreken. Deze stap is belangrijk voor het bepalen van Hallo mate van vooraf verwerken die nodig zijn voor formuleren hypothesen die kunnen voorstellen meest relevante Hallo-functies of typ van analyse en voor het plannen voor het verzamelen van aanvullende gegevens te formuleren. Beschrijvende statistiek berekenen en uitzetten van visualisaties zijn nuttige technieken voor inspectie van gegevens. Voor meer informatie over hoe tooexplore een gegevensset in verschillende Azure-omgevingen, Zie [gegevens in Hallo Team gegevens wetenschap proces](machine-learning-data-science-explore-data.md).
2. **Vereist Hallo gegevens vooraf verwerken of reinigen?**
   Vooraf verwerken en het opruimen van gegevens zijn belangrijke taken die normaal gesproken plaatsvinden moeten voordat gegevensset effectief kan worden gebruikt voor machine learning. Onbewerkte gegevens is vaak veel ruis veroorzaken en onbetrouwbare mogelijk ontbreken waarden. Met deze gegevens voor modellering kan misleidende resultaten opleveren. Zie voor een beschrijving [tooprepare taakgegevens voor verbeterde machine learning](machine-learning-data-science-prepare-data.md).

## <a name="tools-and-languages-questions"></a>Hulpprogramma's en talen vragen
Er zijn veel opties, afhankelijk van welke talen en ontwikkelomgevingen of hulpprogramma's of u kunt met behulp van meest conformable zijn.

1. **Welke talen wilt u liever toouse voor analyse?**  
   
   * R
   * Python
   * SQL
2. **Welke hulpprogramma's moet u voor data-analyse gebruiken?**
   
   * [Microsoft Azure Powershell](/powershell/azure/overview) -een scripttaal tooadminister uw Azure-resources in een scripttaal gebruikt.
   * [Azure Machine Learning Studio](machine-learning-what-is-ml-studio.md)
   * [Revolution Analytics](http://www.revolutionanalytics.com/revolution-r-open)
   * [RStudio](http://www.rstudio.com)
   * [Python Tools for Visual Studio](http://microsoft.github.io/PTVS/)
   * [Anaconda](https://www.continuum.io/why-anaconda)
   * [Jupyter-notebooks](http://jupyter.org/)
   * [Microsoft Power BI](http://powerbi.microsoft.com)

## <a name="identify-your-advanced-analytics-scenario"></a>Identificeren van uw scenario geavanceerde analyses
Zodra u de vragen in de vorige sectie Hallo Hallo hebt beantwoord, bent u klaar toodetermine welke scenario best past bij uw aanvraag. Hallo voorbeeldscenario's worden beschreven in [scenario's voor geavanceerde analyses in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md).

