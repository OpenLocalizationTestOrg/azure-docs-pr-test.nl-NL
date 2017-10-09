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
# <a name="connect-tooan-azure-analysis-services-server"></a><span data-ttu-id="fb629-103">Verbinding maken met tooan Azure Analysis Services-server</span><span class="sxs-lookup"><span data-stu-id="fb629-103">Connect tooan Azure Analysis Services server</span></span>

<span data-ttu-id="fb629-104">Dit artikel worden aangesloten tooa server met behulp van gegevens modelleren en toepassingen zoals SQL Server Management Studio (SSMS) of SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="fb629-104">This article describes connecting tooa server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT).</span></span> <span data-ttu-id="fb629-105">Of met client reporting toepassingen zoals Microsoft Excel, Power BI Desktop of aangepaste toepassingen.</span><span class="sxs-lookup"><span data-stu-id="fb629-105">Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications.</span></span> <span data-ttu-id="fb629-106">HTTPS gebruikt voor verbindingen tooAzure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="fb629-106">Connections tooAzure Analysis Services use HTTPS.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="fb629-107">Clientbibliotheken</span><span class="sxs-lookup"><span data-stu-id="fb629-107">Client libraries</span></span>
[<span data-ttu-id="fb629-108">De meest recente clientbibliotheken Hallo ophalen</span><span class="sxs-lookup"><span data-stu-id="fb629-108">Get hello latest Client libraries</span></span>](analysis-services-data-providers.md)

<span data-ttu-id="fb629-109">Alle verbindingen tooa server, ongeacht het type, vereisen bijgewerkte AMO ADOMD.NET en OLEDB-bibliotheken tooconnect tooand clientinterface met een Analysis Services-server.</span><span class="sxs-lookup"><span data-stu-id="fb629-109">All connections tooa server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries tooconnect tooand interface with an Analysis Services server.</span></span> <span data-ttu-id="fb629-110">Voor SSMS, SSDT, Excel 2016 en Power BI, worden de meest recente clientbibliotheken Hallo geïnstalleerd of bijgewerkt met maandelijkse releases.</span><span class="sxs-lookup"><span data-stu-id="fb629-110">For SSMS, SSDT, Excel 2016, and Power BI, hello latest client libraries are installed or updated with monthly releases.</span></span> <span data-ttu-id="fb629-111">In sommige gevallen is het echter mogelijk dat een toepassing mogelijk geen Hallo meest recente.</span><span class="sxs-lookup"><span data-stu-id="fb629-111">However, in some cases, it's possible an application may not have hello latest.</span></span> <span data-ttu-id="fb629-112">Bijvoorbeeld, zijn als beleid vertraging worden bijgewerkt of Office 365-updates op Hallo uitgesteld kanaal.</span><span class="sxs-lookup"><span data-stu-id="fb629-112">For example, when policies delay updates, or Office 365 updates are on hello Deferred Channel.</span></span>

## <a name="server-name"></a><span data-ttu-id="fb629-113">Servernaam</span><span class="sxs-lookup"><span data-stu-id="fb629-113">Server name</span></span>

<span data-ttu-id="fb629-114">Wanneer u een Analysis Services-server in Azure maakt, geeft u een unieke naam en het Hallo de regio waar Hallo server toobe gemaakt is.</span><span class="sxs-lookup"><span data-stu-id="fb629-114">When you create an Analysis Services server in Azure, you specify a unique name and hello region where hello server is toobe created.</span></span> <span data-ttu-id="fb629-115">Wanneer u Hallo servernaam opgeeft in een verbinding, is de schematische Hallo-server:</span><span class="sxs-lookup"><span data-stu-id="fb629-115">When specifying hello server name in a connection, hello server naming scheme is:</span></span>

```
<protocol>://<region>/<servername>
```
 <span data-ttu-id="fb629-116">Protocol is waar tekenreeks **asazure**, regio is Hallo Uri waar Hallo-server is gemaakt (bijvoorbeeld westus.asazure.windows.net) en servernaam Hallo-naam van uw unieke server binnen Hallo regio.</span><span class="sxs-lookup"><span data-stu-id="fb629-116">Where protocol is string **asazure**, region is hello Uri where hello server was created (for example, westus.asazure.windows.net) and servername is hello name of your unique server within hello region.</span></span>

### <a name="get-hello-server-name"></a><span data-ttu-id="fb629-117">Hallo-servernaam ophalen</span><span class="sxs-lookup"><span data-stu-id="fb629-117">Get hello server name</span></span>
<span data-ttu-id="fb629-118">In **Azure-portal** > server > **overzicht** > **servernaam**, de naam van de hele server Hallo kopiëren.</span><span class="sxs-lookup"><span data-stu-id="fb629-118">In **Azure portal** > server > **Overview** > **Server name**, copy hello entire server name.</span></span> <span data-ttu-id="fb629-119">Als andere gebruikers in uw organisatie toothis server te verbinden zijn, kunt u de naam van deze server met hen kunt delen.</span><span class="sxs-lookup"><span data-stu-id="fb629-119">If other users in your organization are connecting toothis server too, you can share this server name with them.</span></span> <span data-ttu-id="fb629-120">Wanneer u een servernaam opgeeft, moet het volledige pad hello worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fb629-120">When specifying a server name, hello entire path must be used.</span></span>

![Servernaam bepalen in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a><span data-ttu-id="fb629-122">Verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="fb629-122">Connection string</span></span>

<span data-ttu-id="fb629-123">Wanneer u verbinding maakt tooAzure Hallo Analysis Services met behulp van objectmodel in tabelvorm, gebruik Hallo verbinding tekenreeksindelingen na:</span><span class="sxs-lookup"><span data-stu-id="fb629-123">When connecting tooAzure Analysis Services using hello Tabular Object Model, use hello following connection string formats:</span></span>

###### <a name="integrated-azure-active-directory-authentication"></a><span data-ttu-id="fb629-124">Geïntegreerde Azure Active Directory-verificatie</span><span class="sxs-lookup"><span data-stu-id="fb629-124">Integrated Azure Active Directory authentication</span></span>
<span data-ttu-id="fb629-125">Geïntegreerde verificatie hervat hello Azure Active Directory-referentiecache indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="fb629-125">Integrated authentication picks up hello Azure Active Directory credential cache if available.</span></span> <span data-ttu-id="fb629-126">Als dat niet het geval is, hello Azure-aanmeldingsvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fb629-126">If not, hello Azure login window is shown.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a><span data-ttu-id="fb629-127">Azure Active Directory-verificatie met gebruikersnaam en wachtwoord</span><span class="sxs-lookup"><span data-stu-id="fb629-127">Azure Active Directory authentication with username and password</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a><span data-ttu-id="fb629-128">Windows-verificatie (geïntegreerde beveiliging)</span><span class="sxs-lookup"><span data-stu-id="fb629-128">Windows authentication (Integrated security)</span></span>
<span data-ttu-id="fb629-129">Hallo Windows-account met het huidige proces hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fb629-129">Use hello Windows account running hello current process.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a><span data-ttu-id="fb629-130">Verbinding maken met behulp van een ODC-bestand</span><span class="sxs-lookup"><span data-stu-id="fb629-130">Connect using an .odc file</span></span>
<span data-ttu-id="fb629-131">Gebruikers kunnen tooan Azure Analysis Services-server verbinding met een Office Data Connection (.odc)-bestand met oudere versies van Excel.</span><span class="sxs-lookup"><span data-stu-id="fb629-131">With older versions of Excel, users can connect tooan Azure Analysis Services server by using an Office Data Connection (.odc) file.</span></span> <span data-ttu-id="fb629-132">toolearn meer, Zie [maakt u een bestand Office Data Connection (.odc)](analysis-services-odc.md).</span><span class="sxs-lookup"><span data-stu-id="fb629-132">toolearn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="fb629-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fb629-133">Next steps</span></span>
<span data-ttu-id="fb629-134">[Verbinding maken met Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="fb629-134">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
<span data-ttu-id="fb629-135">[Verbinding maken met Power BI](analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="fb629-135">[Connect with Power BI](analysis-services-connect-pbi.md) </span></span>  
[<span data-ttu-id="fb629-136">Beheren van uw server</span><span class="sxs-lookup"><span data-stu-id="fb629-136">Manage your server</span></span>](analysis-services-manage.md)   

