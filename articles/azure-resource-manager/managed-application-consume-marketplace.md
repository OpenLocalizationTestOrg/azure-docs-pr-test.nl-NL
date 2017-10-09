---
title: aaaConsume Azure beheerde toepassing in de marketplace | Microsoft Docs
description: Describeshow toocreate een Azure beheerde toepassing die beschikbaar is via Hallo Marketplace.
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 9ae6e11a3f63eb58a9f3199364b5606a7afe5618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="consume-azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="b5822-103">Azure gebruiken beheerde toepassingen in Hallo Marketplace</span><span class="sxs-lookup"><span data-stu-id="b5822-103">Consume Azure managed applications in hello Marketplace</span></span>

<span data-ttu-id="b5822-104">Zoals beschreven in Hallo [overzicht van beheerde toepassingen](managed-application-overview.md) artikel, er zijn twee scenario's in Hallo end tooend ervaring.</span><span class="sxs-lookup"><span data-stu-id="b5822-104">As discussed in hello [Managed Application overview](managed-application-overview.md) article, there are two scenarios in hello end tooend experience.</span></span> <span data-ttu-id="b5822-105">Een is Hallo uitgever of de leverancier die wil toocreate een beheerde toepassing voor gebruik door klanten.</span><span class="sxs-lookup"><span data-stu-id="b5822-105">One is hello publisher or vendor who wants toocreate a managed application for use by customers.</span></span> <span data-ttu-id="b5822-106">Hallo is het tweede Hallo end klant of Hallo consumer van de toepassing hello beheerd.</span><span class="sxs-lookup"><span data-stu-id="b5822-106">hello second is hello end customer or hello consumer of hello managed application.</span></span> <span data-ttu-id="b5822-107">In dit artikel bevat informatie over het tweede scenario Hallo.</span><span class="sxs-lookup"><span data-stu-id="b5822-107">This article covers hello second scenario.</span></span> <span data-ttu-id="b5822-108">Hierin wordt beschreven hoe u een beheerde toepassing van Microsoft Azure Marketplace Hallo kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="b5822-108">It describes how you can deploy a managed application from hello Microsoft Azure Marketplace.</span></span>

## <a name="create-from-hello-marketplace"></a><span data-ttu-id="b5822-109">Maken van Hallo Marketplace</span><span class="sxs-lookup"><span data-stu-id="b5822-109">Create from hello Marketplace</span></span>

<span data-ttu-id="b5822-110">Implementatie van een beheerde toepassing hello Marketplace is vergelijkbaar toodeploying elk type resources uit Hallo Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b5822-110">Deploying a managed application from hello Marketplace is similar toodeploying any type of resources from hello Marketplace.</span></span> 

<span data-ttu-id="b5822-111">Selecteer in de portal Hallo **+ nieuw** en zoek naar de oplossing toodeploy Hallo type.</span><span class="sxs-lookup"><span data-stu-id="b5822-111">In hello portal, select **+ New** and search for hello type of solution toodeploy.</span></span> <span data-ttu-id="b5822-112">Selecteer uit de beschikbare opties hello, Hallo gewenste.</span><span class="sxs-lookup"><span data-stu-id="b5822-112">From hello available options, select hello one you need.</span></span>

![zoekoplossingen](./media/managed-application-consume-marketplace/search-apps.png)

<span data-ttu-id="b5822-114">Hallo staat een overzicht van de toepassing hello en selecteer **maken**.</span><span class="sxs-lookup"><span data-stu-id="b5822-114">Review hello summary of hello application, and select **Create**.</span></span>

![beheerde toepassing maken](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

<span data-ttu-id="b5822-116">Als een andere oplossing krijgt u velden tooprovide waarden voor.</span><span class="sxs-lookup"><span data-stu-id="b5822-116">Like any other solution, you are presented with fields tooprovide values for.</span></span> <span data-ttu-id="b5822-117">Deze velden verschillen per Hallo type beheerde toepassing die u maakt.</span><span class="sxs-lookup"><span data-stu-id="b5822-117">These fields vary by hello type of managed application you create.</span></span> 

## <a name="view-support-information"></a><span data-ttu-id="b5822-118">Informatie over de ondersteuning van weergeven</span><span class="sxs-lookup"><span data-stu-id="b5822-118">View support information</span></span>

<span data-ttu-id="b5822-119">Nadat uw beheerde toepassing heeft geïmplementeerd, Hallo ondersteuning gegevens weergeven voor de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="b5822-119">After your managed application has deployed, view hello support information for hello application.</span></span> <span data-ttu-id="b5822-120">In de blade beheerde toepassing hello wordt Hallo ondersteuningsinformatie vermeld.</span><span class="sxs-lookup"><span data-stu-id="b5822-120">In hello managed application blade, hello support information is listed.</span></span>

![Ondersteuning](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a><span data-ttu-id="b5822-122">Machtigingen van de uitgever weergeven</span><span class="sxs-lookup"><span data-stu-id="b5822-122">View publisher permissions</span></span>

<span data-ttu-id="b5822-123">Hallo-leverancier die uw toepassing beheert krijgt toegang tot tooyour bronnen.</span><span class="sxs-lookup"><span data-stu-id="b5822-123">hello vendor that manages your application is granted access tooyour resources.</span></span> <span data-ttu-id="b5822-124">selecteert u deze machtigingen toosee **autorisaties**.</span><span class="sxs-lookup"><span data-stu-id="b5822-124">toosee those permissions, select **Authorizations**.</span></span>

![autorisaties](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a><span data-ttu-id="b5822-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b5822-126">Next steps</span></span>

* <span data-ttu-id="b5822-127">Zie voor meer informatie over het publiceren van een beheerde toepassing in Hallo Marketplace [Azure beheerde toepassingen in de Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="b5822-127">For information about publishing a managed application in hello Marketplace, see [Azure Managed Applications in Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="b5822-128">toopublish beheerde toepassingen die alleen beschikbaar toousers in uw organisatie zijn, Zie [maken en publiceren van beheerde servicetoepassing catalogus](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="b5822-128">toopublish managed applications that are only available toousers in your organization, see [Create and publish Service Catalog Managed Application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="b5822-129">tooconsume beheerde toepassingen die alleen beschikbaar toousers in uw organisatie zijn, Zie [Service catalogus beheerde toepassingen gebruiken](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="b5822-129">tooconsume managed applications that are only available toousers in your organization, see [Consume a Service Catalog Managed Application](managed-application-consumption.md).</span></span>
