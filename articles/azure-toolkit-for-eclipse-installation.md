---
title: De installatie van de Azure Toolkit voor Eclipse | Microsoft Docs
description: Informatie over het installeren van de Azure-werkset voor Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35cddba38c364dfb2f6a8646b0014d48ca4cb795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a>De installatie van de Azure Toolkit voor Eclipse
De Azure-werkset voor Eclipse biedt sjablonen en functionaliteit kunt u gemakkelijk maken, ontwikkelen, testen en implementeren van Azure-toepassingen met behulp van de Eclipse-ontwikkelomgeving. De Azure-werkset voor Eclipse is een Open Source-project. De broncode is beschikbaar in de MIT-licentie van <https://github.com/microsoft/azure-tools-for-java>.

De volgende stappen laten zien hoe de Azure-werkset voor Eclipse installeren.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a>Voor het installeren van de Azure-werkset voor Eclipse
1. Start Eclipse.
2. Klik op de **Help** menu en klik vervolgens op **nieuwe Software installeren**, zoals wordt weergegeven in de volgende afbeelding.
   
    ![De installatie van de Azure Toolkit voor Eclipse][01]
3. In de **beschikbare Software** dialoogvenster, binnen de **werken met** in het tekstvak `http://dl.microsoft.com/eclipse` gevolgd door de **Enter** sleutel.
4. In de **naam** deelvenster controle **Azure Toolkit voor Eclipse**, en schakelt u **Neem contact op met alle updatewebsites tijdens de installatie vereiste software vinden**. Uw scherm ziet er ongeveer als volgt:
   
    ![De installatie van de Azure Toolkit voor Eclipse][02]
5. Als u wilt uitbreiden de **Azure Toolkit voor Eclipse**, ziet u de volgende items:
   
   * **Application Insights-invoegtoepassing voor Java**: dit onderdeel kunt u met Azure telemetrie logboekregistratie en analysis services voor uw toepassingen en serverinstanties.
   * **Azure Access Control-servicefilter**: dit onderdeel biedt ondersteuning voor het verifiëren van toepassingsgebruikers met Azure ACS, het inschakelen van eenmalige aanmelding scenario's en het externalizing logica van de identiteit van de toepassing.
   * **Azure algemene invoegtoepassing**: dit onderdeel biedt de algemene functionaliteit die nodig zijn voor andere onderdelen van de toolkit.
   * **Azure Explorer voor Eclipse**: dit onderdeel biedt de algemene functionaliteit die nodig zijn voor andere onderdelen van de toolkit.
   * **Azure-invoegtoepassing voor Eclipse met Java**: dit onderdeel biedt ondersteuning voor het ontwikkelen van projecten waarmee bouwen, testen en implementeren van Java-toepassingen voor de Microsoft Azure-cloud in Eclipse en via de opdrachtregel.
   * **Azure Web Apps invoegtoepassing met Java**: dit onderdeel biedt ondersteuning voor het implementeren van Java-webtoepassingen op Microsoft Azure Web App containers.
   * **Microsoft JDBC-stuurprogramma 4.2 voor SQL Server**: dit onderdeel biedt JDBC API voor SQL Server en Microsoft Azure SQL Database voor Java Platform Enterprise Edition 8.
   * **Pakket voor Apache Qpid clientbibliotheken voor JMS**: dit onderdeel biedt het clientonderdeel JMS uit het project Apache Qpid om te zorgen dat uw toepassing voor gebruik met AMQP messaging in Microsoft Azure.
   * **Pakket voor Microsoft Azure-beheerbibliotheken voor Java**: dit onderdeel biedt API's voor toegang tot Microsoft Azure-services, zoals opslag, servicebus, service-runtime, enzovoort.
6. Klik op **Volgende**. (Als er vreemde vertragingen optreden bij het installeren van de toolkit, zorg ervoor dat **Neem contact op met alle updatewebsites tijdens de installatie vereiste software vinden** is uitgeschakeld.)
7. In de **Details installeren** dialoogvenster, klikt u op **volgende**.
   
    ![Bekijk de Details van de installatie][03]
8. In de **licenties bekijken** dialoogvenster Lees de voorwaarden van de licentieovereenkomsten. Als u de voorwaarden van de gebruiksrechtovereenkomst accepteert, klikt u op **ik ga akkoord met de voorwaarden van de licentieovereenkomsten** en klik vervolgens op **voltooien**. (De resterende stappen wordt ervan uitgegaan dat u de voorwaarden van de licentievoorwaarden accepteert. Als u de voorwaarden van de licentievoorwaarden niet accepteert, sluit u het installatieproces.)
   
    ![Bekijk licenties][04]
   
    Eclipse downloaden en installeren van de vereiste pakketten.
   
    ![Installatievoortgang][05]
9. Als u wordt gevraagd om opnieuw te starten Eclipse om installatie te voltooien, klikt u op **Ja**.
   
    ![Prompt voor opnieuw opstarten][06]

## <a name="see-also"></a>Zie ook
Voor meer informatie over de Azure Toolkits voor Java-IDE's klikt u op de volgende koppelingen:

* [Azure Toolkit voor Eclipse]
  * [What's New in the Azure Toolkit for Eclipse] (Nieuw in de Azure Toolkit voor Eclipse)
  * *De installatie van de Azure Toolkit voor Eclipse (in dit artikel)*
  * [Sign In Instructions for the Azure Toolkit for Eclipse] (Aanmeldingsinstructies voor de Azure Toolkit voor Eclipse)
  * [Een Hallo wereld Web-App maken voor Azure in Eclipse]
* [Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)
  * [What's New in the Azure Toolkit for IntelliJ] (Nieuw in de Azure Toolkit voor IntelliJ)
  * [Installing the Azure Toolkit for IntelliJ] (De Azure Toolkit voor IntelliJ installeren)
  * [Sign In Instructions for the Azure Toolkit for IntelliJ] (Aanmeldingsinstructies voor de Azure Toolkit voor IntelliJ)
  * [Een Hallo wereld Web-App maken voor Azure in IntelliJ]

In het [Azure Java Developer Center] vindt u meer informatie over het gebruik van Azure met Java.

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld Web-App maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld Web-App maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)
[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md (Aanmeldingsinstructies voor de Azure Toolkit voor Eclipse)
[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md (Aanmeldingsinstructies voor de Azure Toolkit voor IntelliJ)
[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md (Nieuw in de Azure Toolkit voor Eclipse)
[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md (Nieuw in de Azure Toolkit voor IntelliJ)

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
