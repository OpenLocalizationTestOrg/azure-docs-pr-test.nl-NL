---
title: beheertaken voor aaaCommon cloud-service (klassiek) | Microsoft Docs
description: Meer informatie over hoe toomanage cloud-services in Hallo klassieke Azure-portal.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 41a30e50-067c-485b-96fd-434a6d057abc
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 03b1d632f1480d0f65c87b7f8ffc747417acf7b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a>Hoe tooManage Cloud-Services
> [!div class="op_single_selector"]
> * [Azure Portal](cloud-services-how-to-manage-portal.md)
> * [Klassieke Azure Portal](cloud-services-how-to-manage.md)
>
>

In Hallo **Cloudservices** gebied Hallo klassieke Azure portal, kunt u de functie van een service of een implementatie bijwerken, promoveren van een gefaseerde implementatie tooproduction, resources tooyour cloudservice koppelen zodat u Hallo resource zien kunt afhankelijkheden en schaal Hallo resources samen en verwijder een cloudservice of een implementatie.

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>Procedure: een functieservice van de cloud of implementatie bijwerken
Als u tooupdate Hallo toepassingscode voor de cloudservice moet, gebruikt **Update** op Hallo dashboard **Cloudservices** pagina of **exemplaren** pagina. U kunt een enkele of alle functies bijwerken. U moet een nieuw servicepakket tooupload en serviceconfiguratiebestand.

1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com/), op Hallo dashboard **Cloudservices** pagina of **exemplaren** pagina, klikt u op **Update**.

    ![UpdateDeployment](./media/cloud-services-how-to-manage/CloudServices_UpdateDeployment.png)

2. In **implementatielabel**, voer een naam tooidentify Hallo implementatie (bijvoorbeeld mycloudservice4). U vindt de implementatielabel Hallo onder **snel starten** op Hallo-dashboard.
3. In **pakket**, gebruik **Bladeren** tooupload Hallo pakketbestand (.cspkg).
4. In **configuratie**, gebruik **Bladeren** tooupload Hallo service-configuratiebestand (.cscfg).
5. In **rol**, selecteer **alle** als u wilt dat tooupgrade alle rollen in Hallo cloudservice. tooperform één rol bijwerkt, worden de gewenste tooupdate Selecteer Hallo-rol. Zelfs als u een specifieke rol tooupdate selecteert, zijn Hallo-updates in het serviceconfiguratiebestand Hallo toegepaste tooall rollen.
6. Als u wijzigingen in de update Hallo hello aantal rollen of Hallo grootte van alle functies, selecteert u Hallo **update toestaan als grootten van de functie of het aantal rollen verandert** selectievakje tooenable Hallo update tooproceed.

    Let wel dat als u Hallo grootte van een rol (dat wil zeggen, Hallo grootte van een virtuele machine die als host fungeert voor een rolinstantie) wijzigen of het aantal rollen Hallo, elke rolinstantie (virtuele machine) siteservercomputer moet, en geen lokale gegevens gaan verloren.

7. Als een service-rollen slechts één rolexemplaar hebt, selecteert u Hallo **bijwerken, zelfs als een of meer rollen bevatten een selectievakje voor één exemplaar** tooenable Hallo upgrade tooproceed.

    Azure kan alleen garanderen van 99,95% servicebeschikbaarheid tijdens een cloud service-update als elke rol ten minste twee rolexemplaren (virtuele machines heeft). Waarmee een virtuele machine tooprocess clientaanvragen terwijl andere hello wordt bijgewerkt.

8. Klik op **OK** (ingeschakeld) toobegin Hallo service bijwerken.

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a>Procedure: een gefaseerde implementatie tooproduction voor implementaties toopromote wisselen
Gebruik **wisselen** toopromote een gefaseerde installatie implementatie van een cloud service tooproduction. Wanneer u een nieuwe release van een cloudservice toodeploy beslist, kunt u Faseren en testen van uw nieuwe release in uw cloud service-testomgeving terwijl uw klanten met de huidige release Hallo in productie. Wanneer u klaar bent toopromote Hallo nieuwe release tooproduction, kunt u **wisselen** tooswitch Hallo URL's door welke Hallo twee implementaties worden aangepakt.

U kunt implementaties van Hallo omwisselen **Cloudservices** pagina of het Hallo-dashboard.

1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com/), klikt u op **Cloudservices**.
2. Klik in de lijst van de Hallo van cloudservices, op Hallo cloud service tooselect deze.
3. Klik op **wisselen**.

    Hallo volgende bevestiging wordt gevraagd wordt geopend.

    ![Wisseling van cloud-Services](./media/cloud-services-how-to-manage/CloudServices_Swap.png)

4. Nadat u informatie over het implementeren van Hallo controleren, klikt u op **Ja** tooswap Hallo implementaties.

    Hallo implementatie wisselen plaatsvindt snel omdat Hallo die wijzigingen alleen Hallo virtuele IP-adressen (VIP's heeft) voor Hallo-implementaties.

    toosave compute-kosten, kunt u verwijderen Hallo-implementatie in Hallo staging-omgeving als u zeker weet dat Hallo nieuwe productie-implementatie wordt uitgevoerd zoals verwacht.

### <a name="common-questions-about-swapping-deployments"></a>Veelgestelde vragen over het wisselen van implementaties

**Wat zijn Hallo-vereisten voor implementaties wisselen?**

Er zijn twee belangrijke vereisten voor een geslaagde implementatie wisseling:

- Als u toouse een statisch IP-adres voor de productiesite wilt, moet u één voor de faseringsite ook reserveren. Anders mislukt Hallo wisselen.

- Alle exemplaren van uw rollen moeten worden uitgevoerd voordat u Hallo wisselen kunt uitvoeren. U kunt Hallo status controleren van uw exemplaren in Hallo klassieke Azure-portal of met behulp van [Hallo van de opdracht Get-AzureRole in Windows PowerShell](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0).

Houd er rekening mee dat Gast OS-updates en herstel van de operations-service kunnen ook worden veroorzaakt implementatie worden verwisseld toofail. Zie [problemen met cloud service-implementatie oplossen](cloud-services-troubleshoot-deployment-problems.md) voor meer informatie.

**Heeft een wisseling gevolgen voor de uitvaltijd voor de toepassing? Hoe moet ik verwerken?**

Zoals beschreven in de laatste sectie hello, is een wisseling implementatie meestal erg snel omdat het een configuratiewijziging in hello Azure load balancer. In sommige gevallen kan echter kunt tien of meer seconden duren en leiden tot tijdelijke verbindingsfouten. toolimit impact tooyour klanten, Overweeg de implementatie van [client Pogingslogica](../best-practices-retry-general.md).

## <a name="how-to-link-a-resource-tooa-cloud-service"></a>Procedure: een bronservice tooa-cloud koppelen
tooshow uw cloudservice afhankelijkheden van andere bronnen, kunt u een Azure SQL Database-exemplaar of een cloudservice voor toohello van storage-account koppelen. U kunt koppelen en ontkoppelen van bronnen op Hallo **gekoppelde Resources** pagina en vervolgens controleren hun gebruik op Hallo cloud service-dashboard. Als een gekoppeld opslagaccount bewaking ingeschakeld heeft, kunt u totaal aantal aanvragen op Hallo cloud servicedashboard kunt bewaken.

Gebruik **koppeling** toolink een nieuwe of bestaande SQL-Database-exemplaar of storage account tooyour cloudservice. U kunt vervolgens Hallo database samen met de Hallo cloud service-rol die wordt gebruikt op Hallo schalen **Scale** pagina. (Een opslagaccount schaalt automatisch als gebruik toeneemt.) Zie voor meer informatie [hoe tooScale een Cloudservice en de gekoppelde Resources](cloud-services-how-to-scale.md).

U ook kunt bewaken, beheren en schalen Hallo-database in Hallo **Databases** knooppunt Hallo klassieke Azure-portal.

Een resource in deze zin ' koppelen' biedt geen verbinding maken uw app toohello resource. Als u een nieuwe database via maakt **koppeling**, moet u tooadd Hallo verbinding tekenreeksen tooyour toepassingscode en vervolgens een upgrade uitvoeren Hallo-cloudservice. U moet de verbindingsreeksen tooadd als uw app gebruikmaakt van resources in een gekoppelde opslagaccount.

Hallo na procedure beschrijft hoe toolink een nieuw exemplaar van de SQL-Database geïmplementeerd op een nieuwe SQL-Database-server, tooa-cloudservice.

### <a name="toolink-a-sql-database-instance-tooa-cloud-service"></a>een cloudservice van SQL Database-exemplaar tooa toolink
1. In Hallo [klassieke Azure-portal](http://manage.windowsazure.com/), klikt u op **Cloudservices**. Klik vervolgens op Hallo-naam van Hallo cloud service tooopen Hallo dashboard.
2. Klik op **gekoppelde Resources**.

    Hallo **gekoppelde Resources** pagina wordt geopend.

    ![LinkedResourcesPage](./media/cloud-services-how-to-manage/CloudServices_LinkedResourcesPage.png)

3. Klik op **koppelen van een Resource** of **koppeling**.

    Hallo **koppeling Resource** wizard wordt gestart.

    ![Koppeling pagina 1](./media/cloud-services-how-to-manage/CloudServices_LinkedResources_LinkPage1.png)

4. Klik op **Maak een nieuwe resource** of **koppelen van een bestaande resource**.
5. Hallo type resource toolink kiezen. In Hallo [klassieke Azure-portal](http://manage.windowsazure.com/), klikt u op **SQL-Database**. (Alleen Hallo klassieke Azure-portal ondersteunt een cloudservice voor tooa van storage-account koppelen.)
6. toocomplete hello databaseconfiguratie, volg de instructies in de help voor Hallo **SQL-Databases** gebied Hallo klassieke Azure-portal.

    Hallo voortgang van Hallo bewerking in het berichtgedeelte Hallo koppelen, kunt u volgen.

    Wanneer koppelen voltooid is, kunt u Hallo status van de bron gekoppeld Hallo op Hallo cloud servicedashboard bewaken. Zie voor meer informatie over het schalen van een gekoppelde SQL-Database [hoe tooScale een Cloudservice en de gekoppelde Resources](cloud-services-how-to-scale.md).

### <a name="toounlink-a-linked-resource"></a>een gekoppelde resource toounlink
1. In Hallo [klassieke Azure-portal](http://manage.windowsazure.com/), klikt u op **Cloudservices**. Klik vervolgens op Hallo-naam van Hallo cloud service tooopen Hallo dashboard.
2. Klik op **gekoppelde Resources**, en selecteer vervolgens Hallo resource.
3. Klik op **ontkoppelen**. Klik vervolgens op **Ja** op Hallo bevestiging wordt gevraagd.

    Ontkoppelen van een SQL-Database heeft geen effect op Hallo of van de toepassing hello verbindingen toohello database. U kunt nog steeds beheren Hallo-database in Hallo **SQL-Databases** gebied Hallo klassieke Azure-portal.

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>Hoe: implementaties en een cloudservice verwijderen
Voordat u een cloudservice verwijderen kunt, moet u elke bestaande implementatie verwijderen.

toosave compute-kosten, kunt u de staging-implementatie verwijderen nadat u hebt gecontroleerd of uw productie-implementatie werkt zoals verwacht. U bent gefactureerd compute-kosten voor rolinstanties, zelfs als een cloudservice wordt niet uitgevoerd.

Gebruik Hallo procedure toodelete na een implementatie of uw cloudservice.

1. In Hallo [klassieke Azure-portal](http://manage.windowsazure.com/), klikt u op **Cloudservices**.
2. Hallo-cloudservice selecteren en klik vervolgens op **verwijderen**. (tooselect een cloudservice zonder te openen Hallo dashboard Klik ergens behalve Hallo-naam in het Hallo cloud service-item.)

    Als u een implementatie in test- of productieomgeving hebt, ziet u een menu met opties vergelijkbare toohello na een venster Hallo Hallo onder aan. Voordat u de cloudservice Hallo verwijderen kunt, moet u eventuele bestaande implementaties verwijderen.

    ![Menu verwijderen](./media/cloud-services-how-to-manage/CloudServices_DeleteMenu.png)

3. toodelete een implementatie, klikt u op **productie-implementatie verwijderen** of **verwijderen van fasering implementatie**. Klik vervolgens op Hallo bevestiging wordt gevraagd, op **Ja**.
4. Als u van plan toodelete Hallo-cloudservice bent, herhaalt u stap 3, indien nodig, uw andere implementatie toodelete.
5. toodelete Hallo-cloudservice, klikt u op **cloudservice verwijderen**. Klik vervolgens op Hallo bevestiging wordt gevraagd, op **Ja**.

> [!NOTE]
> Als uitgebreide bewaking is geconfigureerd voor uw cloudservice, wordt in Azure Hallo bewakingsgegevens van uw opslagaccount wanneer u de cloudservice Hallo verwijdert niet verwijderen. U moet handmatig toodelete Hallo gegevens. Zie voor meer informatie over waar toofind metrische gegevens tabellen Hallo ' How to: toegangsgegevens uitgebreide bewaking buiten de klassieke Azure-portal Hallo ' in [hoe tooMonitor Cloud Services](cloud-services-how-to-monitor.md).
>
>

## <a name="next-steps"></a>Volgende stappen
* [Algemene configuratie van uw cloudservice](cloud-services-how-to-configure.md).
* Meer informatie over hoe te[implementeren van een cloudservice](cloud-services-how-to-create-deploy.md).
* Configureer een [aangepaste domeinnaam](cloud-services-custom-domain-name.md).
* Configureer [ssl-certificaten](cloud-services-configure-ssl-certificate.md).
