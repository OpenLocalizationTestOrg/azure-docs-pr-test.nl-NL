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
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a>Azure aanmelden instructies voor de Azure Toolkit voor Eclipse

De Azure-werkset voor Eclipse biedt twee methoden voor het aanmelden bij uw Azure-account:

  * **Interactieve** : wanneer u van deze methode gebruikmaakt voert u uw Azure-referenties telkens wanneer u zich bij uw Azure-account.
  * **Automatische** : wanneer u van deze methode gebruikmaakt maakt u een referentiebestand waarin uw belangrijkste servicegegevens, waarna u het referentiebestand automatisch aanmelden bij uw Azure-account kunt gebruiken.

De stappen in de volgende secties wordt beschreven hoe elke methode gebruiken.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a>Interactief aanmelden bij uw Azure-account

De volgende stappen ziet u hoe melden bij Azure door uw Azure-referenties handmatig worden ingevoerd.

1. Open uw project met Eclipse.

1. Klik op **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **aanmelden**.

   ![Eclipse Menu voor Azure aanmelden][I01]

1. Wanneer de **Azure aanmelden** in het dialoogvenster wordt weergegeven, selecteert u **interactief**, en klik vervolgens op **aanmelden**.

   ![Meld u aan het dialoogvenster][I02]

1. Wanneer de **Azure Log In** dialoogvenster wordt weergegeven, Voer uw Azure-referenties en klik vervolgens op **aanmelden**.

   ![Het aanmeldingsvenster van Azure][I03]

1. Wanneer de **Selecteer abonnementen** dialoogvenster wordt weergegeven, selecteert u de abonnementen die u wilt gebruiken en klik vervolgens op **OK**.

   ![Dialoogvenster Selecteer abonnementen][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>Ondertekening buiten uw Azure-account wanneer u zich interactief aangemeld

Nadat u de stappen in de vorige sectie hebt geconfigureerd, wordt u automatisch afgemeld bij uw Azure-account elke keer dat Eclipse opnieuw wordt opgestart. Als u afmelden bij uw Azure-account wilt zonder Eclipse opnieuw te starten, gebruikt u de volgende stappen uit.

1. Klik in Eclipse **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **Afmelden**.

   ![Eclipse Menu voor Azure afmelden][L01]

1. Wanneer de **Azure Afmelden** dialoogvenster wordt weergegeven, klikt u op **Ja**.

   ![In het dialoogvenster afmelden][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a>Automatisch aanmelden bij uw Azure-account en maken van een referentiebestand moeten worden gebruikt in de toekomst

De volgende stappen begeleidt u bij het maken van een referentiebestand die uw service-principal gegevens bevat. Nadat u deze stappen hebt voltooid, gebruiken Eclipse automatisch het referentiebestand automatisch aanmelden bij Azure telkens wanneer die u uw project opent.

1. Open uw project met Eclipse.

1. Klik op **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **aanmelden**.

   ![Eclipse Menu voor Azure aanmelden][A01]

1. Wanneer de **Azure aanmelden** in het dialoogvenster wordt weergegeven, selecteert u **automatisch**, en klik vervolgens op **nieuw**.

   ![Meld u aan het dialoogvenster][A02]

1. Wanneer de **Azure Log In** dialoogvenster wordt weergegeven, Voer uw Azure-referenties en klik vervolgens op **aanmelden**.

   ![Het aanmeldingsvenster van Azure][A03]

1. Wanneer de **verificatiebestanden maken** dialoogvenster wordt weergegeven, selecteert u de abonnementen die u wilt gebruiken, de doelmap en klik vervolgens op **Start**.

   ![Het aanmeldingsvenster van Azure][A04]

1. De **Service-Principal Creatation Status** in het dialoogvenster wordt weergegeven, en nadat de bestanden zijn gemaakt, klikt u op **OK**.

   ![Dialoogvenster Service-Principal Creatation Status][A05]

1. Wanneer de **Azure aanmelden** dialoogvenster wordt weergegeven, klikt u op **aanmelden**.

   ![Het aanmeldingsvenster van Azure][A06]

1. Wanneer de **Selecteer abonnementen** dialoogvenster wordt weergegeven, selecteert u de abonnementen die u wilt gebruiken en klik vervolgens op **OK**.

   ![Dialoogvenster Selecteer abonnementen][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>Ondertekening buiten uw Azure-account wanneer u automatisch aangemeld

Nadat u de stappen in de vorige sectie hebt geconfigureerd, wordt de Azure-Toolkit automatisch aangemeld bij uw Azure-account elke keer dat Eclipse opnieuw wordt opgestart. Echter wilt afmelden bij uw Azure-account en voorkomen dat de Toolkit Azure automatisch aanmelden, gebruiken de volgende stappen uit.

1. Klik in Eclipse **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **Afmelden**.

   ![Eclipse Menu voor Azure afmelden][L01]

1. Wanneer de **Azure Afmelden** dialoogvenster wordt weergegeven, klikt u op **Ja**.

   ![In het dialoogvenster afmelden][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>Aanmelden bij uw Azure-account automatisch met behulp van een referentiebestand die u al hebt gemaakt

Als u zich af bij Azure wanneer u Eclipse gebruikt, moet u opnieuw configureren van de Azure-werkset voor Eclipse een referentiebestand die u hebt gemaakt voordat u kunt automatisch aanmelden bij uw Azure-account te gebruiken. De volgende stappen begeleidt u stapsgewijs door de Azure-Toolkit voor het gebruik van een bestaand referentiebestand configureren.

1. Open uw project met Eclipse.

1. Klik op **extra**, klikt u vervolgens op **Azure**, en klik vervolgens op **aanmelden**.

   ![Eclipse Menu voor Azure aanmelden][A01]

1. Wanneer de **Azure aanmelden** in het dialoogvenster wordt weergegeven, selecteert u **automatisch**, en klik vervolgens op **Bladeren**.

   ![Meld u aan het dialoogvenster][A02]

1. Wanneer de **geverifieerd bestand selecteren** dialoogvenster wordt weergegeven, selecteert u een referentiebestand die u eerder hebt gemaakt en klik vervolgens op **Selecteer**.

   ![Meld u aan het dialoogvenster][A08]

1. Wanneer de **Azure aanmelden** dialoogvenster wordt weergegeven, klikt u op **aanmelden**.

   ![Het aanmeldingsvenster van Azure][A06]

1. Wanneer de **Selecteer abonnementen** dialoogvenster wordt weergegeven, selecteert u de abonnementen die u wilt gebruiken en klik vervolgens op **OK**.

   ![Dialoogvenster Selecteer abonnementen][A07]

## <a name="see-also"></a>Zie ook
Voor meer informatie over de Azure Toolkits voor Java-IDE's klikt u op de volgende koppelingen:

* [Azure Toolkit voor Eclipse]
  * [What's New in the Azure Toolkit for Eclipse] (Nieuw in de Azure Toolkit voor Eclipse)
  * [Installing the Azure Toolkit for Eclipse] (De Azure Toolkit voor Eclipse installeren)
  * *Meld u aan de instructies voor de Azure Toolkit voor Eclipse (in dit artikel)*
  * [Een Hallo wereld Web-App maken voor Azure in Eclipse]
* [Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)
  * [What's New in the Azure Toolkit for IntelliJ] (Nieuw in de Azure Toolkit voor IntelliJ)
  * [Installing the Azure Toolkit for IntelliJ] (De Azure Toolkit voor IntelliJ installeren)
  * [Sign In Instructions for the Azure Toolkit for IntelliJ] (Aanmeldingsinstructies voor de Azure Toolkit voor IntelliJ)
  * [Een Hallo wereld Web-App maken voor Azure in IntelliJ]

Voor meer informatie over het gebruik van Azure met Java raadpleegt u het [Azure Java-ontwikkelaarscentrum] en de [Java Tools voor Visual Studio Team Services].

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld Web-App maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld Web-App maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (De Azure Toolkit voor Eclipse installeren)
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)
[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md (Aanmeldingsinstructies voor de Azure Toolkit voor IntelliJ)
[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md (Nieuw in de Azure Toolkit voor Eclipse)
[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md (Nieuw in de Azure Toolkit voor IntelliJ)

[Azure Java-ontwikkelaarscentrum]: https://azure.microsoft.com/develop/java/
[Java Tools voor Visual Studio Team Services]: https://java.visualstudio.com/

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
