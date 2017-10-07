---
title: aaaEnable controle en diagnostische gegevens in Microsoft Azure | Microsoft Docs
description: Meer informatie over hoe tooset van diagnostische gegevens voor uw resources in Azure.
author: rboucher
manager: carolz
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: af1947a9-c211-4aa1-8924-880a86240be4
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 865d010c5846fff6d871e20eca2bc4ac35028354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-monitoring-and-diagnostics"></a>Controle en diagnose inschakelen
In Hallo [Azure Portal](https://portal.azure.com), kunt u uitgebreide, regelmatig, controle en diagnostische gegevens over uw resources. U kunt ook Hallo [REST-API](https://msdn.microsoft.com/library/azure/dn931932.aspx) of [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooconfigure diagnostische gegevens via een programma.

Diagnostische gegevens, bewaken en metriek gegevens in Azure wordt opgeslagen in een opslagaccount van uw keuze. Hiermee kunt u toouse ongeacht tooling u tooread Hallo gegevens vanuit een Opslagverkenner tooPower BI toothird derden tooling.

## <a name="when-you-create-a-resource"></a>Wanneer u een resource maken
De meeste services kunnen u tooenable diagnostische gegevens wanneer u ze eerst in Hallo maakt [Azure Portal](https://portal.azure.com).

1. Ga te**nieuw** en kiest u geïnteresseerd in het bent Hallo-resource.
2. Selecteer **optionele configuratie**.
    ![Blade diagnostische gegevens](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)
3. Selecteer **Diagnostics**, en klik op **op**. U moet toochoose Hallo Storage-account dat u wilt dat diagnostics toobe opgeslagen. U hebt in rekening gebracht normale gegevenskosten voor opslag en transacties wanneer u een opslagaccount voor diagnostische gegevens tooa verzendt.
4. Klik op **OK** en maak Hallo-resource.

## <a name="change-settings-for-an-existing-resource"></a>Instellingen voor een bestaande resource wijzigen
Als u al een resource hebt gemaakt en u toochange Hallo-instellingen voor diagnostische gegevens (toochange Hallo niveau van gegevensverzameling voor voorbeeld wilt), kunt u dit recht in hello Azure Portal doen.

1. Ga toohello resource en klikt u op Hallo **instellingen** opdracht.
2. Selecteer **Diagnostics**.
3. Hallo **Diagnostics** blade bevat alle Hallo mogelijke diagnostische gegevens en gegevens te verzamelen voor die bron bewaking. Voor enkele informatiebronnen die u kunt ook een **bewaren** beleid voor Hallo gegevens, tooclean het vanuit uw opslagaccount.
    ![Diagnostische gegevens van opslag](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)
4. Nadat u uw instellingen hebt gekozen, klikt u op Hallo **opslaan** opdracht. Het duurt even terwijl voor het bewaken van gegevens tooshow up als u zijn ingeschakeld voor Hallo eerst.

### <a name="categories-of-data-collection-for-virtual-machines"></a>Categorieën van gegevensverzameling voor virtuele machines
Voor virtuele machines worden alle logboeken en metrische gegevens vastgelegd met een interval van één minuut, zodat u kunt altijd Hallo meeste actuele informatie over uw computer.

* **Basismetrieken** : Health metrische gegevens over uw virtuele machine, zoals de processor en geheugen
* **Netwerk- en webmetriek** : metrische gegevens over uw netwerkverbindingen en -webservices
* **Metrische gegevens voor .NET** : metrische gegevens over Hallo .NET en ASP.NET-toepassingen op uw virtuele machine
* **SQL metrische gegevens** : als u werkt met Microsoft SQL-Service, de maatstaven voor prestaties
* **Windows-gebeurtenislogboeken toepassing** : Windows-gebeurtenissen die worden verzonden toohello toepassing kanaal
* **Windows-gebeurtenislogboeken system** : Windows-gebeurtenissen die worden verzonden toohello systeemkanaal. Dit omvat ook alle gebeurtenissen uit [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409).
* **Windows-gebeurtenislogboeken beveiliging** : Windows-gebeurtenissen die worden verzonden toohello beveiligingskanaal
* **Diagnostische gegevens infrastructuur logboeken** : logboekregistratie over Hallo diagnostics verzameling infrastructuur
* **IIS-logboeken** : logboeken over uw IIS-server

Houd er rekening mee dat op dit moment bepaalde Linux-distributies worden niet ondersteund en, Hallo Guest-Agent moet worden geïnstalleerd op Hallo virtuele machine.

## <a name="next-steps"></a>Volgende stappen
* [Ontvang waarschuwingsmeldingen](insights-receive-alert-notifications.md) wanneer er operationele gebeurtenissen plaatsvinden of metrische gegevens een drempelwaarde overschrijden.
* [Service metrische gegevens controleren](insights-how-to-customize-monitoring.md) toomake ervoor dat uw service beschikbaar is en reageert.
* [Aantal exemplaren automatisch schalen](insights-how-to-scale.md) toomake ervoor dat de schaal van uw service op basis van vraag.
* [Bewaken van toepassingsprestaties](../application-insights/app-insights-azure-web-apps.md) als u wilt dat toounderstand precies hoe uw code uitvoert in de cloud Hallo.
* [Weergeven van gebeurtenissen en het activiteitenlogboek](insights-debugging-with-events.md) toolearn alles wat u in uw service heeft plaatsgevonden.
* [Servicestatus bijhouden](insights-service-health.md) toofind uit wanneer Azure prestaties vermindering of service-onderbrekingen is opgetreden.

