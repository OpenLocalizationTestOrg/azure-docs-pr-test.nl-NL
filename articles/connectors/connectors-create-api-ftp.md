---
title: aaaLearn hoe toouse Hallo FTP-connector in logic apps | Microsoft Docs
description: Logic apps maken met Azure App service. Verbinding maken met uw bestanden tooFTP server toomanage. U kunt uitvoeren van verschillende acties zoals het uploaden, bijwerken, ophalen en verwijderen van bestanden in de FTP-server.
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a>Aan de slag met Hallo FTP-connector
Hallo FTP-connector toomonitor gebruiken, beheren en bestanden op een FTP-server maken. 

toouse [elke connector](apis-list.md), moet u eerst toocreate een logische app. U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooftp"></a>Verbinding maken met tooFTP
Om uw logische app toegang alle services tot, moet u eerst toocreate een *verbinding* toohello service. Een [verbinding](connectors-overview.md) biedt connectiviteit tussen een logische app en een andere service.  

### <a name="create-a-connection-tooftp"></a>Een tooFTP verbinding maken
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a>Een FTP-trigger te gebruiken
Een trigger is een gebeurtenis die gebruikt toostart Hallo werkstroom gedefinieerd in een logische app worden kan. [Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!IMPORTANT]
> Hallo FTP-connector vereist een FTP-server die toegankelijk is vanaf Internet Hallo en toooperate geconfigureerd met de passieve modus. Hallo FTP-connector is ook **niet compatibel met impliciete FTPS (FTP via SSL)**. Hallo FTP-connector ondersteunt alleen expliciete FTPS (FTP via SSL).  
> 
> 

In dit voorbeeld, leest u hoe toouse hello **FTP - wanneer een bestand wordt toegevoegd of gewijzigd** tooinitiate een logic app-werkstroom wordt geactiveerd wanneer een bestand wordt toegevoegd aan of gewijzigd op een FTP-server. In een enterprise-voorbeeld: u kunt deze trigger toomonitor een FTP-map voor nieuwe bestanden die die de orders van klanten vertegenwoordigt.  U kunt vervolgens een FTP-connector actie, zoals **bestandsinhoud ophalen** tooget Hallo inhoud van Hallo order voor verdere verwerking en opslag in uw orderdatabase.

1. Voer *ftp* Selecteer in het zoekvak Hallo op Hallo logic apps designer Hallo **FTP - wanneer een bestand wordt toegevoegd of gewijzigd** trigger   
   ![FTP-triggerafbeelding 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)  
   Hallo **wanneer een bestand wordt toegevoegd of gewijzigd** besturingselement wordt geopend  
   ![FTP-triggerafbeelding 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)  
2. Selecteer Hallo **...**  zich aan de rechterkant Hallo van Hallo-besturingselement. Hiermee opent u Hallo map kiezerbesturingselement  
   ![FTP-triggerafbeelding 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)  
3. Selecteer Hallo  **>**  (pijl naar rechts) en blader toofind Hallo map wilt u toomonitor voor nieuwe en gewijzigde bestanden. Selecteer Hallo-map en u ziet Hallo map wordt nu weergegeven in Hallo **map** besturingselement.  
   ![FTP-triggerafbeelding 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)   

Op dit moment is uw logische app geconfigureerd met een trigger die wordt gestart een uitvoering van Hallo andere triggers en acties in de werkstroom Hallo wanneer een bestand wordt gewijzigd of in Hallo specifieke FTP-map gemaakt. 

> [!NOTE]
> Voor een logische app toobe functionele, moet er ten minste één trigger en één actie bevatten. Hallo stappen in de volgende sectie tooadd een actie van Hallo.  
> 
> 

## <a name="use-a-ftp-action"></a>Gebruik een FTP-actie
Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app. [Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Nu u een trigger hebt toegevoegd, volgt u deze stappen tooadd een actie die u krijgt Hallo inhoud van Hallo nieuwe of gewijzigde bestand door Hallo trigger gevonden.    

1. Selecteer **+ een nieuwe stap** tooadd Hallo Hallo actie tooget Hallo inhoud van het Hallo-bestand op Hallo FTP-server  
2. Selecteer Hallo **een actie toevoegen** koppeling.  
   ![FTP-afbeelding 1](./media/connectors-create-api-ftp/ftp-action-1.png)  
3. Voer *FTP* toosearch voor alle acties tooFTP gerelateerd.
4. Selecteer **FTP - bestandsinhoud ophalen** zoals actie tootake Hallo als een nieuwe of gewijzigde bestand wordt gevonden in Hallo FTP-map.      
   ![FTP-afbeelding 2](./media/connectors-create-api-ftp/ftp-action-2.png)  
   Hallo **bestandsinhoud ophalen** beheren wordt geopend. **Opmerking**: u na vragen aan gebruiker tooauthorize uw logische app tooaccess uw FTP-server als u nog niet gedaan eerder account zijn.  
   ![FTP-afbeelding 3](./media/connectors-create-api-ftp/ftp-action-3.png)   
5. Selecteer Hallo **bestand** besturingselement (Hallo witruimte zich onder **bestand***). Hier kunt u een Hallo verschillende eigenschappen van Hallo nieuwe of gewijzigde bestand gevonden op Hallo FTP-server.  
6. Selecteer Hallo **inhoud bestand** optie.  
   ![FTP-afbeelding 4](./media/connectors-create-api-ftp/ftp-action-4.png)   
7. Hallo-besturingselement wordt bijgewerkt, die aangeeft dat Hallo **FTP - bestandsinhoud ophalen** actie krijgt Hallo *inhoud bestand* van Hallo nieuwe of gewijzigde bestand op Hallo FTP-server.      
   ![FTP-afbeelding 5](./media/connectors-create-api-ftp/ftp-action-5.png)     
8. Sla uw werk en vervolgens voegt u een bestand toohello FTP-map tootest uw werkstroom.    

Op dit moment Hallo logische app is geconfigureerd met een trigger toomonitor een map van een FTP-server en een werkstroom starten Hallo wanneer er een nieuw bestand of een gewijzigd bestand op Hallo FTP-server. 

Hallo logische app is ook geconfigureerd met een actie tooget Hallo inhoud van de nieuwe of gewijzigde bestand Hallo.

U kunt nu een andere actie zoals Hallo toevoegen [SQL Server - invoegrij](connectors-create-api-sqlazure.md) actie tooinsert Hallo inhoud van Hallo nieuwe of gewijzigde bestand in een SQL-databasetabel.  

## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/ftpconnector/). 

## <a name="next-steps"></a>Volgende stappen
[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md)

