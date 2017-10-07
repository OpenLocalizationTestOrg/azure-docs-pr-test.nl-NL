---
title: aaaUse Robomongo voor Azure Cosmos DB | Microsoft Docs
description: 'Meer informatie over hoe toouse Robomongo met een Cosmos Azure DB: API voor MongoDB-account'
keywords: robomongo
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 3018243e904015426dc69a69b26fb53421e1fe4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a>Robomongo gebruiken met een Cosmos Azure DB: API voor MongoDB-account
tooconnect tooan Azure Cosmos DB: de API voor Robomongo met MongoDB-account, moet u:

* Download en installeer [Robomongo](https://robomongo.org/)
* Uw Azure-Cosmos-DB hebben:-API voor MongoDB account [verbindingsreeks](connect-mongodb-account.md) informatie

## <a name="connect-using-robomongo"></a>Verbinding maken met behulp van Robomongo
tooadd uw Cosmos Azure DB:-API voor MongoDB account toohello Robomongo MongoDB-verbindingen uitvoeren Hallo stappen te volgen.

1. Ophalen van de Cosmos Azure DB:-API voor MongoDB verbinding accountgegevens Hallo instructies [hier](connect-mongodb-account.md).

    ![Schermopname van Hallo connection string-blade](./media/mongodb-robomongo/connectionstringblade.png)
2. Voer *Robomongo.exe*

3. Klikt u op Hallo verbinding onder **bestand** toomanage uw verbindingen. Klik vervolgens op **maken** in Hallo **MongoDB verbindingen** venster geopend Hallo **verbindingsinstellingen** venster.

4. In Hallo **verbindingsinstellingen** venster, kies een naam. Zoek vervolgens Hallo **Host** en **poort** van de verbindingsinformatie in stap 1 en voert u deze in **adres** en **poort**respectievelijk .

    ![Schermopname van het Hallo Robomongo-verbindingen beheren](./media/mongodb-robomongo/manageconnections.png)
5. Op Hallo **verificatie** tabblad **verificatie uitvoeren**. Voer vervolgens de Database (standaardwaarde is *Admin*), **gebruikersnaam** en **wachtwoord**.
Beide **gebruikersnaam** en **wachtwoord** vindt u in de verbindingsinformatie in stap 1.

    ![Schermopname van Hallo tabblad Robomongo-verificatie](./media/mongodb-robomongo/authentication.png)
6. Op Hallo **SSL** tabblad selectievakje **Gebruik SSL-protocol**, wijzigt u vervolgens Hallo **verificatiemethode** te**zelfondertekende certificaten**.

    ![Schermopname van Hallo Robomongo SSL-tabblad](./media/mongodb-robomongo/SSL.png)
7. Tot slot op **Test** tooverify kunnen tooconnect vervolgens te zijn **opslaan**.

## <a name="next-steps"></a>Volgende stappen
* Verkennen Azure Cosmos DB: API voor MongoDB [voorbeelden](mongodb-samples.md).
