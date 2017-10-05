---
title: Virtuele machines beheren met behulp van de Azure-Explorer voor Eclipse | Microsoft Docs
description: Informatie over het beheren van uw virtuele machines in Azure met behulp van de Azure-Explorer voor Eclipse.
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
ms.openlocfilehash: 9784e8af9c530078afee06f08a23403a44b0762f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-eclipse"></a>Virtuele machines beheren met behulp van de Azure-Explorer voor Eclipse

De Azure-Explorer, die deel van de Azure-werkset voor Eclipse uitmaakt, biedt Java ontwikkelaars een oplossing eenvoudig te gebruiken voor het beheren van virtuele machines in de Azure-account uit binnen de Eclipse integrated development environment (IDE).

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a>Een virtuele machine maken in Eclipse

Voor het maken van een virtuele machine met behulp van de Azure-Explorer, het volgende doen:

1. Aanmelden bij uw Azure-account met behulp van de [aanmelden instructies voor de Azure-werkset voor Eclipse].

2. In de **Azure Explorer** weergeven, vouw de **Azure** knooppunt met de rechtermuisknop op **virtuele Machines**, en klik vervolgens op **VM maken**.

   ![De opdracht VM maken][CR01]  
   De **nieuwe virtuele Machine maken** wizard wordt geopend.

3. In de **Kies een abonnement** venster uw abonnement te selecteren en klik vervolgens op **volgende**.

   ![De Kies een abonnement-venster][CR02]

4. In de **selecteert u de installatiekopie van een virtuele Machine** venster, voer de volgende informatie:

   * **Locatie**: Hiermee geeft u op waar uw virtuele machine wordt gemaakt (bijvoorbeeld *VS-West*).

   * **Publisher**: Hiermee geeft u de uitgever die de afbeelding die u gebruikt voor het maken van uw virtuele machine hebt gemaakt (bijvoorbeeld *Microsoft*).

   * **Bieden**: Hiermee geeft u de virtuele machine biedt van de geselecteerde uitgever te gebruiken (bijvoorbeeld *JDK*).

   * **SKU**: Hiermee geeft u de SKU (SKU) van de geselecteerde aanbieding te gebruiken (bijvoorbeeld *JDK_8*).

   * **Versie #**: Hiermee geeft u op welke versie van de geselecteerde SKU te gebruiken.

    ![Selecteer een venster van de installatiekopie van virtuele Machine][CR03]

5. Klik op **Volgende**.

6. In de **basisinstellingen van de virtuele Machine** venster, voer de volgende informatie:

   * **Naam van virtuele Machine**: Hiermee geeft u de naam voor uw nieuwe virtuele machine, die moet beginnen met een letter en mag alleen letters, cijfers en afbreekstreepjes.

   * **De grootte van**: Hiermee geeft u het aantal kernen en het geheugen toewijzen voor uw virtuele machine.

   * **Gebruikersnaam**: Hiermee geeft u het administrator-account maken voor het beheren van uw virtuele machine.

   * **Wachtwoord** en **bevestigen**: Hiermee geeft u het wachtwoord voor uw beheerdersaccount.

    ![Het venster basisinstellingen van de virtuele Machine][CR04]

7. Klik op **Volgende**.

8. In de **nieuw Opslagaccount maken** venster, voer de volgende informatie:

   * **Resourcegroep**: Hiermee geeft u de resourcegroep voor uw virtuele machine. Selecteer een van de volgende opties:
      * **Maken van nieuwe**: geeft aan dat u wilt maken van een nieuwe resourcegroep.
      * **Gebruik bestaande**: geeft aan dat u wilt een resourcegroep die al is gekoppeld aan uw Azure-account selecteren.

      ![Het dialoogvenster Nieuw Opslagaccount maken][CR05]

   * **Storage-account**: Hiermee geeft u het opslagaccount moet worden gebruikt voor het opslaan van uw virtuele machine. U kunt een bestaand opslagaccount gebruiken of een nieuw account maken.

   * **Virtueel netwerk** en **Subnet**: Hiermee geeft u het virtuele netwerk en subnet dat uw virtuele machine maakt verbinding met. U kunt een bestaand netwerk en subnet of kunt u een nieuw netwerk en subnet. Als u selecteert **nieuw**, het volgende dialoogvenster wordt weergegeven:

      ![Het dialoogvenster Nieuw virtueel netwerk maken][CR06]

9. In de **Resources die zijn gekoppeld** venster, voer de volgende informatie:

   * **Openbaar IP-adres**: Hiermee geeft u een extern gerichte IP-adres voor uw virtuele machine. U kunt een nieuw IP-adres maken of, als uw virtuele machine een openbaar IP-adres niet hebt wordt, kunt u **(geen)**.

   * **Netwerkbeveiligingsgroep**: Hiermee geeft u een optionele netwerken firewall voor uw virtuele machine. Kunt u een firewall of, als uw virtuele machine niet voor een netwerkfirewall gebruikt wordt, kunt u **(geen)**.

   * **Beschikbaarheidsset**: Hiermee geeft u een optionele beschikbaarheidsset dat deel van uw virtuele machine uitmaken kunnen. U kunt een bestaande beschikbaarheidsset selecteren of maken van een nieuwe beschikbaarheidsset of de virtuele machine hoort niet bij een beschikbaarheidsset, kunt u **(geen)**.

   ![Het venster Resources die zijn gekoppeld][CR07]

9. Klik op **Voltooien**.  
  Uw nieuwe virtuele machine wordt weergegeven in het venster van het hulpprogramma Azure Explorer.

   ![Nieuwe virtuele Machine][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a>Opnieuw opstarten van een virtuele machine in Eclipse

Als u wilt een virtuele machine opstarten met behulp van de Azure-Explorer in Eclipse, het volgende doen:

1. In de **Azure Explorer** bekijken, met de rechtermuisknop op de virtuele machine en selecteer vervolgens **opnieuw**.

   ![De opdracht van de virtuele machine opnieuw starten][RE01]

2. Klik in het bevestigingsvenster **Ja**.

   ![Het bevestigingsvenster opnieuw opstarten][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a>Een virtuele machine in Eclipse afsluiten

Als u wilt afsluiten een actieve virtuele machine met behulp van de Azure-Explorer in Eclipse, het volgende doen:

1. In de **Azure Explorer** bekijken, met de rechtermuisknop op de virtuele machine en selecteer vervolgens **afsluiten**.

   ![De opdracht van virtuele machines afsluiten][SH01]

2. Klik in het bevestigingsvenster **Ja**.

   ![Het bevestigingsvenster virtuele machines afsluiten][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a>Een virtuele machine in Eclipse verwijderen

Als u wilt verwijderen van een virtuele machine met behulp van de Azure-Explorer in Eclipse, het volgende doen:

1. In de **Azure Explorer** bekijken, met de rechtermuisknop op de virtuele machine en selecteer vervolgens **verwijderen**.

   ![De opdracht van de virtuele machine verwijderen][DE01]

2. Klik in het bevestigingsvenster **Ja**.

   ![Het verwijderen van een virtuele machine bevestigingsvenster][DE02]

## <a name="next-steps"></a>Volgende stappen
Zie de volgende bronnen voor meer informatie over Azure grootten voor virtuele machines en prijzen:

* Azure grootten voor virtuele machines
  * [Grootten voor Windows virtuele machines in Azure]
  * [Grootten voor virtuele Linux-machines in Azure]
* Prijzen voor Azure virtuele machines
  * [Prijzen van virtuele machines in Windows]
  * [Prijzen van Linux virtuele machines]

Zie de volgende bronnen voor meer informatie over de Azure-Toolkits voor IDE voor Java:

* [Azure Toolkit voor Eclipse]
  * [Wat is er nieuw in de Azure-werkset voor Eclipse]
  * [Installing the Azure Toolkit for Eclipse] (De Azure Toolkit voor Eclipse installeren)
  * [aanmelden instructies voor de Azure-werkset voor Eclipse]
  * [Een Hallo wereld-web-app maken voor Azure in Eclipse]
* [Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)
  * [Wat is er nieuw in de Azure-werkset voor IntelliJ]
  * [Installing the Azure Toolkit for IntelliJ] (De Azure Toolkit voor IntelliJ installeren)
  * [Aanmelden instructies voor de Azure-Toolkit voor IntelliJ]
  * [Een Hallo wereld-web-app maken voor Azure in IntelliJ]

Zie voor meer informatie over het gebruik van Azure met Java [Azure Java Developer Center] en [Java-Tools voor Visual Studio Team Services].

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld-web-app maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld-web-app maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (De Azure Toolkit voor Eclipse installeren)
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)
[aanmelden instructies voor de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Aanmelden instructies voor de Azure-Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Wat is er nieuw in de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Wat is er nieuw in de Azure-werkset voor IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/

[Grootten voor Windows virtuele machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Grootten voor virtuele Linux-machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Prijzen van virtuele machines in Windows]: /pricing/details/virtual-machines/windows/
[Prijzen van Linux virtuele machines]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
