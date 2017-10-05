---
title: Lijst met Azure Storage-Account
description: De instellingen van uw storage-account met de Azure-Toolkit voor Eclipse beheren
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
ms.openlocfilehash: f859efa389d3fe0b4b7b16255d57f1aa13123319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="74584-103">Lijst met Azure Storage-Account</span><span class="sxs-lookup"><span data-stu-id="74584-103">Azure Storage Account List</span></span>
<span data-ttu-id="74584-104">Azure storage-accounts inschakelen downloadlocaties moet worden gebruikt voor uw JDK, toepassingsserver en willekeurige onderdelen, evenals voor het opslaan van status wanneer u opslaan in cache.</span><span class="sxs-lookup"><span data-stu-id="74584-104">Azure storage accounts enable download locations to be used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="74584-105">Eclipse houdt een lijst van bekende opslagaccounts die beschikbaar voor uw projecten in uw Eclipse-werkruimte zijn.</span><span class="sxs-lookup"><span data-stu-id="74584-105">Eclipse maintains a list of known storage accounts that are available to your projects in your Eclipse workspace.</span></span> <span data-ttu-id="74584-106">Openen van de **Opslagaccounts** dialoogvenster dat wordt gebruikt voor het beheren van deze lijst, in Eclipse, klikt u op **venster**, klikt u op **voorkeuren**, vouw **Azure**, en klik vervolgens op **Storage-Accounts**.</span><span class="sxs-lookup"><span data-stu-id="74584-106">To open the **Storage Accounts** dialog, which is used to manage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="74584-107">Het volgende bevat de **Opslagaccounts** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="74584-107">The following shows the **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="74584-108">Dit dialoogvenster kan ook worden geopend vanuit een **Accounts** op dialoogvensters met storage-accounts, zoals de volgende koppeling:</span><span class="sxs-lookup"><span data-stu-id="74584-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as the following:</span></span>

* <span data-ttu-id="74584-109">De **JDK** tabblad van de **serverconfiguratie** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="74584-109">The **JDK** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="74584-110">De **Server** tabblad van de **serverconfiguratie** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="74584-110">The **Server** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="74584-111">De **onderdeel toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="74584-111">The **Add Component** dialog.</span></span>
* <span data-ttu-id="74584-112">De **opslaan in cache** dialoogvenster met eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="74584-112">The **Caching** properties dialog.</span></span>

## <a name="to-import-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="74584-113">Uw storage-accounts met behulp van een bestand met publicatie-instellingen importeren</span><span class="sxs-lookup"><span data-stu-id="74584-113">To import your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="74584-114">Binnen de **Opslagaccounts** dialoogvenster, klikt u op **importeren uit bestand publiceren instellingen**.</span><span class="sxs-lookup"><span data-stu-id="74584-114">Within the **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="74584-115">(Deze stap overslaan als u al een bestand met publicatie-instellingen hebt opgeslagen op uw lokale computer). In de **importeren abonnementsgegevens** dialoogvenster, klikt u op **publiceren-SETTINGS-bestand downloaden**.</span><span class="sxs-lookup"><span data-stu-id="74584-115">(Skip this step if you have already saved a publish settings file to your local machine.) In the **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="74584-116">Als u nog niet aangemeld bij uw Azure-account, wordt u gevraagd om aan te melden.</span><span class="sxs-lookup"><span data-stu-id="74584-116">If you are not yet logged into your Azure account, you will be prompted to log in.</span></span> <span data-ttu-id="74584-117">U wordt vervolgens gevraagd te Sla een Azure bestand publicatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="74584-117">Then you'll be prompted to save an Azure publish settings file.</span></span> <span data-ttu-id="74584-118">(Kunt u de resulterende instructies op de pagina's voor aanmelding - negeren ze worden geleverd door de Azure-portal en zijn bedoeld voor gebruikers van de Visual Studio.) Sla deze op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="74584-118">(You can ignore the resulting instructions shown on the logon pages - they are provided by the Azure portal and are intended for Visual Studio users.) Save it to your local machine.</span></span>

3. <span data-ttu-id="74584-119">Nog steeds in de **importeren abonnementsgegevens** dialoogvenster, klikt u op de **Bladeren** , selecteer het instellingenbestand publiceren die u eerder hebt lokaal opgeslagen en klik vervolgens op **Open**.</span><span class="sxs-lookup"><span data-stu-id="74584-119">Still in the **Import Subscription Information** dialog, click the **Browse** button, select the publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="74584-120">Klik op **OK** sluiten de **importeren abonnementsgegevens** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="74584-120">Click **OK** to close the **Import Subscription Information** dialog.</span></span>

## <a name="to-create-a-new-storage-account"></a><span data-ttu-id="74584-121">Een nieuw opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="74584-121">To create a new storage account</span></span>
1. <span data-ttu-id="74584-122">Binnen de **Opslagaccounts** dialoogvenster, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="74584-122">Within the **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="74584-123">Binnen de **Storage-Account toevoegen** dialoogvenster, klikt u op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="74584-123">Within the **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="74584-124">Binnen de **nieuw Opslagaccount** dialoogvenster waarden opgeven voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="74584-124">Within the **New Storage Account** dialog, specify values for the following:</span></span>

   * <span data-ttu-id="74584-125">De naam van opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="74584-125">Storage account name.</span></span>

   * <span data-ttu-id="74584-126">Locatie van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="74584-126">Location of the storage account.</span></span>

   * <span data-ttu-id="74584-127">Beschrijving van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="74584-127">Description of the storage account.</span></span>

   * <span data-ttu-id="74584-128">Het abonnement waaraan het opslagaccount hoort.</span><span class="sxs-lookup"><span data-stu-id="74584-128">The subscription to which the storage account belongs.</span></span>

4. <span data-ttu-id="74584-129">Klik op **OK** sluiten de **nieuw Opslagaccount** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="74584-129">Click **OK** to close the **New Storage Account** dialog.</span></span>

<span data-ttu-id="74584-130">Het kan enkele minuten duren voordat uw storage-account moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="74584-130">It may take several minutes for your storage account to be created.</span></span> <span data-ttu-id="74584-131">Nadat deze is gemaakt, klikt u op **OK** sluiten de **Storage-Account toevoegen** dialoogvenster en uw nieuwe opslagaccount wordt toegevoegd aan de lijst met beschikbare storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="74584-131">After it is created, click **OK** to close the **Add Storage Account** dialog, and your new storage account will be added to the list of available storage accounts.</span></span>

## <a name="to-add-an-existing-storage-account-to-the-list"></a><span data-ttu-id="74584-132">Een bestaand opslagaccount toevoegen aan de lijst</span><span class="sxs-lookup"><span data-stu-id="74584-132">To add an existing storage account to the list</span></span>
1. <span data-ttu-id="74584-133">Als u nog geen Azure storage-account, maken door de stappen die worden vermeld in de **voor het maken van een nieuwe sectie van de storage-account** hierboven.</span><span class="sxs-lookup"><span data-stu-id="74584-133">If you do not already have a Azure storage account, create one by following the steps listed in the **To create a new storage account section** above.</span></span> <span data-ttu-id="74584-134">(U kunt ook kunt u een nieuw opslagaccount op de [Azure Management Portal][Azure Management Portal].)</span><span class="sxs-lookup"><span data-stu-id="74584-134">(Alternatively, you can create a new storage account at the [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="74584-135">Binnen de **Opslagaccounts** dialoogvenster, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="74584-135">Within the **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="74584-136">Binnen de **Storage-Account toevoegen** dialoogvenster waarden opgeven voor **naam** en **toegangssleutel**.</span><span class="sxs-lookup"><span data-stu-id="74584-136">Within the **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="74584-137">De naam en toegangssleutel van het account moet voor een bestaand Azure-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="74584-137">The account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="74584-138">Gebruik de **opslag** sectie van de [Azure Management Portal] [ Azure Management Portal] om de namen van opslagaccounts en de sleutels weer te geven.</span><span class="sxs-lookup"><span data-stu-id="74584-138">Use the **Storage** section of the [Azure Management Portal][Azure Management Portal] to view your storage account names and keys.</span></span> <span data-ttu-id="74584-139">Uw **Storage-Account toevoegen** dialoogvenster ziet er ongeveer als volgt.</span><span class="sxs-lookup"><span data-stu-id="74584-139">Your **Add Storage Account** dialog will look similar to the following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="74584-140">Klik op **OK** sluiten de **Storage-Account toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="74584-140">Click **OK** to close the **Add Storage Account** dialog.</span></span>

## <a name="to-modify-a-storage-account-to-use-a-new-access-key"></a><span data-ttu-id="74584-141">Een opslagaccount voor het gebruik van een nieuwe toegangssleutel wijzigen</span><span class="sxs-lookup"><span data-stu-id="74584-141">To modify a storage account to use a new access key</span></span>
1. <span data-ttu-id="74584-142">Binnen de **Opslagaccounts** dialoogvenster, klikt u op de opslag account dat u wilt bewerken en klik vervolgens op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="74584-142">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Edit**.</span></span>

2. <span data-ttu-id="74584-143">Binnen de **bewerken toegangssleutel voor Opslagaccount** dialoogvenster wijzigen de **toegangssleutel** waarde.</span><span class="sxs-lookup"><span data-stu-id="74584-143">Within the **Edit Storage Account Access Key** dialog, modify the **Access Key** value.</span></span>

3. <span data-ttu-id="74584-144">Klik op **OK** sluiten de **bewerken toegangssleutel voor Opslagaccount** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="74584-144">Click **OK** to close the **Edit Storage Account Access Key** dialog.</span></span>

## <a name="to-remove-a-storage-account-from-the-list-maintained-in-eclipse"></a><span data-ttu-id="74584-145">Een opslagaccount verwijderen uit de lijst die wordt bijgehouden in Eclipse</span><span class="sxs-lookup"><span data-stu-id="74584-145">To remove a storage account from the list maintained in Eclipse</span></span>
1. <span data-ttu-id="74584-146">Binnen de **Opslagaccounts** dialoogvenster, klikt u op de opslag account dat u wilt bewerken en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="74584-146">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Remove**.</span></span>

2. <span data-ttu-id="74584-147">Klik op **OK** wanneer u wordt gevraagd de storage-account te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="74584-147">Click **OK** when prompted to remove the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="74584-148">Verwijderen van het opslagaccount via de **Opslagaccounts** dialoogvenster is alleen verwijderd uit de lijst met opslagaccounts worden bekeken in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="74584-148">Removing the storage account through the **Storage Accounts** dialog only removes it from the list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="74584-149">Deze verwijdert niet de storage-account van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="74584-149">It does not remove the storage account from your Azure subscription.</span></span> <span data-ttu-id="74584-150">Daarnaast het storage-account kan worden weergegeven opnieuw in de lijst met nadat Eclipse opnieuw de details van uw abonnement laadt.</span><span class="sxs-lookup"><span data-stu-id="74584-150">Additionally, the storage account could appear again in your list after Eclipse reloads the details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="74584-151">Zie ook</span><span class="sxs-lookup"><span data-stu-id="74584-151">See Also</span></span>
<span data-ttu-id="74584-152">[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="74584-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="74584-153">[De installatie van de Azure Toolkit voor Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="74584-153">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="74584-154">[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="74584-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="74584-155">Zie voor meer informatie over het gebruik van Azure met Java de [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="74584-155">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
