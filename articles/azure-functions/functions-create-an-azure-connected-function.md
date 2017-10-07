---
title: een functie die verbinding tooAzure services maakt aaaCreate | Microsoft Docs
description: Gebruik van Azure Functions toocreate een toepassing zonder server die is verbonden tooother Azure services.
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: Azure-functies, functies, gebeurtenisverwerking, webhooks, dynamisch berekenen, architectuur zonder server
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 9d1f7d3b236f8d2c1a404c76aee410f6d458fb7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a>Gebruik van Azure Functions toocreate een functie die verbinding tooother Azure maakt services

Dit onderwerp leest u hoe een functie in Azure-functies die toomessages op een Azure Storage-wachtrij en kopieën op Hallo luistert toocreate berichten toorows in een tabel met Azure Storage. Een timerfunctie geactiveerd is gebruikte tooload berichten in wachtrij Hallo. Een tweede functie uit de wachtrij Hallo leest en schrijft van berichten toohello tabel. Hallo wachtrij zowel Hallo tabel zijn voor u gemaakt door Azure Functions op basis van Hallo binding definities. 

toomake dingen interessanter, een functie is geschreven in JavaScript en andere Hallo is geschreven in C# script. Dit laat zien hoe een functie-app functies in verschillende talen kan hebben. 

Dit scenario wordt uitgebeeld in een [video op kanaal 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).

## <a name="create-a-function-that-writes-toohello-queue"></a>Een functie die u toohello wachtrij schrijft maken

Voordat u tooa opslagwachtrij verbinden kunt, moet u een functie die wordt geladen Hallo berichtenwachtrij toocreate. Deze JavaScript-functie maakt gebruik van een timertrigger die een berichtenwachtrij toohello elke 10 seconden schrijft. Als u nog een Azure-account hebt, kijk dan eens Hallo [probeert Azure Functions](https://functions.azure.com/try) ondervindt, of [uw gratis Azure-account maken](https://azure.microsoft.com/free/).

1. Ga toohello Azure-portal en zoek de functie-app.

2. Klik op **Nieuwe functie** > **TimerTrigger-JavaScript**. 

3. Naam van de functie Hallo **FunctionsBindingsDemo1**, voer een waarde van de expressie cron van `0/10 * * * * *` voor **planning**, en klik vervolgens op **maken**.
   
    ![Een door een timer geactiveerde functie toevoegen](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    U hebt nu een door een timer geactiveerde functie gemaakt die elke 10 seconden wordt uitgevoerd.

5. Op Hallo **ontwikkelen** tabblad **logboeken** en Hallo activiteit in Hallo logboek bekijken. U ziet dat er elke 10 seconden een logboekvermelding wordt geschreven.
   
    ![Hallo logboek tooverify Hallo functie werkt weergeven](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a>Een uitvoerbinding voor de berichtenwachtrij toevoegen

1. Op Hallo **integreren** Kies **nieuwe uitvoer** > **Azure Queue Storage** > **Selecteer**.

    ![Een door een timer geactiveerde functie toevoegen](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. Voer `myQueueItem` voor **bericht parameternaam** en `functions-bindings` voor **wachtrijnaam**, selecteer een bestaande **Storage-account verbinding** of klik op **nieuwe** toocreate een opslag-account verbinding en klik vervolgens op **opslaan**.  

    ![Hallo uitvoer binding toohello opslagwachtrij maken](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. Terug in Hallo **ontwikkelen** tabblad, Hallo volgen code toohello functie toevoegen:
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. Zoek Hallo *als* instructie regel ongeveer 9 van Hallo-functie en insert Hallo volgende code na deze instructie.
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    Deze code maakt een **myQueueItem** en stelt de **tijd** eigenschap toohello Huidig timeStamp. Hallo nieuwe wachtrij-item toohello context van toegevoegd **myQueueItem** binding.

3. Klik op **Opslaan en uitvoeren**.

## <a name="view-storage-updates-by-using-storage-explorer"></a>Opslagupdates weergeven met behulp van Opslagverkenner
U kunt controleren of de functie werkt door berichten in wachtrij Hallo die u hebt gemaakt.  U kunt de opslagwachtrij tooyour verbinden via Cloud Explorer in Visual Studio. Hallo-portal maakt het echter eenvoudig tooconnect tooyour storage-account met behulp van Microsoft Azure Storage Explorer.

1. In Hallo **integreren** en klik op de wachtrij binding uitvoer > **documentatie**, zichtbaar Hallo verbindingsreeks voor uw opslagaccount te maken en kopieer Hallo-waarde. U deze waarde tooconnect tooyour storage-account gebruiken.

    ![Azure Opslagverkenner downloaden](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. Als u dat nog niet hebt gedaan, downloadt en installeert u [Microsoft Azure Opslagverkenner](http://storageexplorer.com). 
 
3. Klik in Opslagverkenner op Hallo tooAzure opslag pictogram verbinding en voltooi de wizard Hallo Hallo-verbindingsreeks in Hallo veld plakken.

    ![Een verbinding toevoegen in Opslagverkenner](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. Onder **lokale en gekoppelde**, vouw **Opslagaccounts** > uw storage-account > **wachtrijen** > **functies-bindingen**en controleer of dat berichten toohello wachtrij worden geschreven.

    ![Weergave van berichten in wachtrij Hallo](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    Als Hallo wachtrij niet bestaat of leeg is, is er waarschijnlijk een probleem met uw functiebinding of code.

## <a name="create-a-function-that-reads-from-hello-queue"></a>Maak een functie die uit de wachtrij Hallo lezen

Nu dat u berichten toohello wachtrij wordt toegevoegd hebt, kunt u een andere functie die uit de wachtrij Hallo leest en schrijft Hallo berichten permanent tooan Azure Storage-tabel.

1. Klik op **Nieuwe functie** > **QueueTrigger-CSharp**. 
 
2. Naam van de functie Hallo `FunctionsBindingsDemo2`, voer **functies bindingen** in Hallo **wachtrijnaam** veld, selecteer een bestaand opslagaccount of maak een en klik vervolgens op **maken**.

    ![Een timerfunctie voor de uitvoerwachtrij toevoegen](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. (Optioneel) U kunt controleren dat de nieuwe functie Hallo werkt door de nieuwe wachtrij Hallo in Opslagverkenner als voordat weer te geven. U kunt ook Cloud Explorer gebruiken in Visual Studio.  

4. (Optioneel) Hallo vernieuwen **functies bindingen** wachtrij en Let op dat items zijn verwijderd uit de wachtrij Hallo. Hallo verwijderen doet zich voor omdat Hallo functie gebonden toohello **functies bindingen** wachtrij lezen Hallo wachtrij en een trigger en Hallo-functie. 
 
## <a name="add-a-table-output-binding"></a>Een uitvoerverbinding voor de tabel toevoegen

1. Klik in FunctionsBindingsDemo2 op **Integreren** > **Nieuwe uitvoer** > **Azure Table Storage** > **Selecteren**.

    ![Een binding tooan Azure Storage-tabel toevoegen](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. Voer `functionbindings` in voor **Tabelnaam** en `myTable` voor **Naam van de tabelparameter**, kies een **Opslagaccountverbinding** of maak een nieuwe, en klik vervolgens op **Opslaan**.

    ![Hallo opslag tabelbinding configureren](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. In Hallo **ontwikkelen** tabblad, bestaande functiecode Hallo vervangen door de volgende Hallo:
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add hello item toohello table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    Hallo **TableItem** klasse vertegenwoordigt een rij in Hallo opslag tabel en toevoegen van Hallo item toohello `myTable` verzameling **TableItem** objecten. U moet instellen Hallo **PartitionKey** en **RowKey** eigenschappen toobe kunnen tooinsert in Hallo tabel.

4. Klik op **Opslaan**.  Ten slotte kunt u Hallo functie werkt door bekijkt hello tabel in Opslagverkenner of Visual Studio Cloud Explorer controleren.

5. (Optioneel) Vouw in uw opslagaccount in Opslagverkenner **tabellen** > **functionsbindings** en controleer of rijen toohello tabel worden toegevoegd. U kunt doen Hallo dezelfde in Cloud Explorer in Visual Studio.

    ![Weergave van rijen in de tabel Hallo](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    Als Hallo tabel niet bestaat of leeg is, is er waarschijnlijk een probleem met uw functiebinding of code. 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over Azure Functions Hallo volgende onderwerpen:

* [Naslaginformatie over Azure Functions voor ontwikkelaars](functions-reference.md)  
  Naslaginformatie voor programmeurs over het coderen van functies en het definiëren van triggers en bindingen.
* [Azure Functions testen](functions-test-a-function.md)  
  Beschrijft de verschillende hulpprogramma’s en technieken voor het testen van uw functies.
* [Hoe tooscale Azure Functions](functions-scale.md)  
  Beschrijft de serviceabonnementen die beschikbaar zijn met Azure Functions, zoals Hallo verbruik hosting plannings- en hoe toochoose Hallo juiste abonnement. 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

