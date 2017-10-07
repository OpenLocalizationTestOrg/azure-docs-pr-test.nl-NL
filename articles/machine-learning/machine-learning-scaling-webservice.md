---
title: aaaHow tooincrease gelijktijdigheid van een Azure Machine Learning-webservice | Microsoft Docs
description: Meer informatie over hoe tooincrease gelijktijdigheid van een Azure Machine Learning-webservice door extra eindpunten toe te voegen.
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: Azure machine learning-webservices, uitoefening, schaal, eindpunt, gelijktijdigheid van taken
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="04a35-104">Een Azure Machine Learning-webservice schalen door extra eindpunten toe te voegen</span><span class="sxs-lookup"><span data-stu-id="04a35-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="04a35-105">Dit onderwerp wordt beschreven technieken toepasselijke tooa **klassieke** Machine Learning-webservice.</span><span class="sxs-lookup"><span data-stu-id="04a35-105">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="04a35-106">Standaard elke gepubliceerde webservice geconfigureerde toosupport is 20 gelijktijdige aanvragen en mag maximaal 200 gelijktijdige aanvragen.</span><span class="sxs-lookup"><span data-stu-id="04a35-106">By default, each published Web service is configured toosupport 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="04a35-107">Hoewel Hallo klassieke Azure-portal een manier tooset deze waarde biedt, Azure Machine Learning optimaliseert automatisch Hallo instelling tooprovide Hallo optimale prestaties van uw web-service en portal Hallo-waarde wordt genegeerd.</span><span class="sxs-lookup"><span data-stu-id="04a35-107">While hello Azure classic portal provides a way tooset this value, Azure Machine Learning automatically optimizes hello setting tooprovide hello best performance for your web service and hello portal value is ignored.</span></span> 

<span data-ttu-id="04a35-108">Als u van plan toocall Hallo API met een hogere belasting bent dan een waarde van het maximumaantal gelijktijdige aanroepen van 200 wordt ondersteunen, moet u meerdere eindpunten maken op Hallo dezelfde webservice.</span><span class="sxs-lookup"><span data-stu-id="04a35-108">If you plan toocall hello API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on hello same Web service.</span></span> <span data-ttu-id="04a35-109">U kunt uw load willekeurig distribueren voor alle hiervan.</span><span class="sxs-lookup"><span data-stu-id="04a35-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="04a35-110">Hallo schalen van een webservice is een algemene taak.</span><span class="sxs-lookup"><span data-stu-id="04a35-110">hello scaling of a Web service is a common task.</span></span> <span data-ttu-id="04a35-111">Een aantal redenen tooscale zijn toosupport meer dan 200 gelijktijdige aanvragen, beschikbaarheid via meerdere eindpunten te verbeteren of afzonderlijke eindpunten voor Hallo webservice leveren.</span><span class="sxs-lookup"><span data-stu-id="04a35-111">Some reasons tooscale are toosupport more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for hello web service.</span></span> <span data-ttu-id="04a35-112">U kunt Hallo schaal verhogen door toe te voegen extra eindpunten voor Hallo dezelfde webservice via [klassieke Azure-portal](https://manage.windowsazure.com/) of Hallo [Azure Machine Learning-webservice](https://services.azureml.net/) portal.</span><span class="sxs-lookup"><span data-stu-id="04a35-112">You can increase hello scale by adding additional endpoints for hello same Web service through [Azure classic portal](https://manage.windowsazure.com/) or hello [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="04a35-113">Zie voor meer informatie over het toevoegen van nieuwe eindpunten [eindpunten maken](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="04a35-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="04a35-114">Houd er rekening mee dat met een aantal hoge gelijktijdigheid schadelijk als u geen Hallo API met een navenant hoge frequentie bellen.</span><span class="sxs-lookup"><span data-stu-id="04a35-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling hello API with a correspondingly high rate.</span></span> <span data-ttu-id="04a35-115">U ziet sporadisch time-outs en/of pieken in Hallo latentie als u een relatief lage belasting voor een API die is geconfigureerd voor hoge belasting.</span><span class="sxs-lookup"><span data-stu-id="04a35-115">You might see sporadic timeouts and/or spikes in hello latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="04a35-116">Hallo die synchrone API's worden meestal gebruikt in situaties waarin een lage latentie gewenst is.</span><span class="sxs-lookup"><span data-stu-id="04a35-116">hello synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="04a35-117">Latentie hier impliceert Hallo tijd het duurt voordat een aanvraag van Hallo API toocomplete en niet-account voor elke vertragingen in het netwerk.</span><span class="sxs-lookup"><span data-stu-id="04a35-117">Latency here implies hello time it takes for hello API toocomplete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="04a35-118">Stel dat u hebt een API met een latentie van 50-ms.</span><span class="sxs-lookup"><span data-stu-id="04a35-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="04a35-119">toofully gebruiken voor de beschikbare capaciteit Hallo met vertraging niveau Hoog- en maximumaantal gelijktijdige aanroepen = 20, moet u toocall na deze API 20 * 1000 / 50 = 400 keren per seconde.</span><span class="sxs-lookup"><span data-stu-id="04a35-119">toofully consume hello available capacity with throttle level High and Max Concurrent Calls = 20, you need toocall this API 20 * 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="04a35-120">Dit verder uitbreiden, kunt een maximumaantal gelijktijdige aanroepen van 200 u toocall Hallo API 4000 keren per seconde, ervan uitgaande dat een 50 ms latentie.</span><span class="sxs-lookup"><span data-stu-id="04a35-120">Extending this further, a Max Concurrent Calls of 200 allows you toocall hello API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
