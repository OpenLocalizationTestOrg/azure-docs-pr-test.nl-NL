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
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a>Aanmelden instructies voor de Azure-Toolkit voor IntelliJ

De Azure-werkset voor IntelliJ biedt twee methoden voor het aanmelden bij uw Azure-account:

  * **Interactieve**: U uw Azure-referenties invoeren telkens wanneer u zich aanmeldt bij uw Azure-account.
  * **Automatische**: maken van een referentiebestand die u gebruiken kunt voor het automatisch aanmelden bij uw Azure-account.

De volgende secties wordt beschreven hoe elke methode.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-interactively"></a>Interactief aanmelden bij uw Azure-account

Als u wilt aanmelden bij Azure met uw Azure-referenties handmatig worden ingevoerd, het volgende doen:

1. Open uw project met IntelliJ IDEA.

2. Klik op **extra**, wijs **Azure**, en klik vervolgens op **Azure aanmelden**.

   ![De opdracht IntelliJ Azure aanmelden][I01]

3. In de **Azure aanmelden** Selecteer **interactief**, en klik vervolgens op **aanmelden**.

   ![Het venster Azure aanmelden met interactief geselecteerd][I02]

4. In de **Azure Log In** dialoogvenster wordt weergegeven, Voer uw Azure-referenties en klik vervolgens op **aanmelden**.

   ![Het dialoogvenster Azure-aanmelding][I03]

5. In de **Selecteer abonnementen** in het dialoogvenster, selecteer de abonnementen die u wilt gebruiken en klik vervolgens op **OK**.

   ![Het dialoogvenster abonnementen selecteren][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>Nadat u zich aan interactief u afmelden bij uw Azure-account

Nadat u uw account met behulp van de voorgaande stappen hebt geconfigureerd, wordt u automatisch worden afgemeld bij uw Azure-account elke keer dat IntelliJ IDEA opnieuw wordt opgestart. Echter, als u zich wilt afmelden bij uw Azure-account *zonder* IntelliJ IDEA opnieuw starten de volgende handelingen uit.

1. In IntelliJ IDEA op de **extra** in het menu **Azure**, en klik vervolgens op **Azure Afmelden**.

   ![De opdracht IntelliJ Azure afmelden][L01]

2. In de **Azure Afmelden** bevestigingsvenster, klikt u op **Ja**.

   ![Het bevestigingsvenster Azure afmelden][L02]

## <a name="sign-in-to-your-azure-account-automatically"></a>Automatisch aanmelden bij uw Azure-account

Deze sectie helpt u bij het maken van een referentiebestand die uw service-principal gegevens bevat. Nadat u deze procedure hebt voltooid, wordt in Eclipse het referentiebestand gebruikt om automatisch aanmelden bij Azure telkens wanneer die u uw project opent.

1. Open uw project met IntelliJ IDEA.

2. Op de **extra** in het menu **Azure**, en klik vervolgens op **Azure aanmelden**.

   ![De opdracht IntelliJ Azure aanmelden][A01]

3. In de **Azure aanmelden** Selecteer **automatisch**, en klik vervolgens op **nieuw**.

   ![Het venster Azure aanmelden met automatisch geselecteerd][A02]

4. In de **Azure aanmeldingsdialoogvenster** venster, Voer uw Azure-referenties in en klik vervolgens op **aanmelden**.

   ![Het dialoogvenster Azure-aanmelding][A03]

5. In de **bestanden voor verificatie maken** venster, selecteer de abonnementen die u wilt gebruiken, de doelmap en klik vervolgens op **Start**.

   ![Het venster bestanden voor verificatie maken][A04]

6. In de **Status van het Service-Principal maken** in het dialoogvenster nadat de bestanden zijn gemaakt, klikt u op **OK**.

   ![Het dialoogvenster van de Status van het Service-Principal maken][A05]

7. In de **Azure aanmelden** venster, klikt u op **aanmelden**.

   ![Het aanmeldingsvenster van Azure][A06]

8. In de **Selecteer abonnementen** in het dialoogvenster, selecteer de abonnementen die u wilt gebruiken en klik vervolgens op **OK**.

   ![Het dialoogvenster abonnementen selecteren][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>Afmelden bij uw Azure-account nadat u automatisch hebt aangemeld

Nadat u uw account met behulp van de voorgaande stappen hebt geconfigureerd, de Azure-Toolkit automatisch aangemeld bij uw Azure-account elke keer dat IntelliJ IDEA opnieuw wordt opgestart. Echter, als u wilt afmelden bij uw Azure-account en voorkomen dat de Toolkit Azure automatisch aanmelden, het volgende doen:

1. In IntelliJ IDEA op de **extra** in het menu **Azure**, en klik vervolgens op **Azure Afmelden**.

   ![De opdracht IntelliJ Azure afmelden][L01]

2. In de **Azure Afmelden** bevestigingsvenster, klikt u op **Ja**.

   ![Het bevestigingsvenster Azure afmelden][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a>Aanmelden bij uw Azure-account automatisch met behulp van een bestaand referentiebestand

Als u bij uw Azure-account afmelden wanneer u de IntelliJ IDEA gebruikt, moet u een bestaand referentiebestand automatisch aanmelden bij het account. De Azure-werkset voor Eclipse een bestaand referentiebestand gebruiken, kunt u het volgende configureren:

1. Open uw project met IntelliJ IDEA.

2. Op de **extra** in het menu **Azure**, en klik vervolgens op **Azure aanmelden**.

   ![De opdracht IntelliJ Azure aanmelden][A01]

3. In de **Azure aanmelden** Selecteer **automatisch**, en klik vervolgens op **Bladeren**.

   ![Het venster Azure aanmelden met automatisch geselecteerd][A02]

4. In de **verificatiebestand Selecteer** in het dialoogvenster selecteert u een eerder gemaakte referentiebestand en klik vervolgens op **Selecteer**.

   ![Het dialoogvenster verificatiebestand selecteren][A08]

5. In de **Azure aanmelden** venster, klikt u op **aanmelden**.

   ![Het venster Azure aanmelden met automatisch geselecteerd][A06]

6. In de **Selecteer abonnementen** in het dialoogvenster, selecteer de abonnementen die u wilt gebruiken en klik vervolgens op **OK**.

   ![Het dialoogvenster abonnementen selecteren][A07]

## <a name="next-steps"></a>Volgende stappen
Voor meer informatie over de Azure Toolkits voor Java-IDE's klikt u op de volgende koppelingen:

* [Azure Toolkit voor Eclipse]
  * [Wat is er nieuw in de Azure-werkset voor Eclipse]
  * [Installing the Azure Toolkit for Eclipse] (De Azure Toolkit voor Eclipse installeren)
  * [Aanmelden instructies voor de Azure-werkset voor Eclipse]
  * [Een Hallo wereld-web-app maken voor Azure in Eclipse]
* [Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)
  * [Wat is er nieuw in de Azure-werkset voor IntelliJ]
  * [Installing the Azure Toolkit for IntelliJ] (De Azure Toolkit voor IntelliJ installeren)
  * *Aanmelden instructies voor de Azure-Toolkit voor IntelliJ* (in dit artikel)
  * [Een Hallo wereld-web-app maken voor Azure in IntelliJ]

Voor meer informatie over het gebruik van Azure met Java raadpleegt u het [Azure Java-ontwikkelaarscentrum] en de [Java Tools voor Visual Studio Team Services].

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld Web-App maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld-web-app maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (De Azure Toolkit voor Eclipse installeren)
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)
[Aanmelden instructies voor de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Wat is er nieuw in de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Wat is er nieuw in de Azure-werkset voor IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java-ontwikkelaarscentrum]: https://azure.microsoft.com/develop/java/
[Java Tools voor Visual Studio Team Services]: https://java.visualstudio.com/

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
