---
title: verklarende woordenlijst aaaAzure - Azure woordenlijst | Microsoft Docs
description: Hello Azure verklarende woordenlijst toounderstand cloud terminologie op Hallo Azure-platform gebruiken. Deze korte Azure woordenlijst bevat definities voor algemene voorwaarden van de cloud voor Azure.
keywords: Woordenlijst voor Azure, cloud terminologie, Azure verklarende woordenlijst, termen die, cloud-voorwaarden
services: na
documentationcenter: na
author: MonicaRush
manager: jhubbard
editor: 
ms.assetid: d7ac12f7-24b5-4bcd-9e4d-3d76fbd8d297
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: monicar
ms.openlocfilehash: 486bbbfc71a48a6ebc39b14f7ab71f8604b7a6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-glossary-a-dictionary-of-cloud-terminology-on-hello-azure-platform"></a>Verklarende woordenlijst voor Microsoft Azure: een dictionary van cloud-terminologie op Hallo Azure-platform

Hallo-verklarende woordenlijst voor Microsoft Azure is een korte dictionary van cloud-terminologie voor hello Azure-platform. Zie ook:

* [Microsoft Azure en Amazon Web Services](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/) -definities van Azure-services en hun AWS-equivalenten.<!-- I propose toolink toohttps://azure.microsoft.com/en-us/services/ instead of this -->
* [Cloud computing voorwaarden](https://azure.microsoft.com/overview/cloud-computing-dictionary/) -algemeen bedrijfstak cloud voorwaarden.

## <a name="account"></a>Account
Een account dat is gebruikt tooaccess en het beheer van een Azure-abonnement. Heeft vaak een Azure-account Hoewel een account kan een van deze tooas: een bestaand werk, school, of persoonlijke Microsoft-account of een Office 365-gebruikersnaam en wachtwoord. U kunt ook maken een toomanage account een Azure-abonnement als u zich aanmeldt voor Hallo [gratis proefversie](https://azure.microsoft.com).  
Zie [aanmelden voor een Azure-abonnement met uw Office 365-account](billing/billing-use-existing-office-365-account-azure-subscription.md) en [Accounts kunt u toosign in](active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="api-app"></a>API-app
Een andere naam voor [App Service-app](#app-service-app).

## <a name="app-service-app"></a>App Service-app
Hallo rekenresources die [Azure App Service](app-service/app-service-value-prop-what-is.md) biedt voor het hosten van een [website of webtoepassing](app-service-web/app-service-web-overview.md), [web-API](app-service-api/app-service-api-apps-why-best-platform.md), of [back-end voor mobiele app](app-service-mobile/app-service-mobile-value-prop.md). App Service-apps zijn ook waarnaar wordt verwezen tooas *App Services*, *web-apps*, *API-apps*, en *mobiele apps*.

## <a name="availability-set"></a>Beschikbaarheidsset
Een verzameling van virtuele machines die worden beheerd samen tooprovide toepassing redundantie en betrouwbaarheid. Hallo-gebruik van een beschikbaarheidsset zorgt ervoor dat tijdens beide gepland of ongepland onderhoud ten minste één virtuele machine beschikbaar is.  
Zie [beheren van de beschikbaarheid van virtuele machines van Windows hello](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en [Hallo beschikbaarheid van Linux virtuele machines beheren](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="classic-model"></a>Azure klassieke implementatiemodel
Twee [implementatiemodellen](resource-manager-deployment-model.md) toodeploy resources in Azure gebruikt (Hallo nieuw model is Azure Resource Manager). Sommige Azure-services ondersteunen alleen Hallo Resource Manager-implementatiemodel, sommige browsers ondersteunen alleen Hallo-klassieke implementatiemodel en sommige ondersteunen beide. Hallo-documentatie voor elke Azure-service geeft aan welke modellen ondersteunen.

## <a name="cli"></a>Azure-opdrachtregelinterface (CLI)
Een opdrachtregelinterface die gebruikt toomanage worden kunnen Azure-services van Windows, Mac OS- en Linux.  Bepaalde services of functies van de service kunnen alleen via PowerShell of CLI Hallo worden beheerd. Zie [Azure CLI 2.0](/cli/azure/overview)

## <a name="powershell"></a>Azure PowerShell
Een opdrachtregelinterface toomanage Azure-services via een opdrachtregel van Windows-pc's. Bepaalde services of functies van de service kunnen alleen via PowerShell of CLI Hallo worden beheerd.
Zie [hoe tooinstall Azure PowerShell en configureren](/powershell/azure/overview)

## <a name="arm-model"></a>Azure Resource Manager-implementatiemodel
Twee [implementatiemodellen](resource-manager-deployment-model.md) toodeploy resources gebruikt in Microsoft Azure (Hallo andere is Hallo klassieke implementatiemodel). Sommige Azure-services ondersteunen alleen Hallo Resource Manager-implementatiemodel, sommige browsers ondersteunen alleen Hallo-klassieke implementatiemodel en sommige ondersteunen beide. Hallo-documentatie voor elke Azure-service geeft aan welke modellen ondersteunen.

## <a name="fault-domain"></a>Foutdomein
verzameling van virtuele machines in een beschikbaarheidsset dat mogelijk niet kan op Hallo dezelfde Hallo tijd. Een voorbeeld is een groep van virtuele machines in een rek die een gemeenschappelijk power-bron- en switch delen. In Azure gescheiden zijn automatisch Hallo virtuele machines in een beschikbaarheidsset in meerdere domeinen met fouten.  
Zie [beheren van de beschikbaarheid van virtuele machines van Windows hello](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) of [Hallo beschikbaarheid van Linux virtuele machines beheren](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)  

## <a name="geo"></a>geografisch
De grens van een gedefinieerd voor de hand van gegevens vestigingsplaats waarin doorgaans twee of meer regio's. Hallo grenzen mogelijk binnen of buiten de grenzen voor nationale en zijn beïnvloed door BTW-instelling. Elke geo heeft ten minste één regio. Voorbeelden van geografische gebieden zijn Azië en Stille Oceaan en Japan. Ook wel *Geografie*.  
Zie [Azure-regio's](best-practices-availability-paired-regions.md)

## <a name="geo-replication"></a>geo-replicatie
Hallo-proces voor het repliceren van inhoud zoals blobs, tabellen en wachtrijen in een combinatie van regionale automatisch.  
Zie [actieve Geo-replicatie voor Azure SQL-Database](sql-database/sql-database-geo-replication-overview.md)
<!-- hello meaning of "geo" in this term seems toobe different than hello meaning provided in hello "geo" entry -->

## <a name="image"></a>Afbeelding
Een bestand dat Hallo-besturingssysteem en de configuratie van de toepassing die gebruikt toocreate worden kan bevat een willekeurig aantal virtuele machines. In Azure zijn twee typen installatiekopieën: VM installatiekopie en de installatiekopie van het besturingssysteem. Een VM-installatiekopie bevat een besturingssysteem en alle schijven tooa virtuele machine gekoppeld wanneer het Hallo-installatiekopie is gemaakt. Een installatiekopie van het besturingssysteem bevat alleen een gegeneraliseerde besturingssysteem met schijfconfiguraties die geen gegevens.  
Zie [navigeren door en selecteer installatiekopieën van Windows virtuele machines in Azure met PowerShell of CLI Hallo](virtual-machines/windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="limits"></a>Limieten
Hallo aantal bronnen die kunnen worden gemaakt of Hallo prestaties benchmark die kan worden bereikt. Grenzen zijn meestal gekoppeld aan abonnementen, services en aanbiedingen.  
Zie [Azure-abonnement en Servicelimieten, quota's en beperkingen](azure-subscription-service-limits.md)

## <a name="load-balancer"></a>De load balancer
Een bron die binnenkomend verkeer op de computers in een netwerk distribueert. In Azure distribueert een load balancer verkeer toovirtual machines zijn gedefinieerd in een load balancer-set. Een [netwerktaakverdeler](load-balancer/load-balancer-overview.md) kan internetgerichte of interne kan zijn.  

## <a name="mobile-app"></a>mobiele app
Een andere naam voor [App Service-App](#app-service-app).

## <a name="offer"></a>Aanbieding
Hallo prijzen, tegoeden en verwante termen van toepassing tooan Azure-abonnement.  
Zie Hallo [detailpagina aanbieding voor Azure](https://azure.microsoft.com/support/legal/offer-details/)

## <a name="portal"></a>portal
Hallo beveiligde webportal toodeploy gebruikt en beheren van Azure-services.  Er zijn twee portals: Hallo [Azure-portal](http://portal.azure.com/) en Hallo [klassieke portal](http://manage.windowsazure.com/). Sommige services zijn beschikbaar in beide portals dat anderen alleen beschikbaar in een zijn of andere Hallo. Hallo [Azure portal beschikbaarheid grafiek](https://azure.microsoft.com/features/azure-portal/availability/) lijsten welke services beschikbaar in welke portal zijn.

## <a name="region"></a>Regio
Een gebied binnen een geografisch die niet snijpunt nationale grenzen en bevat een of meer datacenters. Prijzen regionale diensten en aanbiedingstypen beschikbaar worden gesteld op Hallo regioniveau. Een regio worden doorgaans gekoppeld aan een andere regio, wat kan up tooseveral honderden mijl verwijderd. Regionale paren kunnen worden gebruikt als een mechanisme voor herstel na noodgevallen en scenario's voor hoge beschikbaarheid. Ook wel aangeduid tooas *locatie*.  
Zie [Azure-regio's](best-practices-availability-paired-regions.md)

## <a name="resource"></a>Resource
Een item die deel uitmaakt van uw Azure-oplossing. Elke Azure-service kunt u verschillende soorten resources, zoals databases of virtuele machines toodeploy.   
Zie [overzicht van Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="resource-group"></a>resourcegroep
Een container in de Resource-Manager met verwante resources voor een toepassing. Hallo resourcegroep kan bevatten alle resources voor een toepassing hello of alleen de resources die logisch zijn gegroepeerd. U kunt bepalen hoe u resources tooallocate tooresource groepen op basis van het wat zinvol Hallo meeste voor uw organisatie.  
Zie [overzicht van Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="arm-template"></a>Resource Manager-sjabloon
Een of meer Azure-resources declaratief te definiëren en die afhankelijkheden tussen Hallo definieert een JSON-bestand geïmplementeerd resources. Hallo sjabloon zijn consistent en herhaaldelijk gebruikte toodeploy Hallo resources.  
Zie [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md)

## <a name="resource-provider"></a>Resourceprovider
Een service die Hallo resources levert die u kunt implementeren en beheren via Resource Manager. Elke resourceprovider biedt bewerkingen voor het werken met Hallo-resources die zijn geïmplementeerd. Resourceproviders kunnen worden geopend via hello Azure-portal, Azure PowerShell en diverse programming SDK's.  
Zie [overzicht van Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="role"></a>Rol
Een methode voor het beheren van toegang die toousers, groepen en services kan worden toegewezen. Rollen zijn kunnen tooperform acties zoals maken, beheren, en gelezen op Azure-resources.  
Zie [RBAC: ingebouwde rollen](active-directory/role-based-access-built-in-roles.md)

## <a name="sla"></a>serviceovereenkomst (SLA)
Hallo-overeenkomst die worden beschreven van Microsoft verbintenissen voor bedrijfstijd en connectiviteit. Elke Azure-service heeft een specifieke SLA.  
Zie [serviceovereenkomsten](https://azure.microsoft.com/support/legal/sla/)

## <a name="sas"></a>Shared access signature (SAS)
Een handtekening waarmee u toogrant beperkte toegang tooa resource, zonder dat de sleutel van uw account. Bijvoorbeeld: [SAS maakt gebruik van Azure Storage](storage/common/storage-dotnet-shared-access-signature-part-1.md) toogrant client access tooobjects zoals blobs. [IoT Hub gebruikt SAS](iot-hub/iot-hub-devguide-security.md#security-tokens) toogrant apparaten machtiging toosend telemetrie.

## <a name="storage-account"></a>Storage-account
Een account waarmee u toegang tot toohello Azure Blob, Queue, Table en bestand-services in Azure Storage. Hallo opslagaccountnaam definieert Hallo unieke naamruimte voor Azure Storage-gegevensobjecten.  
Zie [over Azure storage-accounts](storage/common/storage-create-storage-account.md)

## <a name="subscription"></a>abonnement
Een klant-overeenkomst met Microsoft waarmee deze tooobtain Azure services. Hallo abonnement prijzen en de bijbehorende voorwaarden worden beheerst door het Hallo-aanbieding voor abonnement Hallo gekozen.
Zie [Microsoft Online Subscription overeenkomst](https://azure.microsoft.com/support/legal/subscription-agreement/) en [hoe Azure-abonnementen worden gekoppeld aan Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md)

## <a name="tag"></a>Label
Een indexering term waarmee u toocategorize bronnen op basis van tooyour vereisten voor het beheer of facturering. Wanneer u een complexe verzameling resources hebt, kunt u codes toovisualize deze assets op Hallo manier die zinvol Hallo meeste. U kunt bijvoorbeeld resources die een vergelijkbare rol vervullen in uw organisatie of toohello behoren labelen dezelfde afdeling.  
Zie [Using tags tooorganize uw Azure-resources](resource-group-using-tags.md)

## <a name="update-domain"></a>Bijwerken van domein
verzameling van virtuele machines in een beschikbaarheidsset die zijn bijgewerkt op Hallo Hallo hetzelfde moment. Virtuele machines in Hallo hetzelfde updatedomein tegelijk opnieuw zijn opgestart tijdens gepland onderhoud. Azure start nooit meer dan één updatedomein tegelijk. Ook wel aangeduid tooas een upgradedomein.  
Zie [beheren van de beschikbaarheid van virtuele machines van Windows hello](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en [Hallo beschikbaarheid van Linux virtuele machines beheren](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vm"></a>virtuele machine
Hallo software-implementatie van een fysieke computer waarop een besturingssysteem wordt uitgevoerd. Meerdere virtuele machines tegelijkertijd op kunt uitvoeren Hallo dezelfde hardware. In Azure zijn virtuele machines in een aantal verschillende grootten beschikbaar.  
Zie [documentatie Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/)

## <a name="vm-extension"></a>extensie van virtuele machine
Een bron die gedrag of functies waarmee een andere programma's een werk- of Hallo mogelijkheid bieden voor toointeract met een actieve computer implementeert. U kan bijvoorbeeld Hallo toegang van de VM-extensie tooreset gebruiken of wijzigen van waarden voor externe toegang op een virtuele machine van Azure.
<!-- This definition seems obscure toome; maybe a list of examples would work better than a conceptual definition? -->
Zie [over uitbreidingen van de virtuele machine en -functies (Windows)](virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) of [over uitbreidingen van de virtuele machine en -functies (Linux)](virtual-machines/linux/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vnet"></a>virtueel netwerk
Een netwerk dat biedt connectiviteit tussen uw Azure-resources die is geïsoleerd van andere Azure tenants. Een [Azure VPN-Gateway](vpn-gateway/vpn-gateway-about-vpngateways.md) kunt u verbindingen maken tussen virtuele netwerken en [tussen een virtueel netwerk en een on-premises netwerk](vpn-gateway/vpn-gateway-plan-design.md). U kunt volledig Hallo IP-adresblokken, DNS-instellingen, beveiligingsbeleidsregels en routetabellen binnen een virtueel netwerk beheren.  
Zie [Virtual Network-overzicht](virtual-network/virtual-networks-overview.md)  

## <a name="web-app"></a>Web-app
Een andere naam voor [App Service-App](#app-service-app).

## <a name="see-also"></a>Zie ook

* [Aan de slag met Azure](https://azure.microsoft.com/get-started/)
* [Cloud-resources](https://azure.microsoft.com/resources/)  
* [Azure voor business-toepassing](https://azure.microsoft.com/overview/business-apps-on-azure/)
* [Azure in uw datacenter](https://azure.microsoft.com/overview/business-apps-on-azure/)

