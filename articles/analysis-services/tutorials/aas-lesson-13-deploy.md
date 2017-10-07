---
<span data-ttu-id="b2953-101">titel: aaa "Azure Analysis Services-zelfstudie les 13: implementeren | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toodeploy Hallo zelfstudie project tooAzure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="b2953-101">title: aaa"Azure Analysis Services tutorial lesson 13: Deploy | Microsoft Docs" description:  Describes how toodeploy hello tutorial project tooAzure Analysis Services.</span></span>
<span data-ttu-id="b2953-102">Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''</span><span class="sxs-lookup"><span data-stu-id="b2953-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="b2953-103">MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: n.v.t. ms.date: 17-07/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="b2953-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 07/17/2017 ms.author: owend</span></span>
---
# <a name="lesson-13-deploy"></a><span data-ttu-id="b2953-104">Les 13: Implementeren</span><span class="sxs-lookup"><span data-stu-id="b2953-104">Lesson 13: Deploy</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="b2953-105">In deze les configureert u de eigenschappen van implementatie; een Azure Analysis Services server toodeploy tooand een naam voor het Hallo-model op te geven.</span><span class="sxs-lookup"><span data-stu-id="b2953-105">In this lesson, you configure deployment properties; specifying an Azure Analysis Services server toodeploy tooand a name for hello model.</span></span> <span data-ttu-id="b2953-106">Vervolgens implementeert u Hallo model toothat exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b2953-106">You then deploy hello model toothat instance.</span></span> <span data-ttu-id="b2953-107">Nadat uw model is geïmplementeerd, kunnen gebruikers verbinding maken tooit met behulp van een reporting clienttoepassing.</span><span class="sxs-lookup"><span data-stu-id="b2953-107">After your model is deployed, users can connect tooit by using a reporting client application.</span></span> <span data-ttu-id="b2953-108">toolearn meer, Zie [tooAzure Analysis Services implementeren](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span><span class="sxs-lookup"><span data-stu-id="b2953-108">toolearn more, see [Deploy tooAzure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span></span>  
  
<span data-ttu-id="b2953-109">Geschatte tijd toocomplete deze les: **5 minuten**</span><span class="sxs-lookup"><span data-stu-id="b2953-109">Estimated time toocomplete this lesson: **5 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="b2953-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b2953-110">Prerequisites</span></span>  
<span data-ttu-id="b2953-111">Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b2953-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="b2953-112">Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 12: analyseren in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="b2953-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="b2953-113">U moet hebben [beheerdersmachtigingen](../analysis-services-server-admins.md) op Hallo externe Analysis Services-server in de volgorde toodeploy tooit.</span><span class="sxs-lookup"><span data-stu-id="b2953-113">You must have [Administrator permissions](../analysis-services-server-admins.md) on hello remote Analysis Services server in-order toodeploy tooit.</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="b2953-114">Als u de voorbeelddatabase Hallo AdventureWorksDW2014 geïnstalleerd op een lokale SQL Server en u bij het implementeren van uw model tooan Azure Analysis Services-server een [On-premises gegevensgateway](../analysis-services-gateway.md) is vereist.</span><span class="sxs-lookup"><span data-stu-id="b2953-114">If you installed hello AdventureWorksDW2014 sample database on an on-premises SQL Server, and you're deploying your model tooan Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>
  
## <a name="deploy-hello-model"></a><span data-ttu-id="b2953-115">Hallo model implementeren</span><span class="sxs-lookup"><span data-stu-id="b2953-115">Deploy hello model</span></span>  
  
#### <a name="tooconfigure-deployment-properties"></a><span data-ttu-id="b2953-116">tooconfigure implementatie-eigenschappen</span><span class="sxs-lookup"><span data-stu-id="b2953-116">tooconfigure deployment properties</span></span>  

  
1.  <span data-ttu-id="b2953-117">In **Solution Explorer**, klik met de rechtermuisknop Hallo **AW Internet verkoop** project en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="b2953-117">In **Solution Explorer**, right-click hello **AW Internet Sales** project, and then click **Properties**.</span></span>  
  
2.  <span data-ttu-id="b2953-118">In Hallo **AW Internet verkoop eigenschappenpagina's** dialoogvenster onder **implementatieserver**, in Hallo **Server** -eigenschap geeft u de volledige server Hallo.</span><span class="sxs-lookup"><span data-stu-id="b2953-118">In hello **AW Internet Sales Property Pages** dialog box, under **Deployment Server**, in hello **Server** property, enter hello full server.</span></span>  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  <span data-ttu-id="b2953-120">In Hallo **Database** eigenschap, type **Adventure Works Internet verkoop**.</span><span class="sxs-lookup"><span data-stu-id="b2953-120">In hello **Database** property, type **Adventure Works Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="b2953-121">In Hallo **modelnaam** eigenschap, type **Adventure Works Internet verkoopmodel**.</span><span class="sxs-lookup"><span data-stu-id="b2953-121">In hello **Model Name** property, type **Adventure Works Internet Sales Model**.</span></span>  
  
5.  <span data-ttu-id="b2953-122">Controleer de invoer en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2953-122">Verify your selections and then click **OK**.</span></span>  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a><span data-ttu-id="b2953-123">toodeploy hello Adventure Works Internet verkoop</span><span class="sxs-lookup"><span data-stu-id="b2953-123">toodeploy hello Adventure Works Internet Sales</span></span>
  
1.  <span data-ttu-id="b2953-124">In **Solution Explorer**, klik met de rechtermuisknop Hallo **AW Internet verkoop** project > **bouwen**.</span><span class="sxs-lookup"><span data-stu-id="b2953-124">In **Solution Explorer**, right-click hello **AW Internet Sales** project > **Build**.</span></span>  

2.  <span data-ttu-id="b2953-125">Klik met de rechtermuisknop Hallo **AW Internet verkoop** project > **implementeren**.</span><span class="sxs-lookup"><span data-stu-id="b2953-125">Right-click hello **AW Internet Sales** project > **Deploy**.</span></span>

    <span data-ttu-id="b2953-126">Bij het implementeren van tooAzure Analysis Services kan worden na vragen aan gebruiker tooenter uw account.</span><span class="sxs-lookup"><span data-stu-id="b2953-126">When deploying tooAzure Analysis Services, you may be prompted tooenter your account.</span></span> <span data-ttu-id="b2953-127">Voer in dat geval uw organisatieaccount en het bijbehorende wachtwoord in, zoals nancy@adventureworks.com. Dit account moet zich in beheerders op Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="b2953-127">Enter your organizational account and password, for example nancy@adventureworks.com. This account must be in Admins on hello server.</span></span>
  
    <span data-ttu-id="b2953-128">Hallo implementeren dialoogvenster wordt weergegeven en toont de implementatiestatus Hallo Hallo metagegevens en elke tabel die is opgenomen in het Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="b2953-128">hello Deploy dialog box appears and displays hello deployment status of hello metadata and each table included in hello model.</span></span>  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. <span data-ttu-id="b2953-130">Als de implementatie is voltooid, kunt u op **Close** klikken.</span><span class="sxs-lookup"><span data-stu-id="b2953-130">When deployment successfully completes, go ahead and click **Close**.</span></span>  
  
## <a name="conclusion"></a><span data-ttu-id="b2953-131">Conclusie</span><span class="sxs-lookup"><span data-stu-id="b2953-131">Conclusion</span></span>  
<span data-ttu-id="b2953-132">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="b2953-132">Congratulations!</span></span> <span data-ttu-id="b2953-133">U bent klaar met het ontwerpen en implementeren van uw eerste tabellaire model van Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="b2953-133">You're finished authoring and deploying your first Analysis Services Tabular model.</span></span> <span data-ttu-id="b2953-134">Deze zelfstudie heeft geholpen helpt u bij het voltooien van de meest algemene taken Hallo bij het maken van een model in tabelvorm.</span><span class="sxs-lookup"><span data-stu-id="b2953-134">This tutorial has helped guide you through completing hello most common tasks in creating a tabular model.</span></span> <span data-ttu-id="b2953-135">Nu dat uw Adventure Works Internet verkoop-model is geïmplementeerd, kunt u SQL Server Management Studio toomanage Hallo model; proces-scripts en een back-upplan maken.</span><span class="sxs-lookup"><span data-stu-id="b2953-135">Now that your Adventure Works Internet Sales model is deployed, you can use SQL Server Management Studio toomanage hello model; create process scripts and a backup plan.</span></span> <span data-ttu-id="b2953-136">Gebruikers kunnen nu ook verbinding maken met behulp van een reporting clienttoepassing, zoals Microsoft Excel of Power BI toohello-model.</span><span class="sxs-lookup"><span data-stu-id="b2953-136">Users can also now connect toohello model using a reporting client application such as Microsoft Excel or Power BI.</span></span>  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a><span data-ttu-id="b2953-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b2953-138">What's next?</span></span>
<span data-ttu-id="b2953-139">[Verbinden met Power BI Desktop](../analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="b2953-139">[Connect with Power BI Desktop](../analysis-services-connect-pbi.md) </span></span>  
<span data-ttu-id="b2953-140">[Aanvullende les: Dynamische beveiliging](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span><span class="sxs-lookup"><span data-stu-id="b2953-140">[Supplemental Lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span></span>  
<span data-ttu-id="b2953-141">[Aanvullende les: Detailrijen](../tutorials/aas-supplemental-lesson-detail-rows.md) </span><span class="sxs-lookup"><span data-stu-id="b2953-141">[Supplemental Lesson - Detail rows](../tutorials/aas-supplemental-lesson-detail-rows.md) </span></span>  
[<span data-ttu-id="b2953-142">Aanvullende les: Onregelmatige hiërarchieën</span><span class="sxs-lookup"><span data-stu-id="b2953-142">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
