---
title: Wat is er nieuw in de Azure werkset voor IntelliJ | Microsoft Docs
description: Meer informatie over de nieuwste functies in de Azure-Toolkit voor IntelliJ.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 46ed791f-df59-416a-809e-f52345ad973c
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm;asirveda;martinsawicki
ms.openlocfilehash: 23714856f0f778be04cf321e0726b53ade430f57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="whats-new-in-the-azure-toolkit-for-intellij"></a>Wat is er nieuw in de Azure werkset voor IntelliJ
## <a name="azure-toolkit-for-intellij-releases"></a>Azure Toolkit voor IntelliJ-versies
In dit artikel bevat informatie over de verschillende versies en de meest recente updates voor de Azure-Toolkit voor IntelliJ.

> [!NOTE]
> Er is ook een Azure-werkset voor de Eclipse IDE. Zie voor meer informatie [Azure Toolkit voor Eclipse].
> 
> 

### <a name="april-14-2017"></a>14 april 2017
De Azure-werkset voor IntelliJ - release van April 2017 omvat de volgende verbeteringen:

* **Verbeterde Azure-aanmelding In ervaring**: de Azure-Toolkit voor IntelliJ ondersteunt nu twee methoden voor het aanmelden bij uw Azure-account: *interactief* en *automatisch*. Zie voor meer informatie [Azure aanmelding In instructies voor de Azure-werkset voor IntelliJ].
* **Publiceren met behulp van Docker Containers**: U kunt nu uw webtoepassingen publiceren als Docker-Containers met Azure-Toolkit voor IntelliJ. Zie voor meer informatie [het publiceren van een Web-App als een Docker-Container met de Azure-Toolkit voor IntelliJ].
* **Opslagbeheer voor Account**: de Azure-Toolkit voor IntelliJ biedt nu ondersteuning voor het beheer van uw storage-accounts vanuit de Verkenner-weergave van Azure. Zie voor meer informatie [beheren Storage-Accounts met de Azure-Explorer voor IntelliJ].
* **Virtual Machine Management**: de Azure-Toolkit voor IntelliJ biedt nu ondersteuning voor het beheren van uw virtuele machines in het venster Azure Explorer hulpprogramma. Zie voor meer informatie [het beheren van virtuele Machines met behulp van de Azure-Explorer voor IntelliJ].
* **Verwijderen van de extern-ondersteuning voor foutopsporing**. Foutopsporing op afstand van Java-web-apps op Azure App Service is verwijderd uit de werkset van Azure voor IntelliJ; Dit is het nodig zijn voor het oplossen van problemen die klanten zijn krijgen als ze met de toolkit.

### <a name="august-26-2016"></a>26 augustus 2016
De Azure-werkset voor IntelliJ - augustus 2016-release zijn de volgende uitbreidingen bevat:

* **Aangepaste JDK distributies**. De Azure-werkset voor IntelliJ ondersteunt nu opgeven en het implementeren van een willekeurige versie van de JDK aan uw Azure-Web-App-container:
  * Naast de JDKs verstrekt door Azure, kunt u ook kiezen uit een breed selectie van Zulu OpenJDK versies beschikbaar gesteld in Azure door Azul systemen.
  * U kunt ook uw eigen distributie JDK opgeven als u deze als een ZIP-bestand naar uw opslagaccount uploaden.
* **Verbeteringen in de weergave Azure Explorer**:
  * Ondersteuning voor het beheer van virtuele Machine met behulp van de nieuwe Resource Manager-model van Azure: u kunt weergeven, maken en verwijderen van resource manager gebaseerde virtuele machines zonder de IDE.
  * Ondersteuning voor het Opslagaccount blob beheren met behulp van Azure Resource Manager, die is een aanvulling op de bestaande functionaliteit voor het beheren van 'klassiek' storage-accounts.
* **Microsoft JDBC-stuurprogramma 6.0 voor SQL Server**. Deze update bevat de meest recente JDBC-stuurprogramma voor Microsoft SQL Server (6.0), die is nu opgenomen als een bibliotheek die u eenvoudig aan uw Java-projecten toevoegen kunt, waardoor de oudere versie vervangen.

### <a name="june-29-2016"></a>29 juni 2016
De Azure-werkset voor IntelliJ - release van juni 2016 omvat de volgende verbeteringen:

* **Java 8 vereiste**. De Azure-werkset voor IntelliJ vereist nu Java 8, hoewel deze vereiste alleen voor de toolkit geldt-uw toepassingen kunnen blijven gebruiken van alle versies van Java die worden ondersteund door Azure.
* **Ondersteuning voor de meest recente Java-JDKs**. De nieuwste versies van de Java-JDKs worden nu ondersteund door de Azure-Toolkit voor IntelliJ.
* **Ondersteuning voor Azure SDK v2.9.1**. De nieuwste versie van de Azure SDK is nu de minimale vereiste voor de Azure-werkset voor IntelliJ.
* **Voorbeelden geïntegreerd**. De Azure-werkset voor IntelliJ biedt nu verschillende voorbeeldtoepassingen waarmee ontwikkelaars aan de slag.
* **HDInsight-hulpprogramma integratie**. Azure HDInsight-hulpprogramma's worden nu gebundeld met de Azure-Toolkit voor IntelliJ. Zie voor meer informatie [invoegtoepassing HDInsight Tools for IntelliJ].
* **Foutopsporing op afstand van Java-Web-Apps**. De Azure-werkset voor IntelliJ biedt nu ondersteuning voor foutopsporing op afstand van Java-web-apps op Azure App Service.

### <a name="april-12-2016"></a>12 april 2016
De Azure-werkset voor IntelliJ - release van April 2016 omvat de volgende verbeteringen:

* **Ondersteuning voor Azure SDK v2.9.0**. De nieuwste versie van de Azure SDK is nu de minimale vereiste voor de Azure-werkset voor IntelliJ.
* **Diverse verbeteringen van bruikbaarheid, reactiesnelheid en prestaties gerelateerd aan Azure-Web-App ondersteuning**. Een aantal prestatieverbeteringen in hoe de Toolkit met Azure resultaat communiceert in een responsievere gebruikersinterface.
* **Mogelijkheid tot het verwijderen van een bestaande Web-App-container in Azure uit binnen IntelliJ**. De Azure-werkset voor IntelliJ kunt u nu een bestaande Azure-Web-container zonder IntelliJ verwijderen.

## <a name="see-also"></a>Zie ook
Voor meer informatie over de Azure Toolkits voor Java-IDE's klikt u op de volgende koppelingen:

* [Azure Toolkit voor Eclipse]
  * [What's New in the Azure Toolkit for Eclipse] (Nieuw in de Azure Toolkit voor Eclipse)
  * [Installing the Azure Toolkit for Eclipse] (De Azure Toolkit voor Eclipse installeren)
  * [Een Hallo wereld Web-App maken voor Azure in Eclipse]
  * [Sign In Instructions for the Azure Toolkit for Eclipse] (Aanmeldingsinstructies voor de Azure Toolkit voor Eclipse)
* [Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)
  * *Wat is er nieuw in de Azure werkset voor IntelliJ (in dit artikel)*
  * [Installing the Azure Toolkit for IntelliJ] (De Azure Toolkit voor IntelliJ installeren)
  * [Sign In Instructions for the Azure Toolkit for IntelliJ] (Aanmeldingsinstructies voor de Azure Toolkit voor IntelliJ)
  * [Een Hallo wereld Web-App maken voor Azure in IntelliJ]

In het [Azure Java Developer Center] vindt u meer informatie over het gebruik van Azure met Java.

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld Web-App maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld Web-App maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (De Azure Toolkit voor Eclipse installeren)
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)
[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md (Aanmeldingsinstructies voor de Azure Toolkit voor Eclipse)
[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md (Aanmeldingsinstructies voor de Azure Toolkit voor IntelliJ)
[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md (Nieuw in de Azure Toolkit voor Eclipse)
[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure aanmelding In instructies voor de Azure-werkset voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[het publiceren van een Web-App als een Docker-Container met de Azure-Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[beheren Storage-Accounts met de Azure-Explorer voor IntelliJ]: ./azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer.md
[het beheren van virtuele Machines met behulp van de Azure-Explorer voor IntelliJ]: ./azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer.md

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547

[invoegtoepassing HDInsight Tools for IntelliJ]: ./hdinsight/hdinsight-apache-spark-intellij-tool-plugin.md
