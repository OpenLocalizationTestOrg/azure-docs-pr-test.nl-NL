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
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a>Aanmelden instructies voor hello Azure Toolkit voor IntelliJ

Hello Azure Toolkit voor IntelliJ biedt twee methoden voor het aanmelden tooyour Azure-account:

  * **Interactieve**: U Azure u uw referenties invoeren telkens wanneer u zich aanmeldt tooyour Azure-account.
  * **Automatische**: U maakt een referentiebestand die u kunt tooautomatically aanmelding in tooyour Azure-account gebruiken.

Hallo volgende secties wordt beschreven hoe toouse elke methode.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a>Tooyour Azure-account interactief aanmelden

toosign in tooAzure door uw Azure-referenties handmatig worden ingevoerd Hallo te volgen:

1. Open uw project met IntelliJ IDEA.

2. Klik op **extra**, wijst u te**Azure**, en klik vervolgens op **Azure aanmelden**.

   ![Hallo IntelliJ Azure aanmelden opdracht][I01]

3. In Hallo **Azure aanmelden** Selecteer **interactief**, en klik vervolgens op **aanmelden**.

   ![Hello Azure aanmelden venster met interactief geselecteerd][I02]

4. In Hallo **Azure Log In** dialoogvenster wordt weergegeven, Voer uw Azure-referenties en klik vervolgens op **aanmelden**.

   ![Hello Azure aanmelding dialoogvenster][I03]

5. In Hallo **Selecteer abonnementen** in het dialoogvenster, selecteer Hallo abonnementen wilt toouse en klik vervolgens op **OK**.

   ![dialoogvenster Hallo-abonnementen selecteren][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>Nadat u zich aan interactief u afmelden bij uw Azure-account

Nadat u uw account met behulp van de vorige stappen Hallo hebt geconfigureerd, wordt u automatisch worden afgemeld bij uw Azure-account elke keer dat IntelliJ IDEA opnieuw wordt opgestart. Echter, als u wilt dat toosign buiten uw Azure-account *zonder* opnieuw te starten IntelliJ IDEA Hallo te volgen.

1. In IntelliJ IDEA op Hallo **extra** menu te verwijzen**Azure**, en klik vervolgens op **Azure Afmelden**.

   ![Hallo IntelliJ Azure afmelden opdracht][L01]

2. In Hallo **Azure Afmelden** bevestigingsvenster, klikt u op **Ja**.

   ![Hello Azure afmelden bevestigingsvenster][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a>Tooyour Azure-account automatisch aanmelden

Deze sectie helpt u bij het maken van een referentiebestand die uw service-principal gegevens bevat. Nadat u deze procedure hebt voltooid, opent u Eclipse gebruikt Hallo referenties bestand tooautomatically aanmelding dat in elke tooAzure toen u uw project.

1. Open uw project met IntelliJ IDEA.

2. Op Hallo **extra** menu te verwijzen**Azure**, en klik vervolgens op **Azure aanmelden**.

   ![Hallo IntelliJ Azure aanmelden opdracht][A01]

3. In Hallo **Azure aanmelden** Selecteer **automatisch**, en klik vervolgens op **nieuw**.

   ![Hello Azure aanmelden venster met automatisch geselecteerd][A02]

4. In Hallo **Azure aanmeldingsdialoogvenster** venster, Voer uw Azure-referenties in en klik vervolgens op **aanmelden**.

   ![Hello Azure aanmelding dialoogvenster][A03]

5. In Hallo **bestanden voor verificatie maken** venster, selecteer Hallo abonnementen wilt toouse, de doelmap en klik vervolgens op **Start**.

   ![venster van Hallo-bestanden voor verificatie maken][A04]

6. In Hallo **Status van het Service-Principal maken** in het dialoogvenster nadat de bestanden zijn gemaakt, klikt u op **OK**.

   ![Hallo dialoogvenster van de Status van het Service-Principal maken][A05]

7. In Hallo **Azure aanmelden** venster, klikt u op **aanmelden**.

   ![Het aanmeldingsvenster van Azure][A06]

8. In Hallo **Selecteer abonnementen** in het dialoogvenster, selecteer Hallo abonnementen wilt toouse en klik vervolgens op **OK**.

   ![dialoogvenster Hallo-abonnementen selecteren][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>Afmelden bij uw Azure-account nadat u automatisch hebt aangemeld

Nadat u uw account hebt geconfigureerd met behulp van de vorige stappen hello, hello Azure Toolkit u automatisch afgemeld in tooyour Azure-account elke keer dat IntelliJ IDEA opnieuw wordt opgestart. Echter toosign af van uw Azure-account en hello Azure Toolkit te voorkomen dat u automatisch aanmeldt, Hallo te volgen:

1. In IntelliJ IDEA op Hallo **extra** menu te verwijzen**Azure**, en klik vervolgens op **Azure Afmelden**.

   ![Hallo IntelliJ Azure afmelden opdracht][L01]

2. In Hallo **Azure Afmelden** bevestigingsvenster, klikt u op **Ja**.

   ![Hello Azure afmelden bevestigingsvenster][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a>Tooyour Azure-account automatisch aanmelden met behulp van een bestaand referentiebestand

Als u bij uw Azure-account afmelden wanneer u de IntelliJ IDEA gebruikt, moet u een bestaande referenties bestand tooautomatically teken terug in toohello-account. tooconfigure hello Azure Toolkit voor Eclipse toouse een bestaande referentiebestand Hallo te volgen:

1. Open uw project met IntelliJ IDEA.

2. Op Hallo **extra** menu te verwijzen**Azure**, en klik vervolgens op **Azure aanmelden**.

   ![Hallo IntelliJ Azure aanmelden opdracht][A01]

3. In Hallo **Azure aanmelden** Selecteer **automatisch**, en klik vervolgens op **Bladeren**.

   ![Hello Azure aanmelden venster met automatisch geselecteerd][A02]

4. In Hallo **verificatiebestand Selecteer** in het dialoogvenster selecteert u een eerder gemaakte referentiebestand en klik vervolgens op **Selecteer**.

   ![in het dialoogvenster Hallo-bestand voor verificatie selecteren][A08]

5. In Hallo **Azure aanmelden** venster, klikt u op **aanmelden**.

   ![Hello Azure aanmelden venster met automatisch geselecteerd][A06]

6. In Hallo **Selecteer abonnementen** in het dialoogvenster, selecteer Hallo abonnementen wilt toouse en klik vervolgens op **OK**.

   ![dialoogvenster Hallo-abonnementen selecteren][A07]

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over hello Azure Toolkits voor IDE voor Java Hallo koppelingen te volgen:

* [Azure Toolkit voor Eclipse]
  * [Wat is er nieuw in hello Azure Toolkit voor Eclipse]
  * [Hello Azure Toolkit voor Eclipse installeren]
  * [Aanmelden instructies voor het hello Azure Toolkit voor Eclipse]
  * [Een Hallo wereld-web-app maken voor Azure in Eclipse]
* [Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)
  * [Wat is er nieuw in hello Azure Toolkit voor IntelliJ]
  * [Hello Azure Toolkit voor IntelliJ installeren]
  * *Aanmelden instructies voor hello Azure Toolkit voor IntelliJ* (in dit artikel)
  * [Een Hallo wereld-web-app maken voor Azure in IntelliJ]

Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center] en Hallo [Java-Tools voor Visual Studio Team Services].

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
