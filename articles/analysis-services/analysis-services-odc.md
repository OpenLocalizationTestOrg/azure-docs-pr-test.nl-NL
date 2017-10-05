---
title: Maken van een ODC-bestand verbinding maken met een Azure Analysis Services-server | Microsoft Docs
description: Informatie over het maken van een Office Data Connection-bestand om te verbinden met en gegevens ophalen uit een Analysis Services-server in Azure.
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
ms.date: 08/23/2017
ms.author: owend
ms.openlocfilehash: 530f3b5c9e90cb45ffb6e12d0d08a35f8d687471
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-office-data-connection-file"></a><span data-ttu-id="85722-103">Een Office Data Connection-bestand maken</span><span class="sxs-lookup"><span data-stu-id="85722-103">Create an Office Data Connection file</span></span>

<span data-ttu-id="85722-104">Informatie in dit artikel wordt beschreven hoe u een Office Data Connection-bestand vanaf Excel 2016 versienummer 16.0.7369.2117 verbinding maken met een Azure Analysis Services-server kunt maken of eerder, of Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="85722-104">Information in this article describes how you can create an Office Data Connection file to connect to an Azure Analysis Services server from Excel 2016 version number 16.0.7369.2117 or earlier, or Excel 2013.</span></span> <span data-ttu-id="85722-105">Een bijgewerkte [MSOLAP.7 provider](analysis-services-data-providers.md) is ook vereist.</span><span class="sxs-lookup"><span data-stu-id="85722-105">An updated [MSOLAP.7 provider](analysis-services-data-providers.md) is also required.</span></span>


1. <span data-ttu-id="85722-106">Het verbindingsbestand voorbeeld kopiëren en plakken in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="85722-106">Copy the sample connection file below and paste into a text editor.</span></span> 

2. <span data-ttu-id="85722-107">In `odc:ConnectionString`, wijzigt u de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="85722-107">In `odc:ConnectionString`, change the following properties:</span></span>

    *   <span data-ttu-id="85722-108">In `Data Source=asazure://<region>.asazure.windows.net/<servername>;` wijzigen `<region>` naar de regio van de Analysis Services-server en `<servername>` op de naam van uw server.</span><span class="sxs-lookup"><span data-stu-id="85722-108">In `Data Source=asazure://<region>.asazure.windows.net/<servername>;` change `<region>` to the region of your Analysis Services server and `<servername>` to the name of your  server.</span></span>

    *   <span data-ttu-id="85722-109">In `Initial Catalog=<database>;` wijzigen `<database>` op de naam van uw database.</span><span class="sxs-lookup"><span data-stu-id="85722-109">In `Initial Catalog=<database>;` change `<database>` to the name of your database.</span></span>

3. <span data-ttu-id="85722-110">In `<odc:CommandText>Model</odc:CommandText>` wijzigen `Model` op de naam van uw model of perspectief.</span><span class="sxs-lookup"><span data-stu-id="85722-110">In `<odc:CommandText>Model</odc:CommandText>` change `Model` to the name of your model or perspective.</span></span> 

4. <span data-ttu-id="85722-111">Sla het bestand met een `.odc` -extensie voor de C:\Users\\*gebruikersnaam*map \Documents\My-gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="85722-111">Save the file with an `.odc` extension to the C:\Users\\*username*\Documents\My Data Sources folder.</span></span>

5. <span data-ttu-id="85722-112">Met de rechtermuisknop op het bestand en klik vervolgens op **openen in Excel**.</span><span class="sxs-lookup"><span data-stu-id="85722-112">Right-click the file, and then click **Open in Excel**.</span></span> <span data-ttu-id="85722-113">Of in Excel op het **gegevens** lint, klikt u op **bestaande verbindingen**, selecteer het bestand en klik vervolgens op **Open**.</span><span class="sxs-lookup"><span data-stu-id="85722-113">Or in Excel, on the **Data** ribbon, click **Existing Connections**, select your file, and then click **Open**.</span></span>



<span data-ttu-id="85722-114">**Voorbeeldbestand verbinding**</span><span class="sxs-lookup"><span data-stu-id="85722-114">**Sample connection file**</span></span>
```
<html xmlns:o="urn:schemas-microsoft-com:office:office"
xmlns="http://www.w3.org/TR/REC-html40">

<head>
<meta http-equiv=Content-Type content="text/x-ms-odc; charset=utf-8">
<meta name=ProgId content=ODC.Cube>
<meta name=SourceType content=OLEDB>
<meta name=Catalog content="Database">
<meta name=Table content=Model>
<title>AzureAnalysisServicesConnection</title>
<xml id=docprops><o:DocumentProperties
  xmlns:o="urn:schemas-microsoft-com:office:office"
  xmlns="http://www.w3.org/TR/REC-html40">
  <o:Name>SampleAzureAnalysisServices</o:Name>
 </o:DocumentProperties>
</xml><xml id=msodc><odc:OfficeDataConnection
  xmlns:odc="urn:schemas-microsoft-com:office:odc"
  xmlns="http://www.w3.org/TR/REC-html40">
  <odc:Connection odc:Type="OLEDB">
   <odc:ConnectionString>Provider=MSOLAP.7;Data Source=asazure://<region>.asazure.windows.net/<servername>;Initial Catalog=<database>;</odc:ConnectionString>
   <odc:CommandType>Cube</odc:CommandType>
   <odc:CommandText>Model</odc:CommandText>
  </odc:Connection>
 </odc:OfficeDataConnection>
</xml>
<style>
<!--
    .ODCDataSource
    {
    behavior: url(dataconn.htc);
    }
-->
</style>
 
</head>

<body onload='init()' scroll=no leftmargin=0 topmargin=0 rightmargin=0 style='border: 0px'>
<table style='border: solid 1px threedface; height: 100%; width: 100%' cellpadding=0 cellspacing=0 width='100%'> 
  <tr> 
    <td id=tdName style='font-family:arial; font-size:medium; padding: 3px; background-color: threedface'> 
      &nbsp; 
    </td> 
     <td id=tdTableDropdown style='padding: 3px; background-color: threedface; vertical-align: top; padding-bottom: 3px'>

      &nbsp; 
    </td> 
  </tr> 
  <tr> 
    <td id=tdDesc colspan='2' style='border-bottom: 1px threedshadow solid; font-family: Arial; font-size: 1pt; padding: 2px; background-color: threedface'>

      &nbsp; 
    </td> 
  </tr> 
  <tr> 
    <td colspan='2' style='height: 100%; padding-bottom: 4px; border-top: 1px threedhighlight solid;'> 
      <div id='pt' style='height: 100%' class='ODCDataSource'></div> 
    </td> 
  </tr> 
</table> 

  
<script language='javascript'> 

function init() { 
  var sName, sDescription; 
  var i, j; 
  
  try { 
    sName = unescape(location.href) 
  
    i = sName.lastIndexOf(".") 
    if (i>=0) { sName = sName.substring(1, i); } 
  
    i = sName.lastIndexOf("/") 
    if (i>=0) { sName = sName.substring(i+1, sName.length); } 

    document.title = sName; 
    document.getElementById("tdName").innerText = sName; 

    sDescription = document.getElementById("docprops").innerHTML; 
  
    i = sDescription.indexOf("escription>") 
    if (i>=0) { j = sDescription.indexOf("escription>", i + 11); } 

    if (i>=0 && j >= 0) { 
      j = sDescription.lastIndexOf("</", j); 

      if (j>=0) { 
          sDescription = sDescription.substring(i+11, j); 
        if (sDescription != "") { 
            document.getElementById("tdDesc").style.fontSize="x-small"; 
          document.getElementById("tdDesc").innerHTML = sDescription; 
          } 
        } 
      } 
    } 
  catch(e) { 

    } 
  } 
</script> 

</body> 
 
</html>

```



