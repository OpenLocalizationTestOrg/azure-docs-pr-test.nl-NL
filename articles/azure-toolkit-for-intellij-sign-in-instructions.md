---
title: Aanmelden instructies voor de Azure-Toolkit voor IntelliJ | Microsoft Docs
description: Informatie over het aanmelden bij Microsoft Azure met behulp van de Azure-Toolkit voor IntelliJ.
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
ms.openlocfilehash: 4e2ed072bdaea0a71fef042c0c72b7656a42bbe8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a><span data-ttu-id="e19a4-103">Aanmelden instructies voor de Azure-Toolkit voor IntelliJ</span><span class="sxs-lookup"><span data-stu-id="e19a4-103">Sign-in instructions for the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="e19a4-104">De Azure-werkset voor IntelliJ biedt twee methoden voor het aanmelden bij uw Azure-account:</span><span class="sxs-lookup"><span data-stu-id="e19a4-104">The Azure Toolkit for IntelliJ provides two methods for signing in to your Azure account:</span></span>

  * <span data-ttu-id="e19a4-105">**Interactieve**: U uw Azure-referenties invoeren telkens wanneer u zich aanmeldt bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="e19a4-105">**Interactive**: You enter your Azure credentials each time you sign in to your Azure account.</span></span>
  * <span data-ttu-id="e19a4-106">**Automatische**: maken van een referentiebestand die u gebruiken kunt voor het automatisch aanmelden bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="e19a4-106">**Automated**: You create a credentials file that you can use to automatically sign in to your Azure account.</span></span>

<span data-ttu-id="e19a4-107">De volgende secties wordt beschreven hoe elke methode.</span><span class="sxs-lookup"><span data-stu-id="e19a4-107">The following sections describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-interactively"></a><span data-ttu-id="e19a4-108">Interactief aanmelden bij uw Azure-account</span><span class="sxs-lookup"><span data-stu-id="e19a4-108">Sign in to your Azure account interactively</span></span>

<span data-ttu-id="e19a4-109">Als u wilt aanmelden bij Azure met uw Azure-referenties handmatig worden ingevoerd, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="e19a4-109">To sign in to Azure by manually entering your Azure credentials, do the following:</span></span>

1. <span data-ttu-id="e19a4-110">Open uw project met IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="e19a4-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="e19a4-111">Klik op **extra**, wijs **Azure**, en klik vervolgens op **Azure aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-111">Click **Tools**, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![De opdracht IntelliJ Azure aanmelden][I01]

3. <span data-ttu-id="e19a4-113">In de **Azure aanmelden** Selecteer **interactief**, en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-113">In the **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![Het venster Azure aanmelden met interactief geselecteerd][I02]

4. <span data-ttu-id="e19a4-115">In de **Azure Log In** dialoogvenster wordt weergegeven, Voer uw Azure-referenties en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-115">In the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Het dialoogvenster Azure-aanmelding][I03]

5. <span data-ttu-id="e19a4-117">In de **Selecteer abonnementen** in het dialoogvenster, selecteer de abonnementen die u wilt gebruiken en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-117">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Het dialoogvenster abonnementen selecteren][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="e19a4-119">Nadat u zich aan interactief u afmelden bij uw Azure-account</span><span class="sxs-lookup"><span data-stu-id="e19a4-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="e19a4-120">Nadat u uw account met behulp van de voorgaande stappen hebt geconfigureerd, wordt u automatisch worden afgemeld bij uw Azure-account elke keer dat IntelliJ IDEA opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="e19a4-120">After you have configured your account by using the preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="e19a4-121">Echter, als u zich wilt afmelden bij uw Azure-account *zonder* IntelliJ IDEA opnieuw starten de volgende handelingen uit.</span><span class="sxs-lookup"><span data-stu-id="e19a4-121">However, if you want to sign out of your Azure account *without* restarting IntelliJ IDEA, do the following.</span></span>

1. <span data-ttu-id="e19a4-122">In IntelliJ IDEA op de **extra** in het menu **Azure**, en klik vervolgens op **Azure Afmelden**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-122">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![De opdracht IntelliJ Azure afmelden][L01]

2. <span data-ttu-id="e19a4-124">In de **Azure Afmelden** bevestigingsvenster, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-124">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Het bevestigingsvenster Azure afmelden][L02]

## <a name="sign-in-to-your-azure-account-automatically"></a><span data-ttu-id="e19a4-126">Automatisch aanmelden bij uw Azure-account</span><span class="sxs-lookup"><span data-stu-id="e19a4-126">Sign in to your Azure account automatically</span></span>

<span data-ttu-id="e19a4-127">Deze sectie helpt u bij het maken van een referentiebestand die uw service-principal gegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="e19a4-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="e19a4-128">Nadat u deze procedure hebt voltooid, wordt in Eclipse het referentiebestand gebruikt om automatisch aanmelden bij Azure telkens wanneer die u uw project opent.</span><span class="sxs-lookup"><span data-stu-id="e19a4-128">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure each time you open your project.</span></span>

1. <span data-ttu-id="e19a4-129">Open uw project met IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="e19a4-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="e19a4-130">Op de **extra** in het menu **Azure**, en klik vervolgens op **Azure aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-130">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![De opdracht IntelliJ Azure aanmelden][A01]

3. <span data-ttu-id="e19a4-132">In de **Azure aanmelden** Selecteer **automatisch**, en klik vervolgens op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-132">In the **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![Het venster Azure aanmelden met automatisch geselecteerd][A02]

4. <span data-ttu-id="e19a4-134">In de **Azure aanmeldingsdialoogvenster** venster, Voer uw Azure-referenties in en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-134">In the **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Het dialoogvenster Azure-aanmelding][A03]

5. <span data-ttu-id="e19a4-136">In de **bestanden voor verificatie maken** venster, selecteer de abonnementen die u wilt gebruiken, de doelmap en klik vervolgens op **Start**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-136">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Het venster bestanden voor verificatie maken][A04]

6. <span data-ttu-id="e19a4-138">In de **Status van het Service-Principal maken** in het dialoogvenster nadat de bestanden zijn gemaakt, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-138">In the **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![Het dialoogvenster van de Status van het Service-Principal maken][A05]

7. <span data-ttu-id="e19a4-140">In de **Azure aanmelden** venster, klikt u op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-140">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Het aanmeldingsvenster van Azure][A06]

8. <span data-ttu-id="e19a4-142">In de **Selecteer abonnementen** in het dialoogvenster, selecteer de abonnementen die u wilt gebruiken en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-142">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Het dialoogvenster abonnementen selecteren][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="e19a4-144">Afmelden bij uw Azure-account nadat u automatisch hebt aangemeld</span><span class="sxs-lookup"><span data-stu-id="e19a4-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="e19a4-145">Nadat u uw account met behulp van de voorgaande stappen hebt geconfigureerd, de Azure-Toolkit automatisch aangemeld bij uw Azure-account elke keer dat IntelliJ IDEA opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="e19a4-145">After you have configured your account by using the preceding steps, the Azure Toolkit automatically signs you in to your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="e19a4-146">Echter, als u wilt afmelden bij uw Azure-account en voorkomen dat de Toolkit Azure automatisch aanmelden, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="e19a4-146">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, do the following:</span></span>

1. <span data-ttu-id="e19a4-147">In IntelliJ IDEA op de **extra** in het menu **Azure**, en klik vervolgens op **Azure Afmelden**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-147">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![De opdracht IntelliJ Azure afmelden][L01]

2. <span data-ttu-id="e19a4-149">In de **Azure Afmelden** bevestigingsvenster, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-149">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Het bevestigingsvenster Azure afmelden][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="e19a4-151">Aanmelden bij uw Azure-account automatisch met behulp van een bestaand referentiebestand</span><span class="sxs-lookup"><span data-stu-id="e19a4-151">Sign in to your Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="e19a4-152">Als u bij uw Azure-account afmelden wanneer u de IntelliJ IDEA gebruikt, moet u een bestaand referentiebestand automatisch aanmelden bij het account.</span><span class="sxs-lookup"><span data-stu-id="e19a4-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file to automatically sign back in to the account.</span></span> <span data-ttu-id="e19a4-153">De Azure-werkset voor Eclipse een bestaand referentiebestand gebruiken, kunt u het volgende configureren:</span><span class="sxs-lookup"><span data-stu-id="e19a4-153">To configure the Azure Toolkit for Eclipse to use an existing credentials file, do the following:</span></span>

1. <span data-ttu-id="e19a4-154">Open uw project met IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="e19a4-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="e19a4-155">Op de **extra** in het menu **Azure**, en klik vervolgens op **Azure aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-155">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![De opdracht IntelliJ Azure aanmelden][A01]

3. <span data-ttu-id="e19a4-157">In de **Azure aanmelden** Selecteer **automatisch**, en klik vervolgens op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-157">In the **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![Het venster Azure aanmelden met automatisch geselecteerd][A02]

4. <span data-ttu-id="e19a4-159">In de **verificatiebestand Selecteer** in het dialoogvenster selecteert u een eerder gemaakte referentiebestand en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-159">In the **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![Het dialoogvenster verificatiebestand selecteren][A08]

5. <span data-ttu-id="e19a4-161">In de **Azure aanmelden** venster, klikt u op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-161">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Het venster Azure aanmelden met automatisch geselecteerd][A06]

6. <span data-ttu-id="e19a4-163">In de **Selecteer abonnementen** in het dialoogvenster, selecteer de abonnementen die u wilt gebruiken en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e19a4-163">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Het dialoogvenster abonnementen selecteren][A07]

## <a name="next-steps"></a><span data-ttu-id="e19a4-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e19a4-165">Next steps</span></span>
<span data-ttu-id="e19a4-166">Voor meer informatie over de Azure Toolkits voor Java-IDE's klikt u op de volgende koppelingen:</span><span class="sxs-lookup"><span data-stu-id="e19a4-166">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="e19a4-167">[Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e19a4-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e19a4-168">[Wat is er nieuw in de Azure-werkset voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e19a4-168">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e19a4-169">[Installing the Azure Toolkit for Eclipse] (De Azure Toolkit voor Eclipse installeren)</span><span class="sxs-lookup"><span data-stu-id="e19a4-169">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e19a4-170">[Aanmelden instructies voor de Azure-werkset voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e19a4-170">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e19a4-171">[Een Hallo wereld-web-app maken voor Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e19a4-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="e19a4-172">[Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="e19a4-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e19a4-173">[Wat is er nieuw in de Azure-werkset voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="e19a4-173">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e19a4-174">[Installing the Azure Toolkit for IntelliJ] (De Azure Toolkit voor IntelliJ installeren)</span><span class="sxs-lookup"><span data-stu-id="e19a4-174">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e19a4-175">*Aanmelden instructies voor de Azure-Toolkit voor IntelliJ* (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="e19a4-175">*Sign-in instructions for the Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="e19a4-176">[Een Hallo wereld-web-app maken voor Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="e19a4-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="e19a4-177">Voor meer informatie over het gebruik van Azure met Java raadpleegt u het [Azure Java-ontwikkelaarscentrum] en de [Java Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="e19a4-177">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="e19a4-178">[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="e19a4-178">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="e19a4-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="e19a4-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="e19a4-180">[Een Hallo wereld Web-App maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="e19a4-180">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="e19a4-181">[Een Hallo wereld-web-app maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="e19a4-181">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="e19a4-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (De Azure Toolkit voor Eclipse installeren)</span><span class="sxs-lookup"><span data-stu-id="e19a4-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="e19a4-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)</span><span class="sxs-lookup"><span data-stu-id="e19a4-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="e19a4-184">[Aanmelden instructies voor de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="e19a4-184">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
<span data-ttu-id="e19a4-185">[Wat is er nieuw in de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="e19a4-185">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="e19a4-186">[Wat is er nieuw in de Azure-werkset voor IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="e19a4-186">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="e19a4-187">[Azure Java-ontwikkelaarscentrum]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="e19a4-187">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="e19a4-188">[Java Tools voor Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="e19a4-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
