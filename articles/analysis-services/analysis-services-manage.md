---
title: aaaManage Azure Analysis Services | Microsoft Docs
description: Meer informatie over hoe toomanage een Analysis Services-server in Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a>Analyseservices beheren
Als u een Analysis Services-server hebt gemaakt in Azure, mogelijk zijn er enkele administratie en beheer taken die u tooperform meteen moet of ergens omlaag Hallo weg. Voer bijvoorbeeld verwerken toohello vernieuwen van gegevens, bepalen wie toegang Hallo modellen op uw server of controleren van de status van uw server. Bepaalde beheertaken kunnen alleen worden uitgevoerd in Azure-portal anderen in SQL Server Management Studio (SSMS), en sommige taken kunnen worden uitgevoerd op een.

## <a name="azure-portal"></a>Azure Portal
[Azure-portal](http://portal.azure.com/) is waar u kunt maken en verwijderen van servers, serverbronnen bewaken, grootte wijzigen en beheren wie heeft toegang tot tooyour servers.  Als u problemen ondervindt, kunt u ook een verzoek om ondersteuning te verzenden.

![Servernaam bepalen in Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a>SQL Server Management Studio
Verbinding maken met server tooyour in Azure is net als bij verbinding maken met server-exemplaar tooa in uw eigen organisatie. Van SSMS, kunt u veel van Hallo dezelfde taken zoals gegevens over het installatieproces of maken van een verwerkingsscript, rollen beheren en gebruiken van PowerShell uitvoeren.
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a>Download en installeer SSMS
tooget alle Hallo nieuwste functies en Hallo meest vloeiende ervaring bij het verbinden van tooyour Azure Analysis Services-server, zorg ervoor dat u Hallo meest recente versie van SSMS. 

[SQL Server Management Studio downloaden](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).


### <a name="tooconnect-with-ssms"></a>tooconnect met SSMS
 Wanneer met behulp van SSMS, voordat u verbinding maakt tooyour Hallo van server eerst, zorg er dan voor dat uw gebruikersnaam is opgenomen in Hallo Analysis Services-beheerdersgroep. toolearn meer, Zie [serverbeheerders](#server-administrators) verderop in dit artikel.

1. Voordat u verbinding maakt, moet u tooget Hallo servernaam. In **Azure-portal** > server > **overzicht** > **servernaam**, kopie Hallo servernaam.
   
    ![Servernaam bepalen in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. In SSMS > **Objectverkenner**, klikt u op **Connect** > **Analysis Services**.
3. In Hallo **verbinding tooServer** in het dialoogvenster Plakken Hallo-servernaam, vervolgens in **verificatie**, kies een van de volgende verificatietypen Hallo:
   
    **Windows-verificatie** toouse uw Windows-referenties voor domein\gebruikersnaam en het wachtwoord.

    **Active Directory-wachtwoordverificatie** toouse een organisatieaccount. Bijvoorbeeld, wanneer verbinding maakt vanaf een niet-domein lid zijn van computer.

    **Verificatie van Active Directory-universele** toouse [niet-interactieve of multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md). 
   
    ![Verbinding maken in SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a>Serverbeheerders en databasegebruikers
Er zijn twee typen van gebruikers, beheerders en databasegebruikers in Azure Analysis Services. Beide typen gebruikers, moeten in uw Azure Active Directory en moeten worden opgegeven met de organisatie-e-mailadres of de UPN. toolearn meer, Zie [verificatie en gebruikersmachtigingen](analysis-services-manage-users.md).


## <a name="troubleshooting-connection-problems"></a>Het oplossen van problemen met de verbinding
Wanneer u verbinding maakt met behulp van SSMS, als u op problemen stuit, moet u wellicht tooclear Hallo aanmelding cache. Er is niets is in de cache toodisc. verbinding maken proces tooclear Hallo cache, sluiten en opnieuw opstarten Hallo. 

## <a name="next-steps"></a>Volgende stappen
Als u al een model in tabelvorm tooyour nieuwe server nog niet hebt geïmplementeerd, is een goed moment. toolearn meer, Zie [tooAzure Analysis Services implementeren](analysis-services-deploy.md).

Als u een model tooyour-server hebt geïmplementeerd, bent u klaar tooconnect tooit met behulp van een client of de browser. toolearn meer, Zie [gegevens ophalen uit Azure Analysis Services-server](analysis-services-connect.md).

