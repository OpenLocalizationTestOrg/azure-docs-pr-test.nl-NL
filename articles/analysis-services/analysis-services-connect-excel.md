---
title: aaaConnect tooAzure Analysis Services met Excel | Microsoft Docs
description: Meer informatie over hoe tooconnect tooan Azure Analysis Services-server met behulp van Excel.
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
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 175b83e7d936716a626aa4b3bf22b5598bb983d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-excel"></a>Verbinden met Excel

Nadat u hebt gemaakt van een server in Azure en een model in tabelvorm tooit geïmplementeerd, kunt u bent klaar tooconnect en begint met het verkennen van gegevens.


## <a name="connect-in-excel"></a>Verbinding maken in Excel

Tooa-server in Excel verbinding maken wordt met behulp van de gegevens ophalen in Excel 2016 ondersteund. Verbinding maken met behulp van de Wizard tabel importeren Hallo in Power Pivot wordt niet ondersteund. 

**tooconnect in Excel 2016**

1. In Excel 2016 op Hallo **gegevens** lint, klikt u op **externe gegevens ophalen** > **van andere bronnen** > **van Analysis Services** .

2. Hallo in de Wizard Gegevensverbinding **servernaam**, Voer Hallo servernaam waaronder het protocol en de URI. Klik op **aanmeldingsreferenties**, selecteer **gebruik Hallo volgende gebruikersnaam en wachtwoord**, en typ vervolgens het organisatie-gebruikersnaam hello, bijvoorbeeld nancy@adventureworks.com, en het wachtwoord.

    ![Verbinding maken van Excel-aanmelding](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. In **Database en tabel selecteren**Hallo-database en model of perspectief selecteren en klik vervolgens op **voltooien**.
   
    ![Verbinding maken vanaf Selecteer Excel-gegevensmodel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a>Zie ook
[Clientbibliotheken](analysis-services-data-providers.md)   
[Beheren van uw server](analysis-services-manage.md)     


