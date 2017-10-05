---
title: Azure Data Catalog release-opmerkingen | Microsoft Docs
description: Releaseopmerkingen voor Azure Data Catalog.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: d3db9bee0558cac5fb4f5b8fb4ab67a35ce0f141
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-catalog-release-notes"></a><span data-ttu-id="1aa1a-103">Azure Data Catalog release-opmerkingen</span><span class="sxs-lookup"><span data-stu-id="1aa1a-103">Azure Data Catalog release notes</span></span>
## <a name="notes-for-the-november-20-2015-release-of-azure-data-catalog"></a><span data-ttu-id="1aa1a-104">Informatie voor 20 November 2015-release van Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="1aa1a-104">Notes for the November 20, 2015 release of Azure Data Catalog</span></span>
### <a name="opening-data-sources-in-power-bi-desktop"></a><span data-ttu-id="1aa1a-105">De gegevensbronnen openen in Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="1aa1a-105">Opening Data Sources in Power BI Desktop</span></span>
<span data-ttu-id="1aa1a-106">Wanneer u de optie 'Openen in Power BI Desktop' uit de **Azure Data Catalog** portal gebruikers kunnen ondervinden een van twee problemen in de Power BI Desktop-toepassing:</span><span class="sxs-lookup"><span data-stu-id="1aa1a-106">When using the "Open in Power BI Desktop" option from the **Azure Data Catalog** portal, users may encounter one of two problems in the Power BI Desktop application:</span></span>

* <span data-ttu-id="1aa1a-107">Een dialoogvenster met de titel 'Kan niet aan Open Document' wordt weergegeven</span><span class="sxs-lookup"><span data-stu-id="1aa1a-107">A dialog box with the title "Unable to Open Document" is displayed</span></span>
* <span data-ttu-id="1aa1a-108">De Power BI Desktop-toepassing wordt geopend, maar het bestand is niet leeg zijn</span><span class="sxs-lookup"><span data-stu-id="1aa1a-108">The Power BI Desktop application opens, but the file appears to be empty</span></span>

<span data-ttu-id="1aa1a-109">Voor elke situatie kan het probleem worden opgelost door downloaden en installeren van de nieuwste versie van Power BI Desktop van [PowerBI.com](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="1aa1a-109">For each situation, the problem can be resolved by downloading and installing the latest version of Power BI Desktop from [PowerBI.com](https://powerbi.com).</span></span>

## <a name="notes-for-the-november-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="1aa1a-110">Informatie voor 13 November 2015-release van Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="1aa1a-110">Notes for the November 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-to-teradata"></a><span data-ttu-id="1aa1a-111">Registreren en te verbinden met de Teradata</span><span class="sxs-lookup"><span data-stu-id="1aa1a-111">Registering and connecting to Teradata</span></span>
<span data-ttu-id="1aa1a-112">Bij het verbinden met de Teradata-gegevensbronnen gebruikers het juiste Teradata ODBC-stuurprogramma moeten hebben geïnstalleerd die overeenkomen met de bitness van de software die wordt gebruikt (32-bits of 64-bits).</span><span class="sxs-lookup"><span data-stu-id="1aa1a-112">When connecting to Teradata data sources users must have installed the correct Teradata ODBC driver that match the bitness (32-bit or 64-bit) of the software being used.</span></span>

<span data-ttu-id="1aa1a-113">Vanaf deze datum ADC release is de meest recente [Teradata ODBC-stuurprogramma voor windows (versie 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) is compatibel met Office 2013, maar niet met Office 2016.</span><span class="sxs-lookup"><span data-stu-id="1aa1a-113">As of this ADC release date, the most recent [Teradata ODBC driver for windows ( version 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) is compatible with Office 2013, but not with Office 2016.</span></span>

## <a name="notes-for-the-july-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="1aa1a-114">Informatie voor 13 juli 2015-release van Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="1aa1a-114">Notes for the July 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-to-oracle-database"></a><span data-ttu-id="1aa1a-115">Registreren en te verbinden met de Oracle-Database</span><span class="sxs-lookup"><span data-stu-id="1aa1a-115">Registering and connecting to Oracle Database</span></span>
<span data-ttu-id="1aa1a-116">Bij het verbinden met de Oracle-Database-gegevensbronnen gebruikers moeten de juiste Oracle-stuurprogramma's die overeenkomen met de bitness van de software die wordt gebruikt (32-bits of 64-bits) hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1aa1a-116">When connecting to Oracle Database data sources users must have installed the correct Oracle drivers that match the bitness (32-bit or 64-bit) of the software being used.</span></span>

* <span data-ttu-id="1aa1a-117">De 32-bits Oracle-stuurprogramma's wordt gebruikt bij het registreren van Oracle-gegevensbronnen op een computer met Windows 32-bits</span><span class="sxs-lookup"><span data-stu-id="1aa1a-117">When registering Oracle data sources on a computer running 32-bit Windows, the 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="1aa1a-118">De 64-bits Oracle-stuurprogramma's wordt gebruikt bij het registreren van Oracle-gegevensbronnen op een computer met 64-bits Windows</span><span class="sxs-lookup"><span data-stu-id="1aa1a-118">When registering Oracle data sources on a computer running 64-bit Windows, the 64-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="1aa1a-119">Bij het verbinden met de Oracle-gegevensbronnen met Excel op een computer met de 32-bits versie van Microsoft Office, wordt inclusief op 64-bits Windows de 32-bits Oracle-stuurprogramma's gebruikt</span><span class="sxs-lookup"><span data-stu-id="1aa1a-119">When connecting to Oracle data sources using Excel on a computer running the 32-bit version of Microsoft Office, including on 64-bit Windows, the 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="1aa1a-120">Wanneer u verbinding maakt met de Oracle-gegevensbronnen met Excel op een computer met de 64-bits versie van Microsoft Office, worden de 64-bits Oracle-stuurprogramma's gebruikt</span><span class="sxs-lookup"><span data-stu-id="1aa1a-120">When connecting to Oracle data sources using Excel on a computer running the 64-bit version of Microsoft Office, the 64-bit Oracle drivers will be used</span></span>

### <a name="registering-and-connecting-to-sql-server-reporting-services"></a><span data-ttu-id="1aa1a-121">Registreren en te verbinden met SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="1aa1a-121">Registering and connecting to SQL Server Reporting Services</span></span>
<span data-ttu-id="1aa1a-122">Ondersteuning voor gegevensbronnen van SQL Server Reporting Services (SSRS) is momenteel beperkt tot alleen servers Native-modus.</span><span class="sxs-lookup"><span data-stu-id="1aa1a-122">Support for SQL Server Reporting Services (SSRS) data sources is currently limited to Native Mode servers only.</span></span> <span data-ttu-id="1aa1a-123">Ondersteuning voor SQL Server Reporting Services in de modus SharePoint wordt uitgevoerd wordt in een latere versie toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1aa1a-123">Support for SSRS in SharePoint mode will be added in a later release.</span></span>

### <a name="opening-data-assets-in-excel"></a><span data-ttu-id="1aa1a-124">Gegevensassets openen in Excel</span><span class="sxs-lookup"><span data-stu-id="1aa1a-124">Opening data assets in Excel</span></span>
<span data-ttu-id="1aa1a-125">Bij het openen van gegevensassets in Microsoft Excel uit de **Azure Data Catalog** portal gebruikers mogelijk gevraagd met een **beveiligingsbericht Microsoft Excel** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1aa1a-125">When opening data assets in Microsoft Excel from the **Azure Data Catalog** portal, users may be prompted with a **Microsoft Excel Security Notice** dialog box.</span></span> <span data-ttu-id="1aa1a-126">Dit is standaard, verwacht gedrag en gebruikers kunnen selecteren **inschakelen** om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="1aa1a-126">This is standard, expected behavior, and users can select **Enable** to continue.</span></span>

<span data-ttu-id="1aa1a-127">Zie voor meer informatie [in- of uitschakelen van beveiligingswaarschuwingen over koppelingen en bestanden van verdachte websites](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span><span class="sxs-lookup"><span data-stu-id="1aa1a-127">For more information, see [Enable or disable security alerts about links and files from suspicious websites](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span></span>

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a><span data-ttu-id="1aa1a-128">Proxy- en beleid voor configuratie en gegevens registratie van gegevensbron</span><span class="sxs-lookup"><span data-stu-id="1aa1a-128">Proxy and policy configuration and data source registration</span></span>
<span data-ttu-id="1aa1a-129">Gebruikers kunnen ondervinden een situatie waarin ze zich aanmelden kunnen bij de Azure Data Catalog-portal, maar als ze proberen aan te melden op het hulpprogramma voor registratie dat een foutbericht weergegeven dat voorkomt ze dat zich aanmelden optreden.</span><span class="sxs-lookup"><span data-stu-id="1aa1a-129">Users may encounter a situation where they can log on to the Azure Data Catalog portal, but when they attempt to log on to the data source registration tool they encounter an error message that prevents them from logging on.</span></span>

<span data-ttu-id="1aa1a-130">Er zijn twee mogelijke oorzaken voor dit probleem gedrag:</span><span class="sxs-lookup"><span data-stu-id="1aa1a-130">There are two potential causes for this problem behavior:</span></span>

<span data-ttu-id="1aa1a-131">**1 oorzaak: Active Directory Federation Services configuration** formulierverificatie valideren gebruikersaanmeldingen op basis van Active Directory maakt gebruik van het registratiehulpprogramma van gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="1aa1a-131">**Cause 1: Active Directory Federation Services configuration** The data source registration tool uses Forms Authentication to validate user logons against Active Directory.</span></span> <span data-ttu-id="1aa1a-132">Voor geslaagde aanmelding moet formulierverificatie zijn ingeschakeld in het globale verificatiebeleid door een Active Directory-beheerder.</span><span class="sxs-lookup"><span data-stu-id="1aa1a-132">For successful logon, Forms Authentication must be enabled in the Global Authentication Policy by an Active Directory administrator.</span></span>

<span data-ttu-id="1aa1a-133">In sommige gevallen is kan deze fout gebeuren wanneer de gebruiker op het bedrijfsnetwerk, of alleen wanneer de gebruiker verbinding maakt vanaf buiten het bedrijfsnetwerk.</span><span class="sxs-lookup"><span data-stu-id="1aa1a-133">In some situations, this error behavior may occur only when the user is on the company network, or only when the user is connecting from outside the company network.</span></span> <span data-ttu-id="1aa1a-134">Het globale verificatiebeleid kunt verificatiemethoden afzonderlijk worden ingeschakeld voor het intranet en extranet-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="1aa1a-134">The Global Authentication Policy allows authentication methods to be enabled separately for intranet and extranet connections.</span></span> <span data-ttu-id="1aa1a-135">Aanmeldingsfouten kunnen optreden als formulierverificatie is niet ingeschakeld voor het netwerk van waaruit de gebruiker verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="1aa1a-135">Logon errors may occur if Forms Authentication is not enabled for the network from which the user is connecting.</span></span>

<span data-ttu-id="1aa1a-136">Zie voor meer informatie [Authenticatiebeleid configureren](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="1aa1a-136">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>

<span data-ttu-id="1aa1a-137">**Oorzaak 2: Proxy netwerkconfiguratie** als het bedrijfsnetwerk een proxyserver gebruikt, het registratiehulpprogramma wellicht geen verbinding maken met Azure Active Directory via de proxy.</span><span class="sxs-lookup"><span data-stu-id="1aa1a-137">**Cause 2: Network proxy configuration** If the corporate network uses a proxy server, the registration tool may not be able to connect to Azure Active Directory through the proxy.</span></span> <span data-ttu-id="1aa1a-138">Gebruikers kunnen ervoor zorgen dat het registratiehulpprogramma door het hulpprogramma configuratiebestand, bewerken in deze sectie toe te voegen aan het bestand:</span><span class="sxs-lookup"><span data-stu-id="1aa1a-138">Users can ensure that the registration tool by editing the tool’s configuration file, adding this section to the file:</span></span>

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


<span data-ttu-id="1aa1a-139">Zoek het bestand RegistrationTool.exe.config, start het registratiehulpprogramma en open vervolgens het hulpprogramma Windows Taakbeheer.</span><span class="sxs-lookup"><span data-stu-id="1aa1a-139">To locate the RegistrationTool.exe.config file, launch the registration tool, and then open the Windows Task Manager utility.</span></span> <span data-ttu-id="1aa1a-140">Op het tabblad Details in Taakbeheer met de rechtermuisknop op RegistrationTool.exe en kies bestandslocatie openen in het pop-upmenu.</span><span class="sxs-lookup"><span data-stu-id="1aa1a-140">On the Details tab in Task manager, right-click on RegistrationTool.exe and choose Open file location from the pop-up menu.</span></span>
