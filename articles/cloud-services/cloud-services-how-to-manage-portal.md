---
title: beheertaken voor aaaCommon cloud service | Microsoft Docs
description: Meer informatie over hoe toomanage cloud-services in hello Azure-portal. Deze voorbeelden hello Azure-portal gebruiken.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
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

In Hallo **Cloudservices (klassiek)** gebied van hello Azure portal, kunt u de functie van een service of een implementatie bijwerken, promoveren van een gefaseerde implementatie tooproduction, resources tooyour cloudservice koppelen zodat u Hallo resource zien kunt afhankelijkheden en schaal Hallo resources samen en verwijder een cloudservice of een implementatie.

Meer informatie over hoe tooscale uw cloudservice beschikbaar is [hier](cloud-services-how-to-scale-portal.md).

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>Procedure: een functieservice van de cloud of implementatie bijwerken
Als u tooupdate Hallo toepassingscode voor de cloudservice moet, gebruikt **Update** op Hallo cloud service-blade. U kunt een enkele of alle functies bijwerken. tooupdate, kunt u een nieuw servicepakket of het serviceconfiguratiebestand uploaden.

1. In Hallo [Azure-portal][Azure portal], Hallo cloudservice u tooupdate wilt selecteren. Deze stap wordt geopend blade Hallo cloud service-exemplaar.
2. Klik op Hallo blade Hallo **Update** knop.

    ![Bijwerkknop](./media/cloud-services-how-to-manage-portal/update-button.png)

3. Hallo-implementatie met een nieuwe service-pakketbestand (.cspkg) en service-configuratiebestand (.cscfg) bijgewerkt.

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. **Eventueel** hello implementatielabel en Hallo storage-account bijwerken.
5. Als geen rollen hebt slechts één rolexemplaar, selecteert u Hallo **toch implementeren als een of meer rollen met één exemplaar** tooenable Hallo upgrade tooproceed.

    Azure kan alleen garanderen van 99,95% servicebeschikbaarheid tijdens een cloud service-update als elke rol ten minste twee rolexemplaren (virtuele machines heeft). Één virtuele machine verwerkt aanvragen van clients met twee rolexemplaren, terwijl andere hello wordt bijgewerkt.

6. Controleer **implementatie Start** toohave Hallo update toegepast nadat de upload Hallo van Hallo-pakket is voltooid.
7. Klik op **OK** toobegin Hallo service bijwerken.

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a>Procedure: een gefaseerde implementatie tooproduction voor implementaties toopromote wisselen
Als u besluit een nieuwe release van een cloudservice, fase toodeploy en testen van uw nieuwe release in uw cloud service-testomgeving. Gebruik **wisselen** tooswitch Hallo URL's door welke Hallo twee implementaties worden aangepakt en een nieuwe release tooproduction promoveren.

U kunt implementaties van Hallo omwisselen **Cloudservices** pagina of het Hallo-dashboard.

1. In Hallo [Azure-portal][Azure portal], Hallo cloudservice u tooupdate wilt selecteren. Deze stap wordt geopend blade Hallo cloud service-exemplaar.
2. Klik op Hallo blade Hallo **wisselen** knop.

    ![Wisseling van cloud-Services](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. Hallo volgende bevestiging wordt gevraagd wordt geopend.

    ![Wisseling van cloud-Services](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. Nadat u informatie over het implementeren van Hallo controleren, klikt u op **OK** tooswap Hallo implementaties.

    Hallo implementatie wisselen plaatsvindt snel omdat Hallo die wijzigingen alleen Hallo virtuele IP-adressen (VIP's heeft) voor Hallo-implementaties.

    toosave compute-kosten, kunt u verwijderen Hallo staging-implementatie nadat u hebt gecontroleerd of uw productie-implementatie werkt zoals verwacht.

### <a name="common-questions-about-swapping-deployments"></a>Veelgestelde vragen over het wisselen van implementaties

**Wat zijn Hallo-vereisten voor implementaties wisselen?**

Er zijn twee belangrijke vereisten voor een geslaagde implementatie wisseling:

- Als u toouse een statisch IP-adres voor de productiesite wilt, moet u één voor de faseringsite ook reserveren. Anders mislukt de Hallo wisselen.

- Alle exemplaren van uw rollen moeten worden uitgevoerd voordat u Hallo wisselen kunt uitvoeren. U kunt controleren Hallo status van uw exemplaren in de blade overzicht Hallo Hallo Azure-portal. U kunt ook hello gebruiken [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) opdracht in Windows PowerShell.

Gastbesturingssysteem updates en service operations herstel kan ook leiden tot implementatie worden verwisseld toofail. Zie voor meer informatie [problemen met cloud service-implementatie oplossen](cloud-services-troubleshoot-deployment-problems.md).

**Heeft een wisseling gevolgen voor de uitvaltijd voor de toepassing? Hoe moet ik verwerken?**

Zoals beschreven in de laatste sectie hello, is een wisseling implementatie doorgaans snelle omdat het een configuratiewijziging in hello Azure load balancer. In sommige gevallen kan echter kunt tien of meer seconden duren en leiden tot tijdelijke verbindingsfouten. toolimit impact tooyour klanten, Overweeg de implementatie van [client Pogingslogica](../best-practices-retry-general.md).

## <a name="how-to-link-a-resource-tooa-cloud-service"></a>Procedure: een bronservice tooa-cloud koppelen
Hello Azure-portal is niet gekoppeld aan resources samen zoals Hallo huidige klassieke Azure-portal biedt. In plaats daarvan implementeren aanvullende bronnen toohello dezelfde resourcegroep wordt gebruikt door Hallo Service in de Cloud.

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>Hoe: implementaties en een cloudservice verwijderen
Voordat u een cloudservice verwijderen kunt, moet u elke bestaande implementatie verwijderen.

toosave compute-kosten, kunt u verwijderen Hallo staging-implementatie nadat u hebt gecontroleerd of uw productie-implementatie werkt zoals verwacht. U wordt gefactureerd voor compute-kosten voor geïmplementeerde rolexemplaren die zijn gestopt.

Gebruik Hallo procedure toodelete na een implementatie of uw cloudservice.

1. In Hallo [Azure-portal][Azure portal], Hallo cloudservice u toodelete wilt selecteren. Deze stap wordt geopend blade Hallo cloud service-exemplaar.
2. Klik op Hallo blade Hallo **verwijderen** knop.

    ![Wisseling van cloud-Services](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. U kunt Hallo volledige in de cloudservice verwijderen door het controleren van **Cloud-service en implementaties** of kies een Hallo **productie-implementatie** of Hallo **voorbereide distributie**.

    ![Wisseling van cloud-Services](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. Klik op Hallo **verwijderen** knop Hallo onder aan.
5. toodelete Hallo-cloudservice, klikt u op **cloudservice verwijderen**. Klik vervolgens op Hallo bevestiging wordt gevraagd, op **Ja**.

> [!NOTE]
> Wanneer een cloudservice is verwijderd en uitgebreide bewaking is geconfigureerd, moet u Hallo gegevens handmatig verwijderen uit uw storage-account. Zie voor meer informatie over waar toofind metrische gegevens tabellen Hallo [dit](cloud-services-how-to-monitor.md) artikel.


## <a name="how-to-find-more-information-about-failed-deployments"></a>Hoe: meer informatie over mislukte implementaties
Hallo **overzicht** blade bevat een statusbalk Hallo bovenaan. Als u op de balk hello, wordt een nieuwe blade wordt geopend en wordt alle informatie over de fout weergegeven. Als het Hallo-implementatie bevat geen fouten, is Hallo informatie blade leeg.

![Wisseling van cloud-Services](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a>Volgende stappen
* [Algemene configuratie van uw cloudservice](cloud-services-how-to-configure-portal.md).
* Meer informatie over hoe te[implementeren van een cloudservice](cloud-services-how-to-create-deploy-portal.md).
* Configureer een [aangepaste domeinnaam](cloud-services-custom-domain-name-portal.md).
* Configureer [ssl-certificaten](cloud-services-configure-ssl-certificate-portal.md).
