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
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="02bb5-104">Robomongo gebruiken met een Cosmos Azure DB: API voor MongoDB-account</span><span class="sxs-lookup"><span data-stu-id="02bb5-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span></span>
<span data-ttu-id="02bb5-105">tooconnect tooan Azure Cosmos DB: de API voor Robomongo met MongoDB-account, moet u:</span><span class="sxs-lookup"><span data-stu-id="02bb5-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="02bb5-106">Download en installeer [Robomongo](https://robomongo.org/)</span><span class="sxs-lookup"><span data-stu-id="02bb5-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="02bb5-107">Uw Azure-Cosmos-DB hebben:-API voor MongoDB account [verbindingsreeks](connect-mongodb-account.md) informatie</span><span class="sxs-lookup"><span data-stu-id="02bb5-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="02bb5-108">Verbinding maken met behulp van Robomongo</span><span class="sxs-lookup"><span data-stu-id="02bb5-108">Connect using Robomongo</span></span>
<span data-ttu-id="02bb5-109">tooadd uw Cosmos Azure DB:-API voor MongoDB account toohello Robomongo MongoDB-verbindingen uitvoeren Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="02bb5-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello Robomongo MongoDB Connections, perform hello following steps.</span></span>

1. <span data-ttu-id="02bb5-110">Ophalen van de Cosmos Azure DB:-API voor MongoDB verbinding accountgegevens Hallo instructies [hier](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="02bb5-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Schermopname van Hallo connection string-blade](./media/mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="02bb5-112">Voer *Robomongo.exe*</span><span class="sxs-lookup"><span data-stu-id="02bb5-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="02bb5-113">Klikt u op Hallo verbinding onder **bestand** toomanage uw verbindingen.</span><span class="sxs-lookup"><span data-stu-id="02bb5-113">Click hello connection button under **File** toomanage your connections.</span></span> <span data-ttu-id="02bb5-114">Klik vervolgens op **maken** in Hallo **MongoDB verbindingen** venster geopend Hallo **verbindingsinstellingen** venster.</span><span class="sxs-lookup"><span data-stu-id="02bb5-114">Then, click **Create** in hello **MongoDB Connections** window, which will open up hello **Connection Settings** window.</span></span>

4. <span data-ttu-id="02bb5-115">In Hallo **verbindingsinstellingen** venster, kies een naam.</span><span class="sxs-lookup"><span data-stu-id="02bb5-115">In hello **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="02bb5-116">Zoek vervolgens Hallo **Host** en **poort** van de verbindingsinformatie in stap 1 en voert u deze in **adres** en **poort**respectievelijk .</span><span class="sxs-lookup"><span data-stu-id="02bb5-116">Then, find hello **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![Schermopname van het Hallo Robomongo-verbindingen beheren](./media/mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="02bb5-118">Op Hallo **verificatie** tabblad **verificatie uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="02bb5-118">On hello **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="02bb5-119">Voer vervolgens de Database (standaardwaarde is *Admin*), **gebruikersnaam** en **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="02bb5-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="02bb5-120">Beide **gebruikersnaam** en **wachtwoord** vindt u in de verbindingsinformatie in stap 1.</span><span class="sxs-lookup"><span data-stu-id="02bb5-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Schermopname van Hallo tabblad Robomongo-verificatie](./media/mongodb-robomongo/authentication.png)
6. <span data-ttu-id="02bb5-122">Op Hallo **SSL** tabblad selectievakje **Gebruik SSL-protocol**, wijzigt u vervolgens Hallo **verificatiemethode** te**zelfondertekende certificaten**.</span><span class="sxs-lookup"><span data-stu-id="02bb5-122">On hello **SSL** tab, check **Use SSL protocol**, then change hello **Authentication Method** too**Self-signed Certificate**.</span></span>

    ![Schermopname van Hallo Robomongo SSL-tabblad](./media/mongodb-robomongo/SSL.png)
7. <span data-ttu-id="02bb5-124">Tot slot op **Test** tooverify kunnen tooconnect vervolgens te zijn **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="02bb5-124">Finally, click **Test** tooverify that you are able tooconnect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02bb5-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="02bb5-125">Next steps</span></span>
* <span data-ttu-id="02bb5-126">Verkennen Azure Cosmos DB: API voor MongoDB [voorbeelden](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="02bb5-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
