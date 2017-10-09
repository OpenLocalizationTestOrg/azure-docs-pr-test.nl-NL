---
title: aaaUse Case - klant profileren
description: Informatie over hoe Azure Data Factory gebruikte toocreate een gegevensgestuurde werkstroom (pijplijn) tooprofile games klanten is.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: e07d55cf-8051-4203-9966-bdfa1035104b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 47f5e77242366c80cce2a2db65e3c696505b3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---customer-profiling"></a>Use case: klantprofilering
Azure Data Factory is een veel services gebruikt tooimplement Hallo Cortana Intelligence Suite van oplossing accelerators aan te schaffen.  Voor meer informatie over de Cortana Intelligence, gaat u naar [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics). In dit document, beschrijven we een eenvoudige gebruik case toohelp u aan de slag met informatie over hoe Azure Data Factory algemene analytics problemen kunt oplossen.

## <a name="scenario"></a>Scenario
Contoso is een gaming-bedrijf dat games voor meerdere platforms maakt: game-consoles, handheld apparaten en pc's (pc's). Als deze spelen spelers bevat, wordt dat nummers gebruikspatronen, gaming-stijl en voorkeuren van de gebruiker Hallo Hallo groot aantal logboekgegevens geproduceerd.  In combinatie met demografische gegevens, regio en productgegevens, Contoso kan uitvoeren analytics tooguide ze over hoe tooenhance spelers optreden en doel te definiëren voor upgrades en spel koopt. 

Contoso doel is tooidentify verkopen/cross-Upsell verkoopkansen op basis van Hallo games geschiedenis van de spelers en dwingende zakelijke groei van de functies toodrive toevoegen en een betere ervaring toocustomers. Voor deze aanvraag gebruiken we een gaming-bedrijf gebruiken als een voorbeeld van een bedrijf. Hallo bedrijf wil toooptimize de games op basis van gedrag van spelers. Deze principes tooany bedrijven die tooengage wil toepassen zijn klanten rond de goederen en diensten en hun klanten ervaring te verbeteren.

In deze oplossing wil Contoso tooevaluate Hallo effectiviteit van een marketingcampagne die onlangs zijn gestart. En beginnen met Hallo onbewerkte games Logboeken, het proces we ze aanvullen met geolocatie gegevens, basislid referentiegegevens reclame en ten slotte kopiëren naar een Azure SQL Database tooanalyze Hallo campagne impact.

## <a name="deploy-solution"></a>Oplossing implementeren
Alle gewenste tooaccess en proberen deze eenvoudige gebruiksvoorbeeld is een [Azure-abonnement](https://azure.microsoft.com/pricing/free-trial/), een [Azure Blob storage-account](../storage/common/storage-create-storage-account.md#create-a-storage-account), en een [Azure SQL Database](../sql-database/sql-database-get-started.md). U implementeert Hallo klant profilering pijplijn van Hallo **steekproef pijplijnen** tegel op Hallo-startpagina van uw gegevensfactory.

1. Maak een gegevensfactory of open een bestaande gegevensfactory. Zie [gegevens kopiëren van Blob Storage tooSQL-Database met de Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stappen toocreate een gegevensfactory.
2. In Hallo **DATA FACTORY** blade voor Hallo data factory, klikt u op Hallo **steekproef pijplijnen** tegel.

    ![Voorbeeld pijplijnen tegel](./media/data-factory-samples/SamplePipelinesTile.png)
3. In Hallo **steekproef pijplijnen** blade klikt u op Hallo **klant profilering** dat u wilt dat toodeploy.

    ![Voorbeeld pijplijnen-blade](./media/data-factory-samples/SampleTile.png)
4. Configuratie-instellingen voor Hallo voorbeeld opgeven. Bijvoorbeeld uw Azure-opslag-accountnaam en sleutel, naam van de Azure SQL-server, database, gebruikers-ID en wachtwoord.

    ![Voorbeeld-blade](./media/data-factory-samples/SampleBlade.png)
5. Nadat u klaar bent met het Hallo-configuratie-instellingen opgeven, klikt u op **maken** toocreate/implementeren Hallo voorbeeld pijplijnen en gekoppelde services/tabellen die worden gebruikt door Hallo pijplijnen.
6. U ziet Hallo status van implementatie op Hallo voorbeeld tegel die u eerder hebt geklikt op Hallo **steekproef pijplijnen** blade.

    ![Implementatiestatus](./media/data-factory-samples/DeploymentStatus.png)
7. Wanneer er Hallo **implementatie is voltooid** bericht op de tegel Hallo voor Hallo voorbeeld sluiten Hallo **steekproef pijplijnen** blade.  
8. Op **DATA FACTORY** blade ziet u dat het gekoppelde services, gegevenssets en pijplijnen tooyour data factory worden toegevoegd.  

    ![Blade Gegevensfactory](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="solution-overview"></a>Overzicht van de oplossing
Deze eenvoudige gebruiksvoorbeeld kan worden gebruikt als een voorbeeld van hoe u kunt Azure Data Factory tooingest gebruiken, voorbereiden, transformeren, analyseren en gegevens publiceren.

![End-to-end werkstroom](./media/data-factory-customer-profiling-usecase/EndToEndWorkflow.png)

Deze afbeelding ziet hoe Hallo gegevenspijplijnen worden weergegeven in hello Azure-portal nadat deze zijn geïmplementeerd.

1. Hallo **PartitionGameLogsPipeline** Hallo onbewerkte gebeurtenissen uit de blob-opslag gelezen en wordt gemaakt op basis van het jaar, maand en dag partities.
2. Hallo **EnrichGameLogsPipeline** gepartitioneerde game gebeurtenissen met de referentiegegevens geo-code koppelt en verrijkt Hallo gegevens via het toewijzen van IP-adressen toohello bijbehorende geografische locaties.
3. Hallo **AnalyzeMarketingCampaignPipeline** pijplijn gebruikt Hallo verrijkt gegevens en verwerkt deze Hello reclame gegevens toocreate Hallo uiteindelijke uitvoer met de effectiviteit van marketing campagne.

In dit voorbeeld is de Data Factory gebruikte tooorchestrate activiteiten die invoergegevens, transformeren en proces Hallo gegevens kopiëren en uit te voeren Hallo uiteindelijke gegevens tooan Azure SQL Database.  U kunt ook visualiseren Hallo-netwerk van gegevenspijplijnen, ze beheren en controleren van de status van Hallo gebruikersinterface.

## <a name="benefits"></a>Voordelen
Door het optimaliseren van hun profiel gebruiker analytics en het afstemmen met doelen, games bedrijf is kunnen tooquickly verzamelen gebruikspatronen en Hallo effectiviteit van marketingcampagnes analyseren.

