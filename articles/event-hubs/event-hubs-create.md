---
title: een Azure event hub aaaCreate | Microsoft Docs
description: Maak een Azure Event Hubs-naamruimte en een event hub met hello Azure-portal
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a>Maak een Event Hubs-naamruimte en een event hub met hello Azure-portal

## <a name="create-an-event-hubs-namespace"></a>Een Event Hubs-naamruimte maken
1. Meld u aan toohello [Azure-portal][Azure portal], en klik op **nieuw** op Hallo linksboven welkomstscherm.
1. Klik op **Internet der dingen**, en klik vervolgens op **Event Hubs**.
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. In Hallo **naamruimte maken** blade, voer de naam van een naamruimte. Hallo-systeem wordt onmiddellijk toosee gecontroleerd als Hallo naam beschikbaar is.
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. Nadat u hebt ervoor Hallo naamruimtenaam is beschikbaar, kies Hallo prijscategorie (basis of standaard). Ook een Azure-abonnement, resourcegroep en locatie kiezen in welke toocreate Hallo-resource. 
1. Klik op **maken** toocreate Hallo naamruimte. Mogelijk hebt u toowait een paar minuten voordat Hallo toofully inrichten Hallo systeembronnen.
2. Klik in de Hallo portal lijst met naamruimten, Hallo zojuist-naamruimte gemaakt.
2. Klik op **gedeeld toegangsbeleid**, en klik vervolgens op **RootManageSharedAccessKey**.
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. Klik op Hallo kopie knop toocopy Hallo **RootManageSharedAccessKey** connection string toohello Klembord. Sla deze verbindingsreeks in een tijdelijke locatie, zoals Kladblok, toouse later.
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a>Een Event Hub maken

1. Klik op nieuw gemaakte Hallo naamruimte in Hallo Event Hubs naamruimte lijst.      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. Klik op Hallo naamruimte blade **Event Hubs**.
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. Klik boven Hallo van Hallo-blade op **Event Hub toevoegen**.
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. Typ een naam voor uw event hub en klik vervolgens op **maken**.
   
    ![](./media/event-hubs-create/create-event-hub5.png)

Uw event hub is nu gemaakt en u hebt de verbindingsreeksen Hallo u toosend nodig hebt en gebeurtenissen ontvangen.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over Event Hubs, gaat u naar deze koppelingen:

* [Event Hubs-overzicht](event-hubs-what-is-event-hubs.md)
* [Event Hubs-API-overzicht](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/