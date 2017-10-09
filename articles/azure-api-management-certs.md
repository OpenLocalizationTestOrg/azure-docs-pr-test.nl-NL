---
title: een Azure-API-Beheercertificaat aaaUpload | Microsoft Docs
description: Meer informatie over hoe tooupload athe Management-API van het certificaat voor Hallo klassieke Azure-Portal.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a><span data-ttu-id="91f5f-103">Een Azure Management API Management-certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="91f5f-103">Upload an Azure Management API Management Certificate</span></span>
<span data-ttu-id="91f5f-104">Van beheercertificaten kunnen tooauthenticate met het klassieke implementatiemodel Hallo verstrekt door Azure.</span><span class="sxs-lookup"><span data-stu-id="91f5f-104">Management certificates allow you tooauthenticate with hello classic deployment model provided by Azure.</span></span> <span data-ttu-id="91f5f-105">Veel programma's en hulpprogramma's (zoals Visual Studio of hello Azure SDK) gebruiken deze certificaten tooautomate configuratie en implementatie van verschillende Azure-services.</span><span class="sxs-lookup"><span data-stu-id="91f5f-105">Many programs and tools (such as Visual Studio or hello Azure SDK) use these certificates tooautomate configuration and deployment of various Azure services.</span></span> 

> [!WARNING]
> <span data-ttu-id="91f5f-106">Wees voorzichtig!</span><span class="sxs-lookup"><span data-stu-id="91f5f-106">Be careful!</span></span> <span data-ttu-id="91f5f-107">Deze typen certificaten dat alle gebruikers worden geverifieerd met hen toomanage Hallo abonnement ze zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="91f5f-107">These types of certificates allow anyone who authenticates with them toomanage hello subscription they are associated with.</span></span>
>
>

<span data-ttu-id="91f5f-108">Als u meer informatie over Azure-certificaten (zoals het maken een zelfondertekend certificaat), Zie [certificaten voor Azure Cloud Services-overzicht](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span><span class="sxs-lookup"><span data-stu-id="91f5f-108">If you'd like more information about Azure certificates (including creating a self-signed certificate), see [Certificates overview for Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="91f5f-109">U kunt ook [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate-clientcode voor automatisering doeleinden.</span><span class="sxs-lookup"><span data-stu-id="91f5f-109">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate client-code for automation purposes.</span></span>

## <a name="upload-a-management-certificate"></a><span data-ttu-id="91f5f-110">Een management-certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="91f5f-110">Upload a management certificate</span></span>
<span data-ttu-id="91f5f-111">Zodra u hebt een beheercertificaat dat is gemaakt, (CER-bestand met alleen Hallo openbare sleutel) kunt u deze bij Hallo portal uploaden.</span><span class="sxs-lookup"><span data-stu-id="91f5f-111">Once you have a management certificate created, (.cer file with only hello public key) you can upload it into hello portal.</span></span> <span data-ttu-id="91f5f-112">Wanneer Hallo-certificaat beschikbaar in de portal hello is, kan iedereen met een overeenkomend certificaat (persoonlijke sleutel) verbinding maken via Hallo Management API en de toegang tot bronnen van Hallo voor abonnement Hallo die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="91f5f-112">When hello certificate is available in hello portal, anyone with a matching certificate (private key) can connect through hello Management API and access hello resources for hello associated subscription.</span></span>

1. <span data-ttu-id="91f5f-113">Meld u bij toohello [Azure-portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="91f5f-113">Log in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="91f5f-114">Klik op **meer services** Hallo onder Azure service lijst Selecteer **abonnementen** in Hallo _algemene_ servicegroep.</span><span class="sxs-lookup"><span data-stu-id="91f5f-114">Click **More services** at hello bottom Azure service list, then select **Subscriptions** in hello _General_ service group.</span></span>

    ![Abonnement-menu](./media/azure-api-management-certs/subscriptions_menu.png)

3. <span data-ttu-id="91f5f-116">Zorg ervoor dat tooselect Hallo juiste abonnement dat u wilt dat tooassociate met Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="91f5f-116">Make sure tooselect hello correct subscription that you want tooassociate with hello certificate.</span></span>     
4. <span data-ttu-id="91f5f-117">Nadat u het juiste abonnement Hallo hebt geselecteerd, drukt u op **beheercertificaten** in Hallo _instellingen_ groep.</span><span class="sxs-lookup"><span data-stu-id="91f5f-117">After you have selected hello correct subscription, press **Management certificates** in hello _Settings_ group.</span></span>

    ![Instellingen](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. <span data-ttu-id="91f5f-119">Druk op Hallo **uploaden** knop.</span><span class="sxs-lookup"><span data-stu-id="91f5f-119">Press hello **Upload** button.</span></span>

    ![Op de pagina certificaten uploaden](./media/azure-api-management-certs/certificates_page.png)
6. <span data-ttu-id="91f5f-121">Vul Hallo dialoogvenster informatie en druk op **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="91f5f-121">Fill out hello dialog information and press **Upload**.</span></span>

    ![Instellingen](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a><span data-ttu-id="91f5f-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="91f5f-123">Next steps</span></span>
<span data-ttu-id="91f5f-124">Nu u een beheercertificaat dat is gekoppeld aan een abonnement hebt, kunt u (nadat u hebt geïnstalleerd die overeenkomt met certificaat lokaal Hallo) programmatisch koppelen toohello [klassieke implementatiemodel REST-API](https://msdn.microsoft.com/library/azure/mt420159.aspx) en automatiseren Hallo verschillende Azure-resources die ook gekoppeld aan dat abonnement.</span><span class="sxs-lookup"><span data-stu-id="91f5f-124">Now that you have a management certificate associated with a subscription, you can (after you have installed hello matching certificate locally) programmatically connect toohello [classic deployment model REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate hello various Azure resources that are also associated with that subscription.</span></span>
