---
title: aaaUse een lokale SQL Server in Azure Machine Learning | Microsoft Docs
description: Gegevens uit een lokale SQL Server-database tooperform advanced analytics gebruiken met Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 08e4610d-02b6-4071-aad7-a2340ad8e2ea
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: garye;krishnan
ms.openlocfilehash: c0e9908e296b97b31611ef0192744a59073acd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-analytics-with-azure-machine-learning-using-data-from-an-on-premises-sql-server-database"></a>Geavanceerde analyses uitvoeren met Azure Machine Learning met gegevens van een on-premises SQL Server-database

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

Vaak ondernemingen die met on-premises gegevens werken wilt tootake profiteren van Hallo schaal en flexibiliteit van Hallo cloud voor hun machine learning-werkbelastingen. Maar ze niet toodisrupt willen hun huidige bedrijfsprocessen en werkstromen door hun lokale gegevens toohello cloud te verplaatsen. Azure Machine Learning ondersteunt nu uw gegevens leest uit een on-premises SQL Server database en vervolgens training en score berekenen voor een model met deze gegevens. U hoeft niet langer toomanually kopiëren en sync Hallo gegevens tussen Hallo cloud en uw lokale server. In plaats daarvan Hallo **importgegevens** module in Azure Machine Learning Studio nu rechtstreeks vanuit uw lokale SQL Server-database voor uw training en score berekenen voor taken kan lezen.

Dit artikel bevat een overzicht van hoe tooingress lokale SQL server-gegevens in Azure Machine Learning. Er wordt vanuit gegaan dat u bekend met Azure Machine Learning-concepten zoals werkruimten, modules, gegevenssets, experimenten bent, *enzovoort*.

> [!NOTE]
> Deze functie is niet beschikbaar voor gratis werkruimten. Zie voor meer informatie over Machine Learning-prijzen en lagen [Azure Machine Learning-prijzen](https://azure.microsoft.com/pricing/details/machine-learning/).
>
>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="install-hello-microsoft-data-management-gateway"></a>Hallo Microsoft Data Management Gateway installeren
een lokale SQL Server-database in Azure Machine Learning tooaccess, moet u toodownload en installatie Hallo Microsoft Data Management Gateway. Wanneer u Hallo gatewayverbinding in Machine Learning Studio configureren, hebt u de mogelijkheid Hallo downloaden en installeren van Hallo-gateway met behulp van Hallo **downloaden en registreren gegevensgateway** dialoogvenster die hieronder worden beschreven.

U kunt Hallo Data Management Gateway tevoren ook installeren met het downloaden en uitvoeren van de MSI-installatiepakket Hallo van Hallo [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).
Meest recente versie hello, 32-bits of 64-bits geschikt is voor uw computer selecteren die u kiest. Hallo MSI kan ook worden gebruikt tooupgrade een bestaande Data Management Gateway toohello meest recente versie, met alle instellingen behouden.

Hallo gateway heeft Hallo volgende vereisten:

* Hallo ondersteund Windows-besturingssysteemversies zijn Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012 en Windows Server 2012 R2.
* Hallo aanbevolen configuratie voor de gatewaycomputer Hallo is ten minste 2 GHz, 4 kernen, 8GB RAM-geheugen en schijfruimte 80GB.
* Als de hostmachine Hallo in de slaapstand, won't Hallo gateway toodata aanvragen reageren. Een juiste energiebeheerschema op Hallo computer daarom configureren voordat u Hallo-gateway installeert. Als Hallo machine geconfigureerde toohibernate, weergegeven Hallo gateway-installatie een bericht.
* Omdat kopieeractiviteit op een specifieke frequentie plaatsvindt, volgt Hallo van Resourcegebruik (CPU, geheugen) op Hallo-machine ook Hallo hetzelfde patroon met piek- en niet-actieve tijd. Resourcegebruik ook afhankelijk van geheugenlatentie hello en de hoeveelheid gegevens worden verplaatst. Wanneer meerdere kopie taken uitgevoerd worden, moet u Resourcegebruik tijdens piektijden stijgen zien. Hallo minimale configuratie bovenstaande technisch voldoende is, kunt u een configuratie met meer bronnen dan de minimale configuratie Hallo toohave, afhankelijk van uw specifieke load voor gegevensverplaatsing.

Houd rekening met de volgende Hallo bij het instellen en gebruiken van een Data Management Gateway:

* U kunt slechts één exemplaar van Data Management Gateway installeren op een enkele computer.
* U kunt één gateway voor meerdere on-premises-gegevensbronnen.
* U kunt verbinding maken met meerdere gateways op verschillende computers toohello dezelfde on-premises-gegevensbron.
* U configureren een gateway voor slechts één werkruimte tegelijk. Gateways kunnen niet op dit moment worden gedeeld tussen werkruimten.
* U kunt meerdere gateways voor een enkele werkruimte configureren. U kunt toouse een gateway die is verbonden tooyour test gegevensbronnen tijdens de ontwikkeling en productie-gateway, bijvoorbeeld wanneer u klaar toooperationalize bent.
* Hallo gateway heeft geen toobe op dezelfde computer als de gegevensbron Hallo Hallo nodig. Maar dichter toohello bijwerkt gegevensbron minder tijd Hallo voor Hallo gateway tooconnect toohello-gegevensbron. Het is raadzaam dat u Hallo-gateway op een machine die verschilt van Hallo een hosts Hallo lokale gegevensbron installeert zodat geen hello gateway en de gegevensbron concurreren voor bronnen.
* Als u al een gateway is geïnstalleerd op uw computer voor de Power BI of Azure Data Factory-scenario's, een aparte gateway voor Azure Machine Learning op een andere computer installeren.

  > [!NOTE]
  > Data Management Gateway en de Gateway van Power BI kan niet worden uitgevoerd op Hallo dezelfde computer.
  >
  >
* U moet toouse Hallo Data Management Gateway voor Azure Machine Learning, zelfs als u Azure ExpressRoute voor andere gegevens gebruikt. U moet uw gegevensbron behandelen als een lokale gegevensbron (die zich achter een firewall) zelfs wanneer u ExpressRoute gebruikt. Gebruik Hallo Data Management Gateway tooestablish connectiviteit tussen Machine Learning en Hallo-gegevensbron.

U vindt gedetailleerde informatie over vereisten voor de installatie, installatiestappen en tips voor probleemoplossing in Hallo artikel [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md).

## <a name="span-idusing-the-data-gateway-step-by-step-walk-classanchorspan-idtoc450838866-classanchorspanspaningress-data-from-your-on-premises-sql-server-database-into-azure-machine-learning"></a><span id="using-the-data-gateway-step-by-step-walk" class="anchor"><span id="_Toc450838866" class="anchor"></span></span>Inkomende gegevens van uw lokale SQL Server-database in Azure Machine Learning
In dit scenario maakt u een Data Management Gateway instellen in een Azure Machine Learning-werkruimte, configureert, en vervolgens gegevens lezen uit een on-premises SQL Server database.

> [!TIP]
> Voordat u begint, uitschakelen van de browser pop-upblokkering voor `studio.azureml.net`. Als u Hallo Google Chrome-browser gebruikt, downloadt en installeert een Hallo enkele invoegtoepassingen beschikbaar zijn op Google Chrome webarchief [Klik eenmaal Appuitbreiding](https://chrome.google.com/webstore/search/clickonce?_category=extensions).
>
>

### <a name="step-1-create-a-gateway"></a>Stap 1: Een gateway maken
de eerste stap Hallo is toocreate en Hallo gateway tooaccess instellen met de lokale SQL-database.

1. Meld u bij te[Azure Machine Learning Studio](https://studio.azureml.net/Home/) en selecteer Hallo-werkruimte die u wilt toowork in.
2. Klik op Hallo **instellingen** blade op Hallo links en klik vervolgens op Hallo **GEGEVENSGATEWAYS** Hallo boven op tabblad.
3. Klik op **nieuwe GEGEVENSGATEWAY** Hallo onder welkomstscherm aan.

    ![Nieuwe gegevensgateway](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-button.png)
4. In Hallo **nieuwe gegevensgateway** dialoogvenster Voer Hallo **gatewaynaam** en voeg desgewenst een **beschrijving**. Klik op de pijl Hallo op Hallo onder rechterhoek toogo toohello volgende configuratiestap Hallo.

    ![Gatewaynaam en beschrijving invoeren](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-dialog-enter-name.png)
5. In Hallo downloaden en gegevens gateway dialoogvenster kopiëren Hallo GATEWAY REGISTRATIESLEUTEL toohello Klembord registreren.

    ![Download gegevensgateway en registreren](media/machine-learning-use-data-from-an-on-premises-sql-server/download-and-register-data-gateway.png)
6. <span id="note-1" class="anchor"></span>Als u nog niet hebt gedownload en geïnstalleerd Hallo Microsoft Data Management Gateway en klik vervolgens op **downloaden data management gateway**. Dit vergt toothe Microsoft Download Center waar u de versie van de gegevensgateway Hallo kunt selecteren u nodig hebt, downloaden en installeren. U vindt gedetailleerde informatie over vereisten voor de installatie, installatiestappen en tips voor probleemoplossing in Hallo begin secties van Hallo artikel [gegevens verplaatsen tussen lokale bronnen en cloud met Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).
7. Nadat het Hallo-gateway is geïnstalleerd, Hallo Data Management Gateway Configuration Manager openen en Hallo **gateway registreren** dialoogvenster wordt weergegeven. Plakken Hallo **Gateway registratiesleutel** dat u hebt gekopieerd toohello Klembord en klik op **registreren**.
8. Als u al een gateway is geïnstalleerd, voert u Hallo Data Management Gateway Configuration Manager. Klik op **code wijzigen**, plak de **Gateway registratiesleutel** u toohello Klembord hebt gekopieerd in de vorige stap Hallo en klik op **OK**.
9. Wanneer het Hallo-installatie is voltooid, Hallo **gateway registreren** voor Microsoft Data Management Gateway Configuration Manager-dialoogvenster wordt weergegeven. Plak Hallo GATEWAY REGISTRATIESLEUTEL die u naar Hallo Klembord in de vorige stap hebt gekopieerd en klik op **registreren**.

    ![Gateway registreren](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-register-gateway.png)
10. Hallo gateway-configuratie is voltooid als Hallo volgende waarden zijn ingesteld op Hallo **Start** tabblad in Microsoft Data Management Gateway Configuration Manager:

    * **De gatewaynaam van de** en **exemplaarnaam** toohello de naam van Hallo gateway worden ingesteld.
    * **Registratie** te is ingesteld,**geregistreerde**.
    * **Status** te is ingesteld,**gestart**.
    * Hallo statusbalk Hallo onder geeft **tooData Management Gateway Cloud Service verbonden** samen met een groen vinkje.

      ![Data Management Gateway Manager](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-registered.png)

      Azure Machine Learning Studio wordt ook bijgewerkt wanneer Hallo-registratie geslaagd is.

    ![De registratie van de gateway is geslaagd](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-registered.png)
11. In Hallo **downloaden en registreren gegevensgateway** dialoogvenster, klikt u op het vinkje toocomplete Hallo-instelling. Hallo **instellingen** pagina wordt weergegeven als 'Online' de status van de gateway. In het rechterdeelvenster hello vindt u de status en andere nuttige informatie.

    ![Gateway-instellingen](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-status.png)
12. In Microsoft Data Management Gateway Configuration Manager Hallo overschakelen toohello **certificaat** tabblad Hallo certificaat is opgegeven op dit tabblad is gebruikte tooencrypt/ontsleutelen referenties voor Hallo on-premises gegevensopslag die u opgeeft in het Hallo-portal. Dit certificaat is een standaardcertificaat Hallo. Microsoft raadt u aan deze tooyour eigen certificaat dat u in uw certificaat beheersysteem back-ups wijzigen. Klik op **wijziging** toouse uw eigen certificaat in plaats daarvan.

    ![Het gatewaycertificaat wijzigen](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-certificate.png)
13. (optioneel) Desgewenst kunt u uitgebreide logboekregistratie van tooenable om het oplossen van problemen met het Hallo-gateway in Hallo Microsoft Data Management Gateway Configuration Manager overschakelen toothe **Diagnostics** tabblad en controleer Hallo **inschakelen uitgebreide logboekregistratie voor het oplossen van problemen** optie. Hallo logboekinformatie vindt u in Logboeken van Windows hello onder Hallo **logboeken toepassingen en Services**  - &gt; **Data Management Gateway** knooppunt. U kunt ook Hallo **Diagnostics** tabblad tootest Hallo verbinding tooan lokale gegevensbron met behulp van Hallo-gateway.

    ![Uitgebreide logboekregistratie inschakelen](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-verbose-logging.png)

Dit is het gateway-installatieprocedure Hallo in Azure Machine Learning voltooid.
U bent nu klaar toouse uw on-premises gegevens.

U kunt maken en instellen van meerdere gateways in Studio voor elke werkruimte. Bijvoorbeeld, kan er een gateway wilt u tooconnect tooyour test gegevensbronnen tijdens het ontwikkelen en een andere gateway voor uw productie-gegevensbronnen. Azure Machine Learning biedt u de flexibiliteit tooset van meerdere gateways, afhankelijk van uw zakelijke omgeving. Momenteel kunt u een gateway tussen werkruimten niet delen en kan slechts één gateway worden geïnstalleerd op een enkele computer. Zie voor meer informatie [gegevens verplaatsen tussen lokale bronnen en cloud met Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).

### <a name="step-2-use-hello-gateway-tooread-data-from-an-on-premises-data-source"></a>Stap 2: Hallo gateway tooread gegevens uit een on-premises gegevensbron gebruiken
Nadat u een gateway Hallo ingesteld, kunt u toevoegen een **importgegevens** module die u wilt een experiment die invoer Hallo gegevens van Hallo lokale SQL Server-database.

1. Selecteer in Machine Learning Studio Hallo **EXPERIMENTEN** en klik op **+ nieuw** in linkerbenedenhoek Hallo en selecteer **leeg Experiment** (of Selecteer een van de verschillende voorbeeld experimenten beschikbaar).
2. Zoek en sleep Hallo **importgegevens** module toohello experimenteren canvas.
3. Klik op **opslaan als** hieronder Hallo canvas. 'Azure Machine Learning On-Premises SQL Server-zelfstudie' Hallo experiment naam invoeren, selecteert u de werkruimte en klikt u op Hallo **OK** selectievakje is ingeschakeld.

   ![Experiment met een nieuwe naam opslaan](media/machine-learning-use-data-from-an-on-premises-sql-server/experiment-save-as.png)
4. Klik op Hallo **gegevens importeren** module tooselect, klik dan in de **eigenschappen** deelvenster toohello rechts van het canvas hello, selecteert u 'On-Premises SQL-Database' in hello **gegevensbron** vervolgkeuzelijst.
5. Selecteer Hallo **gegevensgateway** u geïnstalleerd en geregistreerd. U kunt een andere gateway instellen door te selecteren '(toevoegen van nieuwe gegevensgateway...)'.

   ![Selecteer de gegevensgateway voor gegevens importeren-module](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-select-on-premises-data-source.png)
6. Voer Hallo SQL **databaseservernaam** en **databasenaam**, samen met de Hallo SQL **databasequery** gewenste tooexecute.
7. Klik op **Voer waarden in** onder **gebruikersnaam en wachtwoord** en voer uw databasereferenties. U kunt Windows-verificatie of SQL Server-verificatie, al naar gelang hoe uw lokale SQL Server is geconfigureerd.

   ![Geef databasereferenties op](media/machine-learning-use-data-from-an-on-premises-sql-server/database-credentials.png)

   Hallo-bericht 'waarden voor vereiste' wijzigingen te 'waarden set' met een groen vinkje. U hoeft alleen tooenter Hallo referenties eenmaal tenzij Hallo databasegegevens of het wachtwoord wijzigt. U hebt opgegeven toen u tooencrypt Hallo-Hallo gatewayreferenties geïnstalleerd in de cloud Hallo Hallo-certificaat maakt gebruik van Azure Machine Learning. On-premises referenties zonder versleuteling nooit worden opgeslagen in Azure.

   ![Eigenschappen van de module gegevens importeren](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-properties-entered.png)
8. Klik op **uitvoeren** toorun Hallo experiment.

Zodra het Hallo-experiment is voltooid, kunt u visualiseren Hallo-gegevens die u hebt geïmporteerd uit de database Hallo door te klikken op de uitvoerpoort Hallo Hallo **importgegevens** module en het selecteren van **Visualize**.

Wanneer u klaar bent met het ontwikkelen van uw experiment, kunt u deze kunt implementeren en uw model operationeel. Met behulp van Batch-Service voor uitvoering, gegevens van Hallo lokale SQL Server-database geconfigureerd in Hallo Hallo **importgegevens** module worden gelezen en gebruikt voor score berekenen. U kunt Hallo Request Response-Service gebruiken voor score berekenen voor on-premises gegevens, wordt aangeraden met behulp van de [Excel-invoegtoepassing](machine-learning-excel-add-in-for-web-services.md) in plaats daarvan. Op dit moment schrijven tooan lokale SQL Server-database via **gegevens exporteren** wordt niet ondersteund in uw experimenten of gepubliceerde web-services.
