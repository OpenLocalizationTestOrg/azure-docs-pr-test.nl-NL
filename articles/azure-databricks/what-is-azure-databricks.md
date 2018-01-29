---
title: Wat is Azure Databricks? | Microsoft Docs
description: Meer informatie over wat Azure Databricks is en hoe hiermee Spark Databricks in Azure terechtkomt. Azure Databricks is een op Apache Spark gebaseerd analyseplatform, geoptimaliseerd voor het Microsoft Azure-platform voor cloudservices.
services: azure-databricks
documentationcenter: 
author: nitinme
manager: cgronlun
editor: cgronlun
ms.service: azure-databricks
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 01/22/2018
ms.author: nitinme
ms.custom: mvc
ms.openlocfilehash: 2c42f8a9dd67ec2debecffd7cb2cdb902ab203a2
ms.sourcegitcommit: 9890483687a2b28860ec179f5fd0a292cdf11d22
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/24/2018
---
# <a name="what-is-azure-databricks"></a>Wat is Azure Databricks?

Azure Databricks is een op Apache Spark gebaseerd analyseplatform, geoptimaliseerd voor het Microsoft Azure-platform voor cloudservices. Databricks is ontwikkeld in samenwerking met de grondleggers van Apache Spark en met Azure geïntegreerd. Hierdoor biedt het installatie met één klik, gestroomlijnde werkstromen en een interactieve werkruimte waarmee gegevenswetenschappers, gegevenstechnici en bedrijfsanalisten samen kunnen werken.

![Wat is Azure Databricks? ](./media/what-is-azure-databricks/azure-databricks-overview.png "Wat is Azure Databricks?")

## <a name="apache-spark-based-analytics-platform"></a>Op Apache Spark gebaseerd analyseplatform

Azure Databricks omvat de volledige open source clustertechnologieën en -mogelijkheden van Apache Spark. Spark in Azure Databricks omvat de volgende onderdelen:

![Apache Spark in Azure Databricks](./media/what-is-azure-databricks/apache-spark-ecosystem-databricks.png "Apache Spark in Azure Databricks")

* **Spark SQL en DataFrames**: Spark SQL is de Spark-module voor het werken met gestructureerde gegevens. Een DataFrame is een gedistribueerde verzameling van gegevens die zijn ingedeeld in kolommen met een naam. Er ligt hetzelfde concept aan ten grondslag als aan een tabel in een relationele database of aan een gegevensframe in R/Python.

* **Streaming**: realtime gegevensverwerking en -analyse voor analytische en interactieve toepassingen. Kan worden geïntegreerd met HDFS, Flume en Kafka.

* **MLib**: Machine Learning-bibliotheek die bestaat uit veelgebruikte leeralgoritmen en hulpprogramma's, zoals voor classificatie, regressie, clustering, gezamenlijke filterfuncties, dimensionaliteitsvermindering en in de vorm van onderliggende optimalisatieprimitieven.

* **GraphX**: grafieken en grafiekberekeningen voor een grote diversiteit aan scenario’s, van cognitieve analyses tot gegevensverkenning.

* **Spark Core API**: biedt ondersteuning voor onder andere R, SQL, Python, Scala en Java.

## <a name="apache-spark-in-azure-databricks"></a>Apache Spark in Azure Databricks

Azure Databricks bouwt voort op de mogelijkheden van Spark door een cloudplatform dat niet hoeft te worden beheerd, en omvat:

- Volledig beheerde Spark-clusters
- Een interactieve werkruimte voor verkenning en visualisatie
- Een platform voor het aansturen van uw favoriete Spark-toepassingen

### <a name="fully-managed-apache-spark-clusters-in-the-cloud"></a>Volledig beheerde Apache Spark-clusters in de cloud

Azure Databricks beschikt over een veilige en betrouwbare productieomgeving in de cloud, die wordt beheerd en ondersteund door Spark-experts. U kunt:

* Clusters maken in enkele seconden.
* Clusters automatisch dynamisch omhoog en omlaag schalen, en deze delen tussen teams. 
* Clusters programmatisch gebruiken met behulp van de REST API's. 
* Beveiligde gegevensintegratiefuncties gebruiken die boven op Spark zijn gebouwd, en waarmee u uw gegevens kunt samenbrengen zonder dat er sprake is van centralisering. 
* Directe toegang krijgen tot de nieuwste functies van Apache Spark die elke versie heeft.

### <a name="databricks-runtime"></a>Databricks Runtime
Databricks Runtime is in Apache Spark ingebouwd en is als systeemeigen onderdeel voor de Azure-cloud gebouwd. 

Met de optie om **zonder servers** te werken, ontdoet Azure Databricks de infrastructuur en de noodzaak om gespecialiseerde kennis te hebben, van alle complexiteit die gepaard gaat met het configureren van uw gegevensinfrastructuur. De serverloze optie helpt gegevensanalisten om snel in teamverband herhalende taken uit te voeren.

Voor gegevenstechnici die zijn geïnteresseerd in de prestaties van productietaken, biedt Azure Databricks een Spark-engine die sneller is en prestaties levert via diverse optimalisaties op de I/O- en verwerkingslaag (Databricks I/O).

### <a name="workspace-for-collaboration"></a>Werkruimte voor samenwerking

Azure Databricks is een geïntegreerde samenwerkingsomgeving die het proces voor het verkennen van gegevens, het maken van prototypes en het uitvoeren van gegevensgestuurde toepassingen in Spark stroomlijnt.

* Bepaal zelf hoe u gegevens kunt gebruiken met eenvoudige gegevensverkenning.
* Documenteer uw voortgang in notitieblokken in R, Python, Scala of SQL.
* Visualiseer gegevens met een paar muisklikken, en gebruik vertrouwde hulpprogramma's zoals Matplotlib, ggplot of d3.
* Gebruik interactieve dashboards om dynamische rapporten te maken.
* Gebruik Spark en werk tegelijkertijd met de gegevens.

## <a name="enterprise-security"></a>Beveiliging voor bedrijven

Azure Databricks biedt Azure-beveiliging op bedrijfsniveau, waaronder een integratie met Azure Active Directory, besturingselementen op basis van rollen en SLA's die uw gegevens en uw bedrijf beschermen.

* Door de integratie met Azure Active Directory kunt u volledige Azure-oplossingen uitvoeren met behulp van Azure Databricks.
* De op rollen gebaseerde toegang van Azure Databricks maakt het mogelijk om uiterst gedetailleerde gebruikersmachtigingen voor notitieblokken, clusters, taken en gegevens te gebruiken.
* Hoogwaardige SLA's. 

## <a name="integration-with-azure-services"></a>Integratie met Azure-services

Azure Databricks is diep geïntegreerd in Azure-databases en archieven: SQL Data Warehouse, Cosmos DB Data Lake Store en Blob Storage. 

## <a name="integration-with-power-bi"></a>Integratie met Power BI
Dankzij de uitgebreide integratie met Power BI stelt Azure Databricks u in staat om indrukwekkende inzichten snel en eenvoudig te ontdekken en met anderen te delen. U kunt ook andere BI-tools gebruiken, zoals Tableau Software via JDBC/ODBC-clustereindpunten.

## <a name="next-steps"></a>Volgende stappen

* [Quickstart: Een Spark-taak uitvoeren op Azure Databricks](quickstart-create-databricks-workspace-portal.md)
* [Werken met Spark-clusters](https://docs.azuredatabricks.net/user-guide/clusters/index.html)
* [Werken met notitieblokken](https://docs.azuredatabricks.net/user-guide/notebooks/index.html)
* [Spark taken maken](https://docs.azuredatabricks.net/user-guide/jobs.html)

 









