---
title: aaaDeploy en Hallo multitenant Wingtip SaaS-toepassing die gebruikmaakt van Azure SQL Database verkennen | Microsoft Docs
description: Implementeer en Hallo Wingtip SaaS multitenant toepassing, die u laat zien SaaS patronen met Azure SQL Database verkennen.
keywords: zelfstudie sql-database
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: sstein
ms.openlocfilehash: 7c528ee19472d3b8c7a285b2f86013945e8f4bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-explore-a-multi-tenant-application-that-uses-azure-sql-database---wingtip-saas"></a>Implementeren en een multitenant-toepassing die gebruikmaakt van Azure SQL Database - Wingtip SaaS verkennen

In deze zelfstudie, implementeren en verkennen Hallo Wingtip SaaS-toepassing. Hallo-toepassing gebruikt een database-per-tenant, patroon van de SaaS-toepassing, tooservice meerdere tenants. Hallo-toepassing is ontworpen tooshowcase functies van Azure SQL Database die inschakelen SaaS-scenario's vereenvoudigen.

Vijf minuten na het klikken op Hallo *tooAzure implementeren* hieronder, hebt u een multitenant SaaS-toepassing met behulp van de SQL-Database, Max en uitgevoerd in de cloud Hallo. Hallo-toepassing wordt geïmplementeerd met drie voorbeeld-tenants, elk met een eigen database, alle geïmplementeerde in een elastische SQL-groep. Hallo-app is geïmplementeerd tooyour Azure-abonnement, zodat u volledige toegang tooexplore en werken met Hallo afzonderlijke toepassingsonderdelen. Hallo source code en management toepassingsscripts zijn beschikbaar in Hallo WingtipSaaS GitHub-opslagplaats.


In deze zelfstudie komen deze onderwerpen aan bod:

> [!div class="checklist"]

> * Hoe toodeploy Hallo Wingtip SaaS-toepassing
> * Waar tooget Hallo broncode van de toepassing en beheerscripts schrijven
> * Over het Hallo-servers, -adresgroepen en -databases die gezamenlijk Hallo-app
> * Hoe tenants worden toegewezen tootheir gegevens Hello *catalogus*
> * Hoe een nieuwe tenant tooprovision
> * Hoe toomonitor tenant-activiteit in het Hallo-app

tooexplore verschillende SaaS ontwerp- en patronen, een [reeks zelfstudies gerelateerde](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials) beschikbaar die bouwen voort op deze initiële implementatie. Tijdens het Hallo-zelfstudies doorlopen, Duik in de opgegeven Hallo scripts en bekijk hoe verschillende SaaS-patronen Hallo worden geïmplementeerd. Doorloop Hallo-scripts in elke zelfstudie toogain een beter begrip hoe tooimplement veel SQL-Database Hallo functies vereenvoudigen SaaS-toepassingen te ontwikkelen.

## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie, zorg ervoor dat Hallo volgende vereisten zijn voltooid:

* Azure PowerShell is geïnstalleerd. Zie [Aan de slag met Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps) voor meer informatie.

## <a name="deploy-hello-wingtip-saas-application"></a>Hallo Wingtip SaaS-toepassing implementeren

Hallo Wingtip SaaS-app implementeren:

1. Te klikken op Hallo **tooAzure implementeren** knop opent u hello Azure portal toohello Wingtip SaaS-implementatiesjabloon. Hallo sjabloon vereist twee parameterwaarden; een naam voor een nieuwe resourcegroep en de naam van een gebruiker die deze implementatie van andere implementaties van Hallo Wingtip SaaS app onderscheidt. de volgende stap Hallo biedt details voor het instellen van deze waarden.

   Zorg ervoor dat toonote Hallo exacte waarden die u gebruikt, omdat u moet deze in de configuratie van een bestand later tooenter.

   <a href="http://aka.ms/deploywtpapp" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

1. Geef de vereiste parameterwaarden voor Hallo implementatie:

    > [!IMPORTANT]
    > Om het overzichtelijk te houden zijn bepaalde verificatieprocessen weggelaten. Ook zijn de firewalls op servers uitgeschakeld voor deze zelfstudie. **Maak een nieuwe resourcegroep**, en gebruik niet bestaande resourcegroepen, servers of groepen. Gebruik deze toepassing of alle bronnen die wordt gemaakt, niet voor productie. Deze resource verwijdert wanneer u klaar bent met de Hallo toepassing toostop gerelateerde facturering.

    * **Resourcegroep** : Selecteer **nieuw** en geef een **naam** voor Hallo resourcegroep. Selecteer een **locatie** uit de vervolgkeuzelijst Hallo.
    * **Gebruiker** -resources vereisen namen die globaal uniek zijn. Uniekheid van tooensure telkens wanneer u de toepassing hello implementeren toodifferentiate resources die u maakt, uit bronnen die zijn gemaakt door een andere implementatie van Hallo Wingtip toepassing van een waarde opgeven. Het is raadzaam toouse een korte **gebruiker** naam, zoals uw initialen plus een getal (bijvoorbeeld *bg1*), en gebruikt u dat in de naam van resourcegroep hello (bijvoorbeeld *wingtip-bg1*). De **gebruiker** parameter mag alleen letters, cijfers en afbreekstreepjes (zonder spaties). Hallo moet eerste en laatste teken een letter of cijfer (alle kleine wordt aanbevolen).


1. **Implementeer de toepassing hello**.

    * Klik op tooagree toohello voorwaarden en bepalingen.
    * Klik op **Kopen**.

1. Implementatiestatus controleren door te klikken op **meldingen** (belpictogram rechts van het zoekvak Hallo Hallo). Implementatie Hallo Wingtip SaaS app duurt ongeveer vijf minuten.

   ![implementatie gelukt](media/sql-database-saas-tutorial/succeeded.png)

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a>Download en blokkering Hallo Wingtip SaaS-scripts

Tijdens het implementeren van de toepassing hello, download u Hallo source code en beheerscripts.

> [!IMPORTANT]
> Uitvoerbare inhoud (scripts, dll-bestanden) mogelijk geblokkeerd door Windows als zip-bestanden van een externe bron wordt gedownload en uitgepakt. Bij het uitpakken van Hallo scripts uit een zipbestand, stappen Hallo hieronder toounblock Hallo ZIP-bestand voor het uitpakken van. Dit zorgt ervoor Hallo scripts toorun zijn toegestaan.

1. Te bladeren[github-repo-Hallo Wingtip SaaS](https://github.com/Microsoft/WingtipSaaS).
1. Klik op **klonen of downloaden**.
1. Klik op **ZIP downloaden** en Hallo-bestand op te slaan.
1. Klik met de rechtermuisknop Hallo **WingtipSaaS master.zip** bestand en selecteer **eigenschappen**.
1. Op Hallo **algemene** tabblad **blokkering**, en klik op **toepassen**.
1. Klik op **OK**.
1. Hallo-bestanden extraheren.

Scripts bevinden zich in Hallo *... \\WingtipSaaS master\\Learning-Modules* map.

## <a name="update-hello-configuration-file-for-this-deployment"></a>Hallo-configuratiebestand voor deze implementatie bijwerken

Voordat u de scripts, stelt Hallo *resourcegroep* en *gebruiker* in waarden **UserConfig.psm1**. Stel deze variabelen toohello-waarden tijdens de implementatie.

1. Open... \\Learning-Modules\\*UserConfig.psm1* in Hallo *PowerShell ISE*
1. Update *ResourceGroupName* en *naam* met specifieke waarden Hallo voor uw implementatie (op regels 10 en 11 alleen).
1. Hallo wijzigingen opslaan!

Hier in te stellen gewoon blijft u opheft tooupdate deze implementatie-specifieke waarden in elk script.

## <a name="run-hello-application"></a>Hallo-toepassing uitvoeren

Hallo app gepresenteerd plaatsen, zoals concertzalen, jazz clubs Sport clubs die als host fungeren van gebeurtenissen. Plaatsen registreren als klanten (of tenants) van Hallo Wingtip platform voor een eenvoudige manier toolist gebeurtenissen en tickets verkopen. Elke locatie vast opgehaald van een aangepaste web app toomanage en hun-gebeurtenissen weergeven en verkopen tickets, onafhankelijke en geïsoleerd van andere tenants. Elke tenant opgehaald onder Hallo dekt, een SQL-database die is geïmplementeerd in een elastische SQL-groep.

Een centraal **gebeurtenissen Hub** bevat een lijst met tenant-URL's specifieke tooyour implementatie.

1. Open Hallo _gebeurtenissen Hub_ in uw webbrowser: http://events.wtp.&lt; GEBRUIKER&gt;. trafficmanager.net (vervangen door de naam van uw implementatie gebruiker):

    ![events hub](media/sql-database-saas-tutorial/events-hub.png)

1. Klik in de **Events Hub** op *Fabrikam Jazz Club*.

   ![Gebeurtenissen](./media/sql-database-saas-tutorial/fabrikam.png)


toocontrol hello distributie van inkomende aanvragen en Hallo app gebruikt [ *Azure Traffic Manager*](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview). Hallo gebeurtenissen-pagina's, die tenantspecifieke, vereist dat de namen van de tenant zijn opgenomen in Hallo URL's. Alle tenant Hallo URL's opnemen in uw specifieke *gebruiker* waarde en volgt deze indeling: http://events.wtp.&lt; GEBRUIKER&gt;.trafficmanager.net/*fabrikamjazzclub*. Hallo gebeurtenissen app parseert hello tenantnaam van Hallo-URL en gebruikt deze toocreate een sleutel tooaccess een catalogus met [ *shard kaart management*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-scale-shard-map-management). Hallo catalogus maps Hallo databaselocatie sleutel toohello-tenant. Hallo **gebeurtenissen Hub** uitgebreide metagegevens in Hallo catalogus tooretrieve Hallo van tenant-naam die is gekoppeld aan elke database tooprovide Hallo lijst met URL's gebruikt.

In een productieomgeving zou u meestal een DNS CNAME-record te maken [ *het internetdomein van een bedrijf wijzen* ](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-point-internet-domain) naar Hallo traffic manager-profiel.

## <a name="start-generating-load-on-hello-tenant-databases"></a>Genereren van belasting op Hallo tenant databases starten

Nu dat hello app is geïmplementeerd, laten we het toowork! Hallo *Demo LoadGenerator* PowerShell-script wordt gestart van een werkbelasting die wordt uitgevoerd op alle databases van de tenant. Hallo echte belasting van veel SaaS-apps is doorgaans sporadisch onvoorspelbaar. toosimulate belasting, Hallo generator produceert een werklast verdeeld over alle tenants, met willekeurige bursts op elke tenant optreedt op willekeurige intervallen. Het is daarom best toolet Hallo generator uitvoeren voor ten minste drie Hierdoor duurt het enkele minuten Hallo load patroon tooemerge of vier minuten voor bewaking Hallo laden.

1. In Hallo *PowerShell ISE*Open Hallo... \\Learning-Modules\\hulpprogramma's\\*Demo LoadGenerator.ps1* script.
1. Druk op **F5** Hallo-script uitvoeren en Hallo load generator (laat Hallo standaardparameterwaarden nu) starten.

> [!IMPORTANT]
> toorun andere scripts, een nieuw PowerShell ISE-venster openen. Hallo load generator wordt uitgevoerd als een reeks taken in uw lokale PowerShell-sessie. Hallo *Demo LoadGenerator.ps1* script serversysteemstatus Hallo daadwerkelijke laadbewerking generator script, dat wordt uitgevoerd als een taak voorgrond plus een reeks achtergrond generatie load-taken. Een taak load-generator wordt voor elke database die is geregistreerd in de catalogus hello aangeroepen. Hallo-taken worden uitgevoerd in uw lokale PowerShell-sessie, zodat alle taken Hallo PowerShell-sessie afsluit stopt. Als u uw machine onderbreekt, kan load generatie is onderbroken en wordt hervat wanneer u uw machine ontwaken.

Zodra het Hallo load generator roept generatie load-taken voor elke tenant, blijft Hallo voorgrond taak in een status-taak wordt aangeroepen, waarbij aanvullende achtergrondtaken wordt gestart voor een nieuwe tenants die vervolgens zijn ingericht. U kunt *Ctrl-C* of druk op Hallo *stoppen* knop toostop Hallo voorgrond taak, maar bestaande achtergrond taken zal doorgaan met het genereren van belasting op elke database. Als u moet toomonitor Hallo achtergrondtaken beheren, gebruikt *Get-Job*, *Receive-Job* en *taak stoppen*. Tijdens de Hallo voorgrond uitvoering taak u kan geen gebruik Hallo dezelfde PowerShell-sessie tooexecute andere scripts. toorun andere scripts, een nieuw PowerShell ISE-venster openen.

Als u wilt dat toorestart Hallo load generator sessie, bijvoorbeeld met andere parameters kunt u stoppen Hallo voorgrond taak en vervolgens opnieuw uitvoeren Hallo *Demo LoadGenerator.ps1* script. Opnieuw uit te voeren *Demo LoadGenerator.ps1* eerst alle actieve taken en opnieuw wordt opgestart Hallo generator, die een nieuwe set taken met de huidige parameters Hallo serversysteemstatus wordt gestopt.

Op dit moment laat Hallo load generator Hallo aanroepen van de taak status wordt uitgevoerd.


## <a name="provision-a-new-tenant"></a>Een nieuwe tenant inrichten

de eerste implementatie Hallo drie voorbeeld tenants wordt gemaakt, maar maken we een andere tenant toosee hoe dit heeft gevolgen voor de toepassing hello geïmplementeerd. Hallo inrichting Wingtip SaaS-tenants werkstroom wordt beschreven in Hallo [inrichten en catalogus zelfstudie](sql-database-saas-tutorial-provision-and-catalog.md). In deze stap maakt maken u snel een nieuwe tenant.

1. Open... \\Learning Modules\Provision en catalogus\\*Demo ProvisionAndCatalog.ps1* in Hallo *PowerShell ISE*.
1. Druk op **F5** Hallo-script (laat Hallo standaardwaarden nu) uit te voeren.

   > [!NOTE]
   > Veel Wingtip SaaS-scripts gebruiken *$PSScriptRoot* tooallow navigeren door mappen toocall functies in andere scripts. Deze variabele wordt alleen geëvalueerd wanneer Hallo-script is uitgevoerd door te drukken **F5**.  Syntaxismarkering en een selectie actief (**F8**) kunnen leiden tot fouten, indrukt **F5** wanneer het uitvoeren van scripts.

Hallo nieuwe tenant-database is gemaakt in een elastische SQL-groep, geïnitialiseerd en geregistreerd in het Hallo-catalogus. Na geslaagde inrichting, de nieuwe tenant Hallo ticket verkopen *gebeurtenissen* site wordt weergegeven in uw browser:

![Nieuwe tenant](./media/sql-database-saas-tutorial/red-maple-racing.png)

Hallo vernieuwen *gebeurtenissen Hub* en er verschijnt nu de nieuwe tenant Hallo in Hallo-lijst.


## <a name="explore-hello-servers-pools-and-tenant-databases"></a>Verken Hallo-servers, pools en tenant-databases

Nu dat u hebt gestart met het uitvoeren van een werklast in Hallo verzameling tenants, bekijken we een aantal van Hallo-resources die zijn geïmplementeerd:

1. In de [Azure-portal](http://portal.azure.com), tooyour lijst met SQL-servers bladeren en open de **catalogus -&lt;gebruiker&gt;**  server. Hallo-catalogusserver bevat twee databases. Hallo **tenantcatalog**, en Hallo **basetenantdb** (een lege *gouden* of sjabloondatabase die is gekopieerd toocreate nieuwe tenants).

   ![databases](./media/sql-database-saas-tutorial/databases.png)

1. Ga terug tooyour lijst met SQL-servers en open Hallo **tenants1 -&lt;gebruiker&gt;**  server die Hallo tenant databases bevat. Elke tenant-database is een _Standard elastische_ database in een standaard 50 eDTU-pool. Ook ziet er is een _Rode esdoorn race_ database, Hallo tenant database die u eerder hebt ingericht.

   ![server](./media/sql-database-saas-tutorial/server.png)

## <a name="monitor-hello-pool"></a>Monitor Hallo van toepassingen

Als Hallo load generator actief is geweest gedurende enkele minuten, moet voldoende gegevens beschikbaar toostart kijken aantal Hallo bewakingsmogelijkheden ingebouwd in groepen en databases.

1. Bladeren door de server toohello **tenants1 -&lt;gebruiker&gt;**, en klik op **Pool1** Resourcegebruik voor Hallo toepassingen weergeven (Hallo load generator uitgevoerd voor een uur in de volgende grafieken Hallo) :

   ![pool bewaken](./media/sql-database-saas-tutorial/monitor-pool.png)

Wat deze twee grafieken mooi laten zien, is dat elastische pools en SQL Database uitermate geschikt zijn voor workloads van SaaS-toepassingen. Vier databases die elk tooas sturen zijn liefst eenvoudig 40 edtu's worden ondersteund in een 50 eDTU-pool. Als ze zijn ingericht als zelfstandige databases, zoals elke toobe moet een S2 (50 DTU) toosupport Hallo bursts. Hallo kosten van 4 zelfstandige S2 databases zijn bijna 3 maal Hallo prijs van Hallo van toepassingen en Hallo van toepassingen heeft nog volop mogelijkheden voor veel meer databases. In de praktijk situaties worden SQL-Database klanten momenteel uitgevoerd van too500 databases in 200 eDTU-toepassingen. Zie voor meer informatie, Hallo [prestatiebewaking zelfstudie](sql-database-saas-tutorial-performance-monitoring.md).


## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u het volgende geleerd:

> [!div class="checklist"]

> * Hoe toodeploy Hallo Wingtip SaaS-toepassing
> * Over het Hallo-servers, -adresgroepen en -databases die gezamenlijk Hallo-app
> * Tenants zijn toegewezen tootheir gegevens Hello *catalogus*
> * Hoe tooprovision nieuwe tenants
> * Hoe tooview groep gebruik toomonitor tenant-activiteit
> * Hoe toodelete voorbeeld resources toostop gerelateerd facturering

Probeer het nu Hallo [inrichten en de catalogus-zelfstudie](sql-database-saas-tutorial-provision-and-catalog.md)



## <a name="additional-resources"></a>Aanvullende bronnen

* Aanvullende [zelfstudies die zijn gebaseerd op Hallo Wingtip SaaS-toepassing](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* Zie toolearn over elastische pools [ *wat is er een Azure SQL elastische pool*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool)
* Zie toolearn over elastische taken [ *beheren cloud uitgebreide databases*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)
* toolearn over multitenant SaaS-toepassingen, Zie [ *ontwerppatronen voor multitenant SaaS-toepassingen*](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)
