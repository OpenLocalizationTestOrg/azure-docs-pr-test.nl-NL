---
title: Aan de slag met Opslagverkenner (Preview) | Microsoft Docs
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
ms.openlocfilehash: 1794a86a4185d587cf184a1f61a5720e2ab65e92
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-storage-explorer-preview"></a><span data-ttu-id="c2279-103">Aan de slag met Opslagverkenner (Preview)</span><span class="sxs-lookup"><span data-stu-id="c2279-103">Get started with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="c2279-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c2279-104">Overview</span></span>
<span data-ttu-id="c2279-105">Azure Storage Explorer (Preview) is een zelfstandige app waarmee u eenvoudig met Azure Storage-gegevens kunt werken via Windows, macOS en Linux.</span><span class="sxs-lookup"><span data-stu-id="c2279-105">Azure Storage Explorer (Preview) is a standalone app that enables you to easily work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="c2279-106">In dit artikel leert u op welke manieren u verbinding kunt maken met Azure Storage-accounts en hoe u deze kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="c2279-106">In this article, you learn the various ways of connecting to and managing your Azure storage accounts.</span></span>

![Microsoft Azure Storage Explorer (voorbeeld)][15]

## <a name="prerequisites"></a><span data-ttu-id="c2279-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c2279-108">Prerequisites</span></span>
* [<span data-ttu-id="c2279-109">Opslagverkenner (Preview) downloaden en installeren</span><span class="sxs-lookup"><span data-stu-id="c2279-109">Download and install Storage Explorer (Preview)</span></span>](http://www.storageexplorer.com)

## <a name="connect-to-a-storage-account-or-service"></a><span data-ttu-id="c2279-110">Verbinding maken met een opslagaccount of -service</span><span class="sxs-lookup"><span data-stu-id="c2279-110">Connect to a storage account or service</span></span>
<span data-ttu-id="c2279-111">Opslagverkenner (Preview) biedt verschillende manieren om verbinding te maken met opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="c2279-111">Storage Explorer (Preview) provides several ways to connect to storage accounts.</span></span> <span data-ttu-id="c2279-112">U kunt bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c2279-112">For example, you can:</span></span>
* <span data-ttu-id="c2279-113">Verbinding maken met de opslagaccounts die zijn gekoppeld aan uw Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="c2279-113">Connect to storage accounts associated with your Azure subscriptions.</span></span>
* <span data-ttu-id="c2279-114">Verbinding maken met de opslagaccounts en -services die via andere Azure-abonnementen worden gedeeld.</span><span class="sxs-lookup"><span data-stu-id="c2279-114">Connect to storage accounts and services that are shared from other Azure subscriptions.</span></span>
* <span data-ttu-id="c2279-115">Verbinding maken met lokale opslag en lokale opslag beheren met de Azure-opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="c2279-115">Connect to and manage local storage by using the Azure Storage Emulator.</span></span> 

<span data-ttu-id="c2279-116">Bovendien kunt u wereldwijd en nationaal werken met opslagaccounts in Azure:</span><span class="sxs-lookup"><span data-stu-id="c2279-116">In addition, you can work with storage accounts in global and national Azure:</span></span>

* <span data-ttu-id="c2279-117">[Verbinding maken met een Azure-abonnement](#connect-to-an-azure-subscription): beheer opslagresources die deel uitmaken van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="c2279-117">[Connect to an Azure subscription](#connect-to-an-azure-subscription): Manage storage resources that belong to your Azure subscription.</span></span>
* <span data-ttu-id="c2279-118">[Verbinding maken met lokale opslag](#work-with-local-development-storage): beheer lokale opslag met de Azure-opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="c2279-118">[Work with local development storage](#work-with-local-development-storage): Manage local storage by using the Azure Storage Emulator.</span></span>
* <span data-ttu-id="c2279-119">[Koppelen aan externe opslag](#attach-or-detach-an-external-storage-account): beheer de opslagresources die deel uitmaken van een ander Azure-abonnement of landelijke Azure-clouds, via de naam, sleutel en eindpunten van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c2279-119">[Attach to external storage](#attach-or-detach-an-external-storage-account): Manage storage resources that belong to another Azure subscription or that are under national Azure clouds by using the storage account's name, key, and endpoints.</span></span>
* <span data-ttu-id="c2279-120">[Een opslagaccount koppelen met behulp van een SAS](#attach-storage-account-using-sas): beheer de opslagresources die deel uitmaken van een ander Azure-abonnement via een handtekening voor gedeelde toegang (SAS).</span><span class="sxs-lookup"><span data-stu-id="c2279-120">[Attach a storage account by using an SAS](#attach-storage-account-using-sas): Manage storage resources that belong to another Azure subscription by using a shared access signature (SAS).</span></span>
* <span data-ttu-id="c2279-121">[Een service koppelen met behulp van een SAS](#attach-service-using-sas): beheer een specifieke opslagservice (blobcontainer, wachtrij of tabel) die deel uitmaakt van een ander Azure-abonnement via een handtekening voor gedeelde toegang (SAS).</span><span class="sxs-lookup"><span data-stu-id="c2279-121">[Attach a service by using an SAS](#attach-service-using-sas): Manage a specific storage service (blob container, queue, or table) that belongs to another Azure subscription by using an SAS.</span></span>

## <a name="connect-to-an-azure-subscription"></a><span data-ttu-id="c2279-122">Verbinding maken met een Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="c2279-122">Connect to an Azure subscription</span></span>
> [!NOTE]
> <span data-ttu-id="c2279-123">Als u geen Azure-account hebt, kunt u zich [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) of [gebruikmaken van uw voordelen als Visual Studio-abonnee](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="c2279-123">If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
>
>

1. <span data-ttu-id="c2279-124">Selecteer in Storage Explorer (voorbeeld) **Azure-accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="c2279-124">In Storage Explorer (Preview), select **Azure Account settings**.</span></span>

    ![Azure-accountinstellingen][0]

2. <span data-ttu-id="c2279-126">In het linkerdeelvenster ziet u alle Microsoft-accounts waarbij u bent aangemeld.</span><span class="sxs-lookup"><span data-stu-id="c2279-126">The left pane displays all the Microsoft accounts you've signed in to.</span></span> <span data-ttu-id="c2279-127">Selecteer **Een account toevoegen** om verbinding te maken met een ander account en volg de instructies om u aan te melden met een Microsoft-account dat is gekoppeld aan ten minste één actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="c2279-127">To connect to another account, select **Add an account**, and then follow the instructions to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>

    >[!NOTE]
    ><span data-ttu-id="c2279-128">Het maken van verbinding met een landelijke Azure (zoals Azure Duitsland, Azure Government en Azure China via aanmelding) wordt momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c2279-128">Connecting to national Azure (such as Azure Germany, Azure Government, and Azure China via sign-in) is currently not supported.</span></span> <span data-ttu-id="c2279-129">Raadpleeg de sectie 'Koppelen aan een extern opslagaccount of de koppeling opheffen' voor informatie over hoe u verbinding maakt met landelijke Azure-opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="c2279-129">See the "Attach or detach an external storage account" section for how to connect to national Azure storage accounts.</span></span>

3. <span data-ttu-id="c2279-130">Nadat u bent aangemeld met een Microsoft-account, worden in het linkerdeelvenster de Azure-abonnementen weergegeven die aan dat account zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="c2279-130">After you successfully sign in with a Microsoft account, the left pane is populated with the Azure subscriptions associated with that account.</span></span> <span data-ttu-id="c2279-131">Selecteer de Azure-abonnementen waarmee u wilt werken en selecteer vervolgens **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="c2279-131">Select the Azure subscriptions that you want to work with, and then select **Apply**.</span></span> <span data-ttu-id="c2279-132">(Door **Alle abonnementen** te selecteren selecteert u alle of geen Azure-abonnementen.)</span><span class="sxs-lookup"><span data-stu-id="c2279-132">(Selecting **All subscriptions** toggles selecting all or none of the listed Azure subscriptions.)</span></span>

    ![Selecteer Azure-abonnementen][3]  
    <span data-ttu-id="c2279-134">In het linkerdeelvenster worden de opslagaccounts weergegeven die aan de geselecteerde Azure-abonnementen zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="c2279-134">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span></span>

    ![Geselecteerde Azure-abonnementen][4]

## <a name="connect-to-an-azure-stack-subscription"></a><span data-ttu-id="c2279-136">Verbinding maken met een Azure Stack-abonnement</span><span class="sxs-lookup"><span data-stu-id="c2279-136">Connect to an Azure Stack subscription</span></span>

<span data-ttu-id="c2279-137">Zie [Connect Storage Explorer to an Azure Stack subscription](azure-stack/azure-stack-storage-connect-se.md) (Opslagverkenner verbinden met een Azure Stack-abonnement) voor meer informatie over hoe u verbinding maakt met een Azure Stack-abonnement.</span><span class="sxs-lookup"><span data-stu-id="c2279-137">For information about connecting to an Azure Stack subscription, see [Connect Storage Explorer to an Azure Stack subscription](azure-stack/azure-stack-storage-connect-se.md).</span></span>

## <a name="work-with-local-development-storage"></a><span data-ttu-id="c2279-138">Werken met lokale ontwikkelingsopslag</span><span class="sxs-lookup"><span data-stu-id="c2279-138">Work with local development storage</span></span>
<span data-ttu-id="c2279-139">Met Opslagverkenner (Preview) kunt u met lokale opslag werken via de Azure-opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="c2279-139">With Storage Explorer (Preview), you can work against local storage by using the Azure Storage Emulator.</span></span> <span data-ttu-id="c2279-140">Hiermee kunt u code schrijven voor opslag en opslag testen zonder dat u een opslagaccount hoeft te hebben geïmplementeerd in Azure, omdat het opslagaccount wordt gesimuleerd door de Azure-opslagemulator.</span><span class="sxs-lookup"><span data-stu-id="c2279-140">This approach lets you write code against and test storage without necessarily having a storage account deployed on Azure, because the storage account is being emulated by the Azure Storage Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="c2279-141">De Azure-opslagemulator wordt momenteel alleen door Windows ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c2279-141">The Azure Storage Emulator is currently supported only for Windows.</span></span>
>
>

1. <span data-ttu-id="c2279-142">Vouw in het linkerdeelvenster van Opslagverkenner (Preview) de node **(Lokale en bijgevoegde)** > **Opslagaccounts** > **(ontwikkeling)** uit.</span><span class="sxs-lookup"><span data-stu-id="c2279-142">In the left pane of Storage Explorer (Preview), expand the **(Local and Attached)** > **Storage Accounts** > **(Development)** node.</span></span>

    ![Node lokale ontwikkeling][21]

2. <span data-ttu-id="c2279-144">Als u de Azure-opslagemulator nog niet hebt geïnstalleerd, wordt u via de informatiebalk gevraagd dit te doen.</span><span class="sxs-lookup"><span data-stu-id="c2279-144">If you have not yet installed the Azure Storage Emulator, you are prompted to do so via an infobar.</span></span> <span data-ttu-id="c2279-145">Wanneer de informatiebalk wordt weergegeven, selecteert u **De nieuwste versie downloaden** en installeert u de emulator.</span><span class="sxs-lookup"><span data-stu-id="c2279-145">If the infobar is displayed, select **Download the latest version**, and then install the emulator.</span></span>

    ![Azure Storage-emulator prompt downloaden][22]

3. <span data-ttu-id="c2279-147">Wanneer de emulator is geïnstalleerd, kunt u lokale blobs, wachtrijen en tabellen maken en hiermee werken.</span><span class="sxs-lookup"><span data-stu-id="c2279-147">After the emulator is installed, you can create and work with local blobs, queues, and tables.</span></span> <span data-ttu-id="c2279-148">Als u wilt leren hoe u met elk type opslagaccount werkt, raadpleegt u een van de volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="c2279-148">To learn how to work with each storage account type, see one of the following:</span></span>

    * [<span data-ttu-id="c2279-149">Resources voor Azure Blob Storage beheren</span><span class="sxs-lookup"><span data-stu-id="c2279-149">Manage Azure blob storage resources</span></span>](vs-azure-tools-storage-explorer-blobs.md)
    * <span data-ttu-id="c2279-150">Opslagresources voor het delen van Azure-bestanden beheren: *binnenkort beschikbaar*</span><span class="sxs-lookup"><span data-stu-id="c2279-150">Manage Azure file share storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="c2279-151">Resources voor Azure Queue Storage beheren: *binnenkort beschikbaar*</span><span class="sxs-lookup"><span data-stu-id="c2279-151">Manage Azure queue storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="c2279-152">Resources voor Azure Table Storage beheren: *binnenkort beschikbaar*</span><span class="sxs-lookup"><span data-stu-id="c2279-152">Manage Azure table storage resources: *Coming soon*</span></span>

## <a name="attach-or-detach-an-external-storage-account"></a><span data-ttu-id="c2279-153">Koppelen aan een extern opslagaccount of de koppeling opheffen</span><span class="sxs-lookup"><span data-stu-id="c2279-153">Attach or detach an external storage account</span></span>
<span data-ttu-id="c2279-154">Met Opslagverkenner (Preview) kunt u externe opslagaccounts koppelen zodat opslagaccounts eenvoudig kunnen worden gedeeld.</span><span class="sxs-lookup"><span data-stu-id="c2279-154">With Storage Explorer (Preview), you can attach to external storage accounts so that storage accounts can be easily shared.</span></span> <span data-ttu-id="c2279-155">In dit gedeelte wordt uitgelegd hoe u externe opslagaccounts koppelt (en hoe u de koppeling opheft).</span><span class="sxs-lookup"><span data-stu-id="c2279-155">This section explains how to attach to (and detach from) external storage accounts.</span></span>

### <a name="get-the-storage-account-credentials"></a><span data-ttu-id="c2279-156">De opslagaccountreferenties ophalen</span><span class="sxs-lookup"><span data-stu-id="c2279-156">Get the storage account credentials</span></span>
<span data-ttu-id="c2279-157">Als u een extern opslagaccount wilt delen, moet de eigenaar van dat account eerst de referenties ontvangen (accountnaam en -sleutel) voor het account en daarna die informatie delen met de persoon die verbinding wil maken met dat (externe) account.</span><span class="sxs-lookup"><span data-stu-id="c2279-157">To share an external storage account, the owner of that account must first get the credentials (account name and key) for the account and then share that information with the person who wants to attach to that (external) account.</span></span> <span data-ttu-id="c2279-158">Ga als volgt te werk om de opslagaccountreferenties te verkrijgen via de Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="c2279-158">You can obtain the storage account credentials via the Azure portal by doing the following:</span></span>

1. <span data-ttu-id="c2279-159">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c2279-159">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="c2279-160">Selecteer **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="c2279-160">Select **Browse**.</span></span>

3. <span data-ttu-id="c2279-161">Selecteer **Opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="c2279-161">Select **Storage Accounts**.</span></span>

4. <span data-ttu-id="c2279-162">Op de blade **Opslagaccounts** selecteert u het gewenste opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c2279-162">On the **Storage Accounts** blade, select the desired storage account.</span></span>

5. <span data-ttu-id="c2279-163">Op de blade **Instellingen** van het geselecteerde opslagaccount selecteert u **Toegangssleutels**.</span><span class="sxs-lookup"><span data-stu-id="c2279-163">On the **Settings** blade for the selected storage account, select **Access keys**.</span></span>

    ![Optie Toegangssleutels][5]

6. <span data-ttu-id="c2279-165">Op de blade **Toegangssleutels** kopieert u de waarden voor **Opslagaccountnaam** en **key1** voor gebruik bij het koppelen aan het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c2279-165">On the **Access keys** blade, copy the **Storage account name** and **key1** values for use when attaching to the storage account.</span></span>

    ![Toegangssleutels][6]

### <a name="attach-to-an-external-storage-account"></a><span data-ttu-id="c2279-167">Koppelen aan een extern opslagaccount</span><span class="sxs-lookup"><span data-stu-id="c2279-167">Attach to an external storage account</span></span>
<span data-ttu-id="c2279-168">Als u verbinding wilt maken met een extern opslagaccount, moet u de accountaam en -sleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="c2279-168">To attach to an external storage account, you need the account's name and key.</span></span> <span data-ttu-id="c2279-169">In het gedeelte 'De opslagaccountreferenties ophalen' wordt uitgelegd hoe u deze waarden verkrijgt in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c2279-169">The "Get the storage account credentials" section explains how to obtain these values from the Azure portal.</span></span> <span data-ttu-id="c2279-170">In de portal wordt de accountsleutel echter **key1** genoemd.</span><span class="sxs-lookup"><span data-stu-id="c2279-170">However, in the portal, the account key is called **key1**.</span></span> <span data-ttu-id="c2279-171">Als Opslagverkenner (Preview) om een accountsleutel vraagt, geeft u dus de waarde **key1** op.</span><span class="sxs-lookup"><span data-stu-id="c2279-171">So where Storage Explorer (Preview) asks for an account key, you enter the **key1** value.</span></span>

1. <span data-ttu-id="c2279-172">Selecteer in Storage Explorer (voorbeeld) **Verbinding maken met Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="c2279-172">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Verbinding maken met de optie Azure Storage][23]

2. <span data-ttu-id="c2279-174">Geef in het dialoogvenster **Verbinding maken met Azure Storage** de accountsleutel (de waarde **key1** van de Azure Portal) op en selecteer **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="c2279-174">In the **Connect to Azure Storage** dialog box, specify the account key (the **key1** value from the Azure portal), and then select **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c2279-175">U kunt een Storage-verbindingsreeks van een opslagaccount invoeren in een landelijk Azure-onderdeel.</span><span class="sxs-lookup"><span data-stu-id="c2279-175">You can enter the storage connection string from a storage account on national Azure.</span></span> <span data-ttu-id="c2279-176">Als u bijvoorbeeld verbinding wilt maken met opslagaccounts van Azure Duitsland, voert u verbindingsreeksen in die vergelijkbaar zijn met de volgende:</span><span class="sxs-lookup"><span data-stu-id="c2279-176">For example, to connect to Azure Germany storage accounts, enter connection strings similar to the following:</span></span> 
    >
    >* <span data-ttu-id="c2279-177">DefaultEndpointsProtocol=https</span><span class="sxs-lookup"><span data-stu-id="c2279-177">DefaultEndpointsProtocol=https</span></span>
    >* <span data-ttu-id="c2279-178">AccountName=cawatest03</span><span class="sxs-lookup"><span data-stu-id="c2279-178">AccountName=cawatest03</span></span>
    >* <span data-ttu-id="c2279-179">AccountKey=<storage_account_key></span><span class="sxs-lookup"><span data-stu-id="c2279-179">AccountKey=<storage_account_key></span></span>
    >* <span data-ttu-id="c2279-180">EndpointSuffix=core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="c2279-180">EndpointSuffix=core.cloudapi.de</span></span>
    
    ><span data-ttu-id="c2279-181">U verkrijgt de verbindingsreeks van de Azure Portal op de manier die wordt beschreven in de sectie 'De opslagaccountreferenties ophalen'.</span><span class="sxs-lookup"><span data-stu-id="c2279-181">You can get the connection string from the Azure portal in the same way as described in the "Get the storage account credentials" section.</span></span>

    ![Verbinding maken met het dialoogvenster Azure Storage][24]

3. <span data-ttu-id="c2279-183">In het dialoogvenster **Externe opslag koppelen** voert u de naam van het opslagaccount in het vak **Accountnaam** in en voert u andere gewenste instellingen in. Selecteer daarna **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="c2279-183">In the **Attach External Storage** dialog box, in the **Account name** box, enter the storage account name, specify any other desired settings, and then select **Next**.</span></span>

    ![Dialoogvenster Externe opslag koppelen][8]

4. <span data-ttu-id="c2279-185">In het dialoogvenster **Samenvatting verbinding** controleert u de gegevens.</span><span class="sxs-lookup"><span data-stu-id="c2279-185">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="c2279-186">Als u iets wilt wijzigen, selecteert u **Terug** en voert u de gewenste instellingen opnieuw in.</span><span class="sxs-lookup"><span data-stu-id="c2279-186">If you want to change anything, select **Back** and reenter the desired settings.</span></span> 

5. <span data-ttu-id="c2279-187">Selecteer **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="c2279-187">Select **Connect**.</span></span>

6. <span data-ttu-id="c2279-188">Nadat de verbinding tot stand is gekomen, wordt het externe opslagaccount weergegeven en **(Extern)** aan de naam van het opslagaccount toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="c2279-188">After it is successfully connected, the external storage account is displayed with **(External)** appended to the storage account name.</span></span>

    ![Resultaat van koppelen met een extern opslagaccount][9]

### <a name="detach-from-an-external-storage-account"></a><span data-ttu-id="c2279-190">De koppeling met een extern opslagaccount opheffen</span><span class="sxs-lookup"><span data-stu-id="c2279-190">Detach from an external storage account</span></span>
1. <span data-ttu-id="c2279-191">Klik met de rechtermuisknop op het externe opslagaccount dat u wilt loskoppelen en selecteer **Loskoppelen**.</span><span class="sxs-lookup"><span data-stu-id="c2279-191">Right-click the external storage account that you want to detach, and then select **Detach**.</span></span>

    ![Loskoppelen van de opslagoptie][10]

2. <span data-ttu-id="c2279-193">Selecteer in het bevestigingsbericht **Ja** om het loskoppelen van het externe opslagaccount te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="c2279-193">In the confirmation message, select **Yes** to confirm the detachment from the external storage account.</span></span>

## <a name="attach-a-storage-account-by-using-an-sas"></a><span data-ttu-id="c2279-194">Een opslagaccount koppelen met behulp van een SAS</span><span class="sxs-lookup"><span data-stu-id="c2279-194">Attach a storage account by using an SAS</span></span>
<span data-ttu-id="c2279-195">Met een [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) kan de beheerder van een Azure-abonnement tijdelijke toegang verlenen tot een opslagaccount zonder Azure-abonnementreferenties op te geven.</span><span class="sxs-lookup"><span data-stu-id="c2279-195">An [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) lets the admin of an Azure subscription grant temporary access to a storage account without having to provide Azure subscription credentials.</span></span>

<span data-ttu-id="c2279-196">Een voorbeeld van dit scenario: stel gebruiker A is beheerder van een Azure-abonnement en gebruiker A wil gebruiker B een beperkte tijd toegang bieden tot een opslagaccount, met bepaalde machtigingen:</span><span class="sxs-lookup"><span data-stu-id="c2279-196">To illustrate this scenario, let's say that UserA is an admin of an Azure subscription, and UserA wants to allow UserB to access a storage account for a limited time with certain permissions:</span></span>

1. <span data-ttu-id="c2279-197">Gebruiker A genereert een SAS (bestaande uit de verbindingsreeks voor het opslagaccount) die een bepaalde tijd geldig is en de gewenste machtigingen heeft.</span><span class="sxs-lookup"><span data-stu-id="c2279-197">UserA generates an SAS (consisting of the connection string for the storage account) for a specific time period and with the desired permissions.</span></span>

2. <span data-ttu-id="c2279-198">Gebruiker A deelt de SAS met de persoon die toegang wil tot het opslagaccount (in ons geval gebruiker B).</span><span class="sxs-lookup"><span data-stu-id="c2279-198">UserA shares the SAS with the person (UserB, in our example) who wants access to the storage account.</span></span>  

3. <span data-ttu-id="c2279-199">Gebruiker B gebruikt Opslagverkenner (Preview) om verbinding te maken met het account van gebruiker A via de opgegeven SAS.</span><span class="sxs-lookup"><span data-stu-id="c2279-199">UserB uses Storage Explorer (Preview) to attach to the account that belongs to UserA by using the supplied SAS.</span></span>

### <a name="get-an-sas-for-the-account-you-want-to-share"></a><span data-ttu-id="c2279-200">Een SAS ophalen voor het account dat u wilt delen</span><span class="sxs-lookup"><span data-stu-id="c2279-200">Get an SAS for the account you want to share</span></span>
1. <span data-ttu-id="c2279-201">Klik in de Storage Explorer (Preview) met de rechtermuisknop op het opslagaccount dat u wilt delen en selecteer **Shared Access Signature ophalen**.</span><span class="sxs-lookup"><span data-stu-id="c2279-201">In Storage Explorer (Preview), right-click the storage account you want share, and then select **Get Shared Access Signature**.</span></span>

    ![Optie SAS-contextmenu ophalen][13]

2. <span data-ttu-id="c2279-203">Geef in het dialoogvenster **Shared Access Signature** het tijdsbestek op en de machtigingen die u wilt gebruiken voor het account en selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="c2279-203">In the **Shared Access Signature** dialog box, specify the time frame and permissions that you want for the account, and then select **Create**.</span></span>

    <span data-ttu-id="c2279-204">![Dialoogvenster SAS ophalen][14]</span><span class="sxs-lookup"><span data-stu-id="c2279-204">![Get SAS dialog box][14]</span></span>  
    <span data-ttu-id="c2279-205">Het dialoogvenster **Shared Access Signature** wordt geopend met de SAS weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c2279-205">The **Shared Access Signature** dialog box opens and displays the SAS.</span></span>

3. <span data-ttu-id="c2279-206">Selecteer **Kopiëren** naast de **verbindingsreeks** om de handtekening naar het klembord te kopiëren. Selecteer daarna **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="c2279-206">Next to the **Connection String**, select **Copy** to copy it to the clipboard, and then select **Close**.</span></span>

### <a name="attach-to-the-shared-account-by-using-the-sas"></a><span data-ttu-id="c2279-207">Koppelen aan het gedeelde account met behulp van de SAS</span><span class="sxs-lookup"><span data-stu-id="c2279-207">Attach to the shared account by using the SAS</span></span>
1. <span data-ttu-id="c2279-208">Selecteer in Storage Explorer (voorbeeld) **Verbinding maken met Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="c2279-208">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Verbinding maken met de optie Azure Storage][23]

2. <span data-ttu-id="c2279-210">Geef in het dialoogvenster **Verbinding maken met Azure Storage** de verbindingsreeks op en selecteer **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="c2279-210">In the **Connect to Azure Storage** dialog box, specify the connection string, and then select **Next**.</span></span>

    ![Verbinding maken met het dialoogvenster Azure Storage][24]

3. <span data-ttu-id="c2279-212">In het dialoogvenster **Samenvatting verbinding** controleert u de gegevens.</span><span class="sxs-lookup"><span data-stu-id="c2279-212">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="c2279-213">Als u wijzigingen wilt aanbrengen, selecteert u **Terug**, en voert u vervolgens de gewenste instellingen in.</span><span class="sxs-lookup"><span data-stu-id="c2279-213">To make changes, select **Back**, and then enter the settings you want.</span></span> 

4. <span data-ttu-id="c2279-214">Selecteer **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="c2279-214">Select **Connect**.</span></span>

5. <span data-ttu-id="c2279-215">Nadat het opslagaccount is gekoppeld, wordt het weergegeven met de **(SAS)** toegevoegd aan de door u opgegeven accountnaam.</span><span class="sxs-lookup"><span data-stu-id="c2279-215">After it is attached, the storage account is displayed with **(SAS)** appended to the account name that you supplied.</span></span>

    ![Resultaat van koppeling met een account via SAS][17]

## <a name="attach-a-service-by-using-an-sas"></a><span data-ttu-id="c2279-217">Een service koppelen met behulp van een SAS</span><span class="sxs-lookup"><span data-stu-id="c2279-217">Attach a service by using an SAS</span></span>
<span data-ttu-id="c2279-218">In het gedeelte Een opslagaccount koppelen via SAS wordt uitgelegd hoe de beheerder van een Azure-abonnement tijdelijke toegang kan verlenen tot een opslagaccount door een SAS te genereren en te delen voor het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c2279-218">The "Attach a storage account by using an SAS" section explains how an Azure subscription admin can grant temporary access to a storage account by generating and sharing an SAS for the storage account.</span></span> <span data-ttu-id="c2279-219">Op deze manier kunt u ook een SAS genereren voor een bepaalde service (blobcontainer, wachtrij of tabel) binnen een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c2279-219">Similarly, an SAS can be generated for a specific service (blob container, queue, or table) within a storage account.</span></span>  

### <a name="generate-an-sas-for-the-service-that-you-want-to-share"></a><span data-ttu-id="c2279-220">Een SAS genereren voor de service die u wilt delen</span><span class="sxs-lookup"><span data-stu-id="c2279-220">Generate an SAS for the service that you want to share</span></span>
<span data-ttu-id="c2279-221">In deze context is een service een blobcontainer, een wachtrij of een tabel.</span><span class="sxs-lookup"><span data-stu-id="c2279-221">In this context, a service can be a blob container, queue, or table.</span></span> <span data-ttu-id="c2279-222">Zie voor het genereren van de SAS voor een vermelde service:</span><span class="sxs-lookup"><span data-stu-id="c2279-222">To generate the SAS for a listed service, see:</span></span>

* [<span data-ttu-id="c2279-223">De SAS ophalen voor een blobcontainer</span><span class="sxs-lookup"><span data-stu-id="c2279-223">Get the SAS for a blob container</span></span>](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* <span data-ttu-id="c2279-224">De SAS ophalen voor het delen van bestanden: *binnenkort beschikbaar*</span><span class="sxs-lookup"><span data-stu-id="c2279-224">Get the SAS for a file share: *Coming soon*</span></span>
* <span data-ttu-id="c2279-225">De SAS ophalen voor een wachtrij: *binnenkort beschikbaar*</span><span class="sxs-lookup"><span data-stu-id="c2279-225">Get the SAS for a queue: *Coming soon*</span></span>
* <span data-ttu-id="c2279-226">De SAS ophalen voor een tabel: *binnenkort beschikbaar*</span><span class="sxs-lookup"><span data-stu-id="c2279-226">Get the SAS for a table: *Coming soon*</span></span>

### <a name="attach-to-the-shared-account-service-by-using-the-sas"></a><span data-ttu-id="c2279-227">Koppelen aan de gedeelde-accountservice met behulp van de SAS</span><span class="sxs-lookup"><span data-stu-id="c2279-227">Attach to the shared account service by using the SAS</span></span>
1. <span data-ttu-id="c2279-228">Selecteer in Storage Explorer (voorbeeld) **Verbinding maken met Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="c2279-228">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Verbinding maken met de optie Azure Storage][23]

2. <span data-ttu-id="c2279-230">Geef in het dialoogvenster **Verbinding maken met Azure Storage** de SAS-URI op en selecteer vervolgens **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="c2279-230">In the **Connect to Azure Storage** dialog box, specify the SAS URI, and then select **Next**.</span></span>

    ![Verbinding maken met het dialoogvenster Azure Storage][24]

3. <span data-ttu-id="c2279-232">In het dialoogvenster **Samenvatting verbinding** controleert u de gegevens.</span><span class="sxs-lookup"><span data-stu-id="c2279-232">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="c2279-233">Als u wijzigingen wilt aanbrengen, selecteert u **Terug**, en voert u vervolgens de gewenste instellingen in.</span><span class="sxs-lookup"><span data-stu-id="c2279-233">To make changes, select **Back**, and then enter the settings you want.</span></span> 

4. <span data-ttu-id="c2279-234">Selecteer **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="c2279-234">Select **Connect**.</span></span>

5. <span data-ttu-id="c2279-235">Na het koppelen wordt de nieuw gekoppelde service weergegeven onder het knooppunt **(Service-SAS)**.</span><span class="sxs-lookup"><span data-stu-id="c2279-235">After it is attached, the newly attached service is displayed under the **(Service SAS)** node.</span></span>

    ![Resultaat van het koppelen met een gedeelde-service met behulp van een SAS][20]

## <a name="search-for-storage-accounts"></a><span data-ttu-id="c2279-237">Zoeken naar opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="c2279-237">Search for storage accounts</span></span>
<span data-ttu-id="c2279-238">Als u een lange lijst met opslagaccounts hebt, kunt u via het zoekvak boven aan het linkerdeelvenster snel bepaalde opslagaccounts zoeken.</span><span class="sxs-lookup"><span data-stu-id="c2279-238">If you have a long list of storage accounts, a quick way to locate a particular storage account is to use the search box at the top of the left pane.</span></span>

<span data-ttu-id="c2279-239">Terwijl u in het zoekvak typt, worden in het linkerdeelvenster alleen de opslagaccounts weergegeven die overeenkomen met de zoekwaarde die u tot dan toe hebt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="c2279-239">As you type in the search box, the left pane displays the storage accounts that match the search value you've entered up to that point.</span></span> <span data-ttu-id="c2279-240">Op de volgende schermafbeelding wordt bijvoorbeeld een zoekopdracht weergegeven voor alle opslagaccounts waarvan de naam **tarcher** bevat:</span><span class="sxs-lookup"><span data-stu-id="c2279-240">For example, a search for all storage accounts whose name contains **tarcher** is shown in the following screenshot:</span></span>

![Zoeken naar Storage-account][11]

## <a name="next-steps"></a><span data-ttu-id="c2279-242">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c2279-242">Next steps</span></span>
* [<span data-ttu-id="c2279-243">Azure Blob Storage-resources beheren met Opslagverkenner (Preview)</span><span class="sxs-lookup"><span data-stu-id="c2279-243">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>](vs-azure-tools-storage-explorer-blobs.md)

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
