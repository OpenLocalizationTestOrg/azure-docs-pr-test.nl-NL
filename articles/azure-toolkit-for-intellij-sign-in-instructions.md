---
title: aaaSign in instructies voor hello Azure Toolkit voor IntelliJ | Microsoft Docs
description: Meer informatie over hoe toosign in tooMicrosoft Azure met behulp van Azure Toolkit Hallo voor IntelliJ.
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
ms.openlocfilehash: 2de781fc19267cce133b1e6456481497e165fce4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="146f0-103">Aanmelden instructies voor hello Azure Toolkit voor IntelliJ</span><span class="sxs-lookup"><span data-stu-id="146f0-103">Sign-in instructions for hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="146f0-104">Hello Azure Toolkit voor IntelliJ biedt twee methoden voor het aanmelden tooyour Azure-account:</span><span class="sxs-lookup"><span data-stu-id="146f0-104">hello Azure Toolkit for IntelliJ provides two methods for signing in tooyour Azure account:</span></span>

  * <span data-ttu-id="146f0-105">**Interactieve**: U Azure u uw referenties invoeren telkens wanneer u zich aanmeldt tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="146f0-105">**Interactive**: You enter your Azure credentials each time you sign in tooyour Azure account.</span></span>
  * <span data-ttu-id="146f0-106">**Automatische**: U maakt een referentiebestand die u kunt tooautomatically aanmelding in tooyour Azure-account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="146f0-106">**Automated**: You create a credentials file that you can use tooautomatically sign in tooyour Azure account.</span></span>

<span data-ttu-id="146f0-107">Hallo volgende secties wordt beschreven hoe toouse elke methode.</span><span class="sxs-lookup"><span data-stu-id="146f0-107">hello following sections describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a><span data-ttu-id="146f0-108">Tooyour Azure-account interactief aanmelden</span><span class="sxs-lookup"><span data-stu-id="146f0-108">Sign in tooyour Azure account interactively</span></span>

<span data-ttu-id="146f0-109">toosign in tooAzure door uw Azure-referenties handmatig worden ingevoerd Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="146f0-109">toosign in tooAzure by manually entering your Azure credentials, do hello following:</span></span>

1. <span data-ttu-id="146f0-110">Open uw project met IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="146f0-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="146f0-111">Klik op **extra**, wijst u te**Azure**, en klik vervolgens op **Azure aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="146f0-111">Click **Tools**, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Hallo IntelliJ Azure aanmelden opdracht][I01]

3. <span data-ttu-id="146f0-113">In Hallo **Azure aanmelden** Selecteer **interactief**, en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="146f0-113">In hello **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![Hello Azure aanmelden venster met interactief geselecteerd][I02]

4. <span data-ttu-id="146f0-115">In Hallo **Azure Log In** dialoogvenster wordt weergegeven, Voer uw Azure-referenties en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="146f0-115">In hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Hello Azure aanmelding dialoogvenster][I03]

5. <span data-ttu-id="146f0-117">In Hallo **Selecteer abonnementen** in het dialoogvenster, selecteer Hallo abonnementen wilt toouse en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="146f0-117">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![dialoogvenster Hallo-abonnementen selecteren][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="146f0-119">Nadat u zich aan interactief u afmelden bij uw Azure-account</span><span class="sxs-lookup"><span data-stu-id="146f0-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="146f0-120">Nadat u uw account met behulp van de vorige stappen Hallo hebt geconfigureerd, wordt u automatisch worden afgemeld bij uw Azure-account elke keer dat IntelliJ IDEA opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="146f0-120">After you have configured your account by using hello preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="146f0-121">Echter, als u wilt dat toosign buiten uw Azure-account *zonder* opnieuw te starten IntelliJ IDEA Hallo te volgen.</span><span class="sxs-lookup"><span data-stu-id="146f0-121">However, if you want toosign out of your Azure account *without* restarting IntelliJ IDEA, do hello following.</span></span>

1. <span data-ttu-id="146f0-122">In IntelliJ IDEA op Hallo **extra** menu te verwijzen**Azure**, en klik vervolgens op **Azure Afmelden**.</span><span class="sxs-lookup"><span data-stu-id="146f0-122">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![Hallo IntelliJ Azure afmelden opdracht][L01]

2. <span data-ttu-id="146f0-124">In Hallo **Azure Afmelden** bevestigingsvenster, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="146f0-124">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Hello Azure afmelden bevestigingsvenster][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a><span data-ttu-id="146f0-126">Tooyour Azure-account automatisch aanmelden</span><span class="sxs-lookup"><span data-stu-id="146f0-126">Sign in tooyour Azure account automatically</span></span>

<span data-ttu-id="146f0-127">Deze sectie helpt u bij het maken van een referentiebestand die uw service-principal gegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="146f0-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="146f0-128">Nadat u deze procedure hebt voltooid, opent u Eclipse gebruikt Hallo referenties bestand tooautomatically aanmelding dat in elke tooAzure toen u uw project.</span><span class="sxs-lookup"><span data-stu-id="146f0-128">After you have completed this process, Eclipse uses hello credentials file tooautomatically sign you in tooAzure each time you open your project.</span></span>

1. <span data-ttu-id="146f0-129">Open uw project met IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="146f0-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="146f0-130">Op Hallo **extra** menu te verwijzen**Azure**, en klik vervolgens op **Azure aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="146f0-130">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Hallo IntelliJ Azure aanmelden opdracht][A01]

3. <span data-ttu-id="146f0-132">In Hallo **Azure aanmelden** Selecteer **automatisch**, en klik vervolgens op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="146f0-132">In hello **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![Hello Azure aanmelden venster met automatisch geselecteerd][A02]

4. <span data-ttu-id="146f0-134">In Hallo **Azure aanmeldingsdialoogvenster** venster, Voer uw Azure-referenties in en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="146f0-134">In hello **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Hello Azure aanmelding dialoogvenster][A03]

5. <span data-ttu-id="146f0-136">In Hallo **bestanden voor verificatie maken** venster, selecteer Hallo abonnementen wilt toouse, de doelmap en klik vervolgens op **Start**.</span><span class="sxs-lookup"><span data-stu-id="146f0-136">In hello **Create Authentication Files** window, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![venster van Hallo-bestanden voor verificatie maken][A04]

6. <span data-ttu-id="146f0-138">In Hallo **Status van het Service-Principal maken** in het dialoogvenster nadat de bestanden zijn gemaakt, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="146f0-138">In hello **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![Hallo dialoogvenster van de Status van het Service-Principal maken][A05]

7. <span data-ttu-id="146f0-140">In Hallo **Azure aanmelden** venster, klikt u op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="146f0-140">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![Het aanmeldingsvenster van Azure][A06]

8. <span data-ttu-id="146f0-142">In Hallo **Selecteer abonnementen** in het dialoogvenster, selecteer Hallo abonnementen wilt toouse en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="146f0-142">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![dialoogvenster Hallo-abonnementen selecteren][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="146f0-144">Afmelden bij uw Azure-account nadat u automatisch hebt aangemeld</span><span class="sxs-lookup"><span data-stu-id="146f0-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="146f0-145">Nadat u uw account hebt geconfigureerd met behulp van de vorige stappen hello, hello Azure Toolkit u automatisch afgemeld in tooyour Azure-account elke keer dat IntelliJ IDEA opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="146f0-145">After you have configured your account by using hello preceding steps, hello Azure Toolkit automatically signs you in tooyour Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="146f0-146">Echter toosign af van uw Azure-account en hello Azure Toolkit te voorkomen dat u automatisch aanmeldt, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="146f0-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, do hello following:</span></span>

1. <span data-ttu-id="146f0-147">In IntelliJ IDEA op Hallo **extra** menu te verwijzen**Azure**, en klik vervolgens op **Azure Afmelden**.</span><span class="sxs-lookup"><span data-stu-id="146f0-147">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![Hallo IntelliJ Azure afmelden opdracht][L01]

2. <span data-ttu-id="146f0-149">In Hallo **Azure Afmelden** bevestigingsvenster, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="146f0-149">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Hello Azure afmelden bevestigingsvenster][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="146f0-151">Tooyour Azure-account automatisch aanmelden met behulp van een bestaand referentiebestand</span><span class="sxs-lookup"><span data-stu-id="146f0-151">Sign in tooyour Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="146f0-152">Als u bij uw Azure-account afmelden wanneer u de IntelliJ IDEA gebruikt, moet u een bestaande referenties bestand tooautomatically teken terug in toohello-account.</span><span class="sxs-lookup"><span data-stu-id="146f0-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file tooautomatically sign back in toohello account.</span></span> <span data-ttu-id="146f0-153">tooconfigure hello Azure Toolkit voor Eclipse toouse een bestaande referentiebestand Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="146f0-153">tooconfigure hello Azure Toolkit for Eclipse toouse an existing credentials file, do hello following:</span></span>

1. <span data-ttu-id="146f0-154">Open uw project met IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="146f0-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="146f0-155">Op Hallo **extra** menu te verwijzen**Azure**, en klik vervolgens op **Azure aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="146f0-155">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Hallo IntelliJ Azure aanmelden opdracht][A01]

3. <span data-ttu-id="146f0-157">In Hallo **Azure aanmelden** Selecteer **automatisch**, en klik vervolgens op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="146f0-157">In hello **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![Hello Azure aanmelden venster met automatisch geselecteerd][A02]

4. <span data-ttu-id="146f0-159">In Hallo **verificatiebestand Selecteer** in het dialoogvenster selecteert u een eerder gemaakte referentiebestand en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="146f0-159">In hello **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![in het dialoogvenster Hallo-bestand voor verificatie selecteren][A08]

5. <span data-ttu-id="146f0-161">In Hallo **Azure aanmelden** venster, klikt u op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="146f0-161">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![Hello Azure aanmelden venster met automatisch geselecteerd][A06]

6. <span data-ttu-id="146f0-163">In Hallo **Selecteer abonnementen** in het dialoogvenster, selecteer Hallo abonnementen wilt toouse en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="146f0-163">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![dialoogvenster Hallo-abonnementen selecteren][A07]

## <a name="next-steps"></a><span data-ttu-id="146f0-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="146f0-165">Next steps</span></span>
<span data-ttu-id="146f0-166">Zie voor meer informatie over hello Azure Toolkits voor IDE voor Java Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="146f0-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="146f0-167">[Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="146f0-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="146f0-168">[Wat is er nieuw in hello Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="146f0-168">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="146f0-169">[Hello Azure Toolkit voor Eclipse installeren]</span><span class="sxs-lookup"><span data-stu-id="146f0-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="146f0-170">[Aanmelden instructies voor het hello Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="146f0-170">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="146f0-171">[Een Hallo wereld-web-app maken voor Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="146f0-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="146f0-172">[Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="146f0-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="146f0-173">[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="146f0-173">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="146f0-174">[Hello Azure Toolkit voor IntelliJ installeren]</span><span class="sxs-lookup"><span data-stu-id="146f0-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="146f0-175">*Aanmelden instructies voor hello Azure Toolkit voor IntelliJ* (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="146f0-175">*Sign-in instructions for hello Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="146f0-176">[Een Hallo wereld-web-app maken voor Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="146f0-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="146f0-177">Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center] en Hallo [Java-Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="146f0-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld Web-App maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld-web-app maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Hello Azure Toolkit voor Eclipse installeren]: ./azure-toolkit-for-eclipse-installation.md
[Hello Azure Toolkit voor IntelliJ installeren]: ./azure-toolkit-for-intellij-installation.md
[Aanmelden instructies voor het hello Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Wat is er nieuw in hello Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/

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
