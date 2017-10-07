---
title: aaaDeploy SAP S/4HANA of BW/4HANA op een virtuele machine in Azure | Microsoft Docs
description: SAP S/4HANA of BW/4HANA op een virtuele machine in Azure implementeren
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a><span data-ttu-id="3dd83-103">SAP S/4HANA of BW/4HANA in Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="3dd83-103">Deploy SAP S/4HANA or BW/4HANA on Azure</span></span>
<span data-ttu-id="3dd83-104">Dit artikel wordt beschreven hoe toodeploy S/4HANA in Azure met behulp van Hallo SAP toestel Cloudbibliotheek (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="3dd83-104">This article describes how toodeploy S/4HANA on Azure by using hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="3dd83-105">toodeploy andere SAP HANA-oplossingen, zoals BW/4HANA Hallo Volg dezelfde stappen.</span><span class="sxs-lookup"><span data-stu-id="3dd83-105">toodeploy other SAP HANA-based solutions, such as BW/4HANA, follow hello same steps.</span></span>

> [!NOTE]
<span data-ttu-id="3dd83-106">Ga voor meer informatie over Hallo SAP CAL toohello [SAP-Cloudbibliotheek toestel](https://cal.sap.com/) website.</span><span class="sxs-lookup"><span data-stu-id="3dd83-106">For more information about hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="3dd83-107">SAP heeft ook een blog over Hallo [SAP Cloud toestel bibliotheek 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="3dd83-107">SAP also has a blog about hello [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span>

> [!NOTE]
<span data-ttu-id="3dd83-108">Zoals van 29 mei 2017, kunt u hello Azure Resource Manager-implementatiemodel bovendien toohello minder voorkeur klassieke implementatie toodeploy Hallo SAP CAL model.</span><span class="sxs-lookup"><span data-stu-id="3dd83-108">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="3dd83-109">Het is raadzaam om nieuwe Resource Manager-implementatiemodel hello te gebruiken en het klassieke implementatiemodel Hallo negeren.</span><span class="sxs-lookup"><span data-stu-id="3dd83-109">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

## <a name="step-by-step-process-toodeploy-hello-solution"></a><span data-ttu-id="3dd83-110">Stapsgewijs toodeploy Hallo oplossing</span><span class="sxs-lookup"><span data-stu-id="3dd83-110">Step-by-step process toodeploy hello solution</span></span>

<span data-ttu-id="3dd83-111">Hallo volgende schermafbeeldingen reeks ziet u hoe toodeploy S/4HANA in Azure met behulp van SAP CAL Hallo.</span><span class="sxs-lookup"><span data-stu-id="3dd83-111">hello following sequence of screenshots shows you how toodeploy S/4HANA on Azure by using hello SAP CAL.</span></span> <span data-ttu-id="3dd83-112">Hallo-proces werkt Hallo dezelfde manier voor andere oplossingen, zoals BW/4HANA.</span><span class="sxs-lookup"><span data-stu-id="3dd83-112">hello process works hello same way for other solutions, such as BW/4HANA.</span></span>

<span data-ttu-id="3dd83-113">Hallo **oplossingen** pagina bevat een aantal Hallo SAP CAL HANA gebaseerde oplossingen beschikbaar in Azure.</span><span class="sxs-lookup"><span data-stu-id="3dd83-113">hello **Solutions** page shows some of hello SAP CAL HANA-based solutions available on Azure.</span></span> <span data-ttu-id="3dd83-114">**SAP S 4HANA 1610 FPS01, Fully-Activated toestel** bevindt zich in het middelste rij Hallo:</span><span class="sxs-lookup"><span data-stu-id="3dd83-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** is in hello middle row:</span></span>

![SAP CAL oplossingen](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="3dd83-116">Een account maken in Hallo SAP CAL</span><span class="sxs-lookup"><span data-stu-id="3dd83-116">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="3dd83-117">toosign in toohello SAP CAL voor Hallo eerste keer gebruikt uw SAP-gebruiker of een andere gebruiker die is geregistreerd bij SAP.</span><span class="sxs-lookup"><span data-stu-id="3dd83-117">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="3dd83-118">Definieer een SAP CAL-account dat wordt gebruikt door Hallo SAP CAL toodeploy apparaten op Azure.</span><span class="sxs-lookup"><span data-stu-id="3dd83-118">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="3dd83-119">In de definitie van Hallo-account moet u:</span><span class="sxs-lookup"><span data-stu-id="3dd83-119">In hello account definition, you need to:</span></span>

    <span data-ttu-id="3dd83-120">a.</span><span class="sxs-lookup"><span data-stu-id="3dd83-120">a.</span></span> <span data-ttu-id="3dd83-121">Hallo-implementatiemodel in Azure (Resource Manager of klassiek) selecteren.</span><span class="sxs-lookup"><span data-stu-id="3dd83-121">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="3dd83-122">b.</span><span class="sxs-lookup"><span data-stu-id="3dd83-122">b.</span></span> <span data-ttu-id="3dd83-123">Voer uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3dd83-123">Enter your Azure subscription.</span></span> <span data-ttu-id="3dd83-124">Een SAP CAL-account kan alleen tooone abonnement worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="3dd83-124">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="3dd83-125">Als u meer dan één abonnement nodig hebt, moet u toocreate een ander SAP CAL-account.</span><span class="sxs-lookup"><span data-stu-id="3dd83-125">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>

    <span data-ttu-id="3dd83-126">c.</span><span class="sxs-lookup"><span data-stu-id="3dd83-126">c.</span></span> <span data-ttu-id="3dd83-127">Hallo SAP CAL machtiging toodeploy geven in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3dd83-127">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="3dd83-128">Hallo volgende stappen laten zien hoe toocreate een SAP CAL-account voor implementaties van Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3dd83-128">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="3dd83-129">Als u al een SAP CAL-account dat gekoppelde toohello klassieke implementatiemodel, hebt u *moet* toofollow deze toocreate stappen een nieuwe SAP CAL-account.</span><span class="sxs-lookup"><span data-stu-id="3dd83-129">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="3dd83-130">Hallo nieuwe SAP CAL-account moet toodeploy in Hallo Resource Manager-model.</span><span class="sxs-lookup"><span data-stu-id="3dd83-130">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="3dd83-131">Maak een nieuwe SAP CAL-account.</span><span class="sxs-lookup"><span data-stu-id="3dd83-131">Create a new SAP CAL account.</span></span> <span data-ttu-id="3dd83-132">Hallo **Accounts** pagina ziet u drie opties voor Azure:</span><span class="sxs-lookup"><span data-stu-id="3dd83-132">hello **Accounts** page shows three choices for Azure:</span></span> 

    <span data-ttu-id="3dd83-133">a.</span><span class="sxs-lookup"><span data-stu-id="3dd83-133">a.</span></span> <span data-ttu-id="3dd83-134">**Microsoft Azure (klassiek)** Hallo klassieke implementatiemodel is en niet langer voorkeur.</span><span class="sxs-lookup"><span data-stu-id="3dd83-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="3dd83-135">b.</span><span class="sxs-lookup"><span data-stu-id="3dd83-135">b.</span></span> <span data-ttu-id="3dd83-136">**Microsoft Azure** Hallo nieuwe Resource Manager-implementatiemodel is.</span><span class="sxs-lookup"><span data-stu-id="3dd83-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    <span data-ttu-id="3dd83-137">c.</span><span class="sxs-lookup"><span data-stu-id="3dd83-137">c.</span></span> <span data-ttu-id="3dd83-138">**Windows Azure worden beheerd door 21Vianet** is een optie in China die gebruikmaakt van het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="3dd83-138">**Windows Azure operated by 21Vianet** is an option in China that uses hello classic deployment model.</span></span>

    <span data-ttu-id="3dd83-139">toodeploy in Hallo Resource Manager-model, selecteer **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="3dd83-139">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Details van SAP CAL-Account](./media/cal-s4h/s4h-pic-2a.png)

3. <span data-ttu-id="3dd83-141">Voer hello Azure **abonnements-ID** die u kunt vinden op Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3dd83-141">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span>

   ![SAP CAL Accounts](./media/cal-s4h/s4h-pic3c.png)

4. <span data-ttu-id="3dd83-143">tooauthorize hello SAP CAL toodeploy in hello Azure-abonnement dat u hebt gedefinieerd, klikt u op **autoriseren**.</span><span class="sxs-lookup"><span data-stu-id="3dd83-143">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="3dd83-144">Hallo na pagina wordt weergegeven in Hallo browsertabblad:</span><span class="sxs-lookup"><span data-stu-id="3dd83-144">hello following page appears in hello browser tab:</span></span>

   ![Internet Explorer cloud services-aanmeldingspagina](./media/cal-s4h/s4h-pic4c.png)

5. <span data-ttu-id="3dd83-146">Als meer dan één gebruiker wordt weergegeven, kies Hallo Microsoft-account dat is gekoppeld toobe Hallo CO-beheerder van hello Azure-abonnement u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="3dd83-146">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="3dd83-147">Hallo na pagina wordt weergegeven in Hallo browsertabblad:</span><span class="sxs-lookup"><span data-stu-id="3dd83-147">hello following page appears in hello browser tab:</span></span>

   ![Bevestiging van Internet Explorer cloud-services](./media/cal-s4h/s4h-pic5a.png)

6. <span data-ttu-id="3dd83-149">Klik op **accepteren**.</span><span class="sxs-lookup"><span data-stu-id="3dd83-149">Click **Accept**.</span></span> <span data-ttu-id="3dd83-150">Als het Hallo-autorisatie is geslaagd, wordt Hallo SAP CAL-account definitie opnieuw wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3dd83-150">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="3dd83-151">Na korte tijd, wordt een bericht bevestigd Hallo autorisatieproces is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="3dd83-151">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="3dd83-152">nieuw gemaakte SAP CAL-account tooyour gebruiker tooassign hello, Voer uw **gebruikers-ID** in Hallo tekstvak op Hallo rechts en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3dd83-152">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span>

   ![Accountkoppeling toouser](./media/cal-s4h/s4h-pic8a.png)

8. <span data-ttu-id="3dd83-154">Klik op tooassociate uw account met Hallo gebruiker dat u toosign in toohello SAP-CAL **revisie**.</span><span class="sxs-lookup"><span data-stu-id="3dd83-154">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 
 
9. <span data-ttu-id="3dd83-155">toocreate hello koppeling tussen uw gebruikers- en Hallo nieuw gemaakte SAP CAL-account, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="3dd83-155">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

   ![Koppeling van gebruiker tooSAP CAL-account](./media/cal-s4h/s4h-pic9b.png)

<span data-ttu-id="3dd83-157">Een SAP CAL-account dat kan worden gemaakt:</span><span class="sxs-lookup"><span data-stu-id="3dd83-157">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="3dd83-158">Gebruik Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="3dd83-158">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="3dd83-159">SAP-systemen implementeren in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3dd83-159">Deploy SAP systems into your Azure subscription.</span></span>

<span data-ttu-id="3dd83-160">U kunt nu toodeploy S/4HANA starten in uw gebruikerabonnement in Azure.</span><span class="sxs-lookup"><span data-stu-id="3dd83-160">Now you can start toodeploy S/4HANA into your user subscription in Azure.</span></span>

> [!NOTE]
<span data-ttu-id="3dd83-161">Voordat u doorgaat, moet u bepalen of er Azure core quota's voor virtuele machines van Azure H-serie.</span><span class="sxs-lookup"><span data-stu-id="3dd83-161">Before you continue, determine whether you have Azure core quotas for Azure H-Series VMs.</span></span> <span data-ttu-id="3dd83-162">Hallo-momenteel Hallo SAP CAL toodeploy H-serie virtuele machines van Azure gebruikt enkele van Hallo SAP HANA-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="3dd83-162">At hello moment, hello SAP CAL uses H-Series VMs of Azure toodeploy some of hello SAP HANA-based solutions.</span></span> <span data-ttu-id="3dd83-163">Uw Azure-abonnement mogelijk geen quota's core H-serie voor H-serie.</span><span class="sxs-lookup"><span data-stu-id="3dd83-163">Your Azure subscription might not have any H-Series core quotas for H-Series.</span></span> <span data-ttu-id="3dd83-164">Als dit het geval is, moet u mogelijk toocontact ondersteuning van Azure tooget een quotum van ten minste 16 kernen van H-serie.</span><span class="sxs-lookup"><span data-stu-id="3dd83-164">If so, you might need toocontact Azure support tooget a quota of at least 16 H-Series cores.</span></span>

> [!NOTE]
<span data-ttu-id="3dd83-165">Wanneer u een oplossing op Azure in Hallo SAP CAL implementeert, kan het gebeuren dat u slechts één Azure-regio kunt.</span><span class="sxs-lookup"><span data-stu-id="3dd83-165">When you deploy a solution on Azure in hello SAP CAL, you might find that you can choose only one Azure region.</span></span> <span data-ttu-id="3dd83-166">toodeploy in Azure-regio's dan Hallo een voorgesteld door Hallo SAP CAL, moet u een abonnement CAL uit SAP toopurchase.</span><span class="sxs-lookup"><span data-stu-id="3dd83-166">toodeploy into Azure regions other than hello one suggested by hello SAP CAL, you need toopurchase a CAL subscription from SAP.</span></span> <span data-ttu-id="3dd83-167">Ook moet u mogelijk een bericht met SAP toohave tooopen uw toodeliver CAL-account is ingeschakeld in Azure-regio's dan Hallo die in eerste instantie voorgesteld.</span><span class="sxs-lookup"><span data-stu-id="3dd83-167">You also might need tooopen a message with SAP toohave your CAL account enabled toodeliver into Azure regions other than hello ones initially suggested.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="3dd83-168">Een oplossing implementeren</span><span class="sxs-lookup"><span data-stu-id="3dd83-168">Deploy a solution</span></span>

<span data-ttu-id="3dd83-169">We implementeren van een oplossing van Hallo **oplossingen** pagina Hallo SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="3dd83-169">Let's deploy a solution from hello **Solutions** page of hello SAP CAL.</span></span> <span data-ttu-id="3dd83-170">Hallo SAP CAL heeft twee reeksen toodeploy:</span><span class="sxs-lookup"><span data-stu-id="3dd83-170">hello SAP CAL has two sequences toodeploy:</span></span>

- <span data-ttu-id="3dd83-171">Een eenvoudige reeks die gebruikmaakt van één pagina toodefine Hallo system toobe geïmplementeerd</span><span class="sxs-lookup"><span data-stu-id="3dd83-171">A basic sequence that uses one page toodefine hello system toobe deployed</span></span>
- <span data-ttu-id="3dd83-172">Een geavanceerde reeks waarmee u bepaalde keuzes op VM-grootten</span><span class="sxs-lookup"><span data-stu-id="3dd83-172">An advanced sequence that gives you certain choices on VM sizes</span></span> 

<span data-ttu-id="3dd83-173">Hallo basic pad toodeployment Hier ziet.</span><span class="sxs-lookup"><span data-stu-id="3dd83-173">We demonstrate hello basic path toodeployment here.</span></span>

1. <span data-ttu-id="3dd83-174">Op Hallo **accountdetails** pagina, moet u:</span><span class="sxs-lookup"><span data-stu-id="3dd83-174">On hello **Account Details** page, you need to:</span></span>

    <span data-ttu-id="3dd83-175">a.</span><span class="sxs-lookup"><span data-stu-id="3dd83-175">a.</span></span> <span data-ttu-id="3dd83-176">Een SAP CAL-account selecteren.</span><span class="sxs-lookup"><span data-stu-id="3dd83-176">Select an SAP CAL account.</span></span> <span data-ttu-id="3dd83-177">(Gebruik een account dat is gekoppeld toodeploy met Resource Manager-implementatiemodel Hallo.)</span><span class="sxs-lookup"><span data-stu-id="3dd83-177">(Use an account that is associated toodeploy with hello Resource Manager deployment model.)</span></span>

    <span data-ttu-id="3dd83-178">b.</span><span class="sxs-lookup"><span data-stu-id="3dd83-178">b.</span></span> <span data-ttu-id="3dd83-179">Geef het exemplaar van een **naam**.</span><span class="sxs-lookup"><span data-stu-id="3dd83-179">Enter an instance **Name**.</span></span>

    <span data-ttu-id="3dd83-180">c.</span><span class="sxs-lookup"><span data-stu-id="3dd83-180">c.</span></span> <span data-ttu-id="3dd83-181">Selecteer een Azure **regio**.</span><span class="sxs-lookup"><span data-stu-id="3dd83-181">Select an Azure **Region**.</span></span> <span data-ttu-id="3dd83-182">Hallo SAP CAL stelt voor een regio.</span><span class="sxs-lookup"><span data-stu-id="3dd83-182">hello SAP CAL suggests a region.</span></span> <span data-ttu-id="3dd83-183">Als u een andere Azure-regio moet en u een SAP CAL-abonnement hebt, moet u een licentie voor clienttoegang tooorder abonnement met SAP.</span><span class="sxs-lookup"><span data-stu-id="3dd83-183">If you need another Azure region and you don't have an SAP CAL subscription, you need tooorder a CAL subscription with SAP.</span></span>

    <span data-ttu-id="3dd83-184">d.</span><span class="sxs-lookup"><span data-stu-id="3dd83-184">d.</span></span> <span data-ttu-id="3dd83-185">Voer een model **wachtwoord** voor Hallo-oplossing van acht of negen tekens.</span><span class="sxs-lookup"><span data-stu-id="3dd83-185">Enter a master **Password** for hello solution of eight or nine characters.</span></span> <span data-ttu-id="3dd83-186">Hallo-wachtwoord wordt gebruikt voor beheerders van de verschillende onderdelen Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="3dd83-186">hello password is used for hello administrators of hello different components.</span></span>

   ![SAP CAL-standaardmodus: Exemplaar maken](./media/cal-s4h/s4h-pic10a.png)

2. <span data-ttu-id="3dd83-188">Klik op **maken**, en in Hallo-bericht dat wordt weergegeven, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3dd83-188">Click **Create**, and in hello message box that appears, click **OK**.</span></span>

   ![SAP CAL ondersteund VM-grootten](./media/cal-s4h/s4h-pic10b.png)

3. <span data-ttu-id="3dd83-190">In Hallo **persoonlijke sleutel** in het dialoogvenster, klikt u op **Store** toostore Hallo persoonlijke sleutel in Hallo SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="3dd83-190">In hello **Private Key** dialog box, click **Store** toostore hello private key in hello SAP CAL.</span></span> <span data-ttu-id="3dd83-191">wachtwoordbeveiliging toouse voor de persoonlijke sleutel hello, klikt u op **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="3dd83-191">toouse password protection for hello private key, click **Download**.</span></span> 

   ![SAP CAL persoonlijke sleutel](./media/cal-s4h/s4h-pic10c.png)

4. <span data-ttu-id="3dd83-193">Lees Hallo SAP CAL **waarschuwing** bericht en op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3dd83-193">Read hello SAP CAL **Warning** message, and click **OK**.</span></span>

   ![SAP CAL waarschuwing](./media/cal-s4h/s4h-pic10d.png)

    <span data-ttu-id="3dd83-195">Hallo-implementatie wordt nu uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3dd83-195">Now hello deployment takes place.</span></span> <span data-ttu-id="3dd83-196">Na enige tijd, afhankelijk van Hallo omvang en complexiteit van Hallo-oplossing (Hallo SAP CAL een schatting biedt), Hallo status wordt weergegeven als active en klaar voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="3dd83-196">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use.</span></span>

5. <span data-ttu-id="3dd83-197">toofind hello virtuele machines die zijn verzameld met andere gekoppelde resources in één resourcegroep hello, gaat u toohello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="3dd83-197">toofind hello virtual machines collected with hello other associated resources in one resource group, go toohello Azure portal:</span></span> 

   ![SAP CAL-objecten die zijn geïmplementeerd in de nieuwe portal Hallo](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. <span data-ttu-id="3dd83-199">Op Hallo SAP CAL portal Hallo status wordt weergegeven als **Active**.</span><span class="sxs-lookup"><span data-stu-id="3dd83-199">On hello SAP CAL portal, hello status appears as **Active**.</span></span> <span data-ttu-id="3dd83-200">tooconnect toohello oplossing, klikt u op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="3dd83-200">tooconnect toohello solution, click **Connect**.</span></span> <span data-ttu-id="3dd83-201">Verschillende opties tooconnect toohello verschillende onderdelen worden geïmplementeerd in deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="3dd83-201">Different options tooconnect toohello different components are deployed within this solution.</span></span>

   ![SAP CAL exemplaren](./media/cal-s4h/active_solution.png)

7. <span data-ttu-id="3dd83-203">Voordat u een van de Hallo opties tooconnect toohello geïmplementeerd systemen gebruiken kunt, klikt u op **Getting Started Guide**.</span><span class="sxs-lookup"><span data-stu-id="3dd83-203">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> 

   ![Verbinding maken met toohello exemplaar](./media/cal-s4h/connect_to_solution.png)

    <span data-ttu-id="3dd83-205">Hallo documentatie namen Hallo gebruikers voor elk van Hallo connectiviteit methoden.</span><span class="sxs-lookup"><span data-stu-id="3dd83-205">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="3dd83-206">Hallo-wachtwoorden voor die gebruikers toohello master wachtwoord die u hebt gedefinieerd bij Hallo begin van het implementatieproces Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3dd83-206">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="3dd83-207">In de documentatie Hallo andere meer functionaliteit gebruikers worden weergegeven met hun wachtwoorden, kunt u toosign in toohello system geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="3dd83-207">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span> 

    <span data-ttu-id="3dd83-208">Bijvoorbeeld, als u Hallo SAP-GUI die vooraf geïnstalleerd op de extern bureaublad van Windows-machine hello, Hallo S/4 systeem als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="3dd83-208">For example, if you use hello SAP GUI that's preinstalled on hello Windows Remote Desktop machine, hello S/4 system might look like this:</span></span>

   ![SM50 in Hallo SAP-GUI vooraf geïnstalleerd](./media/cal-s4h/gui_sm50.png)

    <span data-ttu-id="3dd83-210">Of als u Hallo DBACockpit, Hallo-exemplaar als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="3dd83-210">Or if you use hello DBACockpit, hello instance might look like this:</span></span>

   ![SM50 in Hallo DBACockpit SAP GUI](./media/cal-s4h/dbacockpit.png)

<span data-ttu-id="3dd83-212">Binnen een paar uur wordt een gezonde SAP S/4 toestel geïmplementeerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="3dd83-212">Within a few hours, a healthy SAP S/4 appliance is deployed in Azure.</span></span>

<span data-ttu-id="3dd83-213">Als u een SAP CAL-abonnement hebt gekocht, ondersteund SAP implementaties via Hallo SAP CAL volledig in Azure.</span><span class="sxs-lookup"><span data-stu-id="3dd83-213">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="3dd83-214">Hallo Ondersteuningswachtrij is BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="3dd83-214">hello support queue is BC-VCM-CAL.</span></span>







