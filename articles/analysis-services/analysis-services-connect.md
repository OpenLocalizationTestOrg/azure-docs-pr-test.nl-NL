---
title: aaaConnect tooAzure Analysis Services | Microsoft Docs
description: Meer informatie over hoe tooconnect tooand gegevens ophalen uit een Analysis Services-server in Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: b37f70a0-9166-4173-932d-935d769539d1
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 5df94492feb48034f156b72e83e1009683988fc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-analysis-services-server"></a>Verbinding maken met tooan Azure Analysis Services-server

Dit artikel worden aangesloten tooa server met behulp van gegevens modelleren en toepassingen zoals SQL Server Management Studio (SSMS) of SQL Server Data Tools (SSDT). Of met client reporting toepassingen zoals Microsoft Excel, Power BI Desktop of aangepaste toepassingen. HTTPS gebruikt voor verbindingen tooAzure Analysis Services.

## <a name="client-libraries"></a>Clientbibliotheken
[De meest recente clientbibliotheken Hallo ophalen](analysis-services-data-providers.md)

Alle verbindingen tooa server, ongeacht het type, vereisen bijgewerkte AMO ADOMD.NET en OLEDB-bibliotheken tooconnect tooand clientinterface met een Analysis Services-server. Voor SSMS, SSDT, Excel 2016 en Power BI, worden de meest recente clientbibliotheken Hallo geïnstalleerd of bijgewerkt met maandelijkse releases. In sommige gevallen is het echter mogelijk dat een toepassing mogelijk geen Hallo meest recente. Bijvoorbeeld, zijn als beleid vertraging worden bijgewerkt of Office 365-updates op Hallo uitgesteld kanaal.

## <a name="server-name"></a>Servernaam

Wanneer u een Analysis Services-server in Azure maakt, geeft u een unieke naam en het Hallo de regio waar Hallo server toobe gemaakt is. Wanneer u Hallo servernaam opgeeft in een verbinding, is de schematische Hallo-server:

```
<protocol>://<region>/<servername>
```
 Protocol is waar tekenreeks **asazure**, regio is Hallo Uri waar Hallo-server is gemaakt (bijvoorbeeld westus.asazure.windows.net) en servernaam Hallo-naam van uw unieke server binnen Hallo regio.

### <a name="get-hello-server-name"></a>Hallo-servernaam ophalen
In **Azure-portal** > server > **overzicht** > **servernaam**, de naam van de hele server Hallo kopiëren. Als andere gebruikers in uw organisatie toothis server te verbinden zijn, kunt u de naam van deze server met hen kunt delen. Wanneer u een servernaam opgeeft, moet het volledige pad hello worden gebruikt.

![Servernaam bepalen in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a>Verbindingsreeks

Wanneer u verbinding maakt tooAzure Hallo Analysis Services met behulp van objectmodel in tabelvorm, gebruik Hallo verbinding tekenreeksindelingen na:

###### <a name="integrated-azure-active-directory-authentication"></a>Geïntegreerde Azure Active Directory-verificatie
Geïntegreerde verificatie hervat hello Azure Active Directory-referentiecache indien beschikbaar. Als dat niet het geval is, hello Azure-aanmeldingsvenster wordt weergegeven.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a>Azure Active Directory-verificatie met gebruikersnaam en wachtwoord

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a>Windows-verificatie (geïntegreerde beveiliging)
Hallo Windows-account met het huidige proces hello gebruiken.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a>Verbinding maken met behulp van een ODC-bestand
Gebruikers kunnen tooan Azure Analysis Services-server verbinding met een Office Data Connection (.odc)-bestand met oudere versies van Excel. toolearn meer, Zie [maakt u een bestand Office Data Connection (.odc)](analysis-services-odc.md).


## <a name="next-steps"></a>Volgende stappen
[Verbinding maken met Excel](analysis-services-connect-excel.md)    
[Verbinding maken met Power BI](analysis-services-connect-pbi.md)   
[Beheren van uw server](analysis-services-manage.md)   

