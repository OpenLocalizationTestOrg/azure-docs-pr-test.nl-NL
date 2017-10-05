---
title: Meld u aan de instructies voor de Azure Toolkit voor Eclipse | Microsoft Docs
description: Informatie over het aanmelden bij Microsoft Azure met behulp van de Azure-Toolkit voor Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 02dd9935086c4c40d9ed54cc9ff2412ca96889f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="631e3-103">Azure aanmelden instructies voor de Azure Toolkit voor Eclipse</span><span class="sxs-lookup"><span data-stu-id="631e3-103">Azure Sign In Instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="631e3-104">De Azure-werkset voor Eclipse biedt twee methoden voor het aanmelden bij uw Azure-account:</span><span class="sxs-lookup"><span data-stu-id="631e3-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="631e3-105">**Interactieve** : wanneer u van deze methode gebruikmaakt voert u uw Azure-referenties telkens wanneer u zich bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="631e3-105">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>
  * <span data-ttu-id="631e3-106">**Automatische** : wanneer u van deze methode gebruikmaakt maakt u een referentiebestand waarin uw belangrijkste servicegegevens, waarna u het referentiebestand automatisch aanmelden bij uw Azure-account kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="631e3-106">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use the credentials file to automatically sign into your Azure account.</span></span>

<span data-ttu-id="631e3-107">De stappen in de volgende secties wordt beschreven hoe elke methode gebruiken.</span><span class="sxs-lookup"><span data-stu-id="631e3-107">The steps in the following sections will describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="631e3-108">Interactief aanmelden bij uw Azure-account</span><span class="sxs-lookup"><span data-stu-id="631e3-108">Signing into your Azure account interactively</span></span>

<span data-ttu-id="631e3-109">De volgende stappen ziet u hoe melden bij Azure door uw Azure-referenties handmatig worden ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="631e3-109">The following steps will illustrate how to sign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="631e3-110">Open uw project met Eclipse.</span><span class="sxs-lookup"><span data-stu-id="631e3-110">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="631e3-111">Klik op **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="631e3-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Eclipse Menu voor Azure aanmelden][I01]

1. <span data-ttu-id="631e3-113">Wanneer de **Azure aanmelden** in het dialoogvenster wordt weergegeven, selecteert u **interactief**, en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="631e3-113">When the **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![Meld u aan het dialoogvenster][I02]

1. <span data-ttu-id="631e3-115">Wanneer de **Azure Log In** dialoogvenster wordt weergegeven, Voer uw Azure-referenties en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="631e3-115">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Het aanmeldingsvenster van Azure][I03]

1. <span data-ttu-id="631e3-117">Wanneer de **Selecteer abonnementen** dialoogvenster wordt weergegeven, selecteert u de abonnementen die u wilt gebruiken en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="631e3-117">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Dialoogvenster Selecteer abonnementen][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="631e3-119">Ondertekening buiten uw Azure-account wanneer u zich interactief aangemeld</span><span class="sxs-lookup"><span data-stu-id="631e3-119">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="631e3-120">Nadat u de stappen in de vorige sectie hebt geconfigureerd, wordt u automatisch afgemeld bij uw Azure-account elke keer dat Eclipse opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="631e3-120">After you have configured the steps in the previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="631e3-121">Als u afmelden bij uw Azure-account wilt zonder Eclipse opnieuw te starten, gebruikt u de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="631e3-121">However, if you want to sign out of your Azure account without restarting Eclipse, use the following steps.</span></span>

1. <span data-ttu-id="631e3-122">Klik in Eclipse **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **Afmelden**.</span><span class="sxs-lookup"><span data-stu-id="631e3-122">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Eclipse Menu voor Azure afmelden][L01]

1. <span data-ttu-id="631e3-124">Wanneer de **Azure Afmelden** dialoogvenster wordt weergegeven, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="631e3-124">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![In het dialoogvenster afmelden][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a><span data-ttu-id="631e3-126">Automatisch aanmelden bij uw Azure-account en maken van een referentiebestand moeten worden gebruikt in de toekomst</span><span class="sxs-lookup"><span data-stu-id="631e3-126">Signing into your Azure account automatically and creating a credentials file to use in the future</span></span>

<span data-ttu-id="631e3-127">De volgende stappen begeleidt u bij het maken van een referentiebestand die uw service-principal gegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="631e3-127">The following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="631e3-128">Nadat u deze stappen hebt voltooid, gebruiken Eclipse automatisch het referentiebestand automatisch aanmelden bij Azure telkens wanneer die u uw project opent.</span><span class="sxs-lookup"><span data-stu-id="631e3-128">Once you have completed these steps, Eclipse will automatically use the credentials file to automatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="631e3-129">Open uw project met Eclipse.</span><span class="sxs-lookup"><span data-stu-id="631e3-129">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="631e3-130">Klik op **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="631e3-130">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Eclipse Menu voor Azure aanmelden][A01]

1. <span data-ttu-id="631e3-132">Wanneer de **Azure aanmelden** in het dialoogvenster wordt weergegeven, selecteert u **automatisch**, en klik vervolgens op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="631e3-132">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![Meld u aan het dialoogvenster][A02]

1. <span data-ttu-id="631e3-134">Wanneer de **Azure Log In** dialoogvenster wordt weergegeven, Voer uw Azure-referenties en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="631e3-134">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Het aanmeldingsvenster van Azure][A03]

1. <span data-ttu-id="631e3-136">Wanneer de **verificatiebestanden maken** dialoogvenster wordt weergegeven, selecteert u de abonnementen die u wilt gebruiken, de doelmap en klik vervolgens op **Start**.</span><span class="sxs-lookup"><span data-stu-id="631e3-136">When the **Create authentication files** dialog box appears, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Het aanmeldingsvenster van Azure][A04]

1. <span data-ttu-id="631e3-138">De **Service-Principal Creatation Status** in het dialoogvenster wordt weergegeven, en nadat de bestanden zijn gemaakt, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="631e3-138">The **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Dialoogvenster Service-Principal Creatation Status][A05]

1. <span data-ttu-id="631e3-140">Wanneer de **Azure aanmelden** dialoogvenster wordt weergegeven, klikt u op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="631e3-140">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Het aanmeldingsvenster van Azure][A06]

1. <span data-ttu-id="631e3-142">Wanneer de **Selecteer abonnementen** dialoogvenster wordt weergegeven, selecteert u de abonnementen die u wilt gebruiken en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="631e3-142">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Dialoogvenster Selecteer abonnementen][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="631e3-144">Ondertekening buiten uw Azure-account wanneer u automatisch aangemeld</span><span class="sxs-lookup"><span data-stu-id="631e3-144">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="631e3-145">Nadat u de stappen in de vorige sectie hebt geconfigureerd, wordt de Azure-Toolkit automatisch aangemeld bij uw Azure-account elke keer dat Eclipse opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="631e3-145">After you have configured the steps in the previous section, the Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="631e3-146">Echter wilt afmelden bij uw Azure-account en voorkomen dat de Toolkit Azure automatisch aanmelden, gebruiken de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="631e3-146">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, use the following steps.</span></span>

1. <span data-ttu-id="631e3-147">Klik in Eclipse **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **Afmelden**.</span><span class="sxs-lookup"><span data-stu-id="631e3-147">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Eclipse Menu voor Azure afmelden][L01]

1. <span data-ttu-id="631e3-149">Wanneer de **Azure Afmelden** dialoogvenster wordt weergegeven, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="631e3-149">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![In het dialoogvenster afmelden][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="631e3-151">Aanmelden bij uw Azure-account automatisch met behulp van een referentiebestand die u al hebt gemaakt</span><span class="sxs-lookup"><span data-stu-id="631e3-151">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="631e3-152">Als u zich af bij Azure wanneer u Eclipse gebruikt, moet u opnieuw configureren van de Azure-werkset voor Eclipse een referentiebestand die u hebt gemaakt voordat u kunt automatisch aanmelden bij uw Azure-account te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="631e3-152">If you sign out of Azure when you are using Eclipse, you will need to reconfigure the Azure Toolkit for Eclipse to use a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="631e3-153">De volgende stappen begeleidt u stapsgewijs door de Azure-Toolkit voor het gebruik van een bestaand referentiebestand configureren.</span><span class="sxs-lookup"><span data-stu-id="631e3-153">The following steps will walk you through configuring the Azure Toolkit to use an existing credentials file.</span></span>

1. <span data-ttu-id="631e3-154">Open uw project met Eclipse.</span><span class="sxs-lookup"><span data-stu-id="631e3-154">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="631e3-155">Klik op **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="631e3-155">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Eclipse Menu voor Azure aanmelden][A01]

1. <span data-ttu-id="631e3-157">Wanneer de **Azure aanmelden** in het dialoogvenster wordt weergegeven, selecteert u **automatisch**, en klik vervolgens op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="631e3-157">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![Meld u aan het dialoogvenster][A02]

1. <span data-ttu-id="631e3-159">Wanneer de **geverifieerd bestand selecteren** dialoogvenster wordt weergegeven, selecteert u een referentiebestand die u eerder hebt gemaakt en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="631e3-159">When the **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Select**.</span></span>

   ![Meld u aan het dialoogvenster][A08]

1. <span data-ttu-id="631e3-161">Wanneer de **Azure aanmelden** dialoogvenster wordt weergegeven, klikt u op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="631e3-161">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Het aanmeldingsvenster van Azure][A06]

1. <span data-ttu-id="631e3-163">Wanneer de **Selecteer abonnementen** dialoogvenster wordt weergegeven, selecteert u de abonnementen die u wilt gebruiken en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="631e3-163">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Dialoogvenster Selecteer abonnementen][A07]

## <a name="see-also"></a><span data-ttu-id="631e3-165">Zie ook</span><span class="sxs-lookup"><span data-stu-id="631e3-165">See Also</span></span>
<span data-ttu-id="631e3-166">Voor meer informatie over de Azure Toolkits voor Java-IDE's klikt u op de volgende koppelingen:</span><span class="sxs-lookup"><span data-stu-id="631e3-166">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="631e3-167">[Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="631e3-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="631e3-168">[What's New in the Azure Toolkit for Eclipse] (Nieuw in de Azure Toolkit voor Eclipse)</span><span class="sxs-lookup"><span data-stu-id="631e3-168">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="631e3-169">[Installing the Azure Toolkit for Eclipse] (De Azure Toolkit voor Eclipse installeren)</span><span class="sxs-lookup"><span data-stu-id="631e3-169">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="631e3-170">*Meld u aan de instructies voor de Azure Toolkit voor Eclipse (in dit artikel)*</span><span class="sxs-lookup"><span data-stu-id="631e3-170">*Sign In Instructions for the Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="631e3-171">[Een Hallo wereld Web-App maken voor Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="631e3-171">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="631e3-172">[Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="631e3-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="631e3-173">[What's New in the Azure Toolkit for IntelliJ] (Nieuw in de Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="631e3-173">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="631e3-174">[Installing the Azure Toolkit for IntelliJ] (De Azure Toolkit voor IntelliJ installeren)</span><span class="sxs-lookup"><span data-stu-id="631e3-174">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="631e3-175">[Sign In Instructions for the Azure Toolkit for IntelliJ] (Aanmeldingsinstructies voor de Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="631e3-175">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="631e3-176">[Een Hallo wereld Web-App maken voor Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="631e3-176">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="631e3-177">Voor meer informatie over het gebruik van Azure met Java raadpleegt u het [Azure Java-ontwikkelaarscentrum] en de [Java Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="631e3-177">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="631e3-178">[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="631e3-178">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="631e3-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="631e3-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="631e3-180">[Een Hallo wereld Web-App maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="631e3-180">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="631e3-181">[Een Hallo wereld Web-App maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="631e3-181">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="631e3-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (De Azure Toolkit voor Eclipse installeren)</span><span class="sxs-lookup"><span data-stu-id="631e3-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="631e3-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)</span><span class="sxs-lookup"><span data-stu-id="631e3-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
<span data-ttu-id="631e3-184">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md (Aanmeldingsinstructies voor de Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="631e3-184">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="631e3-185">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md (Nieuw in de Azure Toolkit voor Eclipse)</span><span class="sxs-lookup"><span data-stu-id="631e3-185">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="631e3-186">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md (Nieuw in de Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="631e3-186">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="631e3-187">[Azure Java-ontwikkelaarscentrum]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="631e3-187">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="631e3-188">[Java Tools voor Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="631e3-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
