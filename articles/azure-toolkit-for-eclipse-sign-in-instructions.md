---
title: aaaSign In instructies voor hello Azure Toolkit voor Eclipse | Microsoft Docs
description: Meer informatie over hoe toosign in Microsoft Azure met behulp van Azure Toolkit voor Eclipse Hallo.
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
ms.openlocfilehash: 95be64750ca0147f76dae8f364fad80cb9ccc969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="70bcc-103">Azure-teken In de instructies voor het hello Azure Toolkit voor Eclipse</span><span class="sxs-lookup"><span data-stu-id="70bcc-103">Azure Sign In Instructions for hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="70bcc-104">Hello Azure Toolkit voor Eclipse biedt twee methoden voor het aanmelden bij uw Azure-account:</span><span class="sxs-lookup"><span data-stu-id="70bcc-104">hello Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="70bcc-105">**Interactieve** : wanneer u van deze methode gebruikmaakt voert u uw Azure-referenties telkens wanneer u zich bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="70bcc-105">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>
  * <span data-ttu-id="70bcc-106">**Automatische** : wanneer u van deze methode gebruikmaakt maakt u een referentiebestand waarin uw belangrijkste servicegegevens, waarna u Hallo referenties bestand tooautomatically aanmelding in uw Azure-account kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="70bcc-106">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use hello credentials file tooautomatically sign into your Azure account.</span></span>

<span data-ttu-id="70bcc-107">Hallo stappen in de volgende secties Hallo wordt beschreven hoe toouse elke methode.</span><span class="sxs-lookup"><span data-stu-id="70bcc-107">hello steps in hello following sections will describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="70bcc-108">Interactief aanmelden bij uw Azure-account</span><span class="sxs-lookup"><span data-stu-id="70bcc-108">Signing into your Azure account interactively</span></span>

<span data-ttu-id="70bcc-109">Hallo volgende stappen wordt laten zien hoe toosign in Azure door uw Azure-referenties handmatig worden ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="70bcc-109">hello following steps will illustrate how toosign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="70bcc-110">Open uw project met Eclipse.</span><span class="sxs-lookup"><span data-stu-id="70bcc-110">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="70bcc-111">Klik op **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Eclipse Menu voor Azure aanmelden][I01]

1. <span data-ttu-id="70bcc-113">Wanneer Hallo **Azure aanmelden** in het dialoogvenster wordt weergegeven, selecteert u **interactief**, en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-113">When hello **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![Meld u aan het dialoogvenster][I02]

1. <span data-ttu-id="70bcc-115">Wanneer Hallo **Azure Log In** dialoogvenster wordt weergegeven, Voer uw Azure-referenties en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-115">When hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Het aanmeldingsvenster van Azure][I03]

1. <span data-ttu-id="70bcc-117">Wanneer Hallo **Selecteer abonnementen** dialoogvenster wordt weergegeven, selecteer Hallo abonnementen wilt toouse en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-117">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Dialoogvenster Selecteer abonnementen][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="70bcc-119">Ondertekening buiten uw Azure-account wanneer u zich interactief aangemeld</span><span class="sxs-lookup"><span data-stu-id="70bcc-119">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="70bcc-120">Nadat u Hallo stappen hebt geconfigureerd in de vorige sectie hello, wordt u automatisch afgemeld bij uw Azure-account elke keer dat Eclipse opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="70bcc-120">After you have configured hello steps in hello previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="70bcc-121">Echter gebruiken als u toosign buiten uw Azure-account wilt zonder Eclipse opnieuw te starten, Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="70bcc-121">However, if you want toosign out of your Azure account without restarting Eclipse, use hello following steps.</span></span>

1. <span data-ttu-id="70bcc-122">Klik in Eclipse **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **Afmelden**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-122">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Eclipse Menu voor Azure afmelden][L01]

1. <span data-ttu-id="70bcc-124">Wanneer Hallo **Azure Afmelden** dialoogvenster wordt weergegeven, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-124">When hello **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![In het dialoogvenster afmelden][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a><span data-ttu-id="70bcc-126">Automatisch aanmelden bij uw Azure-account en het maken van de referenties op een bestand toouse in Hallo toekomstige</span><span class="sxs-lookup"><span data-stu-id="70bcc-126">Signing into your Azure account automatically and creating a credentials file toouse in hello future</span></span>

<span data-ttu-id="70bcc-127">Hallo begeleidt volgt u bij het maken van een referentiebestand die uw service-principal gegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="70bcc-127">hello following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="70bcc-128">Als u klaar bent met deze stappen, Eclipse wordt automatisch open gebruik Hallo referenties bestand tooautomatically aanmelding dat bij Azure elke toen u het project.</span><span class="sxs-lookup"><span data-stu-id="70bcc-128">Once you have completed these steps, Eclipse will automatically use hello credentials file tooautomatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="70bcc-129">Open uw project met Eclipse.</span><span class="sxs-lookup"><span data-stu-id="70bcc-129">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="70bcc-130">Klik op **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-130">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Eclipse Menu voor Azure aanmelden][A01]

1. <span data-ttu-id="70bcc-132">Wanneer Hallo **Azure aanmelden** in het dialoogvenster wordt weergegeven, selecteert u **automatisch**, en klik vervolgens op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-132">When hello **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![Meld u aan het dialoogvenster][A02]

1. <span data-ttu-id="70bcc-134">Wanneer Hallo **Azure Log In** dialoogvenster wordt weergegeven, Voer uw Azure-referenties en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-134">When hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Het aanmeldingsvenster van Azure][A03]

1. <span data-ttu-id="70bcc-136">Wanneer Hallo **verificatiebestanden maken** dialoogvenster wordt weergegeven, selecteer Hallo abonnementen wilt toouse, de doelmap en klik vervolgens op **Start**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-136">When hello **Create authentication files** dialog box appears, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![Het aanmeldingsvenster van Azure][A04]

1. <span data-ttu-id="70bcc-138">Hallo **Service-Principal Creatation Status** in het dialoogvenster wordt weergegeven, en nadat de bestanden zijn gemaakt, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-138">hello **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Dialoogvenster Service-Principal Creatation Status][A05]

1. <span data-ttu-id="70bcc-140">Wanneer Hallo **Azure aanmelden** dialoogvenster wordt weergegeven, klikt u op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-140">When hello **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Het aanmeldingsvenster van Azure][A06]

1. <span data-ttu-id="70bcc-142">Wanneer Hallo **Selecteer abonnementen** dialoogvenster wordt weergegeven, selecteer Hallo abonnementen wilt toouse en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-142">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Dialoogvenster Selecteer abonnementen][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="70bcc-144">Ondertekening buiten uw Azure-account wanneer u automatisch aangemeld</span><span class="sxs-lookup"><span data-stu-id="70bcc-144">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="70bcc-145">Nadat u Hallo stappen hebt geconfigureerd in de vorige sectie hello, wordt hello Azure Toolkit automatisch aangemeld bij uw Azure-account elke keer dat Eclipse opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="70bcc-145">After you have configured hello steps in hello previous section, hello Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="70bcc-146">Toosign wordt echter af van uw Azure-account en te voorkomen dat hello Azure Toolkit aanmelden automatisch gebruik Hallo van de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="70bcc-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, use hello following steps.</span></span>

1. <span data-ttu-id="70bcc-147">Klik in Eclipse **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **Afmelden**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-147">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Eclipse Menu voor Azure afmelden][L01]

1. <span data-ttu-id="70bcc-149">Wanneer Hallo **Azure Afmelden** dialoogvenster wordt weergegeven, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-149">When hello **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![In het dialoogvenster afmelden][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="70bcc-151">Aanmelden bij uw Azure-account automatisch met behulp van een referentiebestand die u al hebt gemaakt</span><span class="sxs-lookup"><span data-stu-id="70bcc-151">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="70bcc-152">Als u zich af bij Azure wanneer u Eclipse gebruikt, moet u tooreconfigure hello Azure Toolkit voor Eclipse toouse een referentiebestand die u hebt gemaakt voordat u kunt automatisch aanmelden bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="70bcc-152">If you sign out of Azure when you are using Eclipse, you will need tooreconfigure hello Azure Toolkit for Eclipse toouse a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="70bcc-153">Hallo begeleidt volgt u stapsgewijs door hello Azure Toolkit toouse configureren een bestaand referentiebestand.</span><span class="sxs-lookup"><span data-stu-id="70bcc-153">hello following steps will walk you through configuring hello Azure Toolkit toouse an existing credentials file.</span></span>

1. <span data-ttu-id="70bcc-154">Open uw project met Eclipse.</span><span class="sxs-lookup"><span data-stu-id="70bcc-154">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="70bcc-155">Klik op **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-155">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Eclipse Menu voor Azure aanmelden][A01]

1. <span data-ttu-id="70bcc-157">Wanneer Hallo **Azure aanmelden** in het dialoogvenster wordt weergegeven, selecteert u **automatisch**, en klik vervolgens op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-157">When hello **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![Meld u aan het dialoogvenster][A02]

1. <span data-ttu-id="70bcc-159">Wanneer Hallo **geverifieerd bestand selecteren** dialoogvenster wordt weergegeven, selecteert u een referentiebestand die u eerder hebt gemaakt en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-159">When hello **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Select**.</span></span>

   ![Meld u aan het dialoogvenster][A08]

1. <span data-ttu-id="70bcc-161">Wanneer Hallo **Azure aanmelden** dialoogvenster wordt weergegeven, klikt u op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-161">When hello **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Het aanmeldingsvenster van Azure][A06]

1. <span data-ttu-id="70bcc-163">Wanneer Hallo **Selecteer abonnementen** dialoogvenster wordt weergegeven, selecteer Hallo abonnementen wilt toouse en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="70bcc-163">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Dialoogvenster Selecteer abonnementen][A07]

## <a name="see-also"></a><span data-ttu-id="70bcc-165">Zie ook</span><span class="sxs-lookup"><span data-stu-id="70bcc-165">See Also</span></span>
<span data-ttu-id="70bcc-166">Zie voor meer informatie over hello Azure Toolkits voor IDE voor Java Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="70bcc-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="70bcc-167">[Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="70bcc-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="70bcc-168">[Wat is er nieuw in hello Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="70bcc-168">[What's New in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="70bcc-169">[Hello Azure Toolkit voor Eclipse installeren]</span><span class="sxs-lookup"><span data-stu-id="70bcc-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="70bcc-170">*Meld u In instructies voor het hello Azure Toolkit voor Eclipse (dit artikel)*</span><span class="sxs-lookup"><span data-stu-id="70bcc-170">*Sign In Instructions for hello Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="70bcc-171">[Een Hallo wereld Web-App maken voor Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="70bcc-171">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="70bcc-172">[Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="70bcc-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="70bcc-173">[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="70bcc-173">[What's New in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="70bcc-174">[Hello Azure Toolkit voor IntelliJ installeren]</span><span class="sxs-lookup"><span data-stu-id="70bcc-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="70bcc-175">[Meld u In instructies voor het hello Azure Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="70bcc-175">[Sign In Instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="70bcc-176">[Een Hallo wereld Web-App maken voor Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="70bcc-176">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="70bcc-177">Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center] en Hallo [Java-Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="70bcc-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld Web-App maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld Web-App maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Hello Azure Toolkit voor Eclipse installeren]: ./azure-toolkit-for-eclipse-installation.md
[Hello Azure Toolkit voor IntelliJ installeren]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Meld u In instructies voor het hello Azure Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Wat is er nieuw in hello Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/

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
