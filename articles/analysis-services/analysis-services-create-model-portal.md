---
title: een model in tabelvorm via hello Azure Analysis Services-webserver designer aaaCreate | Microsoft Docs
description: Meer informatie over hoe een model in tabelvorm Azure Analysis Services met behulp van toocreate Hallo webdesigner in Azure-portal.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: a37b326b76c84fc3a4300827bc1c8706b0584701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-model-in-azure-portal"></a>Een model maken in Azure portal

Hello Azure Analysis Services web designer (preview)-functie in Azure-portal biedt een snelle en gemakkelijke manier toocreate en -modellen in tabelvorm en query model direct in uw browser bewerken. 

Houd er rekening mee, Hallo webdesigner is **preview**. Functionaliteit is beperkt, terwijl de nieuwe functionaliteit alle Hallo tijd, in preview wordt toegevoegd. Voor meer geavanceerde model ontwikkelen en testen is het beste toouse Visual Studio (SSDT) en SQL Server Management Studio (SSMS).

## <a name="prerequisites"></a>Vereisten

- Een Azure Analysis Services-server op Hallo Standard of ontwikkelaar laag. Nieuwe modellen die zijn gemaakt met behulp van Hallo webdesigner zijn DirectQuery, wordt alleen ondersteund door deze lagen.
- Een Azure SQL Database, Azure SQL Data Warehouse of Power BI Desktop (pbix)-bestand als een gegevensbron. Nieuwe modellen gemaakt op basis van Power BI Desktop-ondersteuning voor Azure SQL Database, Azure SQL Data Warehouse, Oracle en Teradata-gegevensbronnen.
- Een SQL Server-account en wachtwoord voor het verbinden van tooAzure SQL-Database of Azure SQL Data Warehouse-gegevensbronnen.

## <a name="toocreate-a-new-tabular-model"></a>toocreate een nieuw model in tabelvorm

1. In de server **overzicht** blade > **webdesigner**, klikt u op **Open**.

    ![Een model maken in Azure portal](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. In **webdesigner** > **modellen**, klikt u op **+ toevoegen**.

    ![Een model maken in Azure portal](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. In **nieuw model**, typ de modelnaam van een en selecteer vervolgens een gegevensbron.

    ![Dialoogvenster voor nieuwe model in Azure-portal](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. In **Connect**, Hallo verbindingseigenschappen invoeren. Gebruikersnaam en het wachtwoord moet een SQL Server-serviceaccount.

     ![Verbinding maken met het dialoogvenster in Azure-portal](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. In **tabellen en weergaven**Hallo tabellen tooinclude selecteren in het model en klik vervolgens op **maken**. Relaties worden automatisch gemaakt tussen de tabellen met een sleutelpaar.

     ![Selecteer tabellen en weergaven](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

Het nieuwe model wordt weergegeven in uw browser. U kunt hier:   

- Modelgegevens query door te slepen velden toohello ontwerpfunctie voor query's en filters toe te voegen.
- Nieuwe maatregelen in tabellen maken.
- De metagegevens van model bewerken met behulp van Hallo json-editor.
- Hallo model openen in Visual Studio (SSDT), Power BI Desktop of Excel.

![Selecteer tabellen en weergaven](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> Wanneer u modelmetagegevens bewerken of maken van nieuwe maatregelen in uw browser, kunt u deze wijzigingen tooyour model wilt opslaan in Azure. Als u op het model in SSDT, Power BI Desktop of Excel werkt, kan het model niet meer synchroon.


## <a name="next-steps"></a>Volgende stappen 
[Databaserollen en gebruikers beheren](analysis-services-database-users.md)  
[Verbinden met Excel](analysis-services-connect-excel.md)  


