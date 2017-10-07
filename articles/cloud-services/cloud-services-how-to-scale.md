---
title: een cloudservice aaaAuto schalen in de klassieke portal Hallo | Microsoft Docs
description: (klassiek) Meer informatie over hoe toouse Hallo regels voor klassieke portal tooconfigure automatisch schalen voor een cloud service-Webrol of worker-rol in Azure.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a>Hoe tooconfigure automatisch schalen voor een Cloudservice in de klassieke portal Hallo
> [!div class="op_single_selector"]
> * [Azure Portal](cloud-services-how-to-scale-portal.md)
> * [Klassieke Azure Portal](cloud-services-how-to-scale.md)

U kunt instellingen voor automatische voor uw Webrol of functie worker configureren op Hallo Scale pagina Hallo klassieke Azure-portal. U kunt ook handmatig schalen in plaats van automatisch schalen op basis van regels.

> [!NOTE]
> Dit artikel is gericht op Cloud Service-web- en werkrollen rollen. Wanneer u een virtuele machine (klassiek) rechtstreeks maakt, wordt deze gehost in een cloudservice. Sommige van deze informatie is van toepassing toothese typen virtuele machines. Schalen van een beschikbaarheidsset van virtuele machines wordt alleen afgesloten ze in- of uitschakelen op basis van Hallo scale regels die u configureert. Zie voor meer informatie over virtuele Machines en beschikbaarheidssets [beheren Hallo beschikbaarheid van virtuele Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

Hallo volgende informatie voordat u de schaal van uw toepassing configureren, moet u overwegen:

* Schalen wordt beïnvloed door de belangrijkste informatie over het gebruik.

    Grotere rolinstanties gebruik meer kernen. U kunt een toepassing alleen binnen het Hallo-limiet van kernen schalen voor uw abonnement. Bijvoorbeeld, Stel dat uw abonnement heeft een limiet van 20 kernen. Als u een toepassing met twee middelgrote cloudservices (in totaal 4 kernen) uitvoert, kunt u alleen opschalen andere cloud service-implementaties in uw abonnement door Hallo resterende 16 kernen. Zie voor meer informatie over grootten [Cloud Service Sizes](cloud-services-sizes-specs.md).

* U moet een wachtrij maken en deze koppelen aan een rol voordat u een toepassing op basis van een bericht drempelwaarde kunt schalen. Zie voor meer informatie [hoe toouse Queue Storage-Service Hallo](../storage/queues/storage-dotnet-how-to-use-queues.md).

* U kunt de resources die gekoppeld tooyour zijn schalen cloudservice. Zie voor meer informatie over het koppelen van resources [hoe: koppelen van een cloudservice voor resource tooa](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).

* tooenable hoge beschikbaarheid van uw toepassing, moet u zorgen dat deze wordt geïmplementeerd met twee of meer rolinstanties. Zie voor meer informatie [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).

## <a name="schedule-scaling"></a>Planning schalen
Standaard alle rollen niet op een specifiek schema. Daarom toepassing instellingen gewijzigd tooall tijdstippen en alle dagen in de loop Hallo jaar. Als u wilt, kunt u handmatig of automatisch schalen voor een van de volgende modi Hallo kunt instellen:

* Weekdagen
* Tijdens het weekend
* Week nachten
* Uitvoeren van de week
* Specifieke datums
* Specifiek datumbereik

Hallo planning instelling is geconfigureerd in Hallo [klassieke Azure-portal](https://manage.windowsazure.com/) op Hallo  
**Cloudservices** > **\[uw cloudservice\]** > **Scale** > **\[productie of Staging\]**  pagina.

Klik op Hallo **instellen van tijden waarop planning** knop voor elke rol die u wilt dat toochange.

![Cloudservice automatisch schalen op basis van een planning][scale_schedules]

## <a name="manual-scale"></a>Handmatig schalen
Op Hallo **Scale** pagina, u kunt handmatig vergroten of verkleinen Hallo aantal exemplaren in een cloudservice. Deze instelling is geconfigureerd voor elke schema dat u hebt gemaakt of tooall tijd als u een planning niet hebt gemaakt.

1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com/), klikt u op **Cloudservices**, en klik vervolgens op Hallo-naam van Hallo cloud service tooopen Hallo dashboard.
   
   > [!TIP]
   > Als u de cloudservice niet ziet, moet u mogelijk toochange van **productie** te**fasering** of vice versa.

2. Klik op **Scale**.
3. Hallo schema u opties voor schaling toochange wilt selecteren. *Geen geplande tijden* is Hallo standaard als er geen schema's gedefinieerd.
4. Hallo zoeken **schaal op metriek** sectie en selecteer ****. Dit is de standaardinstelling Hallo voor alle functies.
5. Elke rol in Hallo cloud-service heeft een schuifregelaar voor het wijzigen van het aantal exemplaren toouse Hallo.
   
    ![De functie van een cloud-service handmatig schalen][manual_scale]
   
    Als u meer exemplaren nodig hebt, moet u mogelijk toochange hello [cloud van de grootte van de virtuele machine service](cloud-services-sizes-specs.md).
6. Klik op **Opslaan**.  
   Rolinstanties worden toegevoegd of verwijderd op basis van uw selecties.

> [!TIP]
> Wanneer u ziet ![][tip_icon] uw tooit muis verplaatsen en u hulp over welke specifieke instelling komt.

## <a name="automatic-scale---cpu"></a>Automatische scale - CPU
Deze modus wordt geschaald als Hallo gemiddelde percentage van CPU-gebruik boven of onder de opgegeven drempelwaarden gaat. Rolinstanties zijn gemaakt of verwijderd als dit gebeurt.

1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com/), klikt u op **Cloudservices**, en klik vervolgens op Hallo-naam van Hallo cloud service tooopen Hallo dashboard.
   
   > [!TIP]
   > Als u de cloudservice niet ziet, moet u mogelijk toochange van **productie** te**fasering** of vice versa.

2. Klik op **Scale**.
3. Hallo schema u opties voor schaling toochange wilt selecteren. *Geen geplande tijden* is Hallo standaard als er geen schema's gedefinieerd.
4. Hallo zoeken **schaal op metriek** sectie en selecteer **CPU**.
5. U kunt nu een minimum en maximum aantal rollen instanties, Hallo doel CPU-gebruik (tootrigger een schaal van) en hoeveel exemplaren tooscale omhoog en omlaag door configureren.

![De functie van een cloud-service schalen door cpu-belasting][cpu_scale]

> [!TIP]
> Wanneer u ziet ![][tip_icon] uw tooit muis verplaatsen en u hulp over welke specifieke instelling komt.

## <a name="automatic-scale---queue"></a>Automatische scale - wachtrij
Deze modus wordt automatisch geschaald als het aantal berichten in een wachtrij Hallo boven of onder een bepaalde drempelwaarde vallen gaat. Rolinstanties zijn gemaakt of verwijderd als dit gebeurt.

1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com/), klikt u op **Cloudservices**, en klik vervolgens op Hallo-naam van Hallo cloud service tooopen Hallo dashboard.
   
   > [!TIP]
   > Als u de cloudservice niet ziet, moet u mogelijk toochange van **productie** te**fasering** of vice versa.

2. Klik op **Scale**.
3. Hallo zoeken **schaal op metriek** sectie en selecteer **wachtrij**.
4. U kunt nu een minimum en maximum aantal exemplaren van de functies, Hallo wachtrij en het aantal van de wachtrij berichten tooprocess voor elk exemplaar en hoeveel exemplaren tooscale omhoog en omlaag door configureren.

![De functie van een cloud-service schalen door een berichtenwachtrij][queue_scale]

> [!TIP]
> Wanneer u ziet ![][tip_icon] uw tooit muis verplaatsen en u hulp over welke specifieke instelling komt.

## <a name="scale-linked-resources"></a>Gekoppelde resources schalen
Vaak wanneer u een rol schalen, is een nuttig tooscale Hallo database die Hallo toepassing ook wordt gebruikt. Als u Hallo database toohello cloudservice koppelt, kunt u instellingen voor die bron schalen door te klikken op de desbetreffende koppeling Hallo Hallo openen.

1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com/), klikt u op **Cloudservices**, en klik vervolgens op Hallo-naam van Hallo cloud service tooopen Hallo dashboard.
   
   > [!TIP]
   > Als u de cloudservice niet ziet, moet u mogelijk toochange van **productie** te**fasering** of vice versa.

2. Klik op **Scale**.
3. Hallo zoeken **gekoppelde resources** sectie en klik op **scale voor deze database beheren**.
   
   > [!NOTE]
   > Als er geen een **gekoppelde resources** sectie u waarschijnlijk geen gekoppelde resources.

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
