---
title: aaaGet slag met Opslagverkenner (Preview) | Microsoft Docs
description: Azure Storage-resources beheren met Opslagverkenner (Preview)
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a><span data-ttu-id="370d4-103">Aan de slag met Opslagverkenner (Preview)</span><span class="sxs-lookup"><span data-stu-id="370d4-103">Get started with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="370d4-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="370d4-104">Overview</span></span>
<span data-ttu-id="370d4-105">Azure Opslagverkenner (Preview) is een zelfstandige app waardoor u tooeasily werken met Azure Storage-gegevens op Windows-, Mac OS- en Linux.</span><span class="sxs-lookup"><span data-stu-id="370d4-105">Azure Storage Explorer (Preview) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="370d4-106">In dit artikel leert u Hallo verschillende manieren van het verbinden van uw Azure storage-accounts beheren tooand.</span><span class="sxs-lookup"><span data-stu-id="370d4-106">In this article, you learn hello various ways of connecting tooand managing your Azure storage accounts.</span></span>

![Microsoft Azure Storage Explorer (voorbeeld)][15]

## <a name="prerequisites"></a><span data-ttu-id="370d4-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="370d4-108">Prerequisites</span></span>
* [<span data-ttu-id="370d4-109">Opslagverkenner (Preview) downloaden en installeren</span><span class="sxs-lookup"><span data-stu-id="370d4-109">Download and install Storage Explorer (Preview)</span></span>](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a><span data-ttu-id="370d4-110">Verbinding maken met tooa storage-account of -service</span><span class="sxs-lookup"><span data-stu-id="370d4-110">Connect tooa storage account or service</span></span>
<span data-ttu-id="370d4-111">Opslagverkenner (Preview) biedt verschillende manieren tooconnect toostorage accounts.</span><span class="sxs-lookup"><span data-stu-id="370d4-111">Storage Explorer (Preview) provides several ways tooconnect toostorage accounts.</span></span> <span data-ttu-id="370d4-112">U kunt bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="370d4-112">For example, you can:</span></span>
* <span data-ttu-id="370d4-113">Verbinding maken met toostorage accounts die zijn gekoppeld aan uw Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="370d4-113">Connect toostorage accounts associated with your Azure subscriptions.</span></span>
* <span data-ttu-id="370d4-114">Sluit toostorage accounts en -services die worden gedeeld van andere Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="370d4-114">Connect toostorage accounts and services that are shared from other Azure subscriptions.</span></span>
* <span data-ttu-id="370d4-115">Verbinding maken met tooand lokale opslag beheren met behulp van hello Azure-Opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="370d4-115">Connect tooand manage local storage by using hello Azure Storage Emulator.</span></span> 

<span data-ttu-id="370d4-116">Bovendien kunt u wereldwijd en nationaal werken met opslagaccounts in Azure:</span><span class="sxs-lookup"><span data-stu-id="370d4-116">In addition, you can work with storage accounts in global and national Azure:</span></span>

* <span data-ttu-id="370d4-117">[Verbinding maken met Azure-abonnement tooan](#connect-to-an-azure-subscription): beheer opslagresources die deel uitmaken van tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="370d4-117">[Connect tooan Azure subscription](#connect-to-an-azure-subscription): Manage storage resources that belong tooyour Azure subscription.</span></span>
* <span data-ttu-id="370d4-118">[Werken met lokale ontwikkeling storage](#work-with-local-development-storage): beheer lokale opslag met behulp van hello Azure-Opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="370d4-118">[Work with local development storage](#work-with-local-development-storage): Manage local storage by using hello Azure Storage Emulator.</span></span>
* <span data-ttu-id="370d4-119">[Koppel tooexternal opslag](#attach-or-detach-an-external-storage-account): beheer opslagresources die deel uitmaken van tooanother Azure-abonnement of die onder nationale clouds voor Azure met behulp van de naam, de sleutel en de eindpunten Hallo van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="370d4-119">[Attach tooexternal storage](#attach-or-detach-an-external-storage-account): Manage storage resources that belong tooanother Azure subscription or that are under national Azure clouds by using hello storage account's name, key, and endpoints.</span></span>
* <span data-ttu-id="370d4-120">[Koppelen van een opslagaccount met behulp van een SAS](#attach-storage-account-using-sas): beheer opslagresources die deel uitmaken van tooanother Azure-abonnement met behulp van een shared access signature (SAS).</span><span class="sxs-lookup"><span data-stu-id="370d4-120">[Attach a storage account by using an SAS](#attach-storage-account-using-sas): Manage storage resources that belong tooanother Azure subscription by using a shared access signature (SAS).</span></span>
* <span data-ttu-id="370d4-121">[Een service koppelen via een SAS](#attach-service-using-sas): een specifieke opslagservice (blobcontainer, wachtrij of tabel) die deel uitmaakt van tooanother Azure-abonnement met behulp van een SAS te beheren.</span><span class="sxs-lookup"><span data-stu-id="370d4-121">[Attach a service by using an SAS](#attach-service-using-sas): Manage a specific storage service (blob container, queue, or table) that belongs tooanother Azure subscription by using an SAS.</span></span>

## <a name="connect-tooan-azure-subscription"></a><span data-ttu-id="370d4-122">Verbinding maken met tooan Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="370d4-122">Connect tooan Azure subscription</span></span>
> [!NOTE]
> <span data-ttu-id="370d4-123">Als u geen Azure-account hebt, kunt u zich [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) of [gebruikmaken van uw voordelen als Visual Studio-abonnee](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="370d4-123">If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
>
>

1. <span data-ttu-id="370d4-124">Selecteer in Storage Explorer (voorbeeld) **Azure-accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="370d4-124">In Storage Explorer (Preview), select **Azure Account settings**.</span></span>

    ![Azure-accountinstellingen][0]

2. <span data-ttu-id="370d4-126">Hallo linkerdeelvenster geeft alle Hallo Microsoft-accounts die hebt aangemeld bij.</span><span class="sxs-lookup"><span data-stu-id="370d4-126">hello left pane displays all hello Microsoft accounts you've signed in to.</span></span> <span data-ttu-id="370d4-127">tooconnect tooanother account, selecteer **account toevoegen**, en volg Hallo instructies toosign met een Microsoft-account dat is gekoppeld aan ten minste één actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="370d4-127">tooconnect tooanother account, select **Add an account**, and then follow hello instructions toosign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>

    >[!NOTE]
    ><span data-ttu-id="370d4-128">Verbinding maken met toonational Azure (zoals Duitse Azure, Azure Government en Azure voor China via aanmelden) is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="370d4-128">Connecting toonational Azure (such as Azure Germany, Azure Government, and Azure China via sign-in) is currently not supported.</span></span> <span data-ttu-id="370d4-129">Zie Hallo ' koppelen of ontkoppelen van een extern opslagaccount ' sectie voor informatie over het tooconnect toonational Azure storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="370d4-129">See hello "Attach or detach an external storage account" section for how tooconnect toonational Azure storage accounts.</span></span>

3. <span data-ttu-id="370d4-130">Nadat u hebt aangemeld met een Microsoft-account Hallo links deelvenster is gevuld met hello Azure-abonnementen die zijn gekoppeld aan dat account.</span><span class="sxs-lookup"><span data-stu-id="370d4-130">After you successfully sign in with a Microsoft account, hello left pane is populated with hello Azure subscriptions associated with that account.</span></span> <span data-ttu-id="370d4-131">Selecteer hello Azure-abonnementen die u wilt toowork met en selecteer vervolgens **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="370d4-131">Select hello Azure subscriptions that you want toowork with, and then select **Apply**.</span></span> <span data-ttu-id="370d4-132">(Selecteren **alle abonnementen** Schakelknoppen selecteren alle of geen hello Azure-abonnementen weergegeven.)</span><span class="sxs-lookup"><span data-stu-id="370d4-132">(Selecting **All subscriptions** toggles selecting all or none of hello listed Azure subscriptions.)</span></span>

    ![Selecteer Azure-abonnementen][3]  
    <span data-ttu-id="370d4-134">Hallo linkerdeelvenster geeft Hallo storage-accounts die zijn gekoppeld aan Azure-abonnementen Hallo geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="370d4-134">hello left pane displays hello storage accounts associated with hello selected Azure subscriptions.</span></span>

    ![Geselecteerde Azure-abonnementen][4]

## <a name="connect-tooan-azure-stack-subscription"></a><span data-ttu-id="370d4-136">Verbinding maken met tooan Stack Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="370d4-136">Connect tooan Azure Stack subscription</span></span>

<span data-ttu-id="370d4-137">Zie voor informatie over verbinding tooan Stack Azure-abonnement [Opslagverkenner verbinding tooan Stack Azure-abonnement](azure-stack/azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="370d4-137">For information about connecting tooan Azure Stack subscription, see [Connect Storage Explorer tooan Azure Stack subscription](azure-stack/azure-stack-storage-connect-se.md).</span></span>

## <a name="work-with-local-development-storage"></a><span data-ttu-id="370d4-138">Werken met lokale ontwikkelingsopslag</span><span class="sxs-lookup"><span data-stu-id="370d4-138">Work with local development storage</span></span>
<span data-ttu-id="370d4-139">Met Opslagverkenner (Preview) kunt u werken met lokale opslag met behulp van hello Azure-Opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="370d4-139">With Storage Explorer (Preview), you can work against local storage by using hello Azure Storage Emulator.</span></span> <span data-ttu-id="370d4-140">Deze aanpak kunt u code schrijven tegen en test opslag schrijven zonder dat hiervoor een opslagaccount dat is geïmplementeerd in Azure, omdat het Hallo-opslagaccount wordt gesimuleerd door hello Azure-Opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="370d4-140">This approach lets you write code against and test storage without necessarily having a storage account deployed on Azure, because hello storage account is being emulated by hello Azure Storage Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="370d4-141">Hello Azure-Opslagemulator wordt momenteel alleen ondersteund voor Windows.</span><span class="sxs-lookup"><span data-stu-id="370d4-141">hello Azure Storage Emulator is currently supported only for Windows.</span></span>
>
>

1. <span data-ttu-id="370d4-142">Vouw in het linkerdeelvenster van Opslagverkenner (Preview) hello, Hallo **(lokaal en Attached)** > **Opslagaccounts** > **(ontwikkeling)** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="370d4-142">In hello left pane of Storage Explorer (Preview), expand hello **(Local and Attached)** > **Storage Accounts** > **(Development)** node.</span></span>

    ![Node lokale ontwikkeling][21]

2. <span data-ttu-id="370d4-144">Als u hello Azure-Opslagemulator nog niet hebt geïnstalleerd, bent u na vragen aan gebruiker toodo geval via de informatiebalk.</span><span class="sxs-lookup"><span data-stu-id="370d4-144">If you have not yet installed hello Azure Storage Emulator, you are prompted toodo so via an infobar.</span></span> <span data-ttu-id="370d4-145">Als Hallo informatiebalk wordt weergegeven, selecteert u **downloaden Hallo meest recente versie**, en installeer vervolgens Hallo-emulator.</span><span class="sxs-lookup"><span data-stu-id="370d4-145">If hello infobar is displayed, select **Download hello latest version**, and then install hello emulator.</span></span>

    ![Azure Storage-emulator prompt downloaden][22]

3. <span data-ttu-id="370d4-147">Nadat het Hallo-emulator is geïnstalleerd, kunt u maken en werken met lokale blobs, wachtrijen en tabellen.</span><span class="sxs-lookup"><span data-stu-id="370d4-147">After hello emulator is installed, you can create and work with local blobs, queues, and tables.</span></span> <span data-ttu-id="370d4-148">toolearn hoe toowork met elk opslagaccount typt, Zie een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="370d4-148">toolearn how toowork with each storage account type, see one of hello following:</span></span>

    * [<span data-ttu-id="370d4-149">Resources voor Azure Blob Storage beheren</span><span class="sxs-lookup"><span data-stu-id="370d4-149">Manage Azure blob storage resources</span></span>](vs-azure-tools-storage-explorer-blobs.md)
    * <span data-ttu-id="370d4-150">Opslagresources voor het delen van Azure-bestanden beheren: *binnenkort beschikbaar*</span><span class="sxs-lookup"><span data-stu-id="370d4-150">Manage Azure file share storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="370d4-151">Resources voor Azure Queue Storage beheren: *binnenkort beschikbaar*</span><span class="sxs-lookup"><span data-stu-id="370d4-151">Manage Azure queue storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="370d4-152">Resources voor Azure Table Storage beheren: *binnenkort beschikbaar*</span><span class="sxs-lookup"><span data-stu-id="370d4-152">Manage Azure table storage resources: *Coming soon*</span></span>

## <a name="attach-or-detach-an-external-storage-account"></a><span data-ttu-id="370d4-153">Koppelen aan een extern opslagaccount of de koppeling opheffen</span><span class="sxs-lookup"><span data-stu-id="370d4-153">Attach or detach an external storage account</span></span>
<span data-ttu-id="370d4-154">Met Opslagverkenner (Preview) kunt u tooexternal storage-accounts koppelen zodat storage-accounts kunnen eenvoudig worden gedeeld.</span><span class="sxs-lookup"><span data-stu-id="370d4-154">With Storage Explorer (Preview), you can attach tooexternal storage accounts so that storage accounts can be easily shared.</span></span> <span data-ttu-id="370d4-155">Deze sectie wordt uitgelegd hoe tooattach too(and detach from) externe opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="370d4-155">This section explains how tooattach too(and detach from) external storage accounts.</span></span>

### <a name="get-hello-storage-account-credentials"></a><span data-ttu-id="370d4-156">Hallo opslagaccountreferenties ophalen</span><span class="sxs-lookup"><span data-stu-id="370d4-156">Get hello storage account credentials</span></span>
<span data-ttu-id="370d4-157">tooshare een extern opslagaccount, Hallo eigenaar van het account moet zich eerst Hallo referenties (accountnaam en -sleutel) niet ophalen voor Hallo-account en daarna die informatie delen met Hallo persoon die wil tooattach toothat (externe) account.</span><span class="sxs-lookup"><span data-stu-id="370d4-157">tooshare an external storage account, hello owner of that account must first get hello credentials (account name and key) for hello account and then share that information with hello person who wants tooattach toothat (external) account.</span></span> <span data-ttu-id="370d4-158">Hallo opslagaccountreferenties via hello Azure-portal kunt u verkrijgen door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="370d4-158">You can obtain hello storage account credentials via hello Azure portal by doing hello following:</span></span>

1. <span data-ttu-id="370d4-159">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="370d4-159">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="370d4-160">Selecteer **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="370d4-160">Select **Browse**.</span></span>

3. <span data-ttu-id="370d4-161">Selecteer **Opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="370d4-161">Select **Storage Accounts**.</span></span>

4. <span data-ttu-id="370d4-162">Op Hallo **Opslagaccounts** blade, selecteer Hallo gewenst storage-account.</span><span class="sxs-lookup"><span data-stu-id="370d4-162">On hello **Storage Accounts** blade, select hello desired storage account.</span></span>

5. <span data-ttu-id="370d4-163">Op Hallo **instellingen** blade voor Hallo storage-account geselecteerd, selecteert u **toegangssleutels**.</span><span class="sxs-lookup"><span data-stu-id="370d4-163">On hello **Settings** blade for hello selected storage account, select **Access keys**.</span></span>

    ![Optie Toegangssleutels][5]

6. <span data-ttu-id="370d4-165">Op Hallo **toegangssleutels** blade, kopie Hallo **opslagaccountnaam** en **key1** waarden voor gebruik bij het toohello storage-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="370d4-165">On hello **Access keys** blade, copy hello **Storage account name** and **key1** values for use when attaching toohello storage account.</span></span>

    ![Toegangssleutels][6]

### <a name="attach-tooan-external-storage-account"></a><span data-ttu-id="370d4-167">Het externe opslagaccount tooan koppelen</span><span class="sxs-lookup"><span data-stu-id="370d4-167">Attach tooan external storage account</span></span>
<span data-ttu-id="370d4-168">tooattach tooan externe storage-account, moet u de naam en sleutel van het Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="370d4-168">tooattach tooan external storage account, you need hello account's name and key.</span></span> <span data-ttu-id="370d4-169">Hallo 'Get Hallo opslagaccountreferenties' sectie wordt uitgelegd hoe deze waarden van tooobtain hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="370d4-169">hello "Get hello storage account credentials" section explains how tooobtain these values from hello Azure portal.</span></span> <span data-ttu-id="370d4-170">Echter Hallo accountsleutel in Hallo-portal wordt aangeroepen **key1**.</span><span class="sxs-lookup"><span data-stu-id="370d4-170">However, in hello portal, hello account key is called **key1**.</span></span> <span data-ttu-id="370d4-171">Dus wanneer Opslagverkenner (Preview) om een accountsleutel wordt gevraagd, u Voer Hallo **key1** waarde.</span><span class="sxs-lookup"><span data-stu-id="370d4-171">So where Storage Explorer (Preview) asks for an account key, you enter hello **key1** value.</span></span>

1. <span data-ttu-id="370d4-172">Selecteer in Opslagverkenner (Preview) **tooAzure opslag koppelt**.</span><span class="sxs-lookup"><span data-stu-id="370d4-172">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Verbinding maken met de opslagoptie tooAzure][23]

2. <span data-ttu-id="370d4-174">In Hallo **tooAzure opslag verbinding** dialoogvenster geeft u de accountsleutel hello (Hallo **key1** waarde van hello Azure-portal), en selecteer vervolgens **volgende**.</span><span class="sxs-lookup"><span data-stu-id="370d4-174">In hello **Connect tooAzure Storage** dialog box, specify hello account key (hello **key1** value from hello Azure portal), and then select **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="370d4-175">U kunt Hallo-verbindingsreeks voor opslag van een opslagaccount op nationale Azure invoeren.</span><span class="sxs-lookup"><span data-stu-id="370d4-175">You can enter hello storage connection string from a storage account on national Azure.</span></span> <span data-ttu-id="370d4-176">Bijvoorbeeld, voer tooconnect tooAzure Duitsland storage-accounts, verbinding tekenreeksen vergelijkbare toohello volgende in:</span><span class="sxs-lookup"><span data-stu-id="370d4-176">For example, tooconnect tooAzure Germany storage accounts, enter connection strings similar toohello following:</span></span> 
    >
    >* <span data-ttu-id="370d4-177">DefaultEndpointsProtocol=https</span><span class="sxs-lookup"><span data-stu-id="370d4-177">DefaultEndpointsProtocol=https</span></span>
    >* <span data-ttu-id="370d4-178">AccountName=cawatest03</span><span class="sxs-lookup"><span data-stu-id="370d4-178">AccountName=cawatest03</span></span>
    >* <span data-ttu-id="370d4-179">AccountKey=<storage_account_key></span><span class="sxs-lookup"><span data-stu-id="370d4-179">AccountKey=<storage_account_key></span></span>
    >* <span data-ttu-id="370d4-180">EndpointSuffix=core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="370d4-180">EndpointSuffix=core.cloudapi.de</span></span>
    
    ><span data-ttu-id="370d4-181">U kunt Hallo-verbindingsreeks ophalen van hello Azure portal in Hallo dezelfde manier zoals beschreven in Hallo sectie 'Hello opslagaccountreferenties ophalen'.</span><span class="sxs-lookup"><span data-stu-id="370d4-181">You can get hello connection string from hello Azure portal in hello same way as described in hello "Get hello storage account credentials" section.</span></span>

    ![Verbinding maken in het dialoogvenster tooAzure-opslag][24]

3. <span data-ttu-id="370d4-183">In Hallo **externe opslag koppelen** dialoogvenster in Hallo **accountnaam** vak, voer opslagaccountnaam hello, geef de gewenste instellingen en selecteer vervolgens **volgende**.</span><span class="sxs-lookup"><span data-stu-id="370d4-183">In hello **Attach External Storage** dialog box, in hello **Account name** box, enter hello storage account name, specify any other desired settings, and then select **Next**.</span></span>

    ![Dialoogvenster Externe opslag koppelen][8]

4. <span data-ttu-id="370d4-185">In Hallo **verbinding samenvatting** dialoogvenster of Hallo informatie.</span><span class="sxs-lookup"><span data-stu-id="370d4-185">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="370d4-186">Als u alles toochange wilt, schakelt u **terug** en voer deze opnieuw Hallo gewenste instellingen.</span><span class="sxs-lookup"><span data-stu-id="370d4-186">If you want toochange anything, select **Back** and reenter hello desired settings.</span></span> 

5. <span data-ttu-id="370d4-187">Selecteer **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="370d4-187">Select **Connect**.</span></span>

6. <span data-ttu-id="370d4-188">Nadat deze is verbonden, Hallo externe opslagaccount weergegeven met **(extern)** toohello opslagaccountnaam toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="370d4-188">After it is successfully connected, hello external storage account is displayed with **(External)** appended toohello storage account name.</span></span>

    ![Resultaat van het verbinden van externe tooan-opslagaccount][9]

### <a name="detach-from-an-external-storage-account"></a><span data-ttu-id="370d4-190">De koppeling met een extern opslagaccount opheffen</span><span class="sxs-lookup"><span data-stu-id="370d4-190">Detach from an external storage account</span></span>
1. <span data-ttu-id="370d4-191">Met de rechtermuisknop op het externe opslagaccount hello wilt toodetach en selecteer vervolgens **Detach**.</span><span class="sxs-lookup"><span data-stu-id="370d4-191">Right-click hello external storage account that you want toodetach, and then select **Detach**.</span></span>

    ![Loskoppelen van de opslagoptie][10]

2. <span data-ttu-id="370d4-193">Selecteer in het bevestigingsbericht hello, **Ja** tooconfirm Hallo loskoppelen van het externe opslagaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="370d4-193">In hello confirmation message, select **Yes** tooconfirm hello detachment from hello external storage account.</span></span>

## <a name="attach-a-storage-account-by-using-an-sas"></a><span data-ttu-id="370d4-194">Een opslagaccount koppelen met behulp van een SAS</span><span class="sxs-lookup"><span data-stu-id="370d4-194">Attach a storage account by using an SAS</span></span>
<span data-ttu-id="370d4-195">Een [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) kunt Hallo beheerder van een Azure-abonnement tijdelijke toegang tooa opslagaccount verlenen zonder tooprovide Azure-abonnementsreferenties.</span><span class="sxs-lookup"><span data-stu-id="370d4-195">An [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) lets hello admin of an Azure subscription grant temporary access tooa storage account without having tooprovide Azure subscription credentials.</span></span>

<span data-ttu-id="370d4-196">tooillustrate dit scenario, laten we zeggen dat GebruikerA is een beheerder van een Azure-abonnement en gebruiker a wil tooallow gebruiker b tooaccess een opslag-account voor een beperkte tijd met bepaalde machtigingen:</span><span class="sxs-lookup"><span data-stu-id="370d4-196">tooillustrate this scenario, let's say that UserA is an admin of an Azure subscription, and UserA wants tooallow UserB tooaccess a storage account for a limited time with certain permissions:</span></span>

1. <span data-ttu-id="370d4-197">Gebruiker a genereert een SAS (bestaande uit Hallo-verbindingsreeks voor Hallo storage-account) voor een bepaald tijdstip en met Hallo gewenst machtigingen.</span><span class="sxs-lookup"><span data-stu-id="370d4-197">UserA generates an SAS (consisting of hello connection string for hello storage account) for a specific time period and with hello desired permissions.</span></span>

2. <span data-ttu-id="370d4-198">Gebruiker a shares Hallo SAS met Hallo persoon (in ons voorbeeld gebruiker b) die toegang toohello storage-account willen.</span><span class="sxs-lookup"><span data-stu-id="370d4-198">UserA shares hello SAS with hello person (UserB, in our example) who wants access toohello storage account.</span></span>  

3. <span data-ttu-id="370d4-199">Gebruiker b gebruikt Opslagverkenner (Preview) tooattach toohello account die deel uitmaakt van tooUserA met behulp van Hallo opgegeven SAS.</span><span class="sxs-lookup"><span data-stu-id="370d4-199">UserB uses Storage Explorer (Preview) tooattach toohello account that belongs tooUserA by using hello supplied SAS.</span></span>

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a><span data-ttu-id="370d4-200">Een SAS ophalen voor de gewenste tooshare Hallo-account</span><span class="sxs-lookup"><span data-stu-id="370d4-200">Get an SAS for hello account you want tooshare</span></span>
1. <span data-ttu-id="370d4-201">In Opslagverkenner (Preview) met de rechtermuisknop op Hallo storage-account u wilt delen, en selecteer vervolgens **Shared Access Signature ophalen**.</span><span class="sxs-lookup"><span data-stu-id="370d4-201">In Storage Explorer (Preview), right-click hello storage account you want share, and then select **Get Shared Access Signature**.</span></span>

    ![Optie SAS-contextmenu ophalen][13]

2. <span data-ttu-id="370d4-203">In Hallo **Shared Access Signature** dialoogvenster geeft u de Hallo tijdsbestek en machtigingen die u wilt voor Hallo-account en selecteer vervolgens **maken**.</span><span class="sxs-lookup"><span data-stu-id="370d4-203">In hello **Shared Access Signature** dialog box, specify hello time frame and permissions that you want for hello account, and then select **Create**.</span></span>

    <span data-ttu-id="370d4-204">![Dialoogvenster SAS ophalen][14]</span><span class="sxs-lookup"><span data-stu-id="370d4-204">![Get SAS dialog box][14]</span></span>  
    <span data-ttu-id="370d4-205">Hallo **Shared Access Signature** in het dialoogvenster wordt geopend en Hallo SAS.</span><span class="sxs-lookup"><span data-stu-id="370d4-205">hello **Shared Access Signature** dialog box opens and displays hello SAS.</span></span>

3. <span data-ttu-id="370d4-206">Volgende toohello **verbindingsreeks**, selecteer **kopie** toocopy het toohello Klembord, en selecteer vervolgens **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="370d4-206">Next toohello **Connection String**, select **Copy** toocopy it toohello clipboard, and then select **Close**.</span></span>

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a><span data-ttu-id="370d4-207">Toohello gedeeld account koppelen via SAS Hallo</span><span class="sxs-lookup"><span data-stu-id="370d4-207">Attach toohello shared account by using hello SAS</span></span>
1. <span data-ttu-id="370d4-208">Selecteer in Opslagverkenner (Preview) **tooAzure opslag koppelt**.</span><span class="sxs-lookup"><span data-stu-id="370d4-208">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Verbinding maken met de opslagoptie tooAzure][23]

2. <span data-ttu-id="370d4-210">In Hallo **tooAzure opslag verbinding** in het dialoogvenster verbindingsreeks Hallo opgeven en selecteer vervolgens **volgende**.</span><span class="sxs-lookup"><span data-stu-id="370d4-210">In hello **Connect tooAzure Storage** dialog box, specify hello connection string, and then select **Next**.</span></span>

    ![Verbinding maken in het dialoogvenster tooAzure-opslag][24]

3. <span data-ttu-id="370d4-212">In Hallo **verbinding samenvatting** dialoogvenster of Hallo informatie.</span><span class="sxs-lookup"><span data-stu-id="370d4-212">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="370d4-213">toomake gewijzigd, schakelt u **terug**, en voer vervolgens de gewenste Hallo-instellingen.</span><span class="sxs-lookup"><span data-stu-id="370d4-213">toomake changes, select **Back**, and then enter hello settings you want.</span></span> 

4. <span data-ttu-id="370d4-214">Selecteer **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="370d4-214">Select **Connect**.</span></span>

5. <span data-ttu-id="370d4-215">Nadat deze is gekoppeld, Hallo opslagaccount weergegeven met **(SAS)** toegevoegd toohello accountnaam op die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="370d4-215">After it is attached, hello storage account is displayed with **(SAS)** appended toohello account name that you supplied.</span></span>

    ![Resultaat van het account van de gekoppelde tooan via SAS][17]

## <a name="attach-a-service-by-using-an-sas"></a><span data-ttu-id="370d4-217">Een service koppelen met behulp van een SAS</span><span class="sxs-lookup"><span data-stu-id="370d4-217">Attach a service by using an SAS</span></span>
<span data-ttu-id="370d4-218">Hallo 'Storage-account koppelen via een SAS' sectie wordt uitgelegd hoe de beheerder van een Azure-abonnement tijdelijke toegang tooa storage-account kunt verlenen door te genereren en delen van een SAS voor Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="370d4-218">hello "Attach a storage account by using an SAS" section explains how an Azure subscription admin can grant temporary access tooa storage account by generating and sharing an SAS for hello storage account.</span></span> <span data-ttu-id="370d4-219">Op deze manier kunt u ook een SAS genereren voor een bepaalde service (blobcontainer, wachtrij of tabel) binnen een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="370d4-219">Similarly, an SAS can be generated for a specific service (blob container, queue, or table) within a storage account.</span></span>  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a><span data-ttu-id="370d4-220">Een SAS voor Hallo-service die u wilt dat tooshare genereren</span><span class="sxs-lookup"><span data-stu-id="370d4-220">Generate an SAS for hello service that you want tooshare</span></span>
<span data-ttu-id="370d4-221">In deze context is een service een blobcontainer, een wachtrij of een tabel.</span><span class="sxs-lookup"><span data-stu-id="370d4-221">In this context, a service can be a blob container, queue, or table.</span></span> <span data-ttu-id="370d4-222">toogenerate hello SAS voor een vermelde service, Zie:</span><span class="sxs-lookup"><span data-stu-id="370d4-222">toogenerate hello SAS for a listed service, see:</span></span>

* [<span data-ttu-id="370d4-223">Hallo SAS ophalen voor een blob-container</span><span class="sxs-lookup"><span data-stu-id="370d4-223">Get hello SAS for a blob container</span></span>](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* <span data-ttu-id="370d4-224">Hallo SAS ophalen voor een bestandsshare: *binnenkort beschikbaar*</span><span class="sxs-lookup"><span data-stu-id="370d4-224">Get hello SAS for a file share: *Coming soon*</span></span>
* <span data-ttu-id="370d4-225">Hallo SAS ophalen voor een wachtrij: *binnenkort beschikbaar*</span><span class="sxs-lookup"><span data-stu-id="370d4-225">Get hello SAS for a queue: *Coming soon*</span></span>
* <span data-ttu-id="370d4-226">Hallo SAS ophalen voor een tabel: *binnenkort beschikbaar*</span><span class="sxs-lookup"><span data-stu-id="370d4-226">Get hello SAS for a table: *Coming soon*</span></span>

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a><span data-ttu-id="370d4-227">Service met behulp van Hallo SAS toohello gedeeld-account koppelen</span><span class="sxs-lookup"><span data-stu-id="370d4-227">Attach toohello shared account service by using hello SAS</span></span>
1. <span data-ttu-id="370d4-228">Selecteer in Opslagverkenner (Preview) **tooAzure opslag koppelt**.</span><span class="sxs-lookup"><span data-stu-id="370d4-228">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Verbinding maken met de opslagoptie tooAzure][23]

2. <span data-ttu-id="370d4-230">In Hallo **tooAzure opslag verbinding** in het dialoogvenster Hallo SAS-URI opgeven en selecteer vervolgens **volgende**.</span><span class="sxs-lookup"><span data-stu-id="370d4-230">In hello **Connect tooAzure Storage** dialog box, specify hello SAS URI, and then select **Next**.</span></span>

    ![Verbinding maken in het dialoogvenster tooAzure-opslag][24]

3. <span data-ttu-id="370d4-232">In Hallo **verbinding samenvatting** dialoogvenster of Hallo informatie.</span><span class="sxs-lookup"><span data-stu-id="370d4-232">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="370d4-233">toomake gewijzigd, schakelt u **terug**, en voer vervolgens de gewenste Hallo-instellingen.</span><span class="sxs-lookup"><span data-stu-id="370d4-233">toomake changes, select **Back**, and then enter hello settings you want.</span></span> 

4. <span data-ttu-id="370d4-234">Selecteer **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="370d4-234">Select **Connect**.</span></span>

5. <span data-ttu-id="370d4-235">Nadat deze is gekoppeld, hello zojuist gekoppelde service wordt weergegeven onder Hallo **(Service-SAS)** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="370d4-235">After it is attached, hello newly attached service is displayed under hello **(Service SAS)** node.</span></span>

    ![Resultaat van het koppelen van tooa shared service met behulp van een SAS][20]

## <a name="search-for-storage-accounts"></a><span data-ttu-id="370d4-237">Zoeken naar opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="370d4-237">Search for storage accounts</span></span>
<span data-ttu-id="370d4-238">Als u een lange lijst met opslagaccounts hebt, is een toolocate snel bepaalde opslagaccounts toouse Hallo zoekvak Hallo boven aan het linkerdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="370d4-238">If you have a long list of storage accounts, a quick way toolocate a particular storage account is toouse hello search box at hello top of hello left pane.</span></span>

<span data-ttu-id="370d4-239">Terwijl u in het zoekvak hello typt, linkerdeelvenster Hallo geeft Hallo storage-accounts die overeenkomen met de Hallo zoekwaarde die u hebt ingevoerd toothat punt.</span><span class="sxs-lookup"><span data-stu-id="370d4-239">As you type in hello search box, hello left pane displays hello storage accounts that match hello search value you've entered up toothat point.</span></span> <span data-ttu-id="370d4-240">Bijvoorbeeld, een zoekopdracht voor alle opslagaccounts waarvan de naam bevat **tarcher** wordt weergegeven in de volgende schermafbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="370d4-240">For example, a search for all storage accounts whose name contains **tarcher** is shown in hello following screenshot:</span></span>

![Zoeken naar Storage-account][11]

## <a name="next-steps"></a><span data-ttu-id="370d4-242">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="370d4-242">Next steps</span></span>
* [<span data-ttu-id="370d4-243">Azure Blob Storage-resources beheren met Opslagverkenner (Preview)</span><span class="sxs-lookup"><span data-stu-id="370d4-243">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
