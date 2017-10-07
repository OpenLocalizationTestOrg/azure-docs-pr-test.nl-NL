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
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a>Azure-teken In de instructies voor het hello Azure Toolkit voor Eclipse

Hello Azure Toolkit voor Eclipse biedt twee methoden voor het aanmelden bij uw Azure-account:

  * **Interactieve** : wanneer u van deze methode gebruikmaakt voert u uw Azure-referenties telkens wanneer u zich bij uw Azure-account.
  * **Automatische** : wanneer u van deze methode gebruikmaakt maakt u een referentiebestand waarin uw belangrijkste servicegegevens, waarna u Hallo referenties bestand tooautomatically aanmelding in uw Azure-account kunt gebruiken.

Hallo stappen in de volgende secties Hallo wordt beschreven hoe toouse elke methode.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a>Interactief aanmelden bij uw Azure-account

Hallo volgende stappen wordt laten zien hoe toosign in Azure door uw Azure-referenties handmatig worden ingevoerd.

1. Open uw project met Eclipse.

1. Klik op **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **aanmelden**.

   ![Eclipse Menu voor Azure aanmelden][I01]

1. Wanneer Hallo **Azure aanmelden** in het dialoogvenster wordt weergegeven, selecteert u **interactief**, en klik vervolgens op **aanmelden**.

   ![Meld u aan het dialoogvenster][I02]

1. Wanneer Hallo **Azure Log In** dialoogvenster wordt weergegeven, Voer uw Azure-referenties en klik vervolgens op **aanmelden**.

   ![Het aanmeldingsvenster van Azure][I03]

1. Wanneer Hallo **Selecteer abonnementen** dialoogvenster wordt weergegeven, selecteer Hallo abonnementen wilt toouse en klik vervolgens op **OK**.

   ![Dialoogvenster Selecteer abonnementen][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>Ondertekening buiten uw Azure-account wanneer u zich interactief aangemeld

Nadat u Hallo stappen hebt geconfigureerd in de vorige sectie hello, wordt u automatisch afgemeld bij uw Azure-account elke keer dat Eclipse opnieuw wordt opgestart. Echter gebruiken als u toosign buiten uw Azure-account wilt zonder Eclipse opnieuw te starten, Hallo stappen te volgen.

1. Klik in Eclipse **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **Afmelden**.

   ![Eclipse Menu voor Azure afmelden][L01]

1. Wanneer Hallo **Azure Afmelden** dialoogvenster wordt weergegeven, klikt u op **Ja**.

   ![In het dialoogvenster afmelden][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a>Automatisch aanmelden bij uw Azure-account en het maken van de referenties op een bestand toouse in Hallo toekomstige

Hallo begeleidt volgt u bij het maken van een referentiebestand die uw service-principal gegevens bevat. Als u klaar bent met deze stappen, Eclipse wordt automatisch open gebruik Hallo referenties bestand tooautomatically aanmelding dat bij Azure elke toen u het project.

1. Open uw project met Eclipse.

1. Klik op **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **aanmelden**.

   ![Eclipse Menu voor Azure aanmelden][A01]

1. Wanneer Hallo **Azure aanmelden** in het dialoogvenster wordt weergegeven, selecteert u **automatisch**, en klik vervolgens op **nieuw**.

   ![Meld u aan het dialoogvenster][A02]

1. Wanneer Hallo **Azure Log In** dialoogvenster wordt weergegeven, Voer uw Azure-referenties en klik vervolgens op **aanmelden**.

   ![Het aanmeldingsvenster van Azure][A03]

1. Wanneer Hallo **verificatiebestanden maken** dialoogvenster wordt weergegeven, selecteer Hallo abonnementen wilt toouse, de doelmap en klik vervolgens op **Start**.

   ![Het aanmeldingsvenster van Azure][A04]

1. Hallo **Service-Principal Creatation Status** in het dialoogvenster wordt weergegeven, en nadat de bestanden zijn gemaakt, klikt u op **OK**.

   ![Dialoogvenster Service-Principal Creatation Status][A05]

1. Wanneer Hallo **Azure aanmelden** dialoogvenster wordt weergegeven, klikt u op **aanmelden**.

   ![Het aanmeldingsvenster van Azure][A06]

1. Wanneer Hallo **Selecteer abonnementen** dialoogvenster wordt weergegeven, selecteer Hallo abonnementen wilt toouse en klik vervolgens op **OK**.

   ![Dialoogvenster Selecteer abonnementen][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>Ondertekening buiten uw Azure-account wanneer u automatisch aangemeld

Nadat u Hallo stappen hebt geconfigureerd in de vorige sectie hello, wordt hello Azure Toolkit automatisch aangemeld bij uw Azure-account elke keer dat Eclipse opnieuw wordt opgestart. Toosign wordt echter af van uw Azure-account en te voorkomen dat hello Azure Toolkit aanmelden automatisch gebruik Hallo van de volgende stappen uit.

1. Klik in Eclipse **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **Afmelden**.

   ![Eclipse Menu voor Azure afmelden][L01]

1. Wanneer Hallo **Azure Afmelden** dialoogvenster wordt weergegeven, klikt u op **Ja**.

   ![In het dialoogvenster afmelden][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>Aanmelden bij uw Azure-account automatisch met behulp van een referentiebestand die u al hebt gemaakt

Als u zich af bij Azure wanneer u Eclipse gebruikt, moet u tooreconfigure hello Azure Toolkit voor Eclipse toouse een referentiebestand die u hebt gemaakt voordat u kunt automatisch aanmelden bij uw Azure-account. Hallo begeleidt volgt u stapsgewijs door hello Azure Toolkit toouse configureren een bestaand referentiebestand.

1. Open uw project met Eclipse.

1. Klik op **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **aanmelden**.

   ![Eclipse Menu voor Azure aanmelden][A01]

1. Wanneer Hallo **Azure aanmelden** in het dialoogvenster wordt weergegeven, selecteert u **automatisch**, en klik vervolgens op **Bladeren**.

   ![Meld u aan het dialoogvenster][A02]

1. Wanneer Hallo **geverifieerd bestand selecteren** dialoogvenster wordt weergegeven, selecteert u een referentiebestand die u eerder hebt gemaakt en klik vervolgens op **Selecteer**.

   ![Meld u aan het dialoogvenster][A08]

1. Wanneer Hallo **Azure aanmelden** dialoogvenster wordt weergegeven, klikt u op **aanmelden**.

   ![Het aanmeldingsvenster van Azure][A06]

1. Wanneer Hallo **Selecteer abonnementen** dialoogvenster wordt weergegeven, selecteer Hallo abonnementen wilt toouse en klik vervolgens op **OK**.

   ![Dialoogvenster Selecteer abonnementen][A07]

## <a name="see-also"></a>Zie ook
Zie voor meer informatie over hello Azure Toolkits voor IDE voor Java Hallo koppelingen te volgen:

* [Azure Toolkit voor Eclipse]
  * [Wat is er nieuw in hello Azure Toolkit voor Eclipse]
  * [Hello Azure Toolkit voor Eclipse installeren]
  * *Meld u In instructies voor het hello Azure Toolkit voor Eclipse (dit artikel)*
  * [Een Hallo wereld Web-App maken voor Azure in Eclipse]
* [Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)
  * [Wat is er nieuw in hello Azure Toolkit voor IntelliJ]
  * [Hello Azure Toolkit voor IntelliJ installeren]
  * [Meld u In instructies voor het hello Azure Toolkit voor IntelliJ]
  * [Een Hallo wereld Web-App maken voor Azure in IntelliJ]

Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center] en Hallo [Java-Tools voor Visual Studio Team Services].

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
