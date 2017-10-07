---
title: aaaFAQ voor ClearDB MySql-databases met Azure App Service | Microsoft Docs
description: Antwoorden op vragen over het gebruik van ClearDB MySQL-databases met Azure App Service toocommon.
documentationcenter: php
services: 
author: sunbuild
manager: yochayk
editor: 
tags: mysql
ms.assetid: c2ed5e78-6d7d-4d0c-b7ee-a52ae41ceab8
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: sumuth
ms.openlocfilehash: 3d9c9daca2b845ede8d3a1fdadefa7e668d62dee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="faq-for-cleardb-mysql-databases-with-azure-app-service"></a>Veelgestelde vragen voor ClearDB MySql-databases met Azure App Service
Deze Veelgestelde vragen over de antwoorden op veelgestelde vragen over het gebruik en de aanschaf van ClearDB MySQL databases voor Web-Apps van Azure.

## <a name="what-options-do-i-have-for-mysql-on-azure"></a>Welke opties heb ik voor MySQL in Azure?
U hebt verschillende mogelijkheden:

* [ClearDB gedeeld MySQL-database](/marketplace/partners/cleardb/databases/)
* [ClearDB MySQL Premium clusters](/marketplace/partners/cleardb-clusters/cluster/)
* [MySQL-cluster uitgevoerd op een virtuele machine in Azure](https://github.com/azure/azure-quickstart-templates/tree/master/mysql-replication)
* [Één exemplaar van MySQL uitgevoerd op een virtuele machine in Azure](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

ClearDB is van een hostingservice MySQL en Hallo MySQL infrastructuur voor u beheert. Wanneer u uw eigen MySQL-cluster of de database op een virtuele Machine van Azure uitvoert, kunt u tooset Hallo MySQL-server hebt en werken met patches.

## <a name="do-i-need-a-credit-card-for-hello-web-app--mysql-template-in-hello-azure-marketplace"></a>Heb ik een creditcard nodig voor de Web-app Hallo + MySQL-sjabloon in hello Azure Marketplace?
Dit is afhankelijk van Hallo-type van het abonnement dat u gebruikt. Hier volgen enkele typen vaak gebruikte abonnement:

* [U betaalt](/offers/ms-azr-0003p/): vereist een creditcard en bij de aankoop van een betaald MySQL-database uw creditcard in rekening gebracht.
* [Gratis proefversie](https://azure.microsoft.com/pricing/free-trial/): tegoed bevat voor gebruik met Microsoft Azure-services, maar aankoop van resources van derden is niet toegestaan. de services van derden toopurchase of een betaald MySQL-database moet u een creditcard toouse ingeschakeld abonnement. U kunt een gratis ClearDB MySQL-database maken voor Web-Apps.
* [MSDN-abonnement](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/) en **omslagstelsel MSDN ontwikkelen, testen**: vergelijkbaar tooFree proef, een MSDN-abonnement, moet u een creditcard toopurchase een betaald MySQL-oplossing van ClearDB toohave.
* [Enterprise Agreement (EA)](https://azure.microsoft.com/pricing/enterprise-agreement/): EA klanten worden gefactureerd tegen hun EA elk kwartaal voor alle hun aankopen Azure Marketplace (derde) op een afzonderlijke, geconsolideerde factuur. U wordt gefactureerd buiten Hallo maandbedrag voor een marketplace-aankopen. Houd er rekening mee dat op dit moment Azure Store niet beschikbaar toocustomers ingeschreven in Azerbeidzjan, Kroatië, Noorwegen en Portorico is. 
* [DreamSpark](https://www.dreamspark.com/Product/Product.aspx?productid=99): U kunt alleen gratis ClearDB databases voor Web-Apps maken. Er is geen limiet voor het aantal vrije ClearDB MySQL-databases die kunt u Hallo. Houd er rekening mee dat gratis databases niet gebruikt voor productie-web-apps toobe zijn als deze service is alleen bedoeld voor proefversie.

## <a name="why-was-i-charged-350-for-a-web-app--mysql-from-hello-azure-marketplace"></a>Waarom is ik $3,50 voor een Web-app + MySQL van hello Azure Marketplace in rekening gebracht?
Hallo database standaardoptie is Titan die $3,50. We geen Hallo kosten weergeven tijdens het maken van de database en u hebt per ongeluk een database die u niet wilt aanschaffen. We proberen toofind een manier tooimprove Hallo-ervaring, maar tot die tijd moet u alle uw geselecteerde Prijscategorieën voor web-app en database controleren voordat u op **maken** en Hallo-implementatie van Hallo-resources te starten.

## <a name="i-am-running-mysql-on-my-own-azure-virtual-machine-can-i-connect-my-azure-web-app-toomy-database"></a>Ik heb MySQL op mijn eigen virtuele machine van Azure. Kan ik mijn Azure-web-app toomy database verbinden?
Ja. U kunt uw web-app tooyour database verbinden, zolang uw Azure VM RAS tooyour web-app heeft gegeven. Zie voor meer informatie [MySQL installeren op een virtuele machine](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="in-which-countries-are-cleardb-premium-mysql-clusters-supported"></a>In welke landen zijn ClearDB Premium MySQL-clusters ondersteund?
[ClearDB Premium MySQL clusters](/marketplace/partners/cleardb-clusters/cluster/) zijn beschikbaar in alle Azure-regio's met uitzondering van India, Australië, Brazilië-Zuid en China Hallo overal ter wereld.

## <a name="can-i-create-a-new-cluster-prior-toocreating-a-database-with-cleardb-premium-cluster-solution"></a>Kan ik een nieuw cluster voorafgaande toocreating een database maken met ClearDB premium clusteroplossing?
Nee, leeg ClearDB-clusters maken wordt niet ondersteund. Hello Azure-portal kunt u toocreate databases in een cluster, waarmee een nieuw cluster kan worden gemaakt op Hallo hetzelfde moment.

## <a name="will-i-be-warned-if-i-try-toodelete-a-cleardb-mysql-database-that-is-in-use-by-one-of-my-applications"></a>Ik gewaarschuwd als ik toodelete een ClearDB MySQL-database die wordt gebruikt door een van mijn toepassingen proberen?
Nee, Azure wordt geen waarschuwing als u een marketplace-aankopen die uw toepassing afhankelijk van is verwijderen.

## <a name="which-regions-can-i-create-cleardb-databases-in"></a>Welke regio's kan ik ClearDB-databases in maken?
Azure Marketplace is niet beschikbaar toocustomers ingeschreven in Azerbeidzjan, Kroatië, Noorwegen of Portorico. ClearDB is niet beschikbaar in deze regio's.

## <a name="what-pricing-tier-should-i-choose-for-a-production-web-app-and-database"></a>Welke prijscategorie moet ik kiezen voor een productie-web-app en database?
Basic of een hogere prijscategorie voor Web-Apps gebruiken. Voor ClearDB, wordt aangeraden een Saturnus of Jupiter plan. Hallo-kenmerken en beperkingen van elke prijscategorie voor zowel lees [Web-Apps](https://azure.microsoft.com/pricing/details/app-service/) en [ClearDB MySQL-databases](/marketplace/partners/cleardb/databases/) toochoose Hallo die past bij uw behoeften.

## <a name="how-do-i-upgrade-my-cleardb-database-from-one-plan-tooanother"></a>Hoe voer ik mijn database ClearDB upgrade uit van een plan tooanother?
In Hallo [Azure-portal](https://portal.azure.com), kunt u een database ClearDB gedeelde hosting opschalen. Lees dit [artikel](https://blogs.msdn.microsoft.com/appserviceteam/2016/10/06/upgrade-your-cleardb-mysql-database-in-azure-portal/) toolearn meer. Momenteel ondersteund niet upgrade voor ClearDB Premium clusters in hello Azure-portal.

## <a name="i-cant-see-my-cleardb-database-in-azure-portal"></a>Ik kan mijn ClearDB-database in Azure-portal niet zien?
Als er ClearDB-database met Azure Resource Manager worden gemaakt of [nieuwe Azure-Portal](https://portal.azure.com), zijn niet zichtbaar in Hallo [oude Azure-Portal](https://manage.windowsazure.com). toowork-dit is toolink de database handmatig toohello web-app. Op dezelfde manier als ClearDB-database maken in Hallo [oude portal](https://manage.windowsazure.com) kun je het niet kunnen toosee worden uw database in Hallo [nieuwe Azure-Portal](https://portal.azure.com). Er is geen tijdelijke oplossing voor het tweede scenario Hallo.

## <a name="who-do-i-contact-for-support-when-my-database-is-down"></a>Wie ik contact opnemen voor ondersteuning bij mijn database niet beschikbaar is?
Neem contact op met [ClearDB ondersteuning](https://www.cleardb.com/developers/help/support) voor alle databasequery gerelateerde problemen. Tooprovide worden voorbereid ze met de informatie van uw Azure-abonnement.

## <a name="can-i-create-additional-users-for-my-cleardb-mysql-database-cluster-solution"></a>Kan ik extra gebruikers maken voor de clusteroplossing van mijn ClearDB MySQL-database?
Nee. U kunt geen extra gebruikers maken, maar u kunt aanvullende databases maken op uw cluster ClearDB-database.  

## <a name="can-basicpro-series-databases-be-upgraded-in-place-similar-tooplanetary-plans-today-on-cleardb-portal"></a>Kunnen Basic/Pro reeks databases zijn bijgewerkte in-place vergelijkbare tooPlanetary plannen vandaag op ClearDB portal?
Ja, basismodule databases kunnen worden bijgewerkt in-place (standaard 60 via Basic 500). Pro-serie kan worden bijgewerkt in-place (Pro 125 via Pro 1000), met uitzondering van Pro 60. Pro 60 database momenteel bijwerken wordt niet ondersteund. 

## <a name="when-i-migrate-my-resources-from-one-subscription-tooanother-does-my-cleardb-mysql-database-get-migrated-as-well"></a>Wanneer ik mijn resources van een abonnement tooanother migreert, Mijn ClearDB MySQL-database worden overgezet ook?
Wanneer u Resourcemigratie uitvoert voor abonnementen, enkele [beperkingen](app-service-web/app-service-move-resources.md) toepassen. Een ClearDB MySQL-database is een service van derden en daarom niet ophalen gemigreerd tijdens de migratie van de Azure-abonnement. Als u niet Hallo migratie van uw MySQL beheert-database voorafgaande toomigrating Azure resources, uw ClearDB MySQL databases kunnen worden uitgeschakeld. Handmatig migreren van uw databases eerst en voert u de migratie van de Azure-abonnement voor uw web-app. 

## <a name="i-hit-hello-spending-limit-on-my-subscription-i-removed-hello-limit-and-my-app-service-is-online-however-hello-database-is-not-accessible-how-do-i-re-enable-hello-cleardb-database"></a>Ik bereikt Hallo uitgavenlimiet op mijn abonnement. Ik heb Hallo limiet verwijderd en Mijn App-Service is online, maar het Hallo-database is niet toegankelijk. Hoe kan ik Hallo ClearDB database opnieuw inschakelen?
Neem contact op met [ClearDB ondersteuning](https://www.cleardb.com/developers/help/support) toore inschakelen Hallo-database. Geef ze met de naam van uw Azure-abonnement en de database.

## <a name="can-i-transfer-a-cleardb-database-from-a-credit-card-subscription-tooan-ea-subscription"></a>Kan ik een database ClearDB overbrengen van een creditcard abonnement tooan EA abonnement?
Bestaande ClearDB databases Hallo creditcard die is gekoppeld aan de bestaande abonnementen hello gebruiken. toouse een EA-abonnement dat u uw gegevens tooa nieuwe database toomigrate nodig:

* Een nieuwe database ClearDB met uw abonnement EA aanschaffen.
* Migreer uw gegevens tooyour nieuwe database.
* Uw toepassing toouse Hallo nieuwe database bijwerken.
* Uw oude ClearDB-database verwijderd.

Wanneer u een nieuwe WebApp met MySQL (ClearDB maken) of een MySQL-database (ClearDB) maakt, Hallo abonnement dat u kiest, bepaalt hoe u betaalt voor Hallo-service. Met een abonnement EA blokkeert we niet Hallo aanschaf van Hallo-services van derden zoals ClearDB in hello Azure-portal. EA abonnementen zijn buiten bedrag in rekening gebracht en worden gefactureerd per kwartaal en achterstallig. Hallo EA klant zou tooset een betalingsmethode zoals een creditcard toopay voor alle services van derden marketplace hebben.

## <a name="where-can-i-see-hello-charges-for-cleardb-resources-in-an-ea-subscription"></a>Waar kan ik Hallo kosten voor ClearDB-resources in een abonnement EA zien?
Azure Marketplace-kosten zijn voor directe EA klanten, zichtbaar op Hallo Enterprise Portal. Houd er rekening mee dat alle marketplace-aankopen en het verbruik buiten bedrag in rekening gebracht zijn en worden gefactureerd per kwartaal en achterstanden. EA klanten hebben toopay rechtstreeks toohello van derden serviceproviders en kan dus doordat een betalingswijze zoals een creditcard met hun EA account.

Indirecte EA klanten vindt hun Azure Marketplace-abonnementen op Hallo **abonnementen beheren** pagina Hallo Enterprise Portal, maar de prijzen is verborgen. Klanten moeten contact opnemen met hun gelaagde Serviceproviders voor informatie over de marketplace-kosten.

Toegang tooAzure Marketplace voor services van derden kan worden beheerd door uw inschrijving EA Azure beheerders. Ze kunnen uitschakelen of toegang too3rd partij aankopen van Hallo-archief van Accounts beheren en abonnementen onder Hallo accountsectie in het Hallo Enterprise Portal opnieuw in te schakelen.

## <a name="who-do-i-contact-for-questions-about-my-bill-for-cleardb-services-in-my-ea-subscription"></a>Wie ik contact opnemen voor vragen over mijn factuur voor ClearDB-services in mijn abonnement EA?
Neem contact op met [Enterprise Customer Support](http://aka.ms/AzureEntSupport) met betrekking toobilling onder hun EA registratie. Hallo EA Portal ondersteuningsteam wordt uw vraag te beantwoorden of uw probleem op te lossen.

## <a name="more-information"></a>Meer informatie
[Veelgestelde vragen over Azure Marketplace](/marketplace/faq/)

