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
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="92b4d-103">De installatie van de Azure Toolkit voor Eclipse</span><span class="sxs-lookup"><span data-stu-id="92b4d-103">Installing the Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="92b4d-104">De Azure-werkset voor Eclipse biedt sjablonen en functionaliteit kunt u gemakkelijk maken, ontwikkelen, testen en implementeren van Azure-toepassingen met behulp van de Eclipse-ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="92b4d-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the Eclipse development environment.</span></span> <span data-ttu-id="92b4d-105">De Azure-werkset voor Eclipse is een Open Source-project.</span><span class="sxs-lookup"><span data-stu-id="92b4d-105">The Azure Toolkit for Eclipse is an Open Source project.</span></span> <span data-ttu-id="92b4d-106">De broncode is beschikbaar in de MIT-licentie van <https://github.com/microsoft/azure-tools-for-java>.</span><span class="sxs-lookup"><span data-stu-id="92b4d-106">The source code is available under the MIT License from <https://github.com/microsoft/azure-tools-for-java>.</span></span>

<span data-ttu-id="92b4d-107">De volgende stappen laten zien hoe de Azure-werkset voor Eclipse installeren.</span><span class="sxs-lookup"><span data-stu-id="92b4d-107">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="92b4d-108">Voor het installeren van de Azure-werkset voor Eclipse</span><span class="sxs-lookup"><span data-stu-id="92b4d-108">To install the Azure Toolkit for Eclipse</span></span>
1. <span data-ttu-id="92b4d-109">Start Eclipse.</span><span class="sxs-lookup"><span data-stu-id="92b4d-109">Start Eclipse.</span></span>
2. <span data-ttu-id="92b4d-110">Klik op de **Help** menu en klik vervolgens op **nieuwe Software installeren**, zoals wordt weergegeven in de volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="92b4d-110">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
    ![De installatie van de Azure Toolkit voor Eclipse][01]
3. <span data-ttu-id="92b4d-112">In de **beschikbare Software** dialoogvenster, binnen de **werken met** in het tekstvak `http://dl.microsoft.com/eclipse` gevolgd door de **Enter** sleutel.</span><span class="sxs-lookup"><span data-stu-id="92b4d-112">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse` followed by the **Enter** key.</span></span>
4. <span data-ttu-id="92b4d-113">In de **naam** deelvenster controle **Azure Toolkit voor Eclipse**, en schakelt u **Neem contact op met alle updatewebsites tijdens de installatie vereiste software vinden**.</span><span class="sxs-lookup"><span data-stu-id="92b4d-113">In the **Name** pane, check **Azure Toolkit for Eclipse**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="92b4d-114">Uw scherm ziet er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="92b4d-114">Your screen should appear similar to the following:</span></span>
   
    ![De installatie van de Azure Toolkit voor Eclipse][02]
5. <span data-ttu-id="92b4d-116">Als u wilt uitbreiden de **Azure Toolkit voor Eclipse**, ziet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="92b4d-116">If you expand the **Azure Toolkit for Eclipse**, you will see the following items:</span></span>
   
   * <span data-ttu-id="92b4d-117">**Application Insights-invoegtoepassing voor Java**: dit onderdeel kunt u met Azure telemetrie logboekregistratie en analysis services voor uw toepassingen en serverinstanties.</span><span class="sxs-lookup"><span data-stu-id="92b4d-117">**Application Insights Plugin for Java**: This component allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span>
   * <span data-ttu-id="92b4d-118">**Azure Access Control-servicefilter**: dit onderdeel biedt ondersteuning voor het verifiëren van toepassingsgebruikers met Azure ACS, het inschakelen van eenmalige aanmelding scenario's en het externalizing logica van de identiteit van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="92b4d-118">**Azure Access Control Services Filter**: This component provides support for authenticating application users with Azure ACS, enabling single sign-on scenarios and externalizing identity logic from the application.</span></span>
   * <span data-ttu-id="92b4d-119">**Azure algemene invoegtoepassing**: dit onderdeel biedt de algemene functionaliteit die nodig zijn voor andere onderdelen van de toolkit.</span><span class="sxs-lookup"><span data-stu-id="92b4d-119">**Azure Common Plugin**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="92b4d-120">**Azure Explorer voor Eclipse**: dit onderdeel biedt de algemene functionaliteit die nodig zijn voor andere onderdelen van de toolkit.</span><span class="sxs-lookup"><span data-stu-id="92b4d-120">**Azure Explorer for Eclipse**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="92b4d-121">**Azure-invoegtoepassing voor Eclipse met Java**: dit onderdeel biedt ondersteuning voor het ontwikkelen van projecten waarmee bouwen, testen en implementeren van Java-toepassingen voor de Microsoft Azure-cloud in Eclipse en via de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="92b4d-121">**Azure Plugin for Eclipse with Java**: This component provides support for developing projects that help build, test and deploy Java applications for the Microsoft Azure cloud in Eclipse and via command line.</span></span>
   * <span data-ttu-id="92b4d-122">**Azure Web Apps invoegtoepassing met Java**: dit onderdeel biedt ondersteuning voor het implementeren van Java-webtoepassingen op Microsoft Azure Web App containers.</span><span class="sxs-lookup"><span data-stu-id="92b4d-122">**Azure Web Apps Plugin with Java**: This component provides support for deploying Java web applications to Microsoft Azure Web App containers.</span></span>
   * <span data-ttu-id="92b4d-123">**Microsoft JDBC-stuurprogramma 4.2 voor SQL Server**: dit onderdeel biedt JDBC API voor SQL Server en Microsoft Azure SQL Database voor Java Platform Enterprise Edition 8.</span><span class="sxs-lookup"><span data-stu-id="92b4d-123">**Microsoft JDBC Driver 4.2 for SQL Server**: This component provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span>
   * <span data-ttu-id="92b4d-124">**Pakket voor Apache Qpid clientbibliotheken voor JMS**: dit onderdeel biedt het clientonderdeel JMS uit het project Apache Qpid om te zorgen dat uw toepassing voor gebruik met AMQP messaging in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="92b4d-124">**Package for Apache Qpid Client Libraries for JMS**: This component provides the JMS client component from the Apache Qpid project to enable your application to use AMQP messaging in Microsoft Azure.</span></span>
   * <span data-ttu-id="92b4d-125">**Pakket voor Microsoft Azure-beheerbibliotheken voor Java**: dit onderdeel biedt API's voor toegang tot Microsoft Azure-services, zoals opslag, servicebus, service-runtime, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="92b4d-125">**Package for Microsoft Azure Libraries for Java**: This component provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span>
6. <span data-ttu-id="92b4d-126">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="92b4d-126">Click **Next**.</span></span> <span data-ttu-id="92b4d-127">(Als er vreemde vertragingen optreden bij het installeren van de toolkit, zorg ervoor dat **Neem contact op met alle updatewebsites tijdens de installatie vereiste software vinden** is uitgeschakeld.)</span><span class="sxs-lookup"><span data-stu-id="92b4d-127">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>
7. <span data-ttu-id="92b4d-128">In de **Details installeren** dialoogvenster, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="92b4d-128">In the **Install Details** dialog, click **Next**.</span></span>
   
    ![Bekijk de Details van de installatie][03]
8. <span data-ttu-id="92b4d-130">In de **licenties bekijken** dialoogvenster Lees de voorwaarden van de licentieovereenkomsten.</span><span class="sxs-lookup"><span data-stu-id="92b4d-130">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="92b4d-131">Als u de voorwaarden van de gebruiksrechtovereenkomst accepteert, klikt u op **ik ga akkoord met de voorwaarden van de licentieovereenkomsten** en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="92b4d-131">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="92b4d-132">(De resterende stappen wordt ervan uitgegaan dat u de voorwaarden van de licentievoorwaarden accepteert.</span><span class="sxs-lookup"><span data-stu-id="92b4d-132">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="92b4d-133">Als u de voorwaarden van de licentievoorwaarden niet accepteert, sluit u het installatieproces.)</span><span class="sxs-lookup"><span data-stu-id="92b4d-133">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
    ![Bekijk licenties][04]
   
    <span data-ttu-id="92b4d-135">Eclipse downloaden en installeren van de vereiste pakketten.</span><span class="sxs-lookup"><span data-stu-id="92b4d-135">Eclipse will download and install the requisite packages.</span></span>
   
    ![Installatievoortgang][05]
9. <span data-ttu-id="92b4d-137">Als u wordt gevraagd om opnieuw te starten Eclipse om installatie te voltooien, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="92b4d-137">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
    ![Prompt voor opnieuw opstarten][06]

## <a name="see-also"></a><span data-ttu-id="92b4d-139">Zie ook</span><span class="sxs-lookup"><span data-stu-id="92b4d-139">See Also</span></span>
<span data-ttu-id="92b4d-140">Voor meer informatie over de Azure Toolkits voor Java-IDE's klikt u op de volgende koppelingen:</span><span class="sxs-lookup"><span data-stu-id="92b4d-140">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="92b4d-141">[Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="92b4d-141">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="92b4d-142">[What's New in the Azure Toolkit for Eclipse] (Nieuw in de Azure Toolkit voor Eclipse)</span><span class="sxs-lookup"><span data-stu-id="92b4d-142">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="92b4d-143">*De installatie van de Azure Toolkit voor Eclipse (in dit artikel)*</span><span class="sxs-lookup"><span data-stu-id="92b4d-143">*Installing the Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="92b4d-144">[Sign In Instructions for the Azure Toolkit for Eclipse] (Aanmeldingsinstructies voor de Azure Toolkit voor Eclipse)</span><span class="sxs-lookup"><span data-stu-id="92b4d-144">[Sign In Instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="92b4d-145">[Een Hallo wereld Web-App maken voor Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="92b4d-145">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="92b4d-146">[Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="92b4d-146">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="92b4d-147">[What's New in the Azure Toolkit for IntelliJ] (Nieuw in de Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="92b4d-147">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="92b4d-148">[Installing the Azure Toolkit for IntelliJ] (De Azure Toolkit voor IntelliJ installeren)</span><span class="sxs-lookup"><span data-stu-id="92b4d-148">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="92b4d-149">[Sign In Instructions for the Azure Toolkit for IntelliJ] (Aanmeldingsinstructies voor de Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="92b4d-149">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="92b4d-150">[Een Hallo wereld Web-App maken voor Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="92b4d-150">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="92b4d-151">In het [Azure Java Developer Center] vindt u meer informatie over het gebruik van Azure met Java.</span><span class="sxs-lookup"><span data-stu-id="92b4d-151">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="92b4d-152">[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="92b4d-152">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="92b4d-153">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="92b4d-153">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="92b4d-154">[Een Hallo wereld Web-App maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="92b4d-154">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="92b4d-155">[Een Hallo wereld Web-App maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="92b4d-155">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
<span data-ttu-id="92b4d-156">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)</span><span class="sxs-lookup"><span data-stu-id="92b4d-156">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="92b4d-157">[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md (Aanmeldingsinstructies voor de Azure Toolkit voor Eclipse)</span><span class="sxs-lookup"><span data-stu-id="92b4d-157">[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="92b4d-158">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md (Aanmeldingsinstructies voor de Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="92b4d-158">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="92b4d-159">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md (Nieuw in de Azure Toolkit voor Eclipse)</span><span class="sxs-lookup"><span data-stu-id="92b4d-159">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="92b4d-160">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md (Nieuw in de Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="92b4d-160">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="92b4d-161">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="92b4d-161">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
