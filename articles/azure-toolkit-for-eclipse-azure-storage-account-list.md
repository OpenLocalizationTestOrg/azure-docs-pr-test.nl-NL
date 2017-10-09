---
title: lijst met Opslagaccounts aaaAzure
description: De instellingen van uw storage-account met hello Azure Toolkit voor Eclipse beheren
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="f5f50-103">Lijst met Azure Storage-Account</span><span class="sxs-lookup"><span data-stu-id="f5f50-103">Azure Storage Account List</span></span>
<span data-ttu-id="f5f50-104">Azure storage accounts inschakelen downloaden locaties toobe gebruikt voor uw JDK, toepassingsserver en willekeurige onderdelen, evenals voor het opslaan van status wanneer u opslaan in cache.</span><span class="sxs-lookup"><span data-stu-id="f5f50-104">Azure storage accounts enable download locations toobe used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="f5f50-105">Eclipse houdt een lijst met bekende storage-accounts die beschikbaar tooyour projecten in uw Eclipse-werkruimte zijn.</span><span class="sxs-lookup"><span data-stu-id="f5f50-105">Eclipse maintains a list of known storage accounts that are available tooyour projects in your Eclipse workspace.</span></span> <span data-ttu-id="f5f50-106">Hallo tooopen **Opslagaccounts** dialoogvenster dat wordt gebruikt toomanage die lijst in Eclipse, klikt u op **venster**, klikt u op **voorkeuren**, vouw **Azure** , en klik vervolgens op **Opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="f5f50-106">tooopen hello **Storage Accounts** dialog, which is used toomanage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="f5f50-107">Hallo hieronder vindt u Hallo **Opslagaccounts** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f5f50-107">hello following shows hello **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="f5f50-108">Dit dialoogvenster kan ook worden geopend vanuit een **Accounts** koppeling op de dialoogvensters die storage-accounts, zoals Hallo volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f5f50-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as hello following:</span></span>

* <span data-ttu-id="f5f50-109">Hallo **JDK** tabblad Hallo **serverconfiguratie** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f5f50-109">hello **JDK** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="f5f50-110">Hallo **Server** tabblad Hallo **serverconfiguratie** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f5f50-110">hello **Server** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="f5f50-111">Hallo **onderdeel toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f5f50-111">hello **Add Component** dialog.</span></span>
* <span data-ttu-id="f5f50-112">Hallo **opslaan in cache** dialoogvenster met eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="f5f50-112">hello **Caching** properties dialog.</span></span>

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="f5f50-113">tooimport uw opslag gebruikersaccounts via een bestand met publicatie-instellingen</span><span class="sxs-lookup"><span data-stu-id="f5f50-113">tooimport your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="f5f50-114">Binnen Hallo **Opslagaccounts** dialoogvenster, klikt u op **importeren uit bestand publiceren instellingen**.</span><span class="sxs-lookup"><span data-stu-id="f5f50-114">Within hello **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="f5f50-115">(Deze stap overslaan als u al een publiceren instellingen bestand tooyour lokale computer opgeslagen). In Hallo **importeren abonnementsgegevens** dialoogvenster, klikt u op **publiceren-SETTINGS-bestand downloaden**.</span><span class="sxs-lookup"><span data-stu-id="f5f50-115">(Skip this step if you have already saved a publish settings file tooyour local machine.) In hello **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="f5f50-116">Als u nog niet aangemeld bij uw Azure-account, kunt u zich na vragen aan gebruiker toolog in.</span><span class="sxs-lookup"><span data-stu-id="f5f50-116">If you are not yet logged into your Azure account, you will be prompted toolog in.</span></span> <span data-ttu-id="f5f50-117">Vervolgens wordt u gevraagd een Azure toosave bestand publicatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="f5f50-117">Then you'll be prompted toosave an Azure publish settings file.</span></span> <span data-ttu-id="f5f50-118">(U kunt resulterende Hallo-instructies weergegeven op pagina's aanmelden van Hallo - negeren ze worden geleverd door hello Azure-portal en zijn bedoeld voor gebruikers van de Visual Studio.) Sla het op de lokale computer tooyour.</span><span class="sxs-lookup"><span data-stu-id="f5f50-118">(You can ignore hello resulting instructions shown on hello logon pages - they are provided by hello Azure portal and are intended for Visual Studio users.) Save it tooyour local machine.</span></span>

3. <span data-ttu-id="f5f50-119">Nog steeds in Hallo **importeren abonnementsgegevens** dialoogvenster, klikt u op Hallo **Bladeren** knop, selecteer Hallo bestand publicatie-instellingen die u eerder hebt lokaal opgeslagen en klik vervolgens op **openen**.</span><span class="sxs-lookup"><span data-stu-id="f5f50-119">Still in hello **Import Subscription Information** dialog, click hello **Browse** button, select hello publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="f5f50-120">Klik op **OK** tooclose hello **importeren abonnementsgegevens** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f5f50-120">Click **OK** tooclose hello **Import Subscription Information** dialog.</span></span>

## <a name="toocreate-a-new-storage-account"></a><span data-ttu-id="f5f50-121">een nieuw opslagaccount toocreate</span><span class="sxs-lookup"><span data-stu-id="f5f50-121">toocreate a new storage account</span></span>
1. <span data-ttu-id="f5f50-122">Binnen Hallo **Opslagaccounts** dialoogvenster, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f5f50-122">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="f5f50-123">Binnen Hallo **Storage-Account toevoegen** dialoogvenster, klikt u op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="f5f50-123">Within hello **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="f5f50-124">Binnen Hallo **nieuw Opslagaccount** dialoogvenster waarden voor Hallo volgende opgeven:</span><span class="sxs-lookup"><span data-stu-id="f5f50-124">Within hello **New Storage Account** dialog, specify values for hello following:</span></span>

   * <span data-ttu-id="f5f50-125">De naam van opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="f5f50-125">Storage account name.</span></span>

   * <span data-ttu-id="f5f50-126">Locatie van Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="f5f50-126">Location of hello storage account.</span></span>

   * <span data-ttu-id="f5f50-127">Beschrijving van Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="f5f50-127">Description of hello storage account.</span></span>

   * <span data-ttu-id="f5f50-128">Hallo abonnement toowhich Hallo storage-account hoort.</span><span class="sxs-lookup"><span data-stu-id="f5f50-128">hello subscription toowhich hello storage account belongs.</span></span>

4. <span data-ttu-id="f5f50-129">Klik op **OK** tooclose hello **nieuw Opslagaccount** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f5f50-129">Click **OK** tooclose hello **New Storage Account** dialog.</span></span>

<span data-ttu-id="f5f50-130">Het kan enkele minuten duren voordat uw storage-account toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f5f50-130">It may take several minutes for your storage account toobe created.</span></span> <span data-ttu-id="f5f50-131">Nadat deze is gemaakt, klikt u op **OK** tooclose hello **Storage-Account toevoegen** dialoogvenster en uw nieuwe opslagaccount worden toohello lijst met beschikbare opslagaccounts toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f5f50-131">After it is created, click **OK** tooclose hello **Add Storage Account** dialog, and your new storage account will be added toohello list of available storage accounts.</span></span>

## <a name="tooadd-an-existing-storage-account-toohello-list"></a><span data-ttu-id="f5f50-132">een bestaande lijst van storage account toohello tooadd</span><span class="sxs-lookup"><span data-stu-id="f5f50-132">tooadd an existing storage account toohello list</span></span>
1. <span data-ttu-id="f5f50-133">Als u nog geen een Azure storage-account, maakt u een Hallo stappen te volgen weergegeven in Hallo **toocreate een nieuwe sectie van de storage-account** hierboven.</span><span class="sxs-lookup"><span data-stu-id="f5f50-133">If you do not already have a Azure storage account, create one by following hello steps listed in hello **toocreate a new storage account section** above.</span></span> <span data-ttu-id="f5f50-134">(U kunt ook een nieuw opslagaccount maken op Hallo [Azure Management Portal][Azure Management Portal].)</span><span class="sxs-lookup"><span data-stu-id="f5f50-134">(Alternatively, you can create a new storage account at hello [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="f5f50-135">Binnen Hallo **Opslagaccounts** dialoogvenster, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f5f50-135">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="f5f50-136">Binnen Hallo **Storage-Account toevoegen** dialoogvenster waarden opgeven voor **naam** en **toegangssleutel**.</span><span class="sxs-lookup"><span data-stu-id="f5f50-136">Within hello **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="f5f50-137">Hallo account naam en toegangssleutel moet zijn voor een bestaand Azure-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="f5f50-137">hello account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="f5f50-138">Gebruik Hallo **opslag** sectie Hallo [Azure Management Portal] [ Azure Management Portal] tooview uw storage-account namen en -sleutels.</span><span class="sxs-lookup"><span data-stu-id="f5f50-138">Use hello **Storage** section of hello [Azure Management Portal][Azure Management Portal] tooview your storage account names and keys.</span></span> <span data-ttu-id="f5f50-139">Uw **Storage-Account toevoegen** dialoogvenster ziet er vergelijkbare toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="f5f50-139">Your **Add Storage Account** dialog will look similar toohello following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="f5f50-140">Klik op **OK** tooclose hello **Storage-Account toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f5f50-140">Click **OK** tooclose hello **Add Storage Account** dialog.</span></span>

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a><span data-ttu-id="f5f50-141">een storage account toouse een nieuwe toegangssleutel toomodify</span><span class="sxs-lookup"><span data-stu-id="f5f50-141">toomodify a storage account toouse a new access key</span></span>
1. <span data-ttu-id="f5f50-142">Binnen Hallo **Opslagaccounts** dialoogvenster, klikt u op Hallo storage-account dat u wilt dat tooedit en klik vervolgens op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="f5f50-142">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Edit**.</span></span>

2. <span data-ttu-id="f5f50-143">Binnen Hallo **bewerken toegangssleutel voor Opslagaccount** dialoogvenster Hallo wijzigen **toegangssleutel** waarde.</span><span class="sxs-lookup"><span data-stu-id="f5f50-143">Within hello **Edit Storage Account Access Key** dialog, modify hello **Access Key** value.</span></span>

3. <span data-ttu-id="f5f50-144">Klik op **OK** tooclose hello **bewerken toegangssleutel voor Opslagaccount** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f5f50-144">Click **OK** tooclose hello **Edit Storage Account Access Key** dialog.</span></span>

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a><span data-ttu-id="f5f50-145">tooremove een opslagaccount in de lijst Hallo onderhouden in Eclipse</span><span class="sxs-lookup"><span data-stu-id="f5f50-145">tooremove a storage account from hello list maintained in Eclipse</span></span>
1. <span data-ttu-id="f5f50-146">Binnen Hallo **Opslagaccounts** dialoogvenster, klikt u op Hallo storage-account dat u wilt dat tooedit en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="f5f50-146">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Remove**.</span></span>

2. <span data-ttu-id="f5f50-147">Klik op **OK** wanneer na vragen aan gebruiker tooremove Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="f5f50-147">Click **OK** when prompted tooremove hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="f5f50-148">Verwijderen van opslagaccount Hallo via Hallo **Opslagaccounts** dialoogvenster alleen, wordt deze verwijderd uit de lijst Hallo met storage-accounts worden bekeken in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f5f50-148">Removing hello storage account through hello **Storage Accounts** dialog only removes it from hello list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="f5f50-149">Dit wordt niet Hallo storage-account van uw Azure-abonnement verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f5f50-149">It does not remove hello storage account from your Azure subscription.</span></span> <span data-ttu-id="f5f50-150">Bovendien Hallo storage-account kan worden weergegeven opnieuw in de lijst met nadat Eclipse opnieuw Hallo details van uw abonnement geladen.</span><span class="sxs-lookup"><span data-stu-id="f5f50-150">Additionally, hello storage account could appear again in your list after Eclipse reloads hello details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="f5f50-151">Zie ook</span><span class="sxs-lookup"><span data-stu-id="f5f50-151">See Also</span></span>
<span data-ttu-id="f5f50-152">[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f5f50-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="f5f50-153">[Hello Azure Toolkit voor Eclipse installeren][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f5f50-153">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="f5f50-154">[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f5f50-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="f5f50-155">Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="f5f50-155">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
