---
title: een Azure DB die Cosmos-account via Azure Portal Hallo aaaManage | Microsoft Docs
description: "Meer informatie over hoe toomanage uw Cosmos Azure DB account via hello Azure-Portal. Een handleiding voor het gebruik van hello Azure Portal tooview, kopiëren, verwijderen en toegang tot accounts vinden."
keywords: Azure-Portal, documentdb, azure, Microsoft azure
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a>Hoe toomanage een Cosmos-DB Azure-account
Meer informatie over hoe tooset globale consistentie, in combinatie met sleutels en verwijderen van een Azure DB die Cosmos-account in hello Azure-portal.

## <a id="consistency"></a>Azure Cosmos DB consistentie instellingen beheren
Hallo rechts consistentieniveau selecteren, is afhankelijk van Hallo semantiek van uw toepassing. U moet vertrouwd raken met Hallo beschikbaar consistentieniveaus in Azure Cosmos DB door te lezen [met behulp van de consistentie niveaus toomaximize beschikbaarheid en prestaties in Azure Cosmos DB][consistency]. Azure Cosmos DB biedt consistentie, beschikbaarheid en prestaties garanties, op elk consistentieniveau beschikbaar voor het account van uw database. Configureren van uw databaseaccount met een sterke consistentie vereist dat uw gegevens beperkt tooa één Azure-regio is en niet algemeen beschikbaar. Op Hallo daarentegen, beperkte consistentieniveaus - gebonden veroudering, session of uiteindelijke inschakelen Hallo tooassociate u een willekeurig aantal Azure-regio's aan uw databaseaccount. Hallo eenvoudige stappen ziet u hoe tooselect Hallo consistentie standaardniveau voor het account van uw database. 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a>toospecify hello standaardconsistentie voor een Azure DB die Cosmos-account
1. In Hallo [Azure-portal](https://portal.azure.com/), toegang tot uw Azure DB die Cosmos-account.
2. Klik op Hallo accountblade **consistentie standaard**.
3. In Hallo **standaard consistentie** blade, selecteer Hallo nieuwe consistentieniveau en klik op **opslaan**.
    ![Standaard consistentie sessie][5]

## <a id="keys"></a>Weergeven, kopiëren en opnieuw genereren toegangstoetsen
Wanneer u een Azure DB die Cosmos-account maakt, genereert Hallo service twee master toegangstoetsen die kunnen worden gebruikt voor verificatie wanneer hello Azure DB die Cosmos-account wordt geopend. Dankzij twee toegangssleutels, kunnen Azure Cosmos DB tooregenerate Hallo sleutels met niets onderbreking tooyour Azure DB die Cosmos-account. 

In Hallo [Azure-portal](https://portal.azure.com/), toegang Hallo **sleutels** blade vanuit Hallo resource-menu op Hallo **Azure Cosmos DB account** blade tooview, kopiëren en opnieuw genereren Hallo toegangstoetsen die gebruikte tooaccess zijn uw Azure DB die Cosmos-account.

![Azure Portal schermafdruk is de blade sleutels](./media/manage-account/keys.png)

> [!NOTE]
> Hallo **sleutels** blade bevat primaire en secundaire verbindingsreeksen die gebruikt tooconnect tooyour worden kunnen rekening van Hallo [hulpprogramma voor gegevensmigratie](import-data.md).
> 
> 

Alleen-lezen sleutels zijn ook beschikbaar in deze blade. Lees- en query's zijn alleen-lezen-bewerkingen tijdens maakt, verwijderen, en vervangt niet.

### <a name="copy-an-access-key-in-hello-azure-portal"></a>Kopieer een toegangssleutel in hello Azure Portal
Op Hallo **sleutels** blade, klikt u op Hallo **kopie** knop toohello rechts van de sleutel Hallo gewenste toocopy.

![Bekijken en kopiëren van een toegangssleutel in hello Azure-Portal blade sleutels](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a>Toegangstoetsen genereren
Hallo sleutels tooyour Azure Cosmos DB toegangsaccount moet u regelmatig toohelp beter te beveiligen uw verbindingen. Twee toegangssleutels toegewezen tooenable u toomaintain verbindingen toohello Azure DB die Cosmos-account met behulp van één toegangssleutel terwijl u genereren Hallo andere toegangssleutel.

> [!WARNING]
> Opnieuw genereren van uw toegangssleutels is van invloed op alle toepassingen die afhankelijk van de huidige sleutel Hallo zijn. Alle clients die gebruikmaken van Hallo sleutel tooaccess hello Azure Cosmos DB toegangsaccount moet bijgewerkte toouse Hallo nieuwe sleutel.
> 
> 

Als u toepassingen of cloudservices met behulp van hello Azure DB die Cosmos-account hebt, wordt u Hallo verbinding verbroken als u opnieuw sleutels genereert, tenzij u uw sleutels rouleert. Hallo volgende stappen wordt uitgelegd Hallo-proces voor het implementeren van uw sleutels.

1. Hallo-toegangssleutel in uw toepassing code tooreference Hallo secundaire toegangssleutel van hello Azure DB die Cosmos-account bijwerken.
2. Opnieuw genereren Hallo primaire toegangssleutel voor uw Azure DB die Cosmos-account. In Hallo [Azure Portal](https://portal.azure.com/), toegang tot uw Azure DB die Cosmos-account.
3. In Hallo **Azure Cosmos-DB Account** blade, klikt u op **sleutels**.
4. Op Hallo **sleutels** blade, klikt u op Hallo opnieuw genereren en klik vervolgens op **Ok** tooconfirm dat u wilt dat een nieuwe sleutel toogenerate.
    ![Toegangstoetsen genereren](./media/manage-account/regenerate-keys.png)
5. Zodra u hebt gecontroleerd dat nieuwe Hallo-sleutel is beschikbaar voor gebruik bijwerken (ongeveer 5 minuten na het opnieuw genereren), Hallo toegangssleutel in uw toepassing code tooreference Hallo nieuwe primaire toegangssleutel.
6. Genereer de secundaire toegangssleutel Hallo opnieuw.
   
    ![Toegangstoetsen genereren](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> Het kan enkele minuten duren voordat een zojuist gegenereerde sleutel gebruikt tooaccess worden kan uw Azure DB die Cosmos-account.
> 
> 

## <a name="get-hello--connection-string"></a>Hallo-verbindingsreeks ophalen
tooretrieve uw verbinding tekenreeks, Hallo te volgen: 

1. In Hallo [Azure-portal](https://portal.azure.com), toegang tot uw Azure DB die Cosmos-account.
2. Hallo resource menu en klik op **sleutels**.
3. Klik op Hallo **kopie** knop volgende toohello **primaire verbindingsreeks** of **secundaire verbindingsreeks** vak. 

Als u de verbindingsreeks Hallo in Hallo [hulpprogramma voor migratie van Azure Cosmos DB Database](import-data.md), Hallo database naam toohello einde van de verbindingsreeks Hallo toevoegen. `AccountEndpoint=< >;AccountKey=< >;Database=< >`.

## <a id="delete"></a>Een Azure DB die Cosmos-account verwijderen
een Cosmos Azure DB tooremove account uit hello Azure-Portal die u niet langer gebruikt, klik met de rechtermuisknop Hallo accountnaam, en klik op **account verwijderen**.

![Hoe een Cosmos Azure DB toodelete account in Azure Portal Hallo](./media/manage-account/deleteaccount.png)

1. In Hallo [Azure-portal](https://portal.azure.com/), toegang tot hello Azure Cosmos DB account u wilt dat toodelete.
2. Op Hallo **Azure Cosmos DB account** blade met de rechtermuisknop op het Hallo-account en klik vervolgens op **Account verwijderen**. 
3. Typ op de resulterende bevestiging blade Hallo hello Azure Cosmos DB account naam tooconfirm gewenste toodelete Hallo-account.
4. Klik op Hallo **verwijderen** knop.

![Hoe een Cosmos Azure DB toodelete account in Azure Portal Hallo](./media/manage-account/delete-account-confirm.png)

## <a id="next"></a>Volgende stappen
Meer informatie over hoe te[aan de slag met uw account voor Azure Cosmos DB](http://go.microsoft.com/fwlink/p/?LinkId=402364).

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
