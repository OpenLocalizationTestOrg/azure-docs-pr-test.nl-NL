---
title: beschikbaarheid van aaaHigh met data management gateway in Azure Data Factory | Microsoft Docs
description: Dit artikel wordt uitgelegd hoe u uit een data management gateway kunt schalen door het toevoegen van meer knooppunten en schaal omhoog door het aantal gelijktijdige taken die kunnen worden uitgevoerd op een knooppunt te verhogen.
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: abnarain
ms.openlocfilehash: 925f63728e23596bca2655636f6535b509fce0b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway---high-availability-and-scalability-preview"></a>Data Management Gateway - hoge beschikbaarheid en schaalbaarheid (Preview)
In dit artikel kunt u hoge beschikbaarheid en schaalbaarheid oplossing configureren met Data Management Gateway.    

> [!NOTE]
> In dit artikel wordt ervan uitgegaan dat u al bekend met de basisprincipes van Data Management Gateway bent. Als u niet het geval is, Zie [Data Management Gateway](data-factory-data-management-gateway.md).

>**Deze preview-functie wordt officieel ondersteund op Data Management Gateway versie 2.12.xxxx.x en hoger**. Zorg ervoor dat u versie 2.12.xxxx.x of hoger. Download de nieuwste versie Hallo van Data Management Gateway [hier](https://www.microsoft.com/download/details.aspx?id=39717).

## <a name="overview"></a>Overzicht
U kunt gegevens management gateways die zijn geïnstalleerd op meerdere lokale computers met een enkele logische gateway vanuit de portal Hallo koppelen. Deze machines heten **knooppunten**. U kunt te hebben van**vier knooppunten** die zijn gekoppeld aan een logische gateway. Hallo voordelen van meerdere knooppunten (op lokale computers met de gateway is geïnstalleerd) voor een logische gateway zijn:  

- Prestaties van de verplaatsing van gegevens tussen on-premises en cloud gegevensarchieven.  
- Als een van de knooppunten hello uitgeschakeld voor een bepaalde reden wordt, nog andere knooppunten steeds beschikbaar voor het Hallo-gegevens te verplaatsen. 
- Als een van de knooppunten Hallo toobe offline gehaald voor onderhoud moet, nog andere knooppunten steeds beschikbaar voor het Hallo-gegevens te verplaatsen.

U kunt ook configureren Hallo aantal **gelijktijdige data movement taken** die kunnen worden uitgevoerd op een knooppunt tooscale up Hallo mogelijkheid om gegevens te verplaatsen tussen on-premises en cloud gegevensarchieven. 

Hello Azure-portal gebruikt, u kunt Hallo status bewaken van deze knooppunten die u kunt bepalen of tooadd of een knooppunt verwijderen uit Hallo logische gateway. 

## <a name="architecture"></a>Architectuur 
Hallo biedt volgende diagram Hallo overzicht van de architectuur van de schaalbaarheid en beschikbaarheidsfunctie Hallo Data Management Gateway: 

![Data Management Gateway - hoge beschikbaarheid en schaalbaarheid](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-high-availability-and-scalability.png)

Een **logische gateway** Hallo gateway u tooa gegevensfactory toevoegen in hello Azure-portal. Eerder, kan u slechts één lokale Windows-machine met Data Management Gateway is geïnstalleerd met een logische gateway koppelen. Dit lokale gateway-apparaat wordt een knooppunt genoemd. Nu u kunt koppelen te**vier fysieke knooppunten** met een logische gateway. Een logische gateway met meerdere knooppunten heet een **met meerdere knooppunten gateway**.  

Alle deze knooppunten zijn **active**. Alle data movement taken toomove gegevens tussen on-premises en cloud kunnen verwerken gegevensarchieven. Een van de knooppunten Hallo fungeren als de dispatcher- en werkrollen. Andere knooppunten in het Hallo-groepen zijn worker-knooppunten. Een **dispatcher** knooppunt gegevens gegevensverplaatsing taken/taken van de cloudservice Hallo ophaalt en verzendt ze tooworker knooppunten (inclusief zelf). Een **worker** knooppunt wordt uitgevoerd gegevens gegevensverplaatsing taken toomove gegevens tussen on-premises en cloud gegevensarchieven. Alle knooppunten zijn werknemers. Slechts één knooppunt kan worden dispatch- en werkrollen.    

Kan u doorgaans begint met één knooppunt en **uitschalen** tooadd meer knooppunten zoals Hallo bestaande knooppunten met laden van de verplaatsing Hallo gegevens worden overbelast. U kunt ook **opschalen** Hallo data movement mogelijkheid van een gateway-knooppunt door het aantal gelijktijdige taken die toorun zijn toegestaan op Hallo knooppunt hello te verhogen. Deze mogelijkheid is ook beschikbaar met één knooppunt gateway (zelfs wanneer de functie schaalbaarheid en beschikbaarheid Hallo niet is ingeschakeld). 

Een gateway met meerdere knooppunten houdt referenties voor gegevensopslag Hallo synchroon op alle knooppunten. Als er een knooppunt naar verbindingsprobleem is, is het mogelijk dat Hallo referenties niet gesynchroniseerd. Bij het instellen van referenties voor een lokale gegevensarchief die gebruikmaakt van een gateway wordt referenties opgeslagen op Hallo dispatcher/werkrolknooppunt. Hallo dispatcher knooppunt wordt gesynchroniseerd met andere worker-knooppunten. Dit proces wordt ook wel **sync referenties**. Hallo communicatiekanaal tussen knooppunten kan worden **versleutelde** door een openbare SSL/TLS-certificaat. 

## <a name="set-up-a-multi-node-gateway"></a>Instellen van een gateway met meerdere knooppunten
Deze sectie wordt ervan uitgegaan dat u na twee artikelen of bekend bent met concepten in deze artikelen Hallo hebben doorlopen: 

- [Data Management Gateway](data-factory-data-management-gateway.md) -bevat een gedetailleerd overzicht van Hallo-gateway.
- [Gegevens verplaatsen tussen on-premises en cloud gegevensarchieven](data-factory-move-data-between-onprem-and-cloud.md) -bevat een overzicht met stapsgewijze instructies voor het gebruik van een gateway met één knooppunt.  

> [!NOTE]
> Raadpleeg voordat u een data management gateway op een lokale Windows-machine installeert, vereisten die worden vermeld [Hallo belangrijkste artikel](data-factory-data-management-gateway.md#prerequisites).

1. In Hallo [scenario](data-factory-move-data-between-onprem-and-cloud.md#create-gateway), tijdens het maken van een logische gateway inschakelen Hallo **hoge beschikbaarheid en schaalbaarheid** functie. 

    ![Data Management Gateway - enable hoge beschikbaarheid en schaalbaarheid](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-enable-high-availability-scalability.png)
2. In Hallo **configureren** pagina, gebruikt u een **snelle installatie** of **handmatige installatie** tooinstall een gateway op Hallo eerste knooppunt (een lokale Windows-machine) koppelen.

    ![Data Management Gateway - expliciete of handmatige installatie](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-express-manual-setup.png)

    > [!NOTE]
    > Als u Hallo snelle installatie-optie gebruikt, de Hallo knooppunt naar communicatie wordt uitgevoerd zonder versleuteling. Hallo knooppuntnaam is hetzelfde als het Hallo-computernaam. Handmatige installatie gebruiken als Hallo knooppunten communicatie toobe versleuteld moet of het gewenste toospecify de naam van een knooppunt van uw keuze. Knooppuntnamen kunnen niet later worden bewerkt.
3. Als u ervoor kiest **snelle installatie**
    1. U ziet Hallo-bericht te volgen nadat Hallo gateway is geïnstalleerd:

        ![Data Management Gateway - snelle installatie geslaagd](media/data-factory-data-management-gateway-high-availability-scalability/express-setup-success.png)
    2. Data Management Configuration Manager voor de gateway Hallo starten door [deze instructies](data-factory-data-management-gateway.md#configuration-manager). Ziet u de naam van de gateway hello, knooppuntnaam, status, enzovoort.

        ![Data Management Gateway - installatie is geslaagd](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-installation-success.png)
4. Als u ervoor kiest **handmatige installatie**:
    1. Hallo-installatiepakket downloaden vanaf Microsoft Download Center hello, tooinstall gateway uitvoeren op uw machine.
    2. Gebruik Hallo **verificatiesleutel** van Hallo **configureren** pagina tooregister Hallo gateway.
    
        ![Data Management Gateway - installatie is geslaagd](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-authentication-key.png)
    3. In Hallo **nieuwe gateway-knooppunt** pagina kunt u een aangepaste bieden **naam** toohello gateway-knooppunt. Naam van het knooppunt is standaard hetzelfde als Hallo-computernaam.    

        ![Data Management Gateway - naam opgeven](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-name.png)
    4. In de volgende pagina hello, kunt u kiezen of te**Schakel versleuteling voor communicatie van knooppunt naar**. Klik op **overslaan** toodisable-versleuteling (standaard).

        ![Data Management Gateway - codering inschakelen](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-node-encryption.png)  
    
        > [!NOTE]
        > Wijzigen van de versleuteling wordt alleen ondersteund als er een enkele gateway-knooppunt in Hallo logische gateway. toochange hello versleuteling modus wanneer een gateway heeft meerdere knooppunten Hallo volgende stappen: verwijderen van alle Hallo knooppunten behalve één knooppunt, Hallo versleuteling modus wijzigen en voeg Hallo knooppunten vervolgens opnieuw.
        > 
        > Zie [vereisten voor TLS/SSL-certificaten](#tlsssl-certificate-requirements) sectie voor een lijst met vereisten voor het gebruik van een TLS/SSL-certificaat. 
    5. Nadat het Hallo-gateway is geïnstalleerd, klikt u op Start Configuration Manager:
    
        ![Handmatige installatie - launch configuration manager](media/data-factory-data-management-gateway-high-availability-scalability/manual-setup-launch-configuration-manager.png)   
    6. u ziet Data Management Gateway Configuration Manager op Hallo-knooppunt (lokale Windows-computer) waarin verbindingsstatus **gatewaynaam**, en **knooppuntnaam**.  

        ![Data Management Gateway - installatie is geslaagd](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-installation-success.png)

        > [!NOTE]
        > Als u Hallo-gateway op een Azure VM inricht, kunt u [deze Azure Resource Manager-sjabloon op GitHub](https://github.com/xiaoyingLJ/vms-with-multiple-data-management-gateway). Dit script maakt een logische gateway, stelt u de virtuele machines met Data Management Gateway-software is geïnstalleerd en registreert deze bij Hallo logische gateway. 
6. Start in Azure-portal Hallo **Gateway** pagina: 
    1. Klik op Hallo data factory startpagina in Hallo-portal op **gekoppelde Services**.
    
        ![Startpagina van de gegevensfactory](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-home-page.png)
    2. Selecteer Hallo **gateway** toosee hello **Gateway** pagina:
    
        ![Startpagina van de gegevensfactory](media/data-factory-data-management-gateway-high-availability-scalability/linked-services-gateway.png)
    4. U ziet Hallo **Gateway** pagina:   

        ![Gateway met één knooppunt weergeven](media/data-factory-data-management-gateway-high-availability-scalability/gateway-first-node-portal-view.png) 
7. Klik op **knooppunt toevoegen** op Hallo werkbalk tooadd een knooppunt toohello logische gateway. Als u van plan bent de snelle installatie toouse, doet u deze stap uit Hallo lokale machine die wordt toegevoegd als een knooppunt toohello gateway. 

    ![Data Management Gateway - knooppunt menu toevoegen](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-add-node-menu.png)
8. Stappen zijn vergelijkbaar toosetting eerste Hallo-knooppunt. Hallo UI Configuration Manager kunt u Hallo knooppuntnaam instellen als u Hallo handmatige installatie-optie kiest: 

    ![Configuration Manager - tweede gateway installeren](media/data-factory-data-management-gateway-high-availability-scalability/install-second-gateway.png)
9. Nadat Hallo gateway is geïnstalleerd op Hallo-knooppunt, weergegeven Hallo Configuration Manager Hallo scherm te volgen:  

    ![Configuration Manager - installatie tweede gateway geslaagd](media/data-factory-data-management-gateway-high-availability-scalability/second-gateway-installation-successful.png)
10. Als u Hallo openen **Gateway** pagina in de portal hello, ziet u twee knooppunten van de gateway nu: 

    ![Gateway met twee knooppunten in het Hallo-portal](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring.png)
11. toodelete een gateway-knooppunt, klik op **knooppunt verwijderen** Selecteer Hallo knooppunt u toodelete wilt en klik vervolgens op op Hallo werkbalk **verwijderen** Hallo werkbalk van. Deze actie worden Hallo geselecteerde knooppunt verwijderd uit groep Hallo. Houd er rekening mee dat deze actie niet Hallo data management gateway-software van het Hallo-knooppunt (lokale Windows-machine verwijderen). Gebruik **software** in het Configuratiescherm op Hallo lokale toouninstall Hallo gateway. Wanneer u gateway van het Hallo-knooppunt verwijdert, wordt deze automatisch verwijderd in Hallo-portal.   

## <a name="upgrade-an-existing-gateway"></a>Upgrade van een bestaande gateway
U kunt een bestaande gateway toouse Hallo hoge beschikbaarheid en schaalbaarheid functie upgraden. Deze functie werkt alleen met knooppunten die Hallo data management gateway versie hebben > = 2.12.xxxx. U ziet Hallo-versie van data management gateway is geïnstalleerd op een computer in Hallo **Help** tabblad Hallo Data Management Gateway Configuration Manager. 

1. Update Hallo gateway op Hallo on-premises machine toohello meest recente versie door volgen door te downloaden en uitvoeren van een MSI-installatiepakket vanaf Hallo [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717). Zie [installatie](data-factory-data-management-gateway.md#installation) sectie voor meer informatie.  
2. Navigeer toohello Azure-portal. Hallo starten **Data Factory pagina** van uw gegevensfactory. Klik op de gekoppelde services tegel toolaunch hello **gekoppelde servicepagina**. Selecteer Hallo gateway toolaunch hello **pagina gateway**. Klik op en schakel **Preview-functie** zoals weergegeven in Hallo installatiekopie te volgen: 

    ![Data Management Gateway - preview-functie inschakelen](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-existing-gateway-enable-high-availability.png)   
2. Zodra Hallo preview-functie is ingeschakeld in de portal hello, sluit u alle pagina's. Open Hallo **pagina gateway** toosee Hallo nieuwe preview gebruikersinterface (UI).
 
    ![Data Management Gateway - enable preview-functie geslaagd](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-preview-success.png)

    ![Data Management Gateway - preview-gebruikersinterface](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-preview.png)

    > [!NOTE]
    > Tijdens de upgrade Hallo is de naam van het eerste knooppunt Hallo Hallo-naam van Hallo machine. 
3. Voeg nu een knooppunt. In Hallo **Gateway** pagina, klikt u op **knooppunt toevoegen**.  

    ![Data Management Gateway - knooppunt menu toevoegen](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-add-node-menu.png)

    Volg de instructies van het vorige gedeelte tooset Hallo Hallo-knooppunt. 

### <a name="installation-best-practices"></a>Best practices voor installatie

- Energiebeheerschema op de hostmachine Hallo voor Hallo gateway zodanig configureren dat hello machine niet in slaapstand. Als de hostmachine Hallo in de slaapstand, reageert Hallo gateway toodata aanvragen niet.
- Back-up Hallo-certificaat dat is gekoppeld met Hallo-gateway.
- Zorg ervoor dat alle knooppunten van vergelijkbare configuratie (aanbevolen) voor ideaal prestaties zijn. 
- Voeg ten minste twee knooppunten tooensure hoge beschikbaarheid.  

### <a name="tlsssl-certificate-requirements"></a>Vereisten voor TLS/SSL-certificaten
Hier volgen Hallo-vereisten voor Hallo TLS/SSL-certificaat dat wordt gebruikt voor het beveiligen van communicatie tussen de gateway-knooppunten:

- Hallo-certificaat moet een openbaar vertrouwde X509 v3-certificaat.
- Alle knooppunten van de gateway, moeten dit certificaat vertrouwen. 
- Het is raadzaam om gebruik te maken van certificaten die zijn uitgegeven door een openbare (derde) certificeringsinstantie (CA).
- Ondersteunt sleutelgrootte voor SSL-certificaten wordt ondersteund door Windows Server 2012 R2.
- Ondersteunt geen certificaten met CNG-sleutels.
- Jokertekens certificaten worden ondersteund. 


## <a name="monitor-a-multi-node-gateway"></a>Monitor voor een gateway met meerdere knooppunten
### <a name="multi-node-gateway-monitoring"></a>Bewaking van de gateway met meerdere knooppunten
In hello Azure-portal, kunt u vrijwel in realtime momentopname van Resourcegebruik (CPU, geheugen, network(in/out), enz.) op elk knooppunt samen met de status van gateway-knooppunten te bekijken. 

![Data Management Gateway - bewaking van meerdere knooppunten](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring.png)

U kunt inschakelen **geavanceerde instellingen** in Hallo **Gateway** toosee metrische gegevens zoals geavanceerde pagina **netwerk**(in/uit), **rol & referentie Status**, die u kan helpen bij foutopsporing gateway-problemen en **gelijktijdige taken** (actief / beperken) die kan worden gewijzigd / gewijzigde dienovereenkomstig tijdens prestaties afstemmen. Hallo volgende tabel bevat beschrijvingen van kolommen in Hallo **Gateway-knooppunten** lijst:  

Bewaking van eigenschap | Beschrijving
:------------------ | :---------- 
Naam | Naam van logische gateway Hallo en knooppunten die zijn gekoppeld aan het Hallo-gateway.  
Status | Status van de logische Hallo-gateway en Hallo gateway-knooppunten. Voorbeeld: Online/Offline/Limited/enz. Zie voor meer informatie over deze statussen [gatewaystatus](#gateway-status) sectie. 
Versie | Toont Hallo-versie van de logische gateway Hallo en elk gateway-knooppunt. Hallo-versie van de logische gateway hello wordt bepaald op basis van de versie van het merendeel van de knooppunten in het Hallo-groep. Als er knooppunten met verschillende versies in Hallo logische gateway setup, Hallo alleen Hallo knooppunten met hetzelfde versienummer als Hallo logische gateway functie goed. Anderen in de beperkte modus Hallo en moeten handmatig worden bijgewerkt (alleen als automatische updates is mislukt) toobe. 
Beschikbaar geheugen | Beschikbaar geheugen op een gateway-knooppunt. Deze waarde is een momentopname van een bijna realtime. 
CPU-gebruik | CPU-gebruik van een gateway-knooppunt. Deze waarde is een momentopname van een bijna realtime. 
Networking (In/Out) | Netwerkgebruik van een gateway-knooppunt. Deze waarde is een momentopname van een bijna realtime. 
Gelijktijdige taken (actief / beperken) | Het aantal taken of taken die op elk knooppunt worden uitgevoerd. Deze waarde is een momentopname van een bijna realtime. Limiet geeft Hallo maximum aantal gelijktijdige taken voor elk knooppunt. Deze waarde is gedefinieerd op basis van de grootte van de machine Hallo. U kunt verhogen Hallo limiet tooscale up gelijktijdige taakuitvoering in geavanceerde scenario's waar CPU / geheugen / netwerk is onder gebruikt, maar de activiteiten worden een time-out opgetreden. Deze mogelijkheid is ook beschikbaar met één knooppunt gateway (zelfs wanneer de functie schaalbaarheid en beschikbaarheid Hallo niet is ingeschakeld). Zie voor meer informatie [schalen overwegingen](#scale-considerations) sectie. 
Rol | Er zijn twee typen rollen – Dispatcher- en werkrollen. Alle knooppunten zijn werknemers, wat betekent dat ze kunnen worden gebruikt tooexecute taken. Er is slechts één dispatcher knooppunt, die wordt gebruikt toopull taken/taken van cloudservices en verzenden ze toodifferent worker-knooppunten (inclusief zelf). 

![Data Management Gateway - geavanceerde bewaking van meerdere knooppunten](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring-advanced.png)

### <a name="gateway-status"></a>Status van gateway

Hallo volgende tabel bevat mogelijke statussen van een **gateway-knooppunt**: 

Status  | Opmerkingen/scenario 's
:------- | :------------------
Online | Knooppunt verbonden tooData Factory-service.
Off line | Knooppunt is offline.
Een upgrade | Hallo-knooppunt wordt automatisch bijgewerkt.
Beperkt | Vervaldatum tooConnectivity probleem. Kan zijn vanwege tooHTTP poort 8050 probleem, service bus-verbindingsprobleem of synchronisatieprobleem in de referentie. 
Inactieve | Er is een knooppunt in een configuratie uit Hallo configuratie van andere knooppunten van de meeste andere.<br/><br/> Een knooppunt mag inactief zijn wanneer er geen verbinding tooother knooppunten maken. 


Hallo volgende tabel bevat mogelijke statussen van een **logische gateway**. Hallo gateway de status is afhankelijk van de statussen van Hallo gateway-knooppunten. 

Status | Opmerkingen
:----- | :-------
Moet worden geregistreerd | Er is geen knooppunt is nog geregistreerde toothis logische gateway
Online | Gateway-knooppunten zijn online.
Off line | Er is geen knooppunt online status.
Beperkt | Niet alle knooppunten in deze gateway zijn in orde. Deze status is een waarschuwing dat een bepaald knooppunt niet beschikbaar. <br/><br/>Mogelijke oorzaken zijn toocredential synchronisatieprobleem op dispatcher/werkrolknooppunt. 

### <a name="pipeline-activities-monitoring"></a>Pijplijn / activiteiten bewaken
Hello Azure-portal biedt een pijplijn implementatiebewakingservaring met gedetailleerde knooppunt mate van details. Bijvoorbeeld: er wordt weergegeven welke activiteiten uitgevoerd op welk knooppunt. Deze informatie kan nuttig zijn bij het begrijpen van prestatieproblemen op een bepaald knooppunt, spreek vanwege toonetwork beperking zijn. 

![Data Management Gateway - bewaking voor pijplijnen van meerdere knooppunten](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring-pipelines.png)

![Data Management Gateway - pipeline-details](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-pipeline-details.png)

## <a name="scale-considerations"></a>Overwegingen met betrekking tot schaal

### <a name="scale-out"></a>Uitschalen
Wanneer Hallo **beschikbaar geheugen laag is** en Hallo **CPU-gebruik is hoog**, een nieuw knooppunt toevoegen scale-out Hallo load helpt over machines. Als activiteiten zijn mislukt vanwege tootime-out- of gateway-knooppunt offline, is het handig als u een knooppunt toohello gateway toevoegt.
 
### <a name="scale-up"></a>Omhoog schalen
Wanneer Hallo beschikbaar geheugen en de CPU niet goed worden benut, maar niet-actieve capaciteit Hallo 0 is, moet u de schaal omhoog door het aantal gelijktijdige taken die kunnen worden uitgevoerd op een knooppunt hello te verhogen. U kunt ook tooscale up wanneer activiteiten zijn een time-out opgetreden omdat Hallo gateway overbelast is. Zoals u in Hallo installatiekopie te volgen, kunt u Hallo maximale capaciteit van een knooppunt verhogen. Het is raadzaam verdubbeling van toostart met.  

![Data Management Gateway - scale-overwegingen](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-scale-considerations.png)


## <a name="known-issuesbreaking-changes"></a>Bekende problemen/recente wijzigingen

- U kunt op dit moment hebben up toofour fysieke gateway knooppunten voor één logische gateway. Als u meer dan vier knooppunten nodig hebt voor betere prestaties, stuurt u een e-mailbericht te[DMGHelp@microsoft.com](mailto:DMGHelp@microsoft.com).
- Een gateway-knooppunt kan niet opnieuw registreren met de verificatiesleutel Hallo van een andere logische gateway tooswitch van Hallo huidige logische gateway. toore registratie Hallo gateway verwijderen van het Hallo-knooppunt, Hallo gateway installeren en andere logische gateway registreren met Hallo-verificatiesleutel voor Hallo. 
- Als HTTP-proxy vereist voor alle gateway-knooppunten is, Hallo proxy instellen in diahost.exe.config en diawp.exe.config en Hallo server manager toomake ervoor dat alle knooppunten hebben dezelfde diahost.exe.config en diawip.exe.config hello gebruiken. Zie [proxy-instellingen configureren](data-factory-data-management-gateway.md#configure-proxy-server-settings) sectie voor meer informatie. 
- alle Hallo knooppunten in de portal Hallo behalve een toochange versleuteling modus voor knooppunt naar communicatie in Gateway Configuration Manager verwijderen Vervolgens voegt u knooppunten terug na het wijzigen van Hallo versleuteling modus.
- Gebruik een officiële SSL-certificaat als u ervoor tooencrypt Hallo knooppunt naar communicatiekanaal kiest. Zelf-ondertekend certificaat mogelijk problemen met de netwerkverbinding als Hallo hetzelfde certificaat kan niet worden vertrouwd in certificeren lijst met op andere computers. 
- U kunt een gateway-knooppunt tooa logische gateway niet registreren wanneer Hallo knooppunt versie lager dan de versie van de logische gegevensgateway Hallo is. Verwijderen van alle knooppunten van de logische gateway Hallo uit portal, zodat u kunt een lagere versie node(downgrade) registreren deze. Als u alle knooppunten van een logische gateway verwijdert, handmatig installeren en registreren van nieuwe knooppunten toothat logische gateway. Snelle installatie wordt in dit geval niet ondersteund.
- U kunt de snelle installatie tooinstall knooppunten tooan bestaande logische gateway is nog steeds gebruik van cloud-referenties niet gebruiken. U kunt controleren waarbij Hallo referenties Hallo Gateway Configuration Manager op tabblad Hallo-instellingen zijn opgeslagen.
- U kunt de snelle installatie tooinstall knooppunten tooan bestaande logische gateway knooppunt naar versleuteling ingeschakeld heeft niet gebruiken. Als de instelling Hallo versleuteling modus ook worden certificaten handmatig toe te voegen, is snelle installatie niet meer een optie. 
- Voor het kopiëren van een bestand vanaf on-premises omgeving, moet niet u \\localhost of C:\files meer sinds localhost of een lokaal station mogelijk niet toegankelijk is via alle knooppunten. Gebruik in plaats daarvan \\ServerName\files toospecify bestanden locatie.


## <a name="rolling-back-from-hello-preview"></a>Terugdraaien van Hallo preview 
tooroll terug van Hallo preview, verwijder alle knooppunten maar één knooppunt. Het maakt niet uit welke knooppunten verwijderen, maar zorg ervoor dat er ten minste één knooppunt in Hallo logische gateway. U kunt een knooppunt verwijderen door de gateway op Hallo machine verwijderen of met behulp van hello Azure-portal. In de Azure-portal, op Hallo Hallo **Data Factory** pagina, klikt u op gekoppelde services toolaunch hello **gekoppelde services** pagina. Selecteer Hallo gateway toolaunch hello **Gateway** pagina. Pagina van de Gateway hello ziet u Hallo knooppunten die zijn gekoppeld aan het Hallo-gateway. Hallo pagina kunt u een knooppunt verwijderen uit het Hallo-gateway.
 
Na het verwijderen, klikt u op **preview-functies** in dezelfde Azure portal-pagina Hallo en Hallo preview-functie uitschakelen. U hebt uw gateway tooone knooppunt GA (algemene beschikbaarheid) gateway opnieuw instellen.


## <a name="next-steps"></a>Volgende stappen
Controleer Hallo artikelen te volgen:
- [Data Management Gateway](data-factory-data-management-gateway.md) -bevat een gedetailleerd overzicht van Hallo-gateway.
- [Gegevens verplaatsen tussen on-premises en cloud gegevensarchieven](data-factory-move-data-between-onprem-and-cloud.md) -bevat een overzicht met stapsgewijze instructies voor het gebruik van een gateway met één knooppunt. 
