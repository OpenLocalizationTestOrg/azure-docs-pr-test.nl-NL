---
title: aaaUse ReportViewer in een website | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe toobuild een Microsoft Azure-website met Hallo Visual Studio ReportViewer-besturingselement dat wordt een rapport opgeslagen op een Microsoft Azure virtuele Machine.
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 78b76318-d9bf-48ef-9d9e-d1b7d8cf3042
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 8e0729d6657f96c32a9ac7dffdff7745ff92b48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-reportviewer-in-a-web-site-hosted-in-azure"></a>ReportViewer gebruiken op een in Azure gehoste website
> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

U kunt een Microsoft Azure-website met de Hallo Visual Studio ReportViewer-besturingselement dat een rapport dat is opgeslagen op een Microsoft Azure virtuele Machine wordt maken. Hallo ReportViewer-besturingselement is in een webtoepassing dat u met behulp van Hallo toepassingssjabloon voor ASP.NET-webtoepassing maken.

> [!IMPORTANT]
> Hallo ASP.NET MVC-webtoepassing sjablonen bieden geen ondersteuning voor Hallo ReportViewer-besturingselement.

tooincorporate ReportViewer in uw Microsoft Azure-website, moet u toocomplete Hallo taken te volgen.

* **Voeg** assembly's toohello implementatiepakket
* **Configureer** verificatie en autorisatie
* **Publiceren** Hallo ASP.NET Web application tooAzure

## <a name="prerequisites"></a>Vereisten
Raadpleeg Hallo 'algemene aanbevelingen en best practices'-sectie in [SQL Server Business Intelligence in Azure Virtual Machines](../classic/ps-sql-bi.md).

> [!NOTE]
> Besturingselementen van rapportviewer zijn verzonden met Visual Studio, Standard Edition of hoger. Als u Hallo Web Developer Express Edition gebruikt, moet u Hallo installeren [MICROSOFT REPORT VIEWER 2012 RUNTIME](https://www.microsoft.com/download/details.aspx?id=35747) toouse hello ReportViewer runtime-onderdelen.
> 
> ReportViewer geconfigureerd in de van de lokale verwerkingsmodus wordt niet ondersteund in Microsoft Azure.

## <a name="adding-assemblies-toohello-deployment-package"></a>Assembly's toohello implementatiepakket toevoegen
Wanneer u uw ASP.NET-toepassing on-premises host, Hallo ReportViewer-assembly's worden meestal geïnstalleerd rechtstreeks in Hallo globale assembly-cache (GAC) van Hallo IIS-server tijdens de installatie van Visual Studio en toegankelijk zijn voor de toepassing hello rechtstreeks. Hallo ReportViewer-assembly's zijn echter lokaal voor uw toepassing beschikbaar wanneer u host uw ASP.NET-toepassing in Microsoft Azure Hallo cloud staat niet toe dat alles toobe geïnstalleerd in Hallo GAC, dus moet u ervoor zorgen. U kunt dit doen door verwijzingen toothem in uw project toevoegen en configureren toobe lokaal gekopieerd.

Hallo ReportViewer-besturingselement gebruikt in de modus externe verwerking Hallo assembly's te volgen:

* **Microsoft.ReportViewer.WebForms.dll**: Hallo ReportViewer-code bevat, die u moet toouse ReportViewer in uw pagina. Een verwijzing voor deze assembly wordt tooyour project toegevoegd wanneer u een ReportViewer-besturingselement naar een ASP.NET-pagina in uw project neerzetten.
* **Microsoft.ReportViewer.Common.dll**: bevat klassen die worden gebruikt door Hallo ReportViewer-besturingselement tijdens runtime. Deze is tooyour project niet automatisch toegevoegd.

### <a name="tooadd-a-reference-toomicrosoftreportviewercommon"></a>een verwijzing tooMicrosoft.ReportViewer.Common tooadd
* Met de rechtermuisknop op uw project **verwijzingen** uit en selecteer **verwijzing toevoegen**, Hallo assembly in Hallo .NET tabblad selecteren en op **OK**.

### <a name="toomake-hello-assemblies-locally-accessible-by-your-aspnet-application"></a>toomake Hallo-assembly's lokaal toegankelijk zijn voor uw ASP.NET-toepassing
1. In Hallo **verwijzingen** map, klikt u op Hallo Microsoft.ReportViewer.Common assembly zodat de eigenschappen in Hallo eigenschappendeelvenster worden weergegeven.
2. In het deelvenster Hallo eigenschappen instellen **lokale kopie** tooTrue.
3. Herhaal stap 1 en 2 voor Microsoft.ReportViewer.WebForms.

### <a name="tooget-reportviewer-language-pack"></a>tooget ReportViewer Language Pack
1. Installeer Hallo juiste Microsoft Report Viewer 2012 Runtime distributiepakket van [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=317386).
2. Selecteer Hallo taal uit de vervolgkeuzelijst Hallo en Hallo pagina omgeleide toohello bijbehorende download center pagina opgehaald.
3. Klik op **downloaden** toostart Hallo downloaden van ReportViewerLP.exe.
4. Nadat u ReportViewerLP.exe downloaden, klikt u op **uitvoeren** tooinstall onmiddellijk, of klik op **opslaan** toosave het tooyour computer. Als u op **opslaan**, houd er rekening mee Hallo-naam van Hallo-map waar u Hallo bestand opslaan.
5. Zoek Hallo map waar u Hallo-bestand opgeslagen. Met de rechtermuisknop op ReportViewerLP.exe, klikt u op **als administrator uitvoeren**, en klik vervolgens op **Ja**.
6. Na het uitvoeren van ReportViewerLP.exe, ziet u Hallo c:\windows\assembly heeft Hallo bronbestanden **Microsoft.ReportViewer.Webforms.Resources** en **Microsoft.ReportViewer.Common.Resources** .

### <a name="tooconfigure-for-localized-reportviewer-control"></a>tooconfigure voor gelokaliseerde ReportViewer-besturingselement
1. Download en installeer herdistribueerbaar pakket van Hallo Microsoft Report Viewer 2012 Runtime door de volgende Hallo hierboven opgegeven instructies.
2. Maak <language> map in het project en kopieer Hallo Hallo assembly bronbestanden bevat die is gekoppeld. Hallo resource assembly bestanden toobe gekopieerd zijn: **Microsoft.ReportViewer.Webforms.Resources.dll** en **Microsoft.ReportViewer.Common.Resources.dll**. Hallo assembly bronbestanden selecteren en in deelvenster Hallo eigenschappen instellen **tooOutput Directory kopiëren** te '**altijd kopiëren**'.
3. Stel hello cultuur & UICulture voor Hallo-webproject. Voor meer informatie over hoe tooset Hallo cultuur en gebruikersinterfacecultuur voor een ASP.NET-webpagina zien [How to: Set Hallo cultuur en gebruikersinterfacecultuur voor ASP.NET-webpagina globalisatie](http://go.microsoft.com/fwlink/?LinkId=237461).

## <a name="configuring-authentication-and-authorization"></a>Verificatie en autorisatie configureren
Hallo ReportViewer moet toouse correcte referenties tooauthenticate met de rapportserver Hallo en Hallo referenties moeten worden geautoriseerd door Hallo tooaccess Hallo rapporten van report server die u wilt. Zie voor informatie over verificatie Hallo witboek [Reporting Services report viewer-besturingselement en Microsoft Azure virtuele machine op basis van rapportservers](https://msdn.microsoft.com/library/azure/dn753698.aspx).

## <a name="publish-hello-aspnet-web-application-tooazure"></a>Hallo tooAzure van ASP.NET-webtoepassing toepassing publiceren
Zie voor instructies over het publiceren van een ASP.NET-webtoepassing toepassing tooAzure [hoe: migreren en publiceren van een webtoepassing tooAzure vanuit Visual Studio](../../../vs-azure-tools-migrate-publish-web-app-to-cloud-service.md) en [aan de slag met Web-Apps en ASP.NET](../../../app-service-web/app-service-web-get-started-dotnet.md).

> [!IMPORTANT]
> Als hello Azure implementatieproject toevoegen of Azure Cloud Service-Project toevoegen-opdracht niet wordt weergegeven in het snelmenu Hallo in Solution Explorer, moet u mogelijk toochange Hallo doel-framework voor Hallo project too.NET Framework 4.
> 
> Hallo twee opdrachten in wezen bieden dezelfde functionaliteit Hallo. Een of Hallo andere opdracht wordt weergegeven in het snelmenu hello, afhankelijk van welke versie van Microsoft Azure SDK Hallo die u hebt geïnstalleerd.
> 
> 

## <a name="resources"></a>Resources
[Rapporten van Microsoft](http://go.microsoft.com/fwlink/?LinkId=205399)

[SQL Server Business Intelligence in virtuele machines van Azure](../classic/ps-sql-bi.md)

[Gebruik PowerShell tooCreate een Azure VM met een Native modus Report Server](../classic/ps-sql-report.md)

