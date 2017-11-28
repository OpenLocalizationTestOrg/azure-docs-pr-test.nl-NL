---
title: Installeren van de lokale data gateway - Azure Logic Apps | Microsoft Docs
description: Voordat u toegang gegevensbronnen on-premises tot, installeert u de lokale data gateway voor snelle gegevensoverdracht en -versleuteling tussen on-premises gegevensbronnen en logic apps
keywords: toegang tot gegevens, op de lokale, gegevensoverdracht, versleuteling en gegevensbronnen
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 34e68ae7d35019848b35c785a2715ec458dc6e73
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="install-the-on-premises-data-gateway-for-azure-logic-apps"></a><span data-ttu-id="12369-104">De lokale data gateway voor Azure Logic Apps installeren</span><span class="sxs-lookup"><span data-stu-id="12369-104">Install the on-premises data gateway for Azure Logic Apps</span></span>

<span data-ttu-id="12369-105">Om uw logische apps toegang on-premises gegevensbronnen tot, moet u het installeren en instellen van de lokale data gateway.</span><span class="sxs-lookup"><span data-stu-id="12369-105">Before your logic apps can access data sources on premises, you must install and set up the on-premises data gateway.</span></span> <span data-ttu-id="12369-106">De gateway fungeert als een brug waarmee snelle gegevensoverdracht en -versleuteling tussen on-premises systemen en uw logische apps.</span><span class="sxs-lookup"><span data-stu-id="12369-106">The gateway acts as a bridge that provides quick data transfer and encryption between on-premises systems and your logic apps.</span></span> <span data-ttu-id="12369-107">De gateway stuurt gegevens van lokale bronnen op gecodeerde kanalen via de Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="12369-107">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="12369-108">Al het verkeer afkomstig is als beveiligde uitgaand verkeer van de gateway-agent.</span><span class="sxs-lookup"><span data-stu-id="12369-108">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="12369-109">Meer informatie over [de werking van de gegevensgateway](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="12369-109">Learn more about [how the data gateway works](#gateway-cloud-service).</span></span>

<span data-ttu-id="12369-110">De gateway ondersteunt verbindingen met deze gegevensbronnen on-premises:</span><span class="sxs-lookup"><span data-stu-id="12369-110">The gateway supports connections to these data sources on premises:</span></span>

*   <span data-ttu-id="12369-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="12369-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="12369-112">DB2</span><span class="sxs-lookup"><span data-stu-id="12369-112">DB2</span></span>  
*   <span data-ttu-id="12369-113">Bestandssysteem</span><span class="sxs-lookup"><span data-stu-id="12369-113">File System</span></span>
*   <span data-ttu-id="12369-114">Informix</span><span class="sxs-lookup"><span data-stu-id="12369-114">Informix</span></span>
*   <span data-ttu-id="12369-115">MQ</span><span class="sxs-lookup"><span data-stu-id="12369-115">MQ</span></span>
*   <span data-ttu-id="12369-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="12369-116">MySQL</span></span>
*   <span data-ttu-id="12369-117">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="12369-117">Oracle Database</span></span>
*   <span data-ttu-id="12369-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="12369-118">PostgreSQL</span></span>
*   <span data-ttu-id="12369-119">SAP-toepassingsserver</span><span class="sxs-lookup"><span data-stu-id="12369-119">SAP Application Server</span></span> 
*   <span data-ttu-id="12369-120">SAP-berichtenserver</span><span class="sxs-lookup"><span data-stu-id="12369-120">SAP Message Server</span></span>
*   <span data-ttu-id="12369-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="12369-121">SharePoint</span></span>
*   <span data-ttu-id="12369-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="12369-122">SQL Server</span></span>
*   <span data-ttu-id="12369-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="12369-123">Teradata</span></span>

<span data-ttu-id="12369-124">Deze stappen laten zien hoe u de lokale data gateway voordat u het eerst installeert [instellen van een verbinding tussen de gateway en uw logische apps](./logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="12369-124">These steps show how to first install the on-premises data gateway before you [set up a connection between the gateway and your logic apps](./logic-apps-gateway-connection.md).</span></span> <span data-ttu-id="12369-125">Zie voor meer informatie over ondersteunde connectors [Connectors voor Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="12369-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span> 

<span data-ttu-id="12369-126">Zie voor informatie over het gebruik van de gateway met andere services, deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="12369-126">For information about how to use the gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="12369-127">Microsoft Power BI lokale gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="12369-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="12369-128">Azure Analysis Services op locatie gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="12369-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="12369-129">Microsoft-Flow lokale gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="12369-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="12369-130">Microsoft PowerApps lokale gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="12369-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a><span data-ttu-id="12369-131">Vereisten</span><span class="sxs-lookup"><span data-stu-id="12369-131">Requirements</span></span>

<span data-ttu-id="12369-132">**Minimale**:</span><span class="sxs-lookup"><span data-stu-id="12369-132">**Minimum**:</span></span>

* <span data-ttu-id="12369-133">.NET 4.5 framework</span><span class="sxs-lookup"><span data-stu-id="12369-133">.NET 4.5 Framework</span></span>
* <span data-ttu-id="12369-134">64-bits versie van Windows 7 of Windows Server 2008 R2 (of hoger)</span><span class="sxs-lookup"><span data-stu-id="12369-134">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="12369-135">**Aanbevolen**:</span><span class="sxs-lookup"><span data-stu-id="12369-135">**Recommended**:</span></span>

* <span data-ttu-id="12369-136">8-core CPU</span><span class="sxs-lookup"><span data-stu-id="12369-136">8 Core CPU</span></span>
* <span data-ttu-id="12369-137">8 GB geheugen</span><span class="sxs-lookup"><span data-stu-id="12369-137">8 GB Memory</span></span>
* <span data-ttu-id="12369-138">64-bits versie van Windows 2012 R2 (of hoger)</span><span class="sxs-lookup"><span data-stu-id="12369-138">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="12369-139">**Belangrijke overwegingen**:</span><span class="sxs-lookup"><span data-stu-id="12369-139">**Important considerations**:</span></span>

* <span data-ttu-id="12369-140">De lokale data gateway alleen op een lokale computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="12369-140">Install the on-premises data gateway only on a local computer.</span></span>
<span data-ttu-id="12369-141">U kunt de gateway niet installeren op een domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="12369-141">You can't install the gateway on a domain controller.</span></span>

   > [!TIP]
   > <span data-ttu-id="12369-142">Er geen gateway installeren op dezelfde computer als uw gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="12369-142">You don't have to install the gateway on the same computer as your data source.</span></span> <span data-ttu-id="12369-143">Om latentie te beperken, kunt u de gateway zo dicht mogelijk tot de gegevensbron, of op dezelfde computer, ervan uitgaande dat u gemachtigd installeren.</span><span class="sxs-lookup"><span data-stu-id="12369-143">To minimize latency, you can install the gateway as close as possible to your data source, or on the same computer, assuming that you have permissions.</span></span>

* <span data-ttu-id="12369-144">Installeer de gateway niet op een computer die wordt uitgeschakeld, gaat u naar de slaapstand, of geen verbinding maken met Internet, omdat de gateway kan niet worden uitgevoerd in deze omstandigheden.</span><span class="sxs-lookup"><span data-stu-id="12369-144">Don't install the gateway on a computer that turns off, goes to sleep, or doesn't connect to the Internet because the gateway can't run under those circumstances.</span></span> <span data-ttu-id="12369-145">Ook de prestaties van de gateway via een draadloos netwerk kan afnemen.</span><span class="sxs-lookup"><span data-stu-id="12369-145">Also, gateway performance might suffer over a wireless network.</span></span>

* <span data-ttu-id="12369-146">Tijdens de installatie, moet u zich aanmelden met een [werk- of schoolaccount](https://docs.microsoft.com/azure/active-directory/sign-up-organization) die wordt beheerd door Azure Active Directory (Azure AD), niet in een Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="12369-146">During installation, you must sign in with a [work or school account](https://docs.microsoft.com/azure/active-directory/sign-up-organization) that's managed by Azure Active Directory (Azure AD), not a Microsoft account.</span></span> 

  <span data-ttu-id="12369-147">U moet dezelfde werk- of schoolaccount verderop in de Azure portal gebruiken bij het maken en koppelen van een gateway-resource met de gateway-installatie.</span><span class="sxs-lookup"><span data-stu-id="12369-147">You have to use the same work or school account later in the Azure portal when you create and associate a gateway resource with your gateway installation.</span></span> <span data-ttu-id="12369-148">Selecteer deze gateway resource vervolgens in bij het maken van de verbinding tussen uw logische app en de on-premises gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="12369-148">You then select this gateway resource when you create the connection between your logic app and the on-premises data source.</span></span> [<span data-ttu-id="12369-149">Waarom moet ik een Azure AD werk- of schoolaccount?</span><span class="sxs-lookup"><span data-stu-id="12369-149">Why must I use an Azure AD work or school account?</span></span>](#why-azure-work-school-account)

  > [!TIP]
  > <span data-ttu-id="12369-150">Als u zich registreerde voor een Office 365-aanbieding en uw werkelijke Werke-mailadres niet opgeven, uw adres aanmelden als volgt uitzien jeff@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="12369-150">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span></span> 

* <span data-ttu-id="12369-151">Als u een bestaande gateway die u hebt ingesteld met een installatieprogramma dat ouder is dan versie 14.16.6317.4 hebt, kunt u uw gateway locatie niet wijzigen door het uitvoeren van de meest recente versie installer.</span><span class="sxs-lookup"><span data-stu-id="12369-151">If you have an existing gateway that you set up with an installer that's earlier than version 14.16.6317.4, you can't change your gateway's location by running the latest installer.</span></span> <span data-ttu-id="12369-152">Echter, kunt u het meest recente installatieprogramma voor het instellen van een nieuwe gateway met de locatie die u in plaats daarvan wilt.</span><span class="sxs-lookup"><span data-stu-id="12369-152">However, you can use the latest installer to set up a new gateway with the location that you want instead.</span></span>
  
  <span data-ttu-id="12369-153">Als u een gateway-installatieprogramma dat ouder is dan versie 14.16.6317.4 hebben, maar u kunt uw gateway nog niet geïnstalleerd maar kunt u downloaden en het meest recente installatieprogramma gebruiken.</span><span class="sxs-lookup"><span data-stu-id="12369-153">If you have a gateway installer that's earlier than version 14.16.6317.4, but you haven't installed your gateway yet, you can download and use the latest installer.</span></span>

<a name="install-gateway"></a>

## <a name="install-the-data-gateway"></a><span data-ttu-id="12369-154">De gegevensgateway installeren</span><span class="sxs-lookup"><span data-stu-id="12369-154">Install the data gateway</span></span>

1.  <span data-ttu-id="12369-155">[Downloaden en uitvoeren van het installatieprogramma van de gateway op een lokale computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="12369-155">[Download and run the gateway installer on a local computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span></span>

2. <span data-ttu-id="12369-156">Lees en accepteer de gebruiksvoorwaarden en de privacyverklaring.</span><span class="sxs-lookup"><span data-stu-id="12369-156">Review and accept the terms of use and privacy statement.</span></span>

3. <span data-ttu-id="12369-157">Geef het pad op de lokale computer waarop u wilt installeren van de gateway.</span><span class="sxs-lookup"><span data-stu-id="12369-157">Specify the path on your local computer where you want to install the gateway.</span></span>

4. <span data-ttu-id="12369-158">Wanneer u wordt gevraagd, meld u aan met uw Azure werk- of schoolaccount, niet in een Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="12369-158">When prompted, sign in with your Azure work or school account, not a Microsoft account.</span></span>

   ![Meld u aan met Azure werk- of schoolaccount](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. <span data-ttu-id="12369-160">Nu registreren van uw gateway is geïnstalleerd met de [gateway-cloudservice](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="12369-160">Now register your installed gateway with the [gateway cloud service](#gateway-cloud-service).</span></span> <span data-ttu-id="12369-161">Kies **registreren van een nieuwe gateway op deze computer**.</span><span class="sxs-lookup"><span data-stu-id="12369-161">Choose **Register a new gateway on this computer**.</span></span>

   <span data-ttu-id="12369-162">De gateway cloudservice versleutelt en slaat de referenties van de gegevensbron en de details van de gateway.</span><span class="sxs-lookup"><span data-stu-id="12369-162">The gateway cloud service encrypts and stores your data source credentials and gateway details.</span></span> 
   <span data-ttu-id="12369-163">De service Routering ook query's en de resultaten tussen uw logische app, de lokale data gateway en uw gegevensbron on-premises.</span><span class="sxs-lookup"><span data-stu-id="12369-163">The service also routes queries and their results between your logic app, the on-premises data gateway, and your data source on premises.</span></span>

6. <span data-ttu-id="12369-164">Geef een naam voor uw gateway-installatie.</span><span class="sxs-lookup"><span data-stu-id="12369-164">Provide a name for your gateway installation.</span></span> <span data-ttu-id="12369-165">Een herstelsleutel maken en bevestig vervolgens uw herstelsleutel.</span><span class="sxs-lookup"><span data-stu-id="12369-165">Create a recovery key, then confirm your recovery key.</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="12369-166">De herstelsleutel moet ten minste acht tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="12369-166">Your recovery key must contain at least eight characters.</span></span> <span data-ttu-id="12369-167">Zorg ervoor dat u opslaat en de sleutel op een veilige plaats bewaren.</span><span class="sxs-lookup"><span data-stu-id="12369-167">Make sure that you save and keep the key in a safe place.</span></span> <span data-ttu-id="12369-168">U moet deze sleutel ook als u wilt migreren, herstellen of overnemen van een bestaande gateway.</span><span class="sxs-lookup"><span data-stu-id="12369-168">You also need this key when you want to migrate, restore, or take over an existing gateway.</span></span>

   1. <span data-ttu-id="12369-169">Als u de standaardregio voor de gateway-cloudservice en de Azure Service Bus gebruikt door de gateway-installatie wijzigen kiezen **regio wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="12369-169">To change the default region for the gateway cloud service and Azure Service Bus used by your gateway installation, choose **Change Region**.</span></span>

      ![Wijziging regio](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      <span data-ttu-id="12369-171">De standaardregio is de regio die is gekoppeld aan uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="12369-171">The default region is the region associated with your Azure AD tenant.</span></span>

   2. <span data-ttu-id="12369-172">Open op het volgende venster de **regio selecteren** kiezen van een andere regio.</span><span class="sxs-lookup"><span data-stu-id="12369-172">On the next pane, open the **Select Region** to choose a different region.</span></span>

      ![Selecteer een andere regio](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      <span data-ttu-id="12369-174">U kunt bijvoorbeeld dezelfde regio als uw logische app selecteren of de regio die het dichtst bij uw on-premises gegevensbron selecteren zodat de latentie te verminderen.</span><span class="sxs-lookup"><span data-stu-id="12369-174">For example, you might select the same region as your logic app, or select the region closest to your on-premises data source so you can reduce latency.</span></span> <span data-ttu-id="12369-175">Uw gateway en logica voor resource app hebben verschillende locaties.</span><span class="sxs-lookup"><span data-stu-id="12369-175">Your gateway resource and logic app can have different locations.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="12369-176">U kunt deze regio niet wijzigen na de installatie.</span><span class="sxs-lookup"><span data-stu-id="12369-176">You can't change this region after installation.</span></span> <span data-ttu-id="12369-177">Deze regio bepaalt ook en Hiermee beperkt u de locatie waar u de Azure-resource voor uw gateway kunt maken.</span><span class="sxs-lookup"><span data-stu-id="12369-177">This region also determines and restricts the location where you can create the Azure resource for your gateway.</span></span> <span data-ttu-id="12369-178">Dus als u uw gateway-resource in Azure maakt, zorg ervoor dat de Resourcelocatie overeenkomt met de regio die u hebt geselecteerd tijdens de installatie van de gateway.</span><span class="sxs-lookup"><span data-stu-id="12369-178">So when you create your gateway resource in Azure, make sure that the resource location matches the region that you selected during gateway installation.</span></span>
      > 
      > <span data-ttu-id="12369-179">Als u wilt een andere regio voor uw gateway om later te gebruiken, moet u een nieuwe gateway instellen.</span><span class="sxs-lookup"><span data-stu-id="12369-179">If you want to use a different region for your gateway later, you must set up a new gateway.</span></span>

   3. <span data-ttu-id="12369-180">Als u klaar bent, kiest u **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="12369-180">When you're ready, choose **Done**.</span></span>

7. <span data-ttu-id="12369-181">Nu als volgt te werk in de Azure portal zodat u kunt [maken van een Azure-resource voor uw gateway](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="12369-181">Now follow these steps in the Azure portal so you can [create an Azure resource for your gateway](../logic-apps/logic-apps-gateway-connection.md).</span></span> 

<span data-ttu-id="12369-182">Meer informatie over [de werking van de gegevensgateway](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="12369-182">Learn more about [how the data gateway works](#gateway-cloud-service).</span></span>

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a><span data-ttu-id="12369-183">Migreren, herstellen of overnemen van een bestaande gateway</span><span class="sxs-lookup"><span data-stu-id="12369-183">Migrate, restore, or take over an existing gateway</span></span>

<span data-ttu-id="12369-184">Om deze taken uitvoeren, moet u de herstelsleutel die is opgegeven voor de gateway is geïnstalleerd hebben.</span><span class="sxs-lookup"><span data-stu-id="12369-184">To perform these tasks, you must have the recovery key that was specified when the gateway was installed.</span></span>

1. <span data-ttu-id="12369-185">Kies in het menu Start uw computer **On-premises gegevensgateway**.</span><span class="sxs-lookup"><span data-stu-id="12369-185">From your computer's Start menu, choose **On-premises data gateway**.</span></span>

2. <span data-ttu-id="12369-186">Nadat het installatieprogramma wordt geopend, meld u aan met hetzelfde Azure werk- of schoolaccount dat eerder werd gebruikt voor het installeren van de gateway.</span><span class="sxs-lookup"><span data-stu-id="12369-186">After the installer opens, sign in with the same Azure work or school account that was previously used to install the gateway.</span></span>

3. <span data-ttu-id="12369-187">Kies **migreren, herstellen of overnemen van een bestaande gateway**.</span><span class="sxs-lookup"><span data-stu-id="12369-187">Choose **Migrate, restore, or take over an existing gateway**.</span></span>

4. <span data-ttu-id="12369-188">Geef de naam en herstel sleutel voor de gateway die u wilt migreren, herstellen of overnemen.</span><span class="sxs-lookup"><span data-stu-id="12369-188">Provide the name and recovery key for the gateway that you want to migrate, restore, or take over.</span></span>

<a name="restart-gateway"></a>
## <a name="restart-the-gateway"></a><span data-ttu-id="12369-189">Start de gateway opnieuw</span><span class="sxs-lookup"><span data-stu-id="12369-189">Restart the gateway</span></span>

<span data-ttu-id="12369-190">De gateway wordt uitgevoerd als een Windows-service.</span><span class="sxs-lookup"><span data-stu-id="12369-190">The gateway runs as a Windows service.</span></span> <span data-ttu-id="12369-191">U kunt net als elke andere Windows-service starten en stoppen van de service op verschillende manieren.</span><span class="sxs-lookup"><span data-stu-id="12369-191">Like any other Windows service, you can start and stop the service in multiple ways.</span></span> <span data-ttu-id="12369-192">U kunt bijvoorbeeld open een opdrachtprompt met verhoogde machtigingen op de computer waarop de gateway wordt uitgevoerd, en beide deze opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="12369-192">For example, you can open a command prompt with elevated permissions on the computer where the gateway is running, and run either these commands:</span></span>

* <span data-ttu-id="12369-193">Voor het stoppen van de service, moet u deze opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="12369-193">To stop the service, run this command:</span></span>
  
    `net stop PBIEgwService`

* <span data-ttu-id="12369-194">De service wilt starten, moet u deze opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="12369-194">To start the service, run this command:</span></span>
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a><span data-ttu-id="12369-195">Windows-serviceaccount</span><span class="sxs-lookup"><span data-stu-id="12369-195">Windows service account</span></span>

<span data-ttu-id="12369-196">De lokale data gateway is ingesteld om te gebruiken `NT SERVICE\PBIEgwService` aanmeldingsreferenties voor het Windows-service.</span><span class="sxs-lookup"><span data-stu-id="12369-196">The on-premises data gateway is set up to use `NT SERVICE\PBIEgwService` for the Windows service logon credentials.</span></span> <span data-ttu-id="12369-197">De gateway heeft standaard het recht 'Aanmelden als service' voor de computer waarop u de gateway installeert.</span><span class="sxs-lookup"><span data-stu-id="12369-197">By default, the gateway has the "Log on as a service" right for the machine where you install the gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="12369-198">Het Windows-service-account verschilt van het account dat wordt gebruikt voor het verbinden met on-premises gegevens bronnen, en van de Azure werk- of schoolaccount gebruikt voor aanmelding bij cloud-services.</span><span class="sxs-lookup"><span data-stu-id="12369-198">The Windows service account differs from the account used for connecting to on-premises data sources, and from the Azure work or school account used to sign in to cloud services.</span></span>

## <a name="configure-a-firewall-or-proxy"></a><span data-ttu-id="12369-199">Een firewall of proxy configureren</span><span class="sxs-lookup"><span data-stu-id="12369-199">Configure a firewall or proxy</span></span>

<span data-ttu-id="12369-200">De gateway maakt een uitgaande verbinding met [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="12369-200">The gateway creates an outbound connection to [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="12369-201">Om proxyinformatie te verstrekken voor uw gateway, Zie [proxy-instellingen configureren](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span><span class="sxs-lookup"><span data-stu-id="12369-201">To provide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span></span>

<span data-ttu-id="12369-202">Controleer of uw machine daadwerkelijk verbinding met internet maken kan om te controleren of uw firewall of proxy, verbindingen mogelijk blokkeren, en de [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="12369-202">To check whether your firewall, or proxy, might block connections, confirm whether your machine can actually connect to the internet and the [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="12369-203">Vanuit een PowerShell-prompt, moet u deze opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="12369-203">From a PowerShell prompt, run this command:</span></span>

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> <span data-ttu-id="12369-204">Met deze opdracht wordt enkel tests netwerkverbinding en een verbinding met de Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="12369-204">This command only tests network connectivity and connectivity to the Azure Service Bus.</span></span> <span data-ttu-id="12369-205">De opdracht heeft dus niets te maken met de gateway of de gateway-cloudservice die versleutelt en slaat uw referenties en de details van de gateway geen.</span><span class="sxs-lookup"><span data-stu-id="12369-205">So the command doesn't have anything to do with the gateway or the gateway cloud service that encrypts and stores your credentials and gateway details.</span></span> 
>
> <span data-ttu-id="12369-206">Ook deze opdracht is alleen beschikbaar op Windows Server 2012 R2 of hoger, en Windows 8.1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="12369-206">Also, this command is only available on Windows Server 2012 R2 or later, and Windows 8.1 or later.</span></span> <span data-ttu-id="12369-207">In eerdere versies van het besturingssysteem, kunt u Telnet-connectiviteit testen.</span><span class="sxs-lookup"><span data-stu-id="12369-207">On earlier OS versions, you can use Telnet to test connectivity.</span></span> <span data-ttu-id="12369-208">Meer informatie over [Azure Service Bus- en hybride oplossingen](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="12369-208">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

<span data-ttu-id="12369-209">De resultaten moeten uitzien in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="12369-209">Your results should look similar to this example:</span></span>

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

<span data-ttu-id="12369-210">Als **TcpTestSucceeded** niet is ingesteld op **True**, u mogelijk geblokkeerd door een firewall.</span><span class="sxs-lookup"><span data-stu-id="12369-210">If **TcpTestSucceeded** is not set to **True**, you might be blocked by a firewall.</span></span> <span data-ttu-id="12369-211">Als u worden uitgebreid wilt, vervangen door de **ComputerName** en **poort** waarden met de waarden die worden vermeld onder [poorten configureren](#configure-ports) in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="12369-211">If you want to be comprehensive, substitute the **ComputerName** and **Port** values with the values listed under [Configure ports](#configure-ports) in this topic.</span></span>

<span data-ttu-id="12369-212">De firewall blokkeren mogelijk ook verbindingen waarmee de Azure Service Bus in de Azure-datacenters.</span><span class="sxs-lookup"><span data-stu-id="12369-212">The firewall might also block connections that the Azure Service Bus makes to the Azure datacenters.</span></span> <span data-ttu-id="12369-213">Als u dit scenario gebeurt, goedkeuren (deblokkeren) de IP-adressen die datacenters in uw regio.</span><span class="sxs-lookup"><span data-stu-id="12369-213">If this scenario happens, approve (unblock) all the IP addresses for those datacenters in your region.</span></span> <span data-ttu-id="12369-214">Voor deze IP-adressen [ophalen van de Azure-IP-adressen lijst hier](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="12369-214">For those IP addresses, [get the Azure IP addresses list here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

## <a name="configure-ports"></a><span data-ttu-id="12369-215">Poorten configureren</span><span class="sxs-lookup"><span data-stu-id="12369-215">Configure ports</span></span>

<span data-ttu-id="12369-216">De gateway maakt een uitgaande verbinding met [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) en op uitgaande poorten communiceert: TCP 443 (standaard), 5671, 5672, 9350 via 9354.</span><span class="sxs-lookup"><span data-stu-id="12369-216">The gateway creates an outbound connection to [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span> <span data-ttu-id="12369-217">De gateway nodig niet poorten voor inkomend verkeer.</span><span class="sxs-lookup"><span data-stu-id="12369-217">The gateway doesn't require inbound ports.</span></span> <span data-ttu-id="12369-218">Meer informatie over [Azure Service Bus- en hybride oplossingen](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="12369-218">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

| <span data-ttu-id="12369-219">DOMEINNAMEN</span><span class="sxs-lookup"><span data-stu-id="12369-219">DOMAIN NAMES</span></span> | <span data-ttu-id="12369-220">UITGAANDE POORTEN</span><span class="sxs-lookup"><span data-stu-id="12369-220">OUTBOUND PORTS</span></span> | <span data-ttu-id="12369-221">BESCHRIJVING</span><span class="sxs-lookup"><span data-stu-id="12369-221">DESCRIPTION</span></span> |
| --- | --- | --- |
| <span data-ttu-id="12369-222">*. analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="12369-222">*.analysis.windows.net</span></span> | <span data-ttu-id="12369-223">443</span><span class="sxs-lookup"><span data-stu-id="12369-223">443</span></span> | <span data-ttu-id="12369-224">HTTPS</span><span class="sxs-lookup"><span data-stu-id="12369-224">HTTPS</span></span> | 
| <span data-ttu-id="12369-225">*. login.windows.net</span><span class="sxs-lookup"><span data-stu-id="12369-225">*.login.windows.net</span></span> | <span data-ttu-id="12369-226">443</span><span class="sxs-lookup"><span data-stu-id="12369-226">443</span></span> | <span data-ttu-id="12369-227">HTTPS</span><span class="sxs-lookup"><span data-stu-id="12369-227">HTTPS</span></span> | 
| <span data-ttu-id="12369-228">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="12369-228">*.servicebus.windows.net</span></span> | <span data-ttu-id="12369-229">5671-5672</span><span class="sxs-lookup"><span data-stu-id="12369-229">5671-5672</span></span> | <span data-ttu-id="12369-230">Geavanceerde Message Queuing-Protocol (AMQP)</span><span class="sxs-lookup"><span data-stu-id="12369-230">Advanced Message Queuing Protocol (AMQP)</span></span> | 
| <span data-ttu-id="12369-231">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="12369-231">*.servicebus.windows.net</span></span> | <span data-ttu-id="12369-232">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="12369-232">443, 9350-9354</span></span> | <span data-ttu-id="12369-233">Listeners op Service Bus Relay via TCP (443 voor toegangsbeheer token aanschaf vereist)</span><span class="sxs-lookup"><span data-stu-id="12369-233">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> | 
| <span data-ttu-id="12369-234">*. frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="12369-234">*.frontend.clouddatahub.net</span></span> | <span data-ttu-id="12369-235">443</span><span class="sxs-lookup"><span data-stu-id="12369-235">443</span></span> | <span data-ttu-id="12369-236">HTTPS</span><span class="sxs-lookup"><span data-stu-id="12369-236">HTTPS</span></span> | 
| <span data-ttu-id="12369-237">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="12369-237">*.core.windows.net</span></span> | <span data-ttu-id="12369-238">443</span><span class="sxs-lookup"><span data-stu-id="12369-238">443</span></span> | <span data-ttu-id="12369-239">HTTPS</span><span class="sxs-lookup"><span data-stu-id="12369-239">HTTPS</span></span> | 
| <span data-ttu-id="12369-240">Login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="12369-240">login.microsoftonline.com</span></span> | <span data-ttu-id="12369-241">443</span><span class="sxs-lookup"><span data-stu-id="12369-241">443</span></span> | <span data-ttu-id="12369-242">HTTPS</span><span class="sxs-lookup"><span data-stu-id="12369-242">HTTPS</span></span> | 
| <span data-ttu-id="12369-243">*. msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="12369-243">*.msftncsi.com</span></span> | <span data-ttu-id="12369-244">443</span><span class="sxs-lookup"><span data-stu-id="12369-244">443</span></span> | <span data-ttu-id="12369-245">Gebruikt voor het testen van verbinding met internet wanneer de gateway onbereikbaar zijn door de Power BI-service is.</span><span class="sxs-lookup"><span data-stu-id="12369-245">Used to test internet connectivity when the gateway is unreachable by the Power BI service.</span></span> | 

<span data-ttu-id="12369-246">Als u goed te keuren IP-adressen in plaats van de domeinen hebt, kunt u downloaden en gebruiken de [Microsoft Azure Datacenter IP-adresbereiken lijst](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="12369-246">If you have to approve IP addresses instead of the domains, you can download and use the [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="12369-247">In sommige gevallen worden de Azure Service Bus-verbindingen gemaakt met IP-adres in plaats van een volledig gekwalificeerde domeinnamen.</span><span class="sxs-lookup"><span data-stu-id="12369-247">In some cases, the Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span></span>

<a name="gateway-cloud-service"></a>
## <a name="how-does-the-data-gateway-work"></a><span data-ttu-id="12369-248">Hoe werkt de gegevensgateway?</span><span class="sxs-lookup"><span data-stu-id="12369-248">How does the data gateway work?</span></span>

<span data-ttu-id="12369-249">De gegevensgateway vergemakkelijkt de snelle en veilige communicatie tussen uw logische app, het gateway-cloudservice en uw on-premises gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="12369-249">The data gateway facilitates quick and secure communication between your logic app, the gateway cloud service, and your on-premises data source.</span></span> 

![diagram-for-on-premises-Data-gateway-flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

<span data-ttu-id="12369-251">Wanneer de gebruiker in de cloud werkt met een element dat verbonden met uw on-premises gegevensbron:</span><span class="sxs-lookup"><span data-stu-id="12369-251">So when the user in the cloud interacts with an element that's connected to your on-premises data source:</span></span>

1. <span data-ttu-id="12369-252">De gateway cloudservice maakt een query, samen met de versleutelde referenties voor de gegevensbron en verzendt de query naar de wachtrij voor de gateway om te verwerken.</span><span class="sxs-lookup"><span data-stu-id="12369-252">The gateway cloud service creates a query, along with the encrypted credentials for the data source, and sends the query to the queue for the gateway to process.</span></span>

2. <span data-ttu-id="12369-253">De gateway cloudservice analyseert de query en de aanvraag verstuurd naar de Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="12369-253">The gateway cloud service analyzes the query and pushes the request to the Azure Service Bus.</span></span>

3. <span data-ttu-id="12369-254">De gegevensgateway lokale Azure Service Bus voor aanvragen in behandeling worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="12369-254">The on-premises data gateway polls the Azure Service Bus for pending requests.</span></span>

4. <span data-ttu-id="12369-255">De gateway opgehaald van de query, ontsleutelt de referenties en verbinding maakt met de gegevensbron met deze referenties.</span><span class="sxs-lookup"><span data-stu-id="12369-255">The gateway gets the query, decrypts the credentials, and connects to the data source with those credentials.</span></span>

5. <span data-ttu-id="12369-256">De gateway stuurt de query met de gegevensbron voor uitvoering.</span><span class="sxs-lookup"><span data-stu-id="12369-256">The gateway sends the query to the data source for execution.</span></span>

6. <span data-ttu-id="12369-257">De resultaten worden uit de gegevensbron verzonden terug naar de gateway en vervolgens naar het gateway-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="12369-257">The results are sent from the data source, back to the gateway, and then to the gateway cloud service.</span></span> <span data-ttu-id="12369-258">De gateway-cloudservice gebruikt vervolgens de resultaten.</span><span class="sxs-lookup"><span data-stu-id="12369-258">The gateway cloud service then uses the results.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="12369-259">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="12369-259">Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="12369-260">Algemeen</span><span class="sxs-lookup"><span data-stu-id="12369-260">General</span></span>

<span data-ttu-id="12369-261">**Q**: moet ik een gateway voor gegevensbronnen in de cloud, zoals SQL Azure?</span><span class="sxs-lookup"><span data-stu-id="12369-261">**Q**: Do I need a gateway for data sources in the cloud, such as SQL Azure?</span></span> <br/><span data-ttu-id="12369-262">
**Een**: Nee.</span><span class="sxs-lookup"><span data-stu-id="12369-262">
**A**: No.</span></span> <span data-ttu-id="12369-263">Een gateway maakt verbinding met on-premises gegevensbronnen alleen.</span><span class="sxs-lookup"><span data-stu-id="12369-263">A gateway connects to on-premises data sources only.</span></span>

<span data-ttu-id="12369-264">**Q**: de gateway hoeft te worden geïnstalleerd op dezelfde computer als de gegevensbron?</span><span class="sxs-lookup"><span data-stu-id="12369-264">**Q**: Does the gateway have to be installed on the same machine as the data source?</span></span> <br/><span data-ttu-id="12369-265">
**Een**: Nee.</span><span class="sxs-lookup"><span data-stu-id="12369-265">
**A**: No.</span></span> <span data-ttu-id="12369-266">De gateway maakt verbinding met de gegevensbron met de verbindingsgegevens die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="12369-266">The gateway connects to the data source using the connection information that was provided.</span></span> <span data-ttu-id="12369-267">Houd rekening met de gateway als een clienttoepassing in deze zin.</span><span class="sxs-lookup"><span data-stu-id="12369-267">Consider the gateway as a client application in this sense.</span></span> <span data-ttu-id="12369-268">De gateway moet alleen de mogelijkheid om te verbinden met de naam van de server die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="12369-268">The gateway just needs the capability to connect to the server name that was provided.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="12369-269">**Q**: Waarom moet ik een Azure werk- of schoolaccount aan te melden?</span><span class="sxs-lookup"><span data-stu-id="12369-269">**Q**: Why must I use an Azure work or school account to sign in?</span></span> <br/><span data-ttu-id="12369-270">
**Een**: U kunt alleen een Azure werk- of schoolaccount bij het installeren van de lokale data gateway.</span><span class="sxs-lookup"><span data-stu-id="12369-270">
**A**: You can only use an Azure work or school account when you install the on-premises data gateway.</span></span> <span data-ttu-id="12369-271">Uw account wordt opgeslagen in een tenant die wordt beheerd door Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="12369-271">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="12369-272">Uw Azure AD-account UPN (user Principal name) normaal gesproken komt overeen met het e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="12369-272">Usually, your Azure AD account's user principal name (UPN) matches the email address.</span></span>

<span data-ttu-id="12369-273">**Q**: waar mijn referenties worden opgeslagen?</span><span class="sxs-lookup"><span data-stu-id="12369-273">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="12369-274">
**Een**: de referenties die u voor een gegevensbron opgeeft zijn versleuteld en opgeslagen in de gateway-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="12369-274">
**A**: The credentials that you enter for a data source are encrypted and stored in the gateway cloud service.</span></span> <span data-ttu-id="12369-275">De referenties worden op de lokale data gateway ontsleuteld.</span><span class="sxs-lookup"><span data-stu-id="12369-275">The credentials are decrypted at the on-premises data gateway.</span></span>

<span data-ttu-id="12369-276">**Q**: zijn er vereisten voor de bandbreedte van het netwerk?</span><span class="sxs-lookup"><span data-stu-id="12369-276">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="12369-277">
**Een**: het is raadzaam dat de netwerkverbinding goed doorvoer heeft.</span><span class="sxs-lookup"><span data-stu-id="12369-277">
**A**: We recommend that your network connection has good throughput.</span></span> <span data-ttu-id="12369-278">Elke omgeving is verschillend en de hoeveelheid gegevens die worden verzonden, is van invloed op de resultaten.</span><span class="sxs-lookup"><span data-stu-id="12369-278">Every environment is different, and the amount of data being sent affects the results.</span></span> <span data-ttu-id="12369-279">Met behulp van ExpressRoute kan helpen om bescherming te bieden een mate van doorvoer tussen on-premises en de Azure-datacenters.</span><span class="sxs-lookup"><span data-stu-id="12369-279">Using ExpressRoute could help to guarantee a level of throughput between on-premises and the Azure datacenters.</span></span>
<span data-ttu-id="12369-280">U kunt de hulpprogramma van derden Azure snelheid testen-app gebruiken om te meten wat de doorvoer.</span><span class="sxs-lookup"><span data-stu-id="12369-280">You can use the third-party tool Azure Speed Test app to help gauge your throughput.</span></span>

<span data-ttu-id="12369-281">**Q**: Wat is de latentie voor het uitvoeren van query's met een gegevensbron van de gateway?</span><span class="sxs-lookup"><span data-stu-id="12369-281">**Q**: What is the latency for running queries to a data source from the gateway?</span></span> <span data-ttu-id="12369-282">Wat is de beste architectuur?</span><span class="sxs-lookup"><span data-stu-id="12369-282">What is the best architecture?</span></span> <br/><span data-ttu-id="12369-283">
**Een**: als u netwerklatentie, kunt u de gateway installeren zo dicht mogelijk bij de gegevensbron mogelijk.</span><span class="sxs-lookup"><span data-stu-id="12369-283">
**A**: To reduce network latency, install the gateway as close to the data source as possible.</span></span> <span data-ttu-id="12369-284">Als u de gateway op de werkelijke gegevensbron installeren kunt, minimaliseert deze nabijheid de latentie geïntroduceerd.</span><span class="sxs-lookup"><span data-stu-id="12369-284">If you can install the gateway on the actual data source, this proximity minimizes the latency introduced.</span></span> <span data-ttu-id="12369-285">Houd rekening met de datacentra te.</span><span class="sxs-lookup"><span data-stu-id="12369-285">Consider the datacenters too.</span></span> <span data-ttu-id="12369-286">Bijvoorbeeld, als uw service het datacenter VS-West gebruikt en u SQL Server gehost in een virtuele machine in Azure hebt, uw Azure VM moet zijn in de VS-West te.</span><span class="sxs-lookup"><span data-stu-id="12369-286">For example, if your service uses the West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in the West US too.</span></span> <span data-ttu-id="12369-287">Deze nabijheid minimaliseert latentie en vermijdt u kosten voor uitgaande op de virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="12369-287">This proximity minimizes latency and avoids egress charges on the Azure VM.</span></span>

<span data-ttu-id="12369-288">**Q**: hoe resultaten, verzonden naar de cloud?</span><span class="sxs-lookup"><span data-stu-id="12369-288">**Q**: How are results sent back to the cloud?</span></span> <br/><span data-ttu-id="12369-289">
**Een**: resultaten worden verzonden via de Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="12369-289">
**A**: Results are sent through the Azure Service Bus.</span></span>

<span data-ttu-id="12369-290">**Q**: zijn er geen inkomende verbindingen met de gateway vanuit de cloud?</span><span class="sxs-lookup"><span data-stu-id="12369-290">**Q**: Are there any inbound connections to the gateway from the cloud?</span></span> <br/><span data-ttu-id="12369-291">
**Een**: Nee.</span><span class="sxs-lookup"><span data-stu-id="12369-291">
**A**: No.</span></span> <span data-ttu-id="12369-292">Uitgaande verbindingen naar Azure Service Bus maakt gebruik van de gateway.</span><span class="sxs-lookup"><span data-stu-id="12369-292">The gateway uses outbound connections to Azure Service Bus.</span></span>

<span data-ttu-id="12369-293">**Q**: Wat gebeurt er als ik uitgaande verbindingen blokkeren?</span><span class="sxs-lookup"><span data-stu-id="12369-293">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="12369-294">Wat moet ik openen?</span><span class="sxs-lookup"><span data-stu-id="12369-294">What do I need to open?</span></span> <br/><span data-ttu-id="12369-295">
**Een**: Zie de poorten en hosts die gebruikmaakt van de gateway.</span><span class="sxs-lookup"><span data-stu-id="12369-295">
**A**: See the ports and hosts that the gateway uses.</span></span>

<span data-ttu-id="12369-296">**Q**: de werkelijke Windows-service zogenaamd?</span><span class="sxs-lookup"><span data-stu-id="12369-296">**Q**: What is the actual Windows service called?</span></span><br/><span data-ttu-id="12369-297">
**Een**: In Services Power BI Enterprise Gateway-Service voor de gateway wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="12369-297">
**A**: In Services, the gateway is called Power BI Enterprise Gateway Service.</span></span>

<span data-ttu-id="12369-298">**Q**: kan de gateway Windows-service worden uitgevoerd met Azure Active Directory-account?</span><span class="sxs-lookup"><span data-stu-id="12369-298">**Q**: Can the gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="12369-299">
**Een**: Nee.</span><span class="sxs-lookup"><span data-stu-id="12369-299">
**A**: No.</span></span> <span data-ttu-id="12369-300">De Windows-service moet een geldige Windows-account hebben.</span><span class="sxs-lookup"><span data-stu-id="12369-300">The Windows service must have a valid Windows account.</span></span> <span data-ttu-id="12369-301">De service wordt standaard uitgevoerd met de Service-SID NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="12369-301">By default, the service runs with the Service SID, NT SERVICE\PBIEgwService.</span></span>

### <a name="high-availability-and-disaster-recovery"></a><span data-ttu-id="12369-302">Hoge beschikbaarheid en herstel na noodgevallen</span><span class="sxs-lookup"><span data-stu-id="12369-302">High availability and disaster recovery</span></span>

<span data-ttu-id="12369-303">**Q**: welke opties zijn beschikbaar voor herstel na noodgevallen?</span><span class="sxs-lookup"><span data-stu-id="12369-303">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="12369-304">
**Een**: U kunt de herstelsleutel gebruiken om te zetten of verplaatsen van een gateway.</span><span class="sxs-lookup"><span data-stu-id="12369-304">
**A**: You can use the recovery key to restore or move a gateway.</span></span> <span data-ttu-id="12369-305">Wanneer u de gateway installeren, geeft u de herstelsleutel.</span><span class="sxs-lookup"><span data-stu-id="12369-305">When you install the gateway, specify the recovery key.</span></span>

<span data-ttu-id="12369-306">**Q**: Wat is het voordeel van de herstelsleutel?</span><span class="sxs-lookup"><span data-stu-id="12369-306">**Q**: What is the benefit of the recovery key?</span></span> <br/><span data-ttu-id="12369-307">
**Een**: de herstelsleutel biedt een manier om te migreren of de gateway-instellingen herstellen na een noodgeval.</span><span class="sxs-lookup"><span data-stu-id="12369-307">
**A**: The recovery key provides a way to migrate or recover your gateway settings after a disaster.</span></span>

<span data-ttu-id="12369-308">**Q**: zijn er plannen voor het inschakelen van hoge beschikbaarheid scenario's met de gateway?</span><span class="sxs-lookup"><span data-stu-id="12369-308">**Q**: Are there any plans for enabling high availability scenarios with the gateway?</span></span> <br/><span data-ttu-id="12369-309">
**Een**: deze scenario's zijn op de roadmap, maar we een tijdlijn nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="12369-309">
**A**: These scenarios are on the roadmap, but we don't have a timeline yet.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="12369-310">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="12369-310">Troubleshooting</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

<span data-ttu-id="12369-311">**Q**: hoe kan ik zien wat query's worden verzonden naar de on-premises gegevensbron?</span><span class="sxs-lookup"><span data-stu-id="12369-311">**Q**: How can I see what queries are being sent to the on-premises data source?</span></span> <br/><span data-ttu-id="12369-312">
**Een**: U kunt inschakelen querytracering, waaronder de query's die worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="12369-312">
**A**: You can enable query tracing, which includes the queries that are sent.</span></span> <span data-ttu-id="12369-313">Vergeet niet om te wijzigen van de query traceren terug naar de oorspronkelijke waarde gedaan bij het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="12369-313">Remember to change query tracing back to the original value when done troubleshooting.</span></span> <span data-ttu-id="12369-314">Querytracering ingeschakeld verlaten maakt grotere Logboeken.</span><span class="sxs-lookup"><span data-stu-id="12369-314">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="12369-315">U kunt ook hulpprogramma's die de gegevensbron voor tracering van query's heeft bekijken.</span><span class="sxs-lookup"><span data-stu-id="12369-315">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="12369-316">U kunt bijvoorbeeld de Extended Events of SQL Profiler gebruiken voor SQL Server en Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="12369-316">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="12369-317">**Q**: waar zich de logboeken van de gateway?</span><span class="sxs-lookup"><span data-stu-id="12369-317">**Q**: Where are the gateway logs?</span></span> <br/><span data-ttu-id="12369-318">
**Een**: Zie's verderop in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="12369-318">
**A**: See Tools later in this topic.</span></span>

### <a name="update-to-the-latest-version"></a><span data-ttu-id="12369-319">Bijwerken naar de meest recente versie</span><span class="sxs-lookup"><span data-stu-id="12369-319">Update to the latest version</span></span>

<span data-ttu-id="12369-320">Veel problemen kunnen surface wanneer de gatewayversie is verouderd.</span><span class="sxs-lookup"><span data-stu-id="12369-320">Many issues can surface when the gateway version becomes outdated.</span></span> <span data-ttu-id="12369-321">Zorg ervoor dat u met de meest recente versie als goed over het algemeen.</span><span class="sxs-lookup"><span data-stu-id="12369-321">As good general practice, make sure that you use the latest version.</span></span> <span data-ttu-id="12369-322">Als u kunt de gateway nog niet hebt bijgewerkt, gedurende een maand of langer, kunt u Overweeg de installatie van de meest recente versie van de gateway en zien als u het probleem kan reproduceren.</span><span class="sxs-lookup"><span data-stu-id="12369-322">If you haven't updated the gateway for a month or longer, you might consider installing the latest version of the gateway, and see if you can reproduce the issue.</span></span>

### <a name="error-failed-to-add-user-to-group--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="12369-323">Fout: Kan gebruiker niet toevoegen aan groep.</span><span class="sxs-lookup"><span data-stu-id="12369-323">Error: Failed to add user to group.</span></span> <span data-ttu-id="12369-324">(-2147463168 PBIEgwService Prestatielogboekgebruikers)</span><span class="sxs-lookup"><span data-stu-id="12369-324">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="12369-325">U kunt deze fout kan ophalen, als u probeert de gateway installeren op een domeincontroller wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="12369-325">You might get this error if you try to install the gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="12369-326">Zorg ervoor dat u de gateway op een computer die een domeincontroller niet implementeert.</span><span class="sxs-lookup"><span data-stu-id="12369-326">Make sure that you deploy the gateway on a machine that isn't a domain controller.</span></span>

## <a name="tools"></a><span data-ttu-id="12369-327">Hulpprogramma's</span><span class="sxs-lookup"><span data-stu-id="12369-327">Tools</span></span>

### <a name="collect-logs-from-the-gateway-configurer"></a><span data-ttu-id="12369-328">Verzamelen van Logboeken van de gateway configurer</span><span class="sxs-lookup"><span data-stu-id="12369-328">Collect logs from the gateway configurer</span></span>

<span data-ttu-id="12369-329">U kunt verschillende logboeken voor de gateway verzamelen.</span><span class="sxs-lookup"><span data-stu-id="12369-329">You can collect several logs for the gateway.</span></span> <span data-ttu-id="12369-330">Begin altijd met de logboeken!</span><span class="sxs-lookup"><span data-stu-id="12369-330">Always start with the logs!</span></span>

#### <a name="installer-logs"></a><span data-ttu-id="12369-331">Installatieprogramma Logboeken</span><span class="sxs-lookup"><span data-stu-id="12369-331">Installer logs</span></span>

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a><span data-ttu-id="12369-332">Configuratielogboeken</span><span class="sxs-lookup"><span data-stu-id="12369-332">Configuration logs</span></span>

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="12369-333">Enterprise gateway-service-Logboeken</span><span class="sxs-lookup"><span data-stu-id="12369-333">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a><span data-ttu-id="12369-334">Gebeurtenislogboeken</span><span class="sxs-lookup"><span data-stu-id="12369-334">Event logs</span></span>

<span data-ttu-id="12369-335">U vindt de logboeken van de Data Management Gateway en PowerBIGateway onder **servicelogboeken voor toepassingen en**.</span><span class="sxs-lookup"><span data-stu-id="12369-335">You can find the Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>

### <a name="fiddler-trace"></a><span data-ttu-id="12369-336">Fiddler traceren</span><span class="sxs-lookup"><span data-stu-id="12369-336">Fiddler Trace</span></span>

<span data-ttu-id="12369-337">[Fiddler](http://www.telerik.com/fiddler) is een gratis hulpprogramma uit Telerik die HTTP-verkeer wordt bewaakt.</span><span class="sxs-lookup"><span data-stu-id="12369-337">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span></span> <span data-ttu-id="12369-338">U ziet dit verkeer met de Power BI-service van de clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="12369-338">You can see this traffic with the Power BI service from the client machine.</span></span> <span data-ttu-id="12369-339">Deze service mogelijk fouten en andere gerelateerde informatie weergeven.</span><span class="sxs-lookup"><span data-stu-id="12369-339">This service might show errors and other related information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12369-340">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="12369-340">Next steps</span></span>
    
* [<span data-ttu-id="12369-341">Verbinding maken met on-premises gegevens vanuit logic apps</span><span class="sxs-lookup"><span data-stu-id="12369-341">Connect to on-premises data from logic apps</span></span>](../logic-apps/logic-apps-gateway-connection.md)
* [<span data-ttu-id="12369-342">Enterprise integration-functies</span><span class="sxs-lookup"><span data-stu-id="12369-342">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="12369-343">Connectors voor Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="12369-343">Connectors for Azure Logic Apps</span></span>](../connectors/apis-list.md)
