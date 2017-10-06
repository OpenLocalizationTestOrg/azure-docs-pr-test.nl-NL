---
title: een cloudservice aaaAuto schalen in Hallo-portal | Microsoft Docs
description: Meer informatie over hoe toouse Hallo regels voor automatisch schalen portal tooconfigure voor een cloud service-Webrol of worker-rol in Azure.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 265f4c8ec5e1ec2f85585df25f18cd0d0c9946a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-portal"></a>Hoe tooconfigure automatisch schalen voor een Cloudservice in Hallo-portal
> [!div class="op_single_selector"]
> * [Azure Portal](cloud-services-how-to-scale-portal.md)
> * [Klassieke Azure Portal](cloud-services-how-to-scale.md)

Voorwaarden kunnen worden ingesteld voor een cloud service-werkrol die een schaal in- of opnieuw activeren. Hallo voorwaarden voor het Hallo-rol kunnen worden gebaseerd op Hallo CPU, schijf of netwerkbelasting van Hallo-rol. U kunt ook een voorwaarde op basis van een bericht wachtrij of Hallo metric van sommige andere Azure-resource die is gekoppeld aan uw abonnement instellen.

> [!NOTE]
> Dit artikel is gericht op Cloud Service-web- en werkrollen rollen. Wanneer u een virtuele machine (klassiek) rechtstreeks maakt, wordt deze gehost in een cloudservice. U kunt een standaard virtuele machine schalen door te koppelen met een [beschikbaarheidsset](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) en handmatig inschakelen of uitschakelen.

## <a name="considerations"></a>Overwegingen
Hallo volgende informatie voordat u de schaal van uw toepassing configureren, moet u overwegen:

* Schalen wordt beïnvloed door de belangrijkste informatie over het gebruik.

    Grotere rolinstanties gebruik meer kernen. U kunt een toepassing alleen binnen het Hallo-limiet van kernen schalen voor uw abonnement. Bijvoorbeeld, Stel dat uw abonnement heeft een limiet van 20 kernen. Als u een toepassing met twee middelgrote cloudservices (in totaal 4 kernen) uitvoert, kunt u alleen opschalen andere cloud service-implementaties in uw abonnement door Hallo resterende 16 kernen. Zie voor meer informatie over grootten [Cloud Service Sizes](cloud-services-sizes-specs.md).

* U kunt schalen op basis van een wachtrij bericht drempelwaarde. Voor meer informatie over het toouse wachtrijen, Zie [hoe toouse Queue Storage-Service Hallo](../storage/queues/storage-dotnet-how-to-use-queues.md).

* U kunt ook andere resources zijn gekoppeld aan uw abonnement schalen.

* tooenable hoge beschikbaarheid van uw toepassing, moet u zorgen dat deze wordt geïmplementeerd met twee of meer rolinstanties. Zie voor meer informatie [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).


## <a name="where-scale-is-located"></a>Waar schaal bevindt
Nadat u uw cloudservice selecteert, moet u Hallo cloud service blade zichtbaar hebben.

1. Op Hallo cloud service blade op Hallo **rollen en instanties** tegel, selecteer Hallo-naam van de cloudservice Hallo.   
   **BELANGRIJKE**: Zorg ervoor dat tooclick Hallo cloud service rol, niet Hallo rolinstantie die lager is dan het Hallo-rol.

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. Selecteer Hallo **scale** tegel.

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a>Automatische schaal
U kunt instellingen voor een rol configureren met de twee modi **handmatige** of **automatische**. Handmatige is zoals u zou verwachten, instellen van Hallo absolute telling van exemplaren. Automatische kunt u echter tooset regels die hoe en door het veel u bepalen wordt geschaald.

Set Hallo **schalen door** te optie**planning en prestaties regels**.

![Cloud services-schaalinstellingen met profiel en de regel](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. Een bestaand profiel.
2. Een regel voor Hallo bovenliggende profiel toevoegen.
3. Voeg een ander profiel.

Selecteer **profiel**. Hallo profiel bepaalt welke modus gewenste toouse voor Hallo schaal: **altijd**, **terugkeerpatroon**, **vaste datum**.

Nadat u hebt geconfigureerd profiel Hallo en regels, selecteert u Hallo **opslaan** pictogram Hallo bovenaan.

#### <a name="profile"></a>Profiel
Hallo profiel stelt minimum en maximum aantal exemplaren voor Hallo schalen en ook als het bereik van deze actief is.

* **Altijd**

    Bewaar dit bereik van de exemplaren beschikbaar.  

    ![Cloudservice, die altijd schalen](./media/cloud-services-how-to-scale-portal/select-always.png)
* **Terugkeerpatroon**

    Kies een set van de dagen van Hallo week tooscale.

    ![Cloud-service schalen met een terugkerende planning](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* **Vaste datum**

    Een vaste datum bereik tooscale Hallo rol.

    ![CLoud-service schalen met een vaste datum](./media/cloud-services-how-to-scale-portal/select-fixed.png)

Nadat u hebt geconfigureerd profiel hello, selecteert u Hallo **OK** knop Hallo Hallo profiel blade onderaan in.

#### <a name="rule"></a>Regel
Regels tooa profiel worden toegevoegd en vertegenwoordigen een voorwaarde waarmee Hallo schaal wordt geactiveerd.

Hallo regel trigger is gebaseerd op een waarde van de cloudservice hello (CPU-gebruik, schijfactiviteit of netwerkactiviteit) toowhich kunt u een waarde voor de voorwaarde toevoegen. U kunt bovendien Hallo-geactiveerd op basis van een bericht wachtrij of Hallo metric van sommige andere Azure-resource die is gekoppeld aan uw abonnement hebben.

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

Nadat u de regel Hallo hebt geconfigureerd, selecteert u Hallo **OK** knop Hallo Hallo regel blade onderaan in.

## <a name="back-toomanual-scale"></a>Back-toomanual schaal
Navigeer toohello [schalen instellingen](#where-scale-is-located) en set Hallo **schalen door** optie te**aantal instanties dat ik handmatig invoeren**.

![Cloud services-schaalinstellingen met profiel en de regel](./media/cloud-services-how-to-scale-portal/manual-basics.png)

Deze instelling verwijdert automatisch schalen uit Hallo-rol en vervolgens kunt u exemplaren Hallo rechtstreeks instellen.

1. optie voor Hallo schaal (handmatig of automatisch).
2. Een rol exemplaar schuifregelaar tooset Hallo exemplaren tooscale aan.
3. Exemplaren van Hallo rol tooscale aan.

Nadat u de schaalinstellingen Hallo hebt geconfigureerd, selecteert u Hallo **opslaan** pictogram Hallo bovenaan.
