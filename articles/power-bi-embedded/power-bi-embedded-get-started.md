---
title: aaaGet de slag met Microsoft Power BI Embedded
description: Power BI Embedded, voeg interactieve Power BI-rapporten toe aan uw BI-toepassing (Business Intelligence)
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a><span data-ttu-id="1ea5d-103">Aan de slag met Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="1ea5d-103">Get started with Microsoft Power BI Embedded</span></span>

<span data-ttu-id="1ea5d-104">**Power BI Embedded** een Azure-service is dat Hiermee toepassing ontwikkelaars tooadd interactieve Power BI-aan hun eigen toepassingen rapporten.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-104">**Power BI Embedded** is an Azure service that enables application developers tooadd interactive Power BI reports into their own applications.</span></span> <span data-ttu-id="1ea5d-105">**Power BI Embedded** werkt met bestaande toepassingen zonder te hoeven ontwerpen of wijzigen van Hallo manier waarop gebruikers zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-105">**Power BI Embedded** works with existing applications without needing redesign or changing hello way users sign in.</span></span>

<span data-ttu-id="1ea5d-106">Bronnen voor **Microsoft Power BI Embedded** zijn ingericht via Hallo [Azure ARM API's](https://msdn.microsoft.com/library/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ea5d-106">Resources for **Microsoft Power BI Embedded** are provisioned through hello [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span></span> <span data-ttu-id="1ea5d-107">In dit geval Hallo-bron die u inricht is een **Power BI-Werkruimteverzameling**.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-107">In this case, hello resource you provision is a **Power BI Workspace Collection**.</span></span>

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a><span data-ttu-id="1ea5d-108">Een werkruimteverzameling maken</span><span class="sxs-lookup"><span data-stu-id="1ea5d-108">Create a workspace collection</span></span>

<span data-ttu-id="1ea5d-109">Een **Werkruimteverzameling** Hallo op het hoogste niveau Azure-resource en een container voor Hallo-inhoud die wordt ingesloten in uw toepassing is.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-109">A **Workspace Collection** is hello top-level Azure resource and a container for hello content that will be embedded in your application.</span></span> <span data-ttu-id="1ea5d-110">U kunt op twee manieren een **werkruimteverzameling** maken:</span><span class="sxs-lookup"><span data-stu-id="1ea5d-110">A **Workspace Collection** can be created in two ways::</span></span>

* <span data-ttu-id="1ea5d-111">Handmatig met behulp van hello Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1ea5d-111">Manually using hello Azure Portal</span></span>
* <span data-ttu-id="1ea5d-112">Programmatisch met behulp van hello Azure Resource Manager (arm) API 's</span><span class="sxs-lookup"><span data-stu-id="1ea5d-112">Programmatically using hello Azure Resource Manager(ARM) APIs</span></span>

<span data-ttu-id="1ea5d-113">We doorlopen Hallo stappen toobuild een **Werkruimteverzameling** met behulp van hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-113">Let's walk through hello steps toobuild a **Workspace Collection** using hello Azure Portal.</span></span>

1. <span data-ttu-id="1ea5d-114">Open de **Azure-portal**: [http://portal.azure.com](http://portal.azure.com) en meld u aan.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-114">Open and sign into **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).</span></span>
2. <span data-ttu-id="1ea5d-115">Klik op **+ nieuw** op Hallo boven in het venster.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-115">Click **+ New** on hello top panel.</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. <span data-ttu-id="1ea5d-116">Klik onder **Gegevens en analyse** op **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-116">Under **Data + Analytics** click **Power BI Embedded**.</span></span>
4. <span data-ttu-id="1ea5d-117">Op Hallo **Blade Werkruimteverzameling**, Geef informatie op Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-117">On hello **Workspace Collection Blade**, enter hello required information.</span></span> <span data-ttu-id="1ea5d-118">Informatie over **prijzen** vindt in [Prijzen van Power BI Embedded](http://go.microsoft.com/fwlink/?LinkID=760527).</span><span class="sxs-lookup"><span data-stu-id="1ea5d-118">For **Pricing**, see [Power BI Embedded pricing](http://go.microsoft.com/fwlink/?LinkID=760527).</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. <span data-ttu-id="1ea5d-119">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-119">Click **Create**.</span></span>

<span data-ttu-id="1ea5d-120">Hallo **Werkruimteverzameling** duurt enkele ogenblikken tooprovision.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-120">hello **Workspace Collection** will take a few moments tooprovision.</span></span> <span data-ttu-id="1ea5d-121">Wanneer voltooid, wordt u geleid toohello **Blade Werkruimteverzameling**.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-121">When completed, you'll be taken toohello **Workspace Collection Blade**.</span></span>

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

<span data-ttu-id="1ea5d-122">Hallo **Blade maken** Hallo-informatie die u nodig hebt toocall Hallo API's die werkruimten maken en implementeren van inhoud toothem bevat.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-122">hello **Creation Blade** contains hello information you need toocall hello APIs that create workspaces and deploy content toothem.</span></span>

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a><span data-ttu-id="1ea5d-123">Toegangssleutels voor Power BI API</span><span class="sxs-lookup"><span data-stu-id="1ea5d-123">View Power BI API access keys</span></span>

<span data-ttu-id="1ea5d-124">Een van de belangrijkste stukjes informatie die nodig is toocall Power BI REST-API's Hallo HALLO hallo zijn **toegangstoetsen**.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-124">One of hello most important pieces of information needed toocall hello Power BI REST APIs are hello **Access Keys**.</span></span> <span data-ttu-id="1ea5d-125">Dit zijn de gebruikte toogenerate hello **app-tokens** die zijn gebruikt tooauthenticate uw API-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-125">These are used toogenerate hello **app tokens** that are used tooauthenticate your API requests.</span></span> <span data-ttu-id="1ea5d-126">tooview uw **toegangssleutels**, klikt u op **toegangssleutels** op Hallo **Instellingenblade**.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-126">tooview your **Access Keys**, click **Access Keys** on hello **Settings Blade**.</span></span> <span data-ttu-id="1ea5d-127">Voor meer informatie over **app-tokens** verwijzen wij u naar [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md) (Verifiëren en autoriseren met Power BI Embedded).</span><span class="sxs-lookup"><span data-stu-id="1ea5d-127">For more about **app tokens**, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

   ![](media/power-bi-embedded-get-started/access-keys.png)

<span data-ttu-id="1ea5d-128">U ziet dat u twee sleutels hebt.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-128">You'll'notice that you have two keys.</span></span>

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

<span data-ttu-id="1ea5d-129">Kopieer deze sleutels en sla ze veilig op in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-129">Copy these keys and store them securely in your application.</span></span> <span data-ttu-id="1ea5d-130">Het is heel belangrijk dat u deze sleutels behandelen net als een wachtwoord, omdat ze bieden toegang tot tooall Hallo inhoud in uw **Werkruimteverzameling**.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-130">It's very important that you treat these keys as you would a password, because they'll provide access tooall hello content in your **Workspace Collection**.</span></span>

<span data-ttu-id="1ea5d-131">Hoewel er twee sleutels worden vermeld, hebt u er slechts één tegelijk nodig.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-131">While two keys are listed, only one key is needed at a particular time.</span></span> <span data-ttu-id="1ea5d-132">de tweede sleutel Hallo wordt geboden zodat u de sleutels regelmatig opnieuw genereert kunt zonder dat toohello-access-service wordt onderbroken.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-132">hello second key is provided so you can periodically regenerate keys without interrupting access toohello service.</span></span>

<span data-ttu-id="1ea5d-133">Nu u een exemplaar van Power BI voor uw toepassing en **toegangssleutels** hebt, kunt u een rapport in uw eigen app importeren.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-133">Now that you have an instance of Power BI for your application, and **Access Keys**, you can import a report into your own app.</span></span> <span data-ttu-id="1ea5d-134">Voordat u meer informatie over hoe maken Power BI-gegevenssets en rapporten tooembed in tooimport een verslag Hallo volgende sectie wordt beschreven in een app.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-134">Before you learn how tooimport a report, hello next section describes creating Power BI datasets and reports tooembed into an app.</span></span>

## <a name="working-with-workspaces"></a><span data-ttu-id="1ea5d-135">Werken met werkruimten</span><span class="sxs-lookup"><span data-stu-id="1ea5d-135">Working with workspaces</span></span>

<span data-ttu-id="1ea5d-136">Nadat u uw werkruimteverzameling hebt gemaakt, moet u toocreate een werkruimte die wordt uw rapporten en gegevenssets bevatten.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-136">After you have created your workspace collection, you will need toocreate a workspace that will house your reports and datasets.</span></span> <span data-ttu-id="1ea5d-137">een werkruimte toocreate, moet u toouse hello [Post Worksapce REST-API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ea5d-137">toocreate a workspace, you will need toouse hello [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a><span data-ttu-id="1ea5d-138">Power BI-gegevenssets en rapporten tooembed maken in een app met behulp van Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="1ea5d-138">Create Power BI datasets and reports tooembed into an app using Power BI Desktop</span></span>

<span data-ttu-id="1ea5d-139">Nu dat u een exemplaar van Power BI voor uw toepassing hebt gemaakt en hebben **toegangstoetsen**, moet u toocreate Hallo Power BI-gegevenssets en rapporten die u tooembed wilt.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-139">Now that you have created an instance of Power BI for your application, and have **Access Keys**, you will need toocreate hello Power BI datasets and reports that you want tooembed.</span></span> <span data-ttu-id="1ea5d-140">Gegevenssets en rapporten kunnen worden gemaakt met behulp van **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-140">Datasets and reports can be created by using **Power BI Desktop**.</span></span> <span data-ttu-id="1ea5d-141">U kunt [Power BI Desktop gratis](https://go.microsoft.com/fwlink/?LinkId=521662) downloaden.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-141">You can download [Power BI Desktop for free](https://go.microsoft.com/fwlink/?LinkId=521662).</span></span> <span data-ttu-id="1ea5d-142">Of, tooquickly aan de slag, kunt u downloaden Hallo [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="1ea5d-142">Or, tooquickly get started, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>

> [!NOTE]
> <span data-ttu-id="1ea5d-143">meer informatie over hoe toolearn toouse **Power BI Desktop**, Zie [aan de slag met Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span><span class="sxs-lookup"><span data-stu-id="1ea5d-143">toolearn more about how toouse **Power BI Desktop**, see [Getting Started with Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span></span>

<span data-ttu-id="1ea5d-144">Met **Power BI Desktop**, u verbinding maken met gegevensbron tooyour door het importeren van een kopie van gegevens in Hallo **Power BI Desktop** of toohello gegevens rechtstreeks verbinding maken met behulp van de gegevensbron **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-144">With **Power BI Desktop**, you connect tooyour data source by importing a copy of hello data into **Power BI Desktop** or connecting directly toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="1ea5d-145">Hier volgen Hallo verschillen tussen het gebruik van **importeren** en **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-145">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="1ea5d-146">Importeren</span><span class="sxs-lookup"><span data-stu-id="1ea5d-146">Import</span></span> | <span data-ttu-id="1ea5d-147">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="1ea5d-147">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="1ea5d-148">Tabellen, kolommen *en gegevens* worden geïmporteerd of gekopieerd naar **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-148">Tables, columns, *and data* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="1ea5d-149">Als u met visualisaties werkt, **Power BI Desktop** een kopie van Hallo gegevens opvraagt.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-149">As you work with visualizations, **Power BI Desktop** queries a copy of hello data.</span></span> <span data-ttu-id="1ea5d-150">toosee eventueel opgetreden toohello onderliggende gegevens wijzigen, moet u vernieuwen of importeren, een volledige, actuele gegevensset opnieuw.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-150">toosee any changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="1ea5d-151">Alleen *tabellen en kolommen* worden geïmporteerd of gekopieerd naar **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-151">Only *tables and columns* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="1ea5d-152">Als u met visualisaties werkt, **Power BI Desktop** query's onderliggende gegevensbron, wat betekent dat u altijd actuele gegevens bekijkt hello.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-152">As you work with visualizations, **Power BI Desktop** queries hello underlying data source, which means you're always viewing current data.</span></span> |

<span data-ttu-id="1ea5d-153">Zie voor meer informatie over het maken van verbinding tooa gegevensbron [Connect tooa gegevensbron](power-bi-embedded-connect-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="1ea5d-153">For more about connecting tooa data source, see [Connect tooa data source](power-bi-embedded-connect-datasource.md).</span></span>

<span data-ttu-id="1ea5d-154">Nadat u uw werk in **Power BI Desktop** hebt opgeslagen, wordt een PBIX-bestand gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-154">After you save your work in **Power BI Desktop**, a PBIX file is created.</span></span> <span data-ttu-id="1ea5d-155">Dit bestand bevat het rapport.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-155">This file contains your report.</span></span> <span data-ttu-id="1ea5d-156">Bovendien, als u gegevens Hallo PBIX bevat importeert Hallo volledige gegevensset of als u **DirectQuery**, Hallo PBIX bevat een gegevensset-schema.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-156">In addition, if you import data hello PBIX contains hello complete dataset, or if you use **DirectQuery**, hello PBIX contains just a dataset schema.</span></span> <span data-ttu-id="1ea5d-157">U Hallo PBIX programmatisch implementeren in de werkruimte op basis van Hallo [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ea5d-157">You programmatically deploy hello PBIX into your workspace using hello [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="1ea5d-158">**Power BI Embedded** heeft aanvullende API's toochange Hallo-server en database dat uw gegevensset tooand set accountreferenties die Hallo gegevensset wijst tooconnect tooyour database gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-158">**Power BI Embedded** has additional APIs toochange hello server and database that your dataset is pointing tooand set a service account credential that hello dataset will use tooconnect tooyour database.</span></span> <span data-ttu-id="1ea5d-159">Zie [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) en [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ea5d-159">See [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) and [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-using-apis"></a><span data-ttu-id="1ea5d-160">Power BI-gegevenssets en -rapporten maken met behulp van API's</span><span class="sxs-lookup"><span data-stu-id="1ea5d-160">Create Power BI datasets and reports using APIs</span></span>

### <a name="datsets"></a><span data-ttu-id="1ea5d-161">Gegevenssets</span><span class="sxs-lookup"><span data-stu-id="1ea5d-161">Datsets</span></span>

<span data-ttu-id="1ea5d-162">U kunt de gegevenssets in Power BI Embedded met Hallo REST-API maken.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-162">You can create datasets within Power BI Embedded using hello REST API.</span></span> <span data-ttu-id="1ea5d-163">Vervolgens kunt u gegevens naar uw gegevensset pushen.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-163">You can then push data into your dataset.</span></span> <span data-ttu-id="1ea5d-164">Hiermee kunt u toowork met gegevens zonder Hallo van Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-164">This allows you toowork with data without hello need of Power BI Desktop.</span></span> <span data-ttu-id="1ea5d-165">Zie [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx) (Gegevenssets posten) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-165">For more information, see [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span></span>

### <a name="reports"></a><span data-ttu-id="1ea5d-166">Rapporten</span><span class="sxs-lookup"><span data-stu-id="1ea5d-166">Reports</span></span>

<span data-ttu-id="1ea5d-167">U kunt een rapport maken uit een gegevensset rechtstreeks in uw toepassing met behulp van Hallo JavaScript-API.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-167">You can create a report from a dataset directly in your application using hello JavaScript API.</span></span> <span data-ttu-id="1ea5d-168">Zie [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Een nieuw rapport maken uit een gegevensset in Power BI Embedded) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1ea5d-168">For more information, see [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="1ea5d-169">Zie ook</span><span class="sxs-lookup"><span data-stu-id="1ea5d-169">See Also</span></span>

[<span data-ttu-id="1ea5d-170">Aan de slag met het voorbeeld</span><span class="sxs-lookup"><span data-stu-id="1ea5d-170">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="1ea5d-171">Verifiëren en autoriseren in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="1ea5d-171">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="1ea5d-172">Een rapport insluiten</span><span class="sxs-lookup"><span data-stu-id="1ea5d-172">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
<span data-ttu-id="1ea5d-173">[Een nieuw rapport maken uit een gegevensset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Rapporten opslaan](power-bi-embedded-save-reports.md)</span><span class="sxs-lookup"><span data-stu-id="1ea5d-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Save reports](power-bi-embedded-save-reports.md)</span></span>  
[<span data-ttu-id="1ea5d-174">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="1ea5d-174">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="1ea5d-175">Voorbeeld van ingesloten JavaScript</span><span class="sxs-lookup"><span data-stu-id="1ea5d-175">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="1ea5d-176">Nog vragen?</span><span class="sxs-lookup"><span data-stu-id="1ea5d-176">More questions?</span></span> [<span data-ttu-id="1ea5d-177">Probeer Hallo Power BI-Community</span><span class="sxs-lookup"><span data-stu-id="1ea5d-177">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

