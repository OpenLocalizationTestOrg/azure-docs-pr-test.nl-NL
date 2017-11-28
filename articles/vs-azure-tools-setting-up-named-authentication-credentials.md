---
title: aaaSetting Up met de naam verificatiereferenties | Microsoft Docs
description: 'Meer informatie over hoe tootooprovide referenties waarmee Visual Studio tooauthenticate aanvragen tooAzure toopublish een tooAzure toepassing vanuit Visual Studio of een bestaande toomonitor kunt cloudservice... '
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="4bf3c-103">Benoemde verificatiereferenties in te stellen</span><span class="sxs-lookup"><span data-stu-id="4bf3c-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="4bf3c-104">een toepassing tooAzure vanuit Visual Studio of een bestaande cloudservice toomonitor toopublish, moet u referenties opgeven waarmee Visual Studio tooauthenticate kunt tooAzure-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-104">toopublish an application tooAzure from Visual Studio or toomonitor an existing cloud service, you must provide credentials that Visual Studio can use tooauthenticate requests tooAzure.</span></span> <span data-ttu-id="4bf3c-105">Er zijn verschillende plaatsen in Visual Studio, waar u zich in tooprovide deze referenties aanmelden kunt.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-105">There are several places in Visual Studio where you can sign in tooprovide these credentials.</span></span> <span data-ttu-id="4bf3c-106">Vanuit Hallo Server Explorer, kunt u bijvoorbeeld Hallo snelmenu voor Hallo openen **Azure** knooppunt en kies **tooMicrosoft Azure-abonnement verbinden...** . Wanneer u zich aanmeldt, Hallo abonnement informatie die is gekoppeld aan uw Azure-account is beschikbaar in Visual Studio en er is niets meer dat u toodo hebt.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-106">For example, from hello Server Explorer, you can open hello shortcut menu for hello **Azure** node and choose **Connect tooMicrosoft Azure Subscription...**. When you sign in, hello subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you have toodo.</span></span>

<span data-ttu-id="4bf3c-107">Azure-hulpprogramma's ondersteunt ook een oudere manier van het bieden van referenties, het gebruik van Hallo abonnementsbestand (.publishsettings-bestand).</span><span class="sxs-lookup"><span data-stu-id="4bf3c-107">Azure Tools also supports an older way of providing credentials, using hello subscription file (.publishsettings file).</span></span> <span data-ttu-id="4bf3c-108">Dit onderwerp beschrijft deze methode wordt nog steeds ondersteund in de Azure SDK 2.2.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-108">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="4bf3c-109">Hallo volgende items zijn vereist voor verificatie tooAzure:</span><span class="sxs-lookup"><span data-stu-id="4bf3c-109">hello following items are required for authentication tooAzure:</span></span>

* <span data-ttu-id="4bf3c-110">Uw abonnements-ID</span><span class="sxs-lookup"><span data-stu-id="4bf3c-110">Your subscription ID</span></span>
* <span data-ttu-id="4bf3c-111">Een geldig X.509 v3-certificaat</span><span class="sxs-lookup"><span data-stu-id="4bf3c-111">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="4bf3c-112">Hallo-lengte van sleutel Hallo X.509 v3-certificaat moet ten minste 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-112">hello length of hello X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="4bf3c-113">Azure weigert alle certificaten die niet voldoen aan deze eis of die is niet geldig.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-113">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="4bf3c-114">Visual Studio gebruikt uw abonnements-ID samen met de certificaatgegevens Hallo als referenties.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-114">Visual Studio uses your subscription ID together with hello certificate data as credentials.</span></span> <span data-ttu-id="4bf3c-115">de juiste referenties Hello wordt verwezen in Hallo abonnementsbestand (.publishsettings-bestand) dat een openbare sleutel voor Hallo certificaat bevat.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-115">hello appropriate credentials are referenced in hello subscription file (.publishsettings file), which contains a public key for hello certificate.</span></span> <span data-ttu-id="4bf3c-116">Hallo abonnementsbestand kan referenties voor meer dan één abonnement bevatten.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-116">hello subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="4bf3c-117">Kunt u de abonnementsgegevens Hallo van Hallo **nieuw/bewerken abonnement** in het dialoogvenster zoals verderop in dit onderwerp wordt uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-117">You can edit hello subscription information from hello **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="4bf3c-118">Als u toocreate een certificaat zelf wilt, raadpleegt u de instructies toohello in [maken en uploaden van een Beheercertificaat voor Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) en vervolgens handmatig uploaden Hallo certificaat toohello [klassieke Azure-portal ](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="4bf3c-118">If you want toocreate a certificate yourself, you can refer toohello instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload hello certificate toohello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="4bf3c-119">Deze referenties die Visual Studio toomanage die uw cloudservices zijn niet vereist Hallo dezelfde referenties die vereist tooauthenticate zijn een aanvraag in voor hello Azure storage-services.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-119">These credentials that Visual Studio requires toomanage your cloud services aren’t hello same credentials that are required tooauthenticate a request against hello Azure storage services.</span></span>
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a><span data-ttu-id="4bf3c-120">Importeren, instellen of bewerken van referenties voor verificatie in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4bf3c-120">Import, set up, or edit authentication credentials in Visual Studio</span></span>
<span data-ttu-id="4bf3c-121">U kunt importeren, instellen of wijzigen van uw referenties voor verificatie in Hallo **nieuw abonnement** in het dialoogvenster dat wordt weergegeven als u Hallo na actie uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="4bf3c-121">You can import, set up, or modify your authentication credentials in hello **New Subscription** dialog box, which appears if you perform hello following action:</span></span>

* <span data-ttu-id="4bf3c-122">In **Server Explorer**Open Hallo snelmenu voor Hallo **Azure** knooppunt, kies **beheren en Filter abonnementen...** , kies Hallo **certificaten** tabblad en voer een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="4bf3c-122">In **Server Explorer**, open hello shortcut menu for hello **Azure** node, choose **Manage and Filter Subscriptions...**, choose hello **Certificates** tab, and do one of hello following:</span></span>

    * <span data-ttu-id="4bf3c-123">Kies **importeren** tooopen Hallo Microsoft Azure-abonnementen importeren dialoogvenster waarin u Hallo abonnementen bestand voor Hallo momenteel downloaden kunt geladen abonnement, bladeren tooits downloadlocatie en vervolgens importeren voor gebruik in -verificatie.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-123">Choose **Import** tooopen hello Import Microsoft Azure Subscriptions dialog where you can download hello  subscriptions file for hello currently loaded subscription, browse tooits download location, and then import it for use in authentication.</span></span>
    * <span data-ttu-id="4bf3c-124">Kies **nieuw** tooopen Hallo nieuw abonnement dialoogvenster waarin u een nieuw abonnement voor gebruik bij verificatie kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-124">Choose **New** tooopen hello New Subscription dialog where you can set up a new subscription for use in authentication.</span></span>
    * <span data-ttu-id="4bf3c-125">Kies **bewerken** (na uw actief abonnement te kiezen) tooopen Hallo abonnement bewerken dialoogvenster waarin u een bestaand abonnement voor gebruik bij verificatie kunt bewerken.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-125">Choose **Edit** (after choosing your active subscription) tooopen hello Edit Subscription dialog where you can edit an existing subscription for use in authentication.</span></span> 

<span data-ttu-id="4bf3c-126">Hallo volgende procedure wordt ervan uitgegaan dat Hallo **nieuw abonnement** dialoogvenster is geopend.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-126">hello following procedure assumes that hello **New Subscription** dialog box is open.</span></span>

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="4bf3c-127">tooset up verificatiereferenties in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4bf3c-127">tooset up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="4bf3c-128">In Hallo **Selecteer een bestaand certificaat** voor verificatielijst, selecteer een certificaat.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-128">In hello **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="4bf3c-129">Kies Hallo **volledig pad kopiëren Hallo** koppeling.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-129">Choose hello **Copy hello full path** link.</span></span> <span data-ttu-id="4bf3c-130">Hallo-pad voor Hallo-certificaat (.cer-bestand) is gekopieerde toohello Klembord.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-130">hello path for hello certificate (.cer file) is copied toohello Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4bf3c-131">toopublish uw Azure-toepassing vanuit Visual Studio, moet u deze toohello certificaat uploaden [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4bf3c-131">toopublish your Azure application from Visual Studio, you must upload this certificate toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   >
   >
3. <span data-ttu-id="4bf3c-132">tooupload hello certificaat toohello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="4bf3c-132">tooupload hello certificate toohello Azure portal:</span></span>

   1. <span data-ttu-id="4bf3c-133">Open Hallo [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4bf3c-133">Open hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   2. <span data-ttu-id="4bf3c-134">Als u wordt gevraagd, toohello portal aanmelden en navigeert u vervolgens te**instellingen**, **Beheercertificaten**.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-134">If prompted, sign in toohello portal and then navigate too**Settings**, **Management Certificates**.</span></span>
   3. <span data-ttu-id="4bf3c-135">Kies in Hallo Management certificaten deelvenster **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-135">In hello Management certificates pane, choose **Upload**.</span></span>
   4. <span data-ttu-id="4bf3c-136">Selecteer uw Azure-abonnement, plak Hallo volledige pad van Hallo cer-bestand dat u zojuist hebt gemaakt en kies **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="4bf3c-136">Select your Azure subscription, paste hello full path of hello .cer file that you just created, and choose **Upload**.</span></span>
