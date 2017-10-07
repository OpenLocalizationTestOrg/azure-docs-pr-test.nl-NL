---
title: aaaCreating webservice-eindpunten in Machine Learning | Microsoft Docs
description: Webservice-eindpunten maken in Azure Machine Learning
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="84dbf-103">Eindpunten maken</span><span class="sxs-lookup"><span data-stu-id="84dbf-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="84dbf-104">Dit onderwerp wordt beschreven technieken toepasselijke tooa **klassieke** Machine Learning-webservice.</span><span class="sxs-lookup"><span data-stu-id="84dbf-104">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="84dbf-105">Wanneer u webservices die u doorsturen tooyour klanten verkoopt maakt, moet u tooprovide getraind modellen tooeach klant die nog steeds gekoppelde toohello experiment uit welke Hallo Web service is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="84dbf-105">When you create Web services that you sell forward tooyour customers, you need tooprovide trained models tooeach customer that are still linked toohello experiment from which hello Web service was created.</span></span> <span data-ttu-id="84dbf-106">Bovendien geen updates toohello experiment moet worden toegepast selectief tooan eindpunt zonder Hallo aanpassingen wordt overschreven.</span><span class="sxs-lookup"><span data-stu-id="84dbf-106">In addition, any updates toohello experiment should be applied selectively tooan endpoint without overwriting hello customizations.</span></span>

<span data-ttu-id="84dbf-107">tooaccomplish, kunt u in Azure Machine Learning toocreate meerdere eindpunten voor een geïmplementeerde webservice.</span><span class="sxs-lookup"><span data-stu-id="84dbf-107">tooaccomplish this, Azure Machine Learning allows you toocreate multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="84dbf-108">Elk eindpunt in Hallo-webservice is onafhankelijk geadresseerd, beperkt en beheerd.</span><span class="sxs-lookup"><span data-stu-id="84dbf-108">Each endpoint in hello Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="84dbf-109">Elk eindpunt is een unieke URL's en autorisatie sleutel tooyour klanten kunt distribueren.</span><span class="sxs-lookup"><span data-stu-id="84dbf-109">Each endpoint is a unique URL and authorization key that you can distribute tooyour customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a><span data-ttu-id="84dbf-110">Toevoegen van eindpunten tooa-webservice</span><span class="sxs-lookup"><span data-stu-id="84dbf-110">Adding endpoints tooa Web service</span></span>
<span data-ttu-id="84dbf-111">Er zijn drie manieren tooadd een eindpunt tooa webservice.</span><span class="sxs-lookup"><span data-stu-id="84dbf-111">There are three ways tooadd an endpoint tooa Web service.</span></span>

* <span data-ttu-id="84dbf-112">Programmatisch</span><span class="sxs-lookup"><span data-stu-id="84dbf-112">Programmatically</span></span>
* <span data-ttu-id="84dbf-113">Via hello Azure Machine Learning-webservices-portal</span><span class="sxs-lookup"><span data-stu-id="84dbf-113">Through hello Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="84dbf-114">Hoewel Hallo klassieke Azure-portal</span><span class="sxs-lookup"><span data-stu-id="84dbf-114">Though hello Azure classic portal</span></span>

<span data-ttu-id="84dbf-115">Zodra het Hallo-eindpunt is gemaakt, kunt u deze via synchrone API's, batch-API's, gebruiken en excel-werkbladen.</span><span class="sxs-lookup"><span data-stu-id="84dbf-115">Once hello endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="84dbf-116">Bovendien tooadding eindpunten via deze gebruikersinterface, u kunt ook Hallo eindpunt Management-API's tooprogrammatically toevoegen van eindpunten.</span><span class="sxs-lookup"><span data-stu-id="84dbf-116">In addition tooadding endpoints through this UI, you can also use hello Endpoint Management APIs tooprogrammatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="84dbf-117">Als u extra eindpunten toohello webservice hebt toegevoegd, kunt u het standaardeindpunt Hallo niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="84dbf-117">If you have added additional endpoints toohello Web service, you cannot delete hello default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="84dbf-118">Een eindpunt toevoegen programmatisch</span><span class="sxs-lookup"><span data-stu-id="84dbf-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="84dbf-119">U kunt een eindpunt tooyour webservice programmatisch met behulp van Hallo toevoegen [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="84dbf-119">You can add an endpoint tooyour Web service programmatically using hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="84dbf-120">Toevoegen van een eindpunt met hello Azure Machine Learning-webservices-portal</span><span class="sxs-lookup"><span data-stu-id="84dbf-120">Adding an endpoint using hello Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="84dbf-121">Klik op Web-Services op Hallo linkernavigatievenster kolom in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="84dbf-121">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="84dbf-122">Aan de onderkant van de Hallo van Hallo Web servicedashboard, klikt u op **eindpunten beheren**.</span><span class="sxs-lookup"><span data-stu-id="84dbf-122">At hello bottom of hello Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="84dbf-123">Hello Azure Machine Learning-webservices portal opent toohello eindpunten pagina voor het Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="84dbf-123">hello Azure Machine Learning Web Services portal opens toohello endpoints page for hello Web service.</span></span>
3. <span data-ttu-id="84dbf-124">Klik op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="84dbf-124">Click **New**.</span></span>
4. <span data-ttu-id="84dbf-125">Typ een naam en beschrijving voor het nieuwe eindpunt Hallo.</span><span class="sxs-lookup"><span data-stu-id="84dbf-125">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="84dbf-126">Namen van eindpunten moeten 24 tekens of minder lang zijn en moeten bestaan uit kleine letters of cijfers.</span><span class="sxs-lookup"><span data-stu-id="84dbf-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="84dbf-127">Selecteer het logboekregistratieniveau Hallo en of voorbeeldgegevens is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="84dbf-127">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="84dbf-128">Zie voor meer informatie over logboekregistratie [inschakelen van logboekregistratie voor Machine Learning-webservices](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="84dbf-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a><span data-ttu-id="84dbf-129">Toevoegen van een eindpunt met behulp van Hallo klassieke Azure-portal</span><span class="sxs-lookup"><span data-stu-id="84dbf-129">Adding an endpoint using hello Azure classic portal</span></span>
1. <span data-ttu-id="84dbf-130">Meld u aan toohello [klassieke Azure-portal](http://manage.windowsazure.com), klikt u op **Machine Learning** in de linkerkolom Hallo.</span><span class="sxs-lookup"><span data-stu-id="84dbf-130">Sign in toohello [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in hello left column.</span></span> <span data-ttu-id="84dbf-131">Klik op Hallo werkruimte waarin Hallo webservice waarin u geïnteresseerd bent.</span><span class="sxs-lookup"><span data-stu-id="84dbf-131">Click hello workspace which contains hello Web service in which you are interested.</span></span>
   
    ![Navigeer tooworkspace](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="84dbf-133">Klik op **webservices**.</span><span class="sxs-lookup"><span data-stu-id="84dbf-133">Click **Web Services**.</span></span>
   
    ![Navigeer tooWeb services](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="84dbf-135">Klik op Hallo webservice u geïnteresseerd bent in toosee Hallo lijst met beschikbare eindpunten.</span><span class="sxs-lookup"><span data-stu-id="84dbf-135">Click hello Web service you're interested in toosee hello list of available endpoints.</span></span>
   
    ![Navigeer tooendpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="84dbf-137">Klik onder aan de pagina Hallo Hallo op **eindpunt toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="84dbf-137">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="84dbf-138">Typ een naam en beschrijving, zorg ervoor dat er zijn geen andere eindpunten met dezelfde naam in deze webservice Hallo.</span><span class="sxs-lookup"><span data-stu-id="84dbf-138">Type a name and description, ensure there are no other endpoints with hello same name in this Web service.</span></span> <span data-ttu-id="84dbf-139">Tenzij u speciale vereisten hebt, laat u Hallo versnelling niveau met de standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="84dbf-139">Leave hello throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="84dbf-140">toolearn meer informatie over beperking, Zie [API-eindpunten schalen](machine-learning-scaling-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="84dbf-140">toolearn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![Eindpunt maken](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="84dbf-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="84dbf-142">Next Steps</span></span>
<span data-ttu-id="84dbf-143">[Hoe een Azure Machine Learning-webservice tooconsume](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="84dbf-143">[How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

