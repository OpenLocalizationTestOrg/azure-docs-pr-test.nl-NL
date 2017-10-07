---
title: de verbindingsreeks aaaMongoDB voor een Azure DB die Cosmos-account | Microsoft Docs
description: Meer informatie over hoe tooconnect uw MongoDB app tooan Azure DB die Cosmos-account met behulp van een verbindingsreeks voor MongoDB.
keywords: mongodb-verbindingsreeks
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a>Verbinding maken met een MongoDB toepassing tooAzure Cosmos-DB
Meer informatie over hoe tooconnect uw MongoDB app tooan Azure DB die Cosmos-account met behulp van een verbindingsreeks voor MongoDB. U kunt vervolgens een Azure DB die Cosmos-database als Hallo gegevens opslaan voor uw app MongoDB. 

Deze zelfstudie biedt twee manieren verbindingsreeksgegevens tooretrieve:

- [Hallo snel starten methode](#QuickstartConnection), voor gebruik met .NET, Node.js, MongoDB-Shell, Java en Python-stuurprogramma's
- [tekenreeks van aangepaste verbindingsmethode Hallo](#GetCustomConnection), voor gebruik met andere stuurprogramma's

## <a name="prerequisites"></a>Vereisten

- Een Azure-account. Als u geen Azure-account hebt, maakt u een [gratis Azure-account](https://azure.microsoft.com/free/) nu. 
- Een Azure Cosmos DB-account. Zie voor instructies [bouwen van een web-app van de MongoDB-API met .NET en Azure-portal Hallo](create-mongodb-dotnet.md).

## <a id="QuickstartConnection"></a>Hallo MongoDB-verbindingsreeks ophalen met behulp van Hallo snel starten
1. Aanmelden in een internetbrowser toohello [Azure-portal](https://portal.azure.com).
2. In Hallo **Azure Cosmos DB** blade Selecteer Hallo-API voor MongoDB-account. 
3. Klik in het linkerdeelvenster Hallo van Hallo accountblade op **snel starten**. 
4. Kies uw platform (**.NET**, **Node.js**, **MongoDB-Shell**, **Java**, **Python**). Als er geen het hulpprogramma wordt weergegeven, of je--Documenteer we continu meer verbinding codefragmenten. Stuur een reactie hieronder op wat u wilt dat toosee. toolearn hoe toocraft uw eigen verbinding Lees [Hallo-account verbindingsreeksgegevens ophalen](#GetCustomConnection).
5. Kopieer en plak Hallo codefragment in uw app MongoDB.

    ![De blade snel starten](./media/connect-mongodb-account/QuickStartBlade.png)

## <a id="GetCustomConnection"></a>Hallo MongoDB connection string toocustomize ophalen
1. Aanmelden in een internetbrowser toohello [Azure-portal](https://portal.azure.com).
2. In Hallo **Azure Cosmos DB** blade Selecteer Hallo-API voor MongoDB-account. 
3. Klik in het linkerdeelvenster Hallo van Hallo accountblade op **verbindingsreeks**. 
4. Hallo **verbindingsreeks** blade wordt geopend. Alle Hallo informatie nodig tooconnect toohello account heeft met behulp van een stuurprogramma voor MongoDB, met inbegrip van een vooraf gedefinieerde verbindingsreeks.

    ![Connection String-blade](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a>Vereisten voor verbinding tekenreeks
> [!Important]
> Azure Cosmos DB heeft strenge beveiligingsvereisten en standaarden. Azure DB Cosmos-accounts vereist verificatie en veilige communicatie via *SSL*. 
>
>

Azure Cosmos DB ondersteunt Hallo standaard MongoDB URI indeling verbindingsreeks, met een aantal specifieke vereisten: Azure Cosmos DB accounts verificatie en veilige communicatie via SSL vereisen. Dus is indeling verbindingsreeks Hallo:

    mongodb://username:password@host:port/[database]?ssl=true

Hallo-waarden van deze tekenreeks zijn beschikbaar in Hallo **verbindingsreeks** blade eerder weergegeven:

* Gebruikersnaam (vereist): Azure DB die Cosmos-accountnaam.
* Wachtwoord (vereist): Azure Cosmos DB accountwachtwoord.
* Host (vereist): FQDN-naam van hello Azure DB die Cosmos-account.
* Poort (vereist): 10255.
* Database (optioneel): Hallo-database die Hallo verbinding wordt gebruikt. Als er geen database wordt opgegeven, is de standaarddatabase Hallo 'test'.
* SSL = true (vereist)

Denk bijvoorbeeld Hallo-account wordt weergegeven in Hallo **verbindingsreeks** blade. Er is een geldige verbindingsreeks:

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[MongoChef gebruiken](mongodb-mongochef.md) met een Azure Cosmos DB-API voor MongoDB-account.
* Hello Azure Cosmos DB-API voor MongoDB verkennen hand [voorbeelden](mongodb-samples.md).
