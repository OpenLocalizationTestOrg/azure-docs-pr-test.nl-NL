---
title: Verbinding maken met Azure analyseservices | Microsoft Docs
description: Informatie over het verbinding maken met en gegevens ophalen uit een Analysis Services-server in Azure.
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
ms.openlocfilehash: deb3ef28d20decef01826450bd6091f87dd069de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-an-azure-analysis-services-server"></a><span data-ttu-id="9a0b0-103">Verbinding maken met een Azure Analysis Services-server</span><span class="sxs-lookup"><span data-stu-id="9a0b0-103">Connect to an Azure Analysis Services server</span></span>

<span data-ttu-id="9a0b0-104">Dit artikel wordt beschreven verbinding maken met een server met behulp van gegevens modelleren en toepassingen zoals SQL Server Management Studio (SSMS) of SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="9a0b0-104">This article describes connecting to a server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT).</span></span> <span data-ttu-id="9a0b0-105">Of met client reporting toepassingen zoals Microsoft Excel, Power BI Desktop of aangepaste toepassingen.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-105">Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications.</span></span> <span data-ttu-id="9a0b0-106">HTTPS gebruikt voor verbindingen met Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-106">Connections to Azure Analysis Services use HTTPS.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="9a0b0-107">Clientbibliotheken</span><span class="sxs-lookup"><span data-stu-id="9a0b0-107">Client libraries</span></span>
[<span data-ttu-id="9a0b0-108">De meest recente clientbibliotheken ophalen</span><span class="sxs-lookup"><span data-stu-id="9a0b0-108">Get the latest Client libraries</span></span>](analysis-services-data-providers.md)

<span data-ttu-id="9a0b0-109">Alle verbindingen met een server, ongeacht het type, bijgewerkte AMO ADOMD.NET en OLEDB-clientbibliotheken verbinding maken met en contact kunnen maken met een Analysis Services-server is vereist.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-109">All connections to a server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries to connect to and interface with an Analysis Services server.</span></span> <span data-ttu-id="9a0b0-110">Voor SSMS, SSDT, Excel 2016 en Power BI, worden de meest recente clientbibliotheken geïnstalleerd of bijgewerkt met maandelijkse releases.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-110">For SSMS, SSDT, Excel 2016, and Power BI, the latest client libraries are installed or updated with monthly releases.</span></span> <span data-ttu-id="9a0b0-111">In sommige gevallen is het echter mogelijk dat een toepassing heeft mogelijk niet de nieuwste versie.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-111">However, in some cases, it's possible an application may not have the latest.</span></span> <span data-ttu-id="9a0b0-112">Bijvoorbeeld, zijn als beleid vertraging worden bijgewerkt of Office 365-updates op het kanaal uitgesteld.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-112">For example, when policies delay updates, or Office 365 updates are on the Deferred Channel.</span></span>

## <a name="server-name"></a><span data-ttu-id="9a0b0-113">Servernaam</span><span class="sxs-lookup"><span data-stu-id="9a0b0-113">Server name</span></span>

<span data-ttu-id="9a0b0-114">Wanneer u een Analysis Services-server in Azure maakt, geeft u een unieke naam en de regio waar de server wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-114">When you create an Analysis Services server in Azure, you specify a unique name and the region where the server is to be created.</span></span> <span data-ttu-id="9a0b0-115">Wanneer u de servernaam opgeeft in een verbinding, is de schematische naam server:</span><span class="sxs-lookup"><span data-stu-id="9a0b0-115">When specifying the server name in a connection, the server naming scheme is:</span></span>

```
<protocol>://<region>/<servername>
```
 <span data-ttu-id="9a0b0-116">Protocol is waar tekenreeks **asazure**, regio is de Uri waar de server is gemaakt (bijvoorbeeld westus.asazure.windows.net) en servername is de naam van uw unieke server binnen de regio.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-116">Where protocol is string **asazure**, region is the Uri where the server was created (for example, westus.asazure.windows.net) and servername is the name of your unique server within the region.</span></span>

### <a name="get-the-server-name"></a><span data-ttu-id="9a0b0-117">Naam van de server ophalen</span><span class="sxs-lookup"><span data-stu-id="9a0b0-117">Get the server name</span></span>
<span data-ttu-id="9a0b0-118">In **Azure-portal** > server > **overzicht** > **servernaam**, de naam van de hele server kopiëren.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-118">In **Azure portal** > server > **Overview** > **Server name**, copy the entire server name.</span></span> <span data-ttu-id="9a0b0-119">Als andere gebruikers in uw organisatie verbinding met deze server te maakt, kunt u de naam van deze server met hen kunt delen.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-119">If other users in your organization are connecting to this server too, you can share this server name with them.</span></span> <span data-ttu-id="9a0b0-120">Wanneer u een servernaam opgeeft, moet het volledige pad worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-120">When specifying a server name, the entire path must be used.</span></span>

![Servernaam bepalen in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a><span data-ttu-id="9a0b0-122">Verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="9a0b0-122">Connection string</span></span>

<span data-ttu-id="9a0b0-123">Bij het verbinden met Azure Analysis Services met behulp van het Model in tabelvorm Object, gebruikt u de volgende indelingen voor verbinding tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="9a0b0-123">When connecting to Azure Analysis Services using the Tabular Object Model, use the following connection string formats:</span></span>

###### <a name="integrated-azure-active-directory-authentication"></a><span data-ttu-id="9a0b0-124">Geïntegreerde Azure Active Directory-verificatie</span><span class="sxs-lookup"><span data-stu-id="9a0b0-124">Integrated Azure Active Directory authentication</span></span>
<span data-ttu-id="9a0b0-125">Geïntegreerde verificatie neemt over de Azure Active Directory-referentiecache indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-125">Integrated authentication picks up the Azure Active Directory credential cache if available.</span></span> <span data-ttu-id="9a0b0-126">Als dat niet het geval is, moet u het venster Azure-aanmelding wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-126">If not, the Azure login window is shown.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a><span data-ttu-id="9a0b0-127">Azure Active Directory-verificatie met gebruikersnaam en wachtwoord</span><span class="sxs-lookup"><span data-stu-id="9a0b0-127">Azure Active Directory authentication with username and password</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a><span data-ttu-id="9a0b0-128">Windows-verificatie (geïntegreerde beveiliging)</span><span class="sxs-lookup"><span data-stu-id="9a0b0-128">Windows authentication (Integrated security)</span></span>
<span data-ttu-id="9a0b0-129">Gebruik het Windows-account met het huidige proces.</span><span class="sxs-lookup"><span data-stu-id="9a0b0-129">Use the Windows account running the current process.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a><span data-ttu-id="9a0b0-130">Verbinding maken met behulp van een ODC-bestand</span><span class="sxs-lookup"><span data-stu-id="9a0b0-130">Connect using an .odc file</span></span>
<span data-ttu-id="9a0b0-131">Gebruikers kunnen met oudere versies van Excel verbinding met een Azure Analysis Services-server met behulp van een bestand Office Data Connection (.odc).</span><span class="sxs-lookup"><span data-stu-id="9a0b0-131">With older versions of Excel, users can connect to an Azure Analysis Services server by using an Office Data Connection (.odc) file.</span></span> <span data-ttu-id="9a0b0-132">Zie voor meer informatie, [maakt u een bestand Office Data Connection (.odc)](analysis-services-odc.md).</span><span class="sxs-lookup"><span data-stu-id="9a0b0-132">To learn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="9a0b0-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9a0b0-133">Next steps</span></span>
<span data-ttu-id="9a0b0-134">[Verbinding maken met Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="9a0b0-134">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
<span data-ttu-id="9a0b0-135">[Verbinding maken met Power BI](analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="9a0b0-135">[Connect with Power BI](analysis-services-connect-pbi.md) </span></span>  
[<span data-ttu-id="9a0b0-136">Beheren van uw server</span><span class="sxs-lookup"><span data-stu-id="9a0b0-136">Manage your server</span></span>](analysis-services-manage.md)   

