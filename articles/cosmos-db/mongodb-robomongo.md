---
title: Robomongo gebruiken voor Azure Cosmos DB | Microsoft Docs
description: 'Informatie over het gebruik van Robomongo met een Cosmos Azure DB: API voor MongoDB-account'
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
ms.openlocfilehash: 8983594776a1bbe413a6d7cf2cd518f0e327648a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="299e3-104">Robomongo gebruiken met een Cosmos Azure DB: API voor MongoDB-account</span><span class="sxs-lookup"><span data-stu-id="299e3-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span></span>
<span data-ttu-id="299e3-105">Verbinding maken met een Cosmos Azure DB: de API voor Robomongo met MongoDB-account, moet u:</span><span class="sxs-lookup"><span data-stu-id="299e3-105">To connect to an Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="299e3-106">Download en installeer [Robomongo](https://robomongo.org/)</span><span class="sxs-lookup"><span data-stu-id="299e3-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="299e3-107">Uw Azure-Cosmos-DB hebben:-API voor MongoDB account [verbindingsreeks](connect-mongodb-account.md) informatie</span><span class="sxs-lookup"><span data-stu-id="299e3-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="299e3-108">Verbinding maken met behulp van Robomongo</span><span class="sxs-lookup"><span data-stu-id="299e3-108">Connect using Robomongo</span></span>
<span data-ttu-id="299e3-109">Toevoegen van uw Azure-Cosmos-DB: API voor MongoDB-account voor de Robomongo MongoDB-verbindingen, de volgende stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="299e3-109">To add your Azure Cosmos DB: API for MongoDB account to the Robomongo MongoDB Connections, perform the following steps.</span></span>

1. <span data-ttu-id="299e3-110">Ophalen van de Cosmos Azure DB:-API voor MongoDB verbinding accountgegevens van de instructies [hier](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="299e3-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using the instructions [here](connect-mongodb-account.md).</span></span>

    ![Schermopname van de connection string-blade](./media/mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="299e3-112">Voer *Robomongo.exe*</span><span class="sxs-lookup"><span data-stu-id="299e3-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="299e3-113">Klik op de verbindingsknop onder **bestand** voor het beheren van uw verbindingen.</span><span class="sxs-lookup"><span data-stu-id="299e3-113">Click the connection button under **File** to manage your connections.</span></span> <span data-ttu-id="299e3-114">Klik vervolgens op **maken** in de **MongoDB verbindingen** venster wordt geopend de **verbindingsinstellingen** venster.</span><span class="sxs-lookup"><span data-stu-id="299e3-114">Then, click **Create** in the **MongoDB Connections** window, which will open up the **Connection Settings** window.</span></span>

4. <span data-ttu-id="299e3-115">In de **verbindingsinstellingen** venster, kies een naam.</span><span class="sxs-lookup"><span data-stu-id="299e3-115">In the **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="299e3-116">Zoek vervolgens de **Host** en **poort** van de verbindingsinformatie in stap 1 en voert u deze in **adres** en **poort**respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="299e3-116">Then, find the **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![Schermopname van de verbindingen Robomongo beheren](./media/mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="299e3-118">Op de **verificatie** tabblad **verificatie uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="299e3-118">On the **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="299e3-119">Voer vervolgens de Database (standaardwaarde is *Admin*), **gebruikersnaam** en **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="299e3-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="299e3-120">Beide **gebruikersnaam** en **wachtwoord** vindt u in de verbindingsinformatie in stap 1.</span><span class="sxs-lookup"><span data-stu-id="299e3-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Schermopname van het tabblad Robomongo verificatie](./media/mongodb-robomongo/authentication.png)
6. <span data-ttu-id="299e3-122">Op de **SSL** tabblad selectievakje **Gebruik SSL-protocol**, wijzigt u vervolgens de **verificatiemethode** naar **zelfondertekende certificaten**.</span><span class="sxs-lookup"><span data-stu-id="299e3-122">On the **SSL** tab, check **Use SSL protocol**, then change the **Authentication Method** to **Self-signed Certificate**.</span></span>

    ![Schermopname van het SSL-tabblad Robomongo](./media/mongodb-robomongo/SSL.png)
7. <span data-ttu-id="299e3-124">Tot slot op **Test** om te controleren of u verbinding maken, klikt u vervolgens **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="299e3-124">Finally, click **Test** to verify that you are able to connect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="299e3-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="299e3-125">Next steps</span></span>
* <span data-ttu-id="299e3-126">Verkennen Azure Cosmos DB: API voor MongoDB [voorbeelden](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="299e3-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
