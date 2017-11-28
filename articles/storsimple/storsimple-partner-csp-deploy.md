---
title: aaaMicrosoft Azure StorSimple- en Cloud-oplossingen Provider programma overzicht | Microsoft Docs
description: Een overzicht over hello StorSimple- en CSP voor StorSimple-partners.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/08/2017
ms.author: alkohli
ms.openlocfilehash: b5d999f2fbb9a27e7404ff454957b29dbef56af6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="de33b-103">Virtuele StorSimple-matrix voor Cloud Solution Provider-programma implementeren</span><span class="sxs-lookup"><span data-stu-id="de33b-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="de33b-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="de33b-104">Overview</span></span>

<span data-ttu-id="de33b-105">Virtuele StorSimple-matrix kan worden geïmplementeerd door Hallo Cloud Solution Provider (CSP) partners voor hun klanten.</span><span class="sxs-lookup"><span data-stu-id="de33b-105">StorSimple Virtual Array can be deployed by hello Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="de33b-106">Een partner CSP kunt maken van een StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="de33b-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="de33b-107">Deze service kan worden gebruikt toodeploy en beheren van virtuele StorSimple-matrix en Hallo bijbehorende shares, volumes en back-ups.</span><span class="sxs-lookup"><span data-stu-id="de33b-107">This service can then be used toodeploy and manage StorSimple Virtual Array and hello associated shares, volumes, and backups.</span></span>

<span data-ttu-id="de33b-108">Dit artikel wordt beschreven hoe een CSP-partner kunt toevoegen of een nieuwe abonnement tooan bestaande klant van de klant en maak vervolgens een toodeploy service een virtueel StorSimple-matrix in de CSP.</span><span class="sxs-lookup"><span data-stu-id="de33b-108">This article describes how a CSP partner can add a customer or a new subscription tooan existing customer and then create a service toodeploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de33b-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="de33b-109">Prerequisites</span></span>

<span data-ttu-id="de33b-110">Voordat u begint, zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="de33b-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="de33b-111">U worden onder Hallo CSP programma geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="de33b-111">You are enrolled under hello CSP program.</span></span>
- <span data-ttu-id="de33b-112">U hebt geldige [Partnercentrum](http://partnercenter.microsoft.com/) aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="de33b-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="de33b-113">Hallo referenties kunnen u toosign toohello Partner portal tooadd nieuwe klanten, zoeken naar klanten of navigeer tooa klantaccount vanuit Hallo Partner dashboard.</span><span class="sxs-lookup"><span data-stu-id="de33b-113">hello credentials enable you toosign in toohello Partner portal tooadd new customers, search for customers, or navigate tooa customer account from hello Partner dashboard.</span></span> <span data-ttu-id="de33b-114">Hallo CSP kan worden gebruikt als een StorSimple-beheerder namens de klant Hallo in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="de33b-114">hello CSP can function as a StorSimple administrator on behalf of hello customer in hello Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="de33b-115">Een klant toevoegen</span><span class="sxs-lookup"><span data-stu-id="de33b-115">Add a customer</span></span>

<span data-ttu-id="de33b-116">Als u een klant toevoegt, wordt er automatisch een abonnement gemaakt.</span><span class="sxs-lookup"><span data-stu-id="de33b-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="de33b-117">een klant tooadd (en automatisch een abonnement maken) uitvoeren van de volgende stappen uit in de Partnerportal Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="de33b-117">tooadd a customer (and automatically create a subscription), perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="de33b-118">Ga toohello [Partnercentrum](http://partnercenter.microsoft.com/) en meld u aan met uw referenties voor de CSP.</span><span class="sxs-lookup"><span data-stu-id="de33b-118">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="de33b-119">Klik op **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="de33b-119">Click **Dashboard**.</span></span>

     ![Dashboard in Partnercentrum](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="de33b-121">Klik in het Hallo linkerdeelvenster **klanten**.</span><span class="sxs-lookup"><span data-stu-id="de33b-121">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="de33b-122">In Hallo rechterdeelvenster, klik op **klanten toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="de33b-122">In hello right-pane, click **Add customers**.</span></span> <span data-ttu-id="de33b-123">Geef gegevens op Hallo van Hallo klant.</span><span class="sxs-lookup"><span data-stu-id="de33b-123">Enter hello details of hello customer.</span></span> <span data-ttu-id="de33b-124">Klik op **volgende: abonnementen** toocreate een klantabonnement.</span><span class="sxs-lookup"><span data-stu-id="de33b-124">Click **Next: Subscriptions** toocreate a customer subscription.</span></span>

    ![Klant toevoegen](./media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="de33b-126">Selecteer **Microsoft Azure** bieden.</span><span class="sxs-lookup"><span data-stu-id="de33b-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="de33b-127">Scroll toohello onder aan het Hallo-pagina en klik op **revisie**.</span><span class="sxs-lookup"><span data-stu-id="de33b-127">Scroll toohello bottom of hello page and click **Review**.</span></span>

    ![Bekijk informatie over abonnementen](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="de33b-129">Raadpleeg Hallo informatie en klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="de33b-129">Review hello information and click **Submit**.</span></span>

    ![Abonnement verzenden](./media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="de33b-131">Bewaar Hallo Bevestigingsgegevens voor toekomstig gebruik.</span><span class="sxs-lookup"><span data-stu-id="de33b-131">Save hello confirmation information for future reference.</span></span>

    ![Opslaan bevestigen](./media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="de33b-133">Zoek of navigeer toohello klant die u zojuist hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="de33b-133">Find or navigate toohello customer you just added.</span></span> <span data-ttu-id="de33b-134">Klik op Hallo **bedrijfsnaam** toodrill omlaag in Hallo details.</span><span class="sxs-lookup"><span data-stu-id="de33b-134">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Zoeken naar Hallo klant](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="de33b-136">Selecteer in de Hallo linkerdeelvenster **servicebeheer**.</span><span class="sxs-lookup"><span data-stu-id="de33b-136">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="de33b-137">Hallo in rechterdeelvenster onder **services beheren**, klikt u op **Microsoft Azure Management Portal** toosign in als een Azure-beheerder voor uw klant.</span><span class="sxs-lookup"><span data-stu-id="de33b-137">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![Meld u bij de portal tooAzure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="de33b-139">toocreate de Manager van een StorSimple-apparaat, klikt u op **+ nieuw** en zoeken of te navigeren**StorSimple virtueel apparaat reeks**.</span><span class="sxs-lookup"><span data-stu-id="de33b-139">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="de33b-140">Voor meer informatie gaat te[implementeren van een service Manager voor StorSimple-apparaat](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="de33b-140">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Apparaatbeheer StorSimple-service maken](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="de33b-142">Een abonnement toevoegen</span><span class="sxs-lookup"><span data-stu-id="de33b-142">Add a subscription</span></span>

<span data-ttu-id="de33b-143">In sommige gevallen moet u wellicht een bestaande klant en moet u een abonnement tooadd.</span><span class="sxs-lookup"><span data-stu-id="de33b-143">In some instances, you may have an existing customer, and you need tooadd a subscription.</span></span> <span data-ttu-id="de33b-144">een abonnement tooan bestaande klant tooadd Hallo stappen te volgen in de Partnerportal Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="de33b-144">tooadd a subscription tooan existing customer, perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="de33b-145">Ga toohello [Partnercentrum](http://partnercenter.microsoft.com/) en meld u aan met uw referenties voor de CSP.</span><span class="sxs-lookup"><span data-stu-id="de33b-145">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="de33b-146">Klik op **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="de33b-146">Click **Dashboard**.</span></span>

     ![Dashboard in Partnercentrum](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="de33b-148">Klik in het Hallo linkerdeelvenster **klanten**.</span><span class="sxs-lookup"><span data-stu-id="de33b-148">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="de33b-149">Zoek of navigeer toohello gewenste klant tooadd een abonnement op.</span><span class="sxs-lookup"><span data-stu-id="de33b-149">Find or navigate toohello customer you want tooadd a subscription to.</span></span> <span data-ttu-id="de33b-150">Klik op Hallo ![pictogram voor uitvouwen](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) pictogram tooexpand Hallo rij voor de bedrijfsnaam Hallo voor uw klant.</span><span class="sxs-lookup"><span data-stu-id="de33b-150">Click hello ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon tooexpand hello row for hello company name for your customer.</span></span> <span data-ttu-id="de33b-151">Klik in het Hallo-details op **toevoegen abonnementen**.</span><span class="sxs-lookup"><span data-stu-id="de33b-151">In hello details, click **Add subscriptions**.</span></span>

    ![Klanten](./media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="de33b-153">Controleer **Microsoft Azure** voor Hallo **aanbiedingen Top** in Hallo-abonnement en op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="de33b-153">Check **Microsoft Azure** for hello **Top offers** in hello subscription and click **Submit**.</span></span> <span data-ttu-id="de33b-154">Hiermee maakt u een nieuw abonnement.</span><span class="sxs-lookup"><span data-stu-id="de33b-154">This creates a new subscription.</span></span>

    ![Nieuw abonnement toevoegen](./media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="de33b-156">Nadat een nieuw abonnement is gemaakt, klikt u op **<--klanten** in Hallo linkerdeelvenster tooreturn toohello **klanten** pagina.</span><span class="sxs-lookup"><span data-stu-id="de33b-156">After a new subscription is created, click **<-- Customers** in hello left-pane tooreturn toohello **Customers** page.</span></span> <span data-ttu-id="de33b-157">Zoeken naar Hallo klant voor wie u een abonnement net hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="de33b-157">Search for hello customer for whom you just created a subscription.</span></span> <span data-ttu-id="de33b-158">Klik op Hallo **bedrijfsnaam** toodrill omlaag in Hallo details.</span><span class="sxs-lookup"><span data-stu-id="de33b-158">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Zoeken naar Hallo klant](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="de33b-160">Selecteer in de Hallo linkerdeelvenster **servicebeheer**.</span><span class="sxs-lookup"><span data-stu-id="de33b-160">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="de33b-161">Hallo in rechterdeelvenster onder **services beheren**, klikt u op **Microsoft Azure Management Portal** toosign in als een Azure-beheerder voor uw klant.</span><span class="sxs-lookup"><span data-stu-id="de33b-161">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![Meld u bij de portal tooAzure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="de33b-163">toocreate de Manager van een StorSimple-apparaat, klikt u op **+ nieuw** en zoeken of te navigeren**StorSimple virtueel apparaat reeks**.</span><span class="sxs-lookup"><span data-stu-id="de33b-163">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="de33b-164">Voor meer informatie gaat te[implementeren van een service Manager voor StorSimple-apparaat](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="de33b-164">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Apparaatbeheer StorSimple-service maken](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="de33b-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="de33b-166">Next steps</span></span>

- <span data-ttu-id="de33b-167">Als u meer vragen met betrekking tot Hallo StorSimple CSP hebt, gaat u verder te[StorSimple in CSP: veelgestelde vragen over](storsimple-partner-csp-faq.md).</span><span class="sxs-lookup"><span data-stu-id="de33b-167">If you have more questions regarding hello StorSimple in CSP, go too[StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="de33b-168">Als u bent klaar toodeploy uw StorSimple, ga te[implementeren van uw StorSimple in CSP](storsimple-partner-csp-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="de33b-168">If you are ready toodeploy your StorSimple, go too[Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>
