---
title: aaaManage virtuele machines met behulp van hello Azure Explorer voor IntelliJ | Microsoft Docs
description: Meer informatie over hoe toomanage uw virtuele machines in Azure met behulp van hello Azure Explorer voor IntelliJ.
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
ms.openlocfilehash: a73dd4f73b311dd3413f6712e3b76c36ee464de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-intellij"></a>Virtuele machines beheren met behulp van hello Azure Explorer voor IntelliJ

Hello Azure Explorer, die deel van hello Azure Toolkit voor IntelliJ uitmaakt, Java-ontwikkelaars met een eenvoudig-en-klare oplossing biedt voor het beheren van virtuele machines in de Azure-account uit binnen Hallo IntelliJ integrated development environment (IDE).

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a>Een virtuele machine maken in IntelliJ

een virtuele machine met behulp van hello Azure Explorer toocreate Hallo te volgen: 

1. Meld u aan tooyour Azure-account met behulp van Hallo stappen in Hallo [aanmelden instructies voor hello Azure Toolkit voor IntelliJ] artikel.

2. In Hallo **Azure Explorer** weergeven, vouwt u Hallo **Azure** knooppunt met de rechtermuisknop op **virtuele Machines**, en klik vervolgens op **VM maken**. 

   ![Hallo opdracht VM maken][CR01]  
    Hallo **nieuwe virtuele Machine maken** wizard wordt geopend.

3. In Hallo **Kies een abonnement** venster uw abonnement te selecteren en klik vervolgens op **volgende**. 

   ![Kies een abonnement venster Hallo][CR02]

4. In Hallo **selecteert u de installatiekopie van een virtuele Machine** venster Voer Hallo volgende informatie:

   * **Locatie**: Hiermee geeft u op waar uw virtuele machine wordt gemaakt (bijvoorbeeld *VS-West*). 

   * **Afbeelding aanbevolen**: Hiermee geeft u op dat u een installatiekopie van een verkorte lijst van veelgebruikte installatiekopieën kiest.

   * **Aangepaste installatiekopie**: Hiermee geeft u een aangepaste installatiekopie dankzij de volgende informatie hello te kiezen:

      * **Publisher**: Hiermee geeft u op Hallo publisher dat Hallo-installatiekopie die u voor uw virtuele machine gebruiken wilt gemaakt (bijvoorbeeld *Microsoft*).

      * **Bieden**: Hiermee geeft u op Hallo virtuele machine toouse aanbieding van de geselecteerde uitgever Hallo (bijvoorbeeld *JDK*).

      * **SKU**: Hiermee geeft u op Hallo SKU (SKU's) toouse van de geselecteerde serviceaanbieding Hallo (bijvoorbeeld *JDK_8*).

      * **Versie #**: Hiermee geeft u op welke versie van Hallo geselecteerd SKU toouse.

   ![Hallo selecteert u het venster van een installatiekopie van virtuele Machine][CR03]

5. Klik op **Volgende**. 

6. In Hallo **basisinstellingen van de virtuele Machine** venster Voer Hallo volgende informatie:

   * **Naam van virtuele machine**: Hiermee geeft u de naam Hallo voor uw nieuwe virtuele machine die moet beginnen met een letter en mag alleen letters, cijfers en afbreekstreepjes.

   * **De grootte van**: Hiermee geeft u Hallo aantal kernen en geheugen tooallocate voor uw virtuele machine.

   * **Gebruikersnaam**: Hiermee geeft u op Hallo beheerder account toocreate voor het beheren van uw virtuele machine.

   * **Wachtwoord** en **bevestigen**: Hallo wachtwoord voor uw beheerdersaccount.

   ![Hallo basisinstellingen van de virtuele Machine venster][CR04]

7. Klik op **Volgende**. 

8. In Hallo **Resources die zijn gekoppeld** venster Voer Hallo volgende informatie:

   * **Resourcegroep**: Hiermee geeft u de resourcegroep Hallo voor uw virtuele machine. Selecteer een Hallo volgende opties:
      * **Maken van nieuwe**: geeft aan dat u wilt dat toocreate een nieuwe resourcegroep.
      * **Gebruik bestaande**: geeft aan dat u wilt tooselect uit een lijst met resourcegroepen die gekoppeld aan uw Azure-account zijn.

       ![venster van de Resources die zijn gekoppeld Hallo][CR07]

   * **Storage-account**: Hiermee geeft u op Hallo storage account toouse voor het opslaan van uw virtuele machine. U kunt ervoor kiezen een bestaand opslagaccount of maak een nieuw account. Als u ervoor kiest **nieuw**, Hallo volgen in het dialoogvenster wordt weergegeven:

      ![dialoogvenster Hallo-Storage-Account maken][CR05]

   * **Virtueel netwerk** en **Subnet**: Hiermee geeft u op Hallo virtueel netwerk en subnet dat uw virtuele machine maakt verbinding met. U kunt een bestaand netwerk en subnet of kunt u een nieuw netwerk en subnet. Als u selecteert **nieuw**, Hallo volgen in het dialoogvenster wordt weergegeven:

      ![dialoogvenster voor Hallo virtueel netwerk maken][CR06]

   * **Openbaar IP-adres**: Hiermee geeft u een extern gerichte IP-adres voor uw virtuele machine. U kunt toocreate een nieuw IP-adres of, als uw virtuele machine een openbaar IP-adres niet hebt wordt, kunt u **(geen)**. 

   * **Netwerkbeveiligingsgroep**: Hiermee geeft u een optionele netwerken firewall voor uw virtuele machine. Kunt u een firewall of, als uw virtuele machine niet voor een netwerkfirewall gebruikt wordt, kunt u **(geen)**. 

   * **Beschikbaarheidsset**: Hiermee geeft u een optionele beschikbaarheidsset dat deel van uw virtuele machine uitmaken kunnen. U kunt een bestaande beschikbaarheidsset, een nieuwe beschikbaarheidsset maken of, als uw virtuele machine geen deel van tooan beschikbaarheidsset uitmaakt, selecteert u **(geen)**.

9. Klik op **Voltooien**.  
    Uw nieuwe virtuele machine weergegeven in hello Azure Explorer hulpprogramma venster. 

   ![Nieuwe virtuele machine in hello Azure Verkenner-weergave][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a>Opnieuw opstarten van een virtuele machine in IntelliJ

een virtuele machine met behulp van hello Azure Explorer in IntelliJ, toorestart Hallo te volgen:

1. In Hallo **Azure Explorer** bekijken, met de rechtermuisknop op Hallo virtuele machine en selecteer vervolgens **opnieuw**.

   ![de opdracht Hallo virtuele machines opnieuw starten][RE01]

2. Klik in het bevestigingsvenster hello, **Ja**. 

   ![Hallo bevestigingsvenster van de virtuele machine opnieuw opstarten][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a>Een virtuele machine in IntelliJ afsluiten

tooshut omlaag een actieve virtuele machine met behulp van hello Azure Explorer in IntelliJ, Hallo te volgen:

1. In Hallo **Azure Explorer** bekijken, met de rechtermuisknop op Hallo virtuele machine en selecteer vervolgens **afsluiten**.

   ![Hallo afsluitopdracht van virtuele machines][SH01]

2. Klik in het bevestigingsvenster hello, **Ja**. 

   ![Hallo bevestigingsvenster van de virtuele machine afsluiten][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a>Een virtuele machine in IntelliJ verwijderen

een virtuele machine met behulp van hello Azure Explorer in IntelliJ, toodelete Hallo te volgen:

1. In Hallo **Azure Explorer** bekijken, met de rechtermuisknop op Hallo virtuele machine en selecteer vervolgens **verwijderen**.

   ![opdracht voor Hallo virtuele machines verwijderen][DE01]

2. Klik in het bevestigingsvenster hello, **Ja**. 

   ![Hallo bevestigingsvenster van de virtuele machine verwijderen][DE02]

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over Azure grootten voor virtuele machines en prijzen Hallo resources te volgen:

* Azure grootten voor virtuele machines
  * [Grootten voor Windows virtuele machines in Azure]
  * [Grootten voor virtuele Linux-machines in Azure]
* Prijzen voor Azure virtuele machines
  * [Prijzen van virtuele machines in Windows]
  * [Prijzen van Linux virtuele machines]

Zie voor meer informatie over hello Azure Toolkits voor IDE voor Java Hallo resources te volgen:

* [Azure Toolkit voor Eclipse]
  * [Wat is er nieuw in hello Azure Toolkit voor Eclipse]
  * [Hello Azure Toolkit voor Eclipse installeren]
  * [Aanmelden instructies voor het hello Azure Toolkit voor Eclipse]
  * [Een Hallo wereld-web-app maken voor Azure in Eclipse]
* [Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)
  * [Wat is er nieuw in hello Azure Toolkit voor IntelliJ]
  * [Hello Azure Toolkit voor IntelliJ installeren]
  * [aanmelden instructies voor hello Azure Toolkit voor IntelliJ]
  * [Een Hallo wereld-web-app maken voor Azure in IntelliJ]

Zie voor meer informatie over het gebruik van Azure met Java [Azure Java Developer Center] en [Java-Tools voor Visual Studio Team Services].

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld-web-app maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld-web-app maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Hello Azure Toolkit voor Eclipse installeren]: ./azure-toolkit-for-eclipse-installation.md
[Hello Azure Toolkit voor IntelliJ installeren]: ./azure-toolkit-for-intellij-installation.md
[Aanmelden instructies voor het hello Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[aanmelden instructies voor hello Azure Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Wat is er nieuw in hello Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/

[Grootten voor Windows virtuele machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Grootten voor virtuele Linux-machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Prijzen van virtuele machines in Windows]: /pricing/details/virtual-machines/windows/
[Prijzen van Linux virtuele machines]: /pricing/details/virtual-machines/linux/


<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
