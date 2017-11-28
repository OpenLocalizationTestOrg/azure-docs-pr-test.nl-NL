---
title: Een Azure Management API-certificaat uploaden | Microsoft Docs
description: Informatie over het uploaden van athe API Management-certificaat voor de klassieke Azure Portal.
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
ms.openlocfilehash: 9dc438e927acd9aef38f06807fabf3dda9b021c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a><span data-ttu-id="2e058-103">Een Azure Management API Management-certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="2e058-103">Upload an Azure Management API Management Certificate</span></span>
<span data-ttu-id="2e058-104">Van beheercertificaten kunnen u verifiëren met het klassieke implementatiemodel verstrekt door Azure.</span><span class="sxs-lookup"><span data-stu-id="2e058-104">Management certificates allow you to authenticate with the classic deployment model provided by Azure.</span></span> <span data-ttu-id="2e058-105">Veel programma's en hulpprogramma's (zoals Visual Studio of de Azure SDK) gebruik van deze certificaten in configuratie en implementatie van verschillende Azure-services te automatiseren.</span><span class="sxs-lookup"><span data-stu-id="2e058-105">Many programs and tools (such as Visual Studio or the Azure SDK) use these certificates to automate configuration and deployment of various Azure services.</span></span> 

> [!WARNING]
> <span data-ttu-id="2e058-106">Wees voorzichtig!</span><span class="sxs-lookup"><span data-stu-id="2e058-106">Be careful!</span></span> <span data-ttu-id="2e058-107">Deze typen certificaten dat alle gebruikers worden geverifieerd met hen voor het beheren van het abonnement dat ze zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="2e058-107">These types of certificates allow anyone who authenticates with them to manage the subscription they are associated with.</span></span>
>
>

<span data-ttu-id="2e058-108">Als u meer informatie over Azure-certificaten (zoals het maken een zelfondertekend certificaat), Zie [certificaten voor Azure Cloud Services-overzicht](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span><span class="sxs-lookup"><span data-stu-id="2e058-108">If you'd like more information about Azure certificates (including creating a self-signed certificate), see [Certificates overview for Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="2e058-109">U kunt ook [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) om te verifiëren clientcode voor automatisering doeleinden.</span><span class="sxs-lookup"><span data-stu-id="2e058-109">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) to authenticate client-code for automation purposes.</span></span>

## <a name="upload-a-management-certificate"></a><span data-ttu-id="2e058-110">Een management-certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="2e058-110">Upload a management certificate</span></span>
<span data-ttu-id="2e058-111">Zodra u hebt een beheercertificaat dat is gemaakt, (CER-bestand met alleen de openbare sleutel) kunt u deze in de portal uploaden.</span><span class="sxs-lookup"><span data-stu-id="2e058-111">Once you have a management certificate created, (.cer file with only the public key) you can upload it into the portal.</span></span> <span data-ttu-id="2e058-112">Wanneer het certificaat in de portal beschikbaar is, kan iedereen met een overeenkomend certificaat (persoonlijke sleutel) verbinding maken via de API Management en toegang tot de bronnen voor het gekoppelde abonnement.</span><span class="sxs-lookup"><span data-stu-id="2e058-112">When the certificate is available in the portal, anyone with a matching certificate (private key) can connect through the Management API and access the resources for the associated subscription.</span></span>

1. <span data-ttu-id="2e058-113">Meld u aan bij [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2e058-113">Log in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="2e058-114">Klik op **meer services** op de lijst van de Azure-service onder Selecteer **abonnementen** in de _algemene_ servicegroep.</span><span class="sxs-lookup"><span data-stu-id="2e058-114">Click **More services** at the bottom Azure service list, then select **Subscriptions** in the _General_ service group.</span></span>

    ![Abonnement-menu](./media/azure-api-management-certs/subscriptions_menu.png)

3. <span data-ttu-id="2e058-116">Zorg ervoor dat het juiste abonnement die u wilt koppelen aan het certificaat te selecteren.</span><span class="sxs-lookup"><span data-stu-id="2e058-116">Make sure to select the correct subscription that you want to associate with the certificate.</span></span>     
4. <span data-ttu-id="2e058-117">Nadat u het juiste abonnement hebt geselecteerd, drukt u op **beheercertificaten** in de _instellingen_ groep.</span><span class="sxs-lookup"><span data-stu-id="2e058-117">After you have selected the correct subscription, press **Management certificates** in the _Settings_ group.</span></span>

    ![Instellingen](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. <span data-ttu-id="2e058-119">Druk op de **uploaden** knop.</span><span class="sxs-lookup"><span data-stu-id="2e058-119">Press the **Upload** button.</span></span>

    ![Op de pagina certificaten uploaden](./media/azure-api-management-certs/certificates_page.png)
6. <span data-ttu-id="2e058-121">Vul het dialoogvenster informatie en druk op **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="2e058-121">Fill out the dialog information and press **Upload**.</span></span>

    ![Instellingen](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a><span data-ttu-id="2e058-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2e058-123">Next steps</span></span>
<span data-ttu-id="2e058-124">Nu u een beheercertificaat dat is gekoppeld aan een abonnement hebt, kunt u (nadat u de overeenkomende certificaat lokaal hebt geïnstalleerd) programmatisch koppelen aan de [klassieke implementatiemodel REST-API](https://msdn.microsoft.com/library/azure/mt420159.aspx) en het automatiseren van de verschillende Azure-resources die ook gekoppeld aan dat abonnement.</span><span class="sxs-lookup"><span data-stu-id="2e058-124">Now that you have a management certificate associated with a subscription, you can (after you have installed the matching certificate locally) programmatically connect to the [classic deployment model REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate the various Azure resources that are also associated with that subscription.</span></span>
