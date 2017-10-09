---
title: nieuwe tenants aaaProvision in een multitenant-app die gebruikmaakt van Azure SQL Database | Microsoft Docs
description: Meer informatie over hoe tooprovision en catalogus nieuwe tenants in Hallo Wingtip SaaS-app
keywords: zelfstudie sql-database
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: sstein
ms.openlocfilehash: eb26f523305650c2124e36707d187dfcdad06fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-new-tenants-and-register-them-in-hello-catalog"></a>Inrichten van nieuwe tenants en registreert u ze in de catalogus Hallo

In deze zelfstudie leert u Hallo inrichten en catalogus SaaS patronen en hoe ze worden geïmplementeerd in Hallo Wingtip SaaS-toepassing. U maakt en initialiseren van de nieuwe tenant-databases en registreert u ze in van de toepassing hello tenant-catalogus. Hallo-catalogus is een database die wordt onderhouden door Hallo toewijzing tussen Hallo SaaS-toepassing van tal van tenants en hun gegevens. Hallo catalogus speelt een belangrijke rol toepassing aanvragen toohello juiste database sturen.  

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]

> * Een enkele nieuwe tenant, met inbegrip van hoe deze wordt geïmplementeerd doorlopen inrichten
> * Verschillende tenants tegelijk inrichten


toocomplete in deze zelfstudie, zorg ervoor dat Hallo volgende vereisten zijn voltooid:

* Hallo Wingtip SaaS-app wordt geïmplementeerd. Zie toodeploy in minder dan vijf minuten [implementeren en verkennen Hallo Wingtip SaaS-toepassing](sql-database-saas-tutorial.md)
* Azure PowerShell is geïnstalleerd. Zie [Aan de slag met Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps) voor meer informatie.

## <a name="introduction-toohello-saas-catalog-pattern"></a>Inleiding toohello patroon van de SaaS-catalogus

Het is belangrijk tooknow waar informatie voor elke tenant wordt opgeslagen in een database back multitenant SaaS-toepassing. In Hallo SaaS catalogus patroon is een catalogusdatabase gebruikte toohold Hallo toewijzing tussen elke tenant en waar hun gegevens worden opgeslagen. Hallo Wingtip SaaS app gebruikmaakt van een één-tenant per database-architectuur, maar Hallo basispatroon voor het opslaan van de toewijzing van de tenant-naar-database in een catalogus van toepassing of een database met meerdere of één tenant wordt gebruikt.

Elke tenant een sleutel die ze kunnen worden geïdentificeerd in de catalogus Hallo is toegewezen en toohello locatie van de juiste database Hallo die is toegewezen. In-app Wingtip SaaS Hallo wordt Hallo-sleutel gevormd door een hash van Hallo tenantnaam. Dit kunt Hallo tenant-gedeelte van Hallo toepassing URL toobe tooconstruct Hallo sleutel gebruikt. Andere schema's voor tenant-sleutel kunnen worden gebruikt.  

Hallo catalogus kunt Hallo-naam of locatie van Hallo database toobe met minimale gevolgen voor de toepassing hello gewijzigd.  In een multitenant databasemodel dit ook geschikt is voor 'verplaatsen' een tenant tussen databases.  Hallo catalogus kan ook worden gebruikt tooindicate of een tenant of database offline is voor onderhoud of andere acties. Dit is verkend in Hallo [herstellen van de zelfstudie voor één tenant](sql-database-saas-tutorial-restore-single-tenant.md).

Bovendien Hallo catalog, wat een management-database voor een SaaS-toepassing actief is, kan extra tenant of database-metagegevens opslaan, zoals Hallo laag of editie van een database, schemaversie, service-abonnement of sla's aangeboden tootenants en andere gegevens die Hiermee kunt toepassingsbeheer, klantenondersteuning of devops-processen.  

Afgezien van SaaS-toepassing hello, kunt Hallo catalogus Databasehulpprogramma's inschakelen.  In voorbeeld Wingtip SaaS Hallo Hallo catalogus gebruikte tooenable cross-tenant query, verkend in Hallo is [ad-hoc analytics zelfstudie](sql-database-saas-tutorial-adhoc-analytics.md). Jobbeheer cross-database wordt verkend in Hallo [Schemabeheer](sql-database-saas-tutorial-schema-management.md) en [tenant analytics](sql-database-saas-tutorial-tenant-analytics.md) zelfstudies. 

In-app Wingtip SaaS Hallo Hallo catalogus wordt geïmplementeerd met het Hallo Shard-beheerfuncties van Hallo met [elastische Database Client bibliotheek (EDCL)](sql-database-elastic-database-client-library.md). Hallo EDCL kunt u een toepassing toocreate, beheren en gebruiken van een database back shard-toewijzing. Een shard-toewijzing bevat een lijst met shards (databases) en Hallo toewijzing tussen sleutels (tenants) en databases.  EDCL functies uit toepassingen of PowerShell-scripts kunnen worden gebruikt tijdens tenant toocreate Hallo vermeldingen in de shard-toewijzing Hallo inrichting en van toepassingen tooefficiently verbinding maken met de juiste database toohello. EDCL in de cache opgeslagen verbinding informatie toominimize Hallo verkeer toohello catalogusdatabase en de toepassing hello te versnellen.  

> [!IMPORTANT]
> Hallo toewijzingsgegevens is toegankelijk in de database van de catalogus hello, maar *niet bewerken*! Wijzig de toewijzingsgegevens alleen via API's van EDCL. Rechtstreeks bewerken van Hallo toewijzingsgegevens risico's te beschadigen Hallo-catalogus en wordt niet ondersteund.


## <a name="introduction-toohello-saas-provisioning-pattern"></a>Inleiding toohello SaaS inrichting patroon

Bij het voorbereiden van een nieuwe tenant in een SaaS-toepassing die gebruikmaakt van moet een databasemodel voor één tenant-een nieuwe tenant-database worden ingericht.  Deze moet worden gemaakt in de juiste locatie Hallo en geïnitialiseerd met het juiste schema- en referentiegegevens samenvoegt en vervolgens geregistreerd in de catalogus Hallo onder de juiste tenantsleutel Hallo servicelaag.  

Verschillende benaderingen kunnen gebruikte toodatabase inrichting, waaronder SQL-scripts uitvoeren, een bacpac implementeren of kopiëren van een sjabloondatabase van de 'gouden' kan worden.  

Hallo inrichting aanpak die u gebruikt moet worden comprehended in de algemene schema beheerstrategie, die u ervoor zorgen moet dat nieuwe databases zijn ingericht met de meest recente schema Hallo.  Dit is verkend in Hallo [schema management zelfstudie](sql-database-saas-tutorial-schema-management.md).  

Hallo Wingtip SaaS app bepalingen nieuwe tenants door het kopiëren van een gouden database met de naam basetenantdb, geïmplementeerd op Hallo-catalogusserver.  Inrichting kan worden geïntegreerd in de toepassing hello als onderdeel van een aanmelding ervaring en/of ondersteunde offline met behulp van scripts. Deze zelfstudie verkennen inrichten met behulp van PowerShell. Hallo inrichting scripts Hallo basetenantdb toocreate een nieuwe tenant-database in een elastische pool kopiëren en vervolgens het met tenant-specifieke gegevens initialiseren en registreren in Hallo catalogus shard-toewijzing.  In de voorbeeld-app Hallo krijgen databases namen op basis van de tenantnaam hello, maar dit is geen een essentieel onderdeel van het Hallo-patroon – Hallo Hallo catalog kunnen elke database met naam toobe toegewezen toohello. + 


## <a name="get-hello-wingtip-application-scripts"></a>Hallo Wingtip toepassingsscripts ophalen

Hallo Wingtip SaaS-scripts en broncode van toepassing zijn beschikbaar in Hallo [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github-opslagplaats. [Stappen toodownload Hallo Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).


## <a name="provision-and-catalog-detailed-walkthrough"></a>Gedetailleerd overzicht van inrichten en catalogiseren

toounderstand hoe Hallo Wingtip toepassing implementeert een nieuwe tenant inrichting, een onderbrekingspunt toevoegen en doorloop Hallo werkstroom tijdens het inrichten van een tenant:

1. Open... \\Learning-Modules\\ProvisionAndCatalog\\_Demo ProvisionAndCatalog.ps1_ en Hallo set parameters te volgen:
   * **$TenantName** = Hallo-naam van de nieuwe wetten hello (bijvoorbeeld *Bushwillow blauwe*).
   * **$VenueType** = Hallo vooraf gedefinieerde wetten soorten: *blauwe*, classicalmusic, dans, jazz, judo, motorracing multipurpose, opera, rockmusic, doel.
   * **$DemoScenario** = **1**stelt te**1** te*inrichten van een enkele tenant*.

1. Een onderbrekingspunt toevoegen door de gegevens van de cursor overal op 48, Hallo regel waarin wordt gemeld: *New-Tenant '*, en druk op **F9**.

   ![onderbrekingspunt](media/sql-database-saas-tutorial-provision-and-catalog/breakpoint.png)

1. Druk op toorun Hallo script **F5**.

1. Nadat de uitvoering van het script Hallo stopt bij onderbrekingspunt Hallo, drukt u op **F11** toostep in Hallo-code.

   ![onderbrekingspunt](media/sql-database-saas-tutorial-provision-and-catalog/debug.png)



Hallo-script uitvoeren met behulp van Hallo traceren **Debug** menuopties - **F10** en **F11** toostep via of in Hallo functies genoemd. Zie voor meer informatie over foutopsporing van PowerShell-scripts [Tips voor het werken met en foutopsporing van PowerShell-scripts](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/how-to-debug-scripts-in-windows-powershell-ise).


Hallo volgen niet tooexplicitly Volg stappen, maar een uitleg van Hallo werkstroom doorlopen tijdens het opsporen van Hallo script:

1. **Importeren Hallo SubscriptionManagement.psm1** module met functies voor tooAzure aanmelden en Hallo u met werkt Azure-abonnement selecteren.
1. **Importeren Hallo CatalogAndDatabaseManagement.psm1** module die voorziet in een catalogus en op tenantniveau abstractie via Hallo [Shard Management](sql-database-elastic-scale-shard-map-management.md) functies. Dit is een belangrijk module die veel Hallo catalogus patroon ingekapseld en waard.
1. **Ophalen van configuratiedetails**. Stap in de Get-configuratie (met F11) en Zie hoe Hallo app-configuratie is opgegeven. Resourcenamen en andere waarden van app-specifiek hier zijn gedefinieerd, maar niet wijzigen van deze waarden totdat u bekend met het Hallo-scripts bent.
1. **Ophalen van Hallo catalogusobject**. Stap in dit stelt het bericht en retourneert een catalogusobject dat wordt gebruikt in een hoger niveau Hallo-script Get-catalogus.  Hierbij wordt gebruikgemaakt van Shard-Management-functies die worden geïmporteerd vanuit **AzureShardManagement.psm1**. Hallo catalog-object van Hallo volgende bestaat:
   * $catalogServerFullyQualifiedName is opgesteld met standaard stam Hallo plus uw gebruikersnaam: _catalogus -\<gebruiker\>. database.windows.net_.
   * $catalogDatabaseName wordt opgehaald uit het Hallo-config: *tenantcatalog*.
   * $shardMapManager object is uit Hallo catalogusdatabase geïnitialiseerd.
   * $shardMap object wordt geïnitialiseerd vanuit Hallo *tenantcatalog* shard-toewijzing in Hallo catalogus-database.
   Een catalogusobject is samengesteld, geretourneerd en gebruikt in een hoger niveau Hallo-script.
1. **Berekenen van de nieuwe tenantsleutel hello**. Een hash-functie is gebruikte toocreate Hallo-tenantsleutel van Hallo tenantnaam.
1. **Controleer of de tenantsleutel Hallo al bestaat**. Hallo-catalogus wordt gecontroleerd tooensure Hallo sleutel beschikbaar is.
1. **Hallo tenant-database is ingericht met New-TenantDatabase.** Gebruik **F11** toostep in en Zie hoe Hallo-database is ingericht met behulp van een [Azure Resource Manager-sjabloon](../azure-resource-manager/resource-manager-template-walkthrough.md).

Hallo-databasenaam is samengesteld uit Hallo tenant naam toomake het wissen welke shard toowhich tenant behoort. (Andere strategieën voor het benoemen van de database kunnen eenvoudig worden gebruikt.) + Een Resource Manager-sjabloon is gebruikte toocreate een tenant-database door het kopiëren van een gouden database (baseTenantDB) op Hallo-catalogusserver. Een alternatieve methode kan worden toocreate een lege database en vervolgens het initialiseren door het importeren van een Bacpac- of tooexecute een script voor initialisatie van een bekende locatie.  

Hallo Resource Manager-sjabloon bevindt zich in Hallo ...\Learning Modules\Common\ map: *tenantdatabasecopytemplate.json*

Nadat het Hallo-tenant-database is gemaakt, is deze verdere **geïnitialiseerd met hello wilt (tenant) naam en type op Hallo wilt**. Hier kunnen ook andere initialisaties plaatsvinden.

Hallo **tenant-database is geregistreerd in de catalogus Hallo** met *toevoegen TenantDatabaseToCatalog* hello tenantsleutel. Gebruik **F11** toostep in Hallo details:

* Hallo catalogusdatabase toegevoegd toohello shard-toewijzing (Hallo lijst met bekende databases).
* toewijzing van die koppelingen Hallo sleutelwaarde toohello shard Hello wordt gemaakt.
* Aanvullende metagegevens (naam van hello wilt) over Hallo-tenant is toohello Tenants tabel toegevoegd in Hallo-catalogus.  Hallo Tenants tabel maakt geen deel uit van Hallo ShardManagement schema en niet is geïnstalleerd door Hallo EDCL.  Deze tabel ziet u hoe Hallo catalogusdatabase kan worden uitgebreid toosupport aanvullende toepassingsspecifieke gegevens.   


Nadat het inrichten is voltooid, uitvoering retourneert toohello oorspronkelijke *Demo ProvisionAndCatalog* script, dat wordt geopend Hallo **gebeurtenissen** pagina voor de nieuwe tenant in de browser Hallo Hallo:

   ![events](media/sql-database-saas-tutorial-provision-and-catalog/new-tenant.png)


## <a name="provision-a-batch-of-tenants"></a>Een batch van tenants inrichten

In deze oefening voorziet in een batch 17 tenants. Het raadzaam dat u deze batch van tenants voordat u andere zelfstudies Wingtip SaaS zodat er meer dan een paar databases toowork met inrichten.

1. Open... \\Learning-Modules\\ProvisionAndCatalog\\*Demo ProvisionAndCatalog.ps1* in Hallo *PowerShell ISE* en wijzig Hallo *$ DemoScenario* parameter too3:
   * **$DemoScenario** = **3**, ook wijzigen**3** te*inrichten van een batch van tenants*.
1. Druk op **F5** Hallo script en uitvoeren.

Hallo-script wordt een reeks extra tentants geïmplementeerd. Dit maakt gebruik van een [Azure Resource Manager-sjabloon](../azure-resource-manager/resource-manager-template-walkthrough.md) die Hallo batch regelt en vervolgens delegeert inrichten van elke database tooa gekoppelde sjabloon. Met behulp van sjablonen op deze manier kunt Azure Resource Manager toobroker Hallo inrichtingsproces voor uw script. Sjablonen inrichten databases parallel waar het kan en pogingen indien nodig, verwerkt Hallo algemene processen te optimaliseren. Hallo script is idempotent dus als dit mislukt of om welke reden gestopt Voer dit opnieuw.

### <a name="verify-hello-batch-of-tenants-successfully-deployed"></a>Controleer of Hallo batch van tenants is geïmplementeerd

* Open Hallo *tenants1* server door te bladeren tooyour lijst met servers in Hallo [Azure-portal](https://portal.azure.com), klikt u op **SQL-databases**, en controleer of Hallo batch van 17 extra databases zijn nu in de lijst Hallo:

   ![databaselijst](media/sql-database-saas-tutorial-provision-and-catalog/database-list.png)



## <a name="other-provisioning-patterns"></a>Andere inrichtingspatronen

Dit zijn twee inrichtingspatronen die niet aan bod zijn gekomen in deze zelfstudie:

**Vooraf inrichten van databases.** Hallo vooraf inrichten patroon aanvallen op Hallo feit dat de databases in een elastische pool Voeg geen extra kosten verbonden. Facturering voor de elastische groep Hallo is, niet Hallo databases en niet-actieve databases geen resources gebruiken. Databases in een pool vooraf worden ingericht en wijzen wanneer dit nodig is, kan de tenant onboarding tijd aanzienlijk worden verkleind. Hallo aantal databases dat vooraf is ingericht kan worden aangepast benodigde tookeep een buffer die geschikt is voor Hallo verwacht snelheid wordt ingericht.

**Automatische inrichting.** In Hallo automatische inrichting patroon een speciale inrichting service is gebruikte tooprovision servers, -adresgroepen en -databases automatisch naar behoefte – waaronder vooraf inrichten databases in een elastische pools indien gewenst. En als de databases zijn opdracht ongedaan en verwijderd, hiaten in de elastische pools kunnen worden gevuld door Hallo-service naar wens inricht. Deze service kan eenvoudig of complex – bijvoorbeeld afhandeling van de inrichting voor meerdere locaties en kan geo-replicatie wordt automatisch ingesteld als deze strategie wordt gebruikt voor herstel na noodgevallen. Hallo automatische inrichting patroon een clienttoepassing of script zou een inrichting wachtrij toobe voor aanvraag tooa verwerkt door het Hallo-service inricht verzenden en zou vervolgens Hallo service toodetermine voltooiing pollen. Als vooraf inrichten wordt gebruikt, zou aanvragen snel worden verwerkt met Hallo-service beheert het inrichten van een vervanging-database op de achtergrond Hallo uitgevoerd.



## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u het volgende geleerd:

> [!div class="checklist"]

> * Eén nieuwe tenant inrichten
> * Verschillende tenants tegelijk inrichten
> * Stap in de details van de inrichting van tenants en geregistreerd in de catalogus Hallo Hallo

Probeer Hallo [prestaties bewaking zelfstudie](sql-database-saas-tutorial-performance-monitoring.md).

## <a name="additional-resources"></a>Aanvullende resources

* Aanvullende [zelfstudies waarin voort op Hallo Wingtip SaaS-toepassing bouwen](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Clientbibliotheek voor Elastic Database](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-database-client-library)
* [Hoe tooDebug Scripts in Windows PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/how-to-debug-scripts-in-windows-powershell-ise)
