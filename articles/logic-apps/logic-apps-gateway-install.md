---
title: aaaInstall lokale gegevensgateway - Azure Logic Apps | Microsoft Docs
description: Voordat u toegang gegevensbronnen on-premises tot, Hallo lokale gegevensgateway voor snelle gegevensoverdracht en -versleuteling tussen on-premises gegevensbronnen en logic apps installeren
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
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a><span data-ttu-id="3286a-104">Installatie Hallo on-premises gegevensgateway voor Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="3286a-104">Install hello on-premises data gateway for Azure Logic Apps</span></span>

<span data-ttu-id="3286a-105">Om uw logische apps toegang on-premises gegevensbronnen tot, moet u het installeren en stel Hallo lokale gegevensgateway.</span><span class="sxs-lookup"><span data-stu-id="3286a-105">Before your logic apps can access data sources on premises, you must install and set up hello on-premises data gateway.</span></span> <span data-ttu-id="3286a-106">Hallo gateway fungeert als een brug waarmee snelle gegevensoverdracht en -versleuteling tussen on-premises systemen en uw logische apps.</span><span class="sxs-lookup"><span data-stu-id="3286a-106">hello gateway acts as a bridge that provides quick data transfer and encryption between on-premises systems and your logic apps.</span></span> <span data-ttu-id="3286a-107">Hallo gateway doorstuurt gegevens van lokale bronnen op gecodeerde kanalen via hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3286a-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="3286a-108">Al het verkeer afkomstig is als beveiligde uitgaand verkeer van Hallo gateway agent.</span><span class="sxs-lookup"><span data-stu-id="3286a-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="3286a-109">Meer informatie over [de werking van de gegevensgateway Hallo](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="3286a-109">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

<span data-ttu-id="3286a-110">Hallo-gateway ondersteunt verbindingen toothese gegevensbronnen on-premises:</span><span class="sxs-lookup"><span data-stu-id="3286a-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="3286a-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="3286a-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="3286a-112">DB2</span><span class="sxs-lookup"><span data-stu-id="3286a-112">DB2</span></span>  
*   <span data-ttu-id="3286a-113">Bestandssysteem</span><span class="sxs-lookup"><span data-stu-id="3286a-113">File System</span></span>
*   <span data-ttu-id="3286a-114">Informix</span><span class="sxs-lookup"><span data-stu-id="3286a-114">Informix</span></span>
*   <span data-ttu-id="3286a-115">MQ</span><span class="sxs-lookup"><span data-stu-id="3286a-115">MQ</span></span>
*   <span data-ttu-id="3286a-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="3286a-116">MySQL</span></span>
*   <span data-ttu-id="3286a-117">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="3286a-117">Oracle Database</span></span>
*   <span data-ttu-id="3286a-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="3286a-118">PostgreSQL</span></span>
*   <span data-ttu-id="3286a-119">SAP-toepassingsserver</span><span class="sxs-lookup"><span data-stu-id="3286a-119">SAP Application Server</span></span> 
*   <span data-ttu-id="3286a-120">SAP-berichtenserver</span><span class="sxs-lookup"><span data-stu-id="3286a-120">SAP Message Server</span></span>
*   <span data-ttu-id="3286a-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="3286a-121">SharePoint</span></span>
*   <span data-ttu-id="3286a-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="3286a-122">SQL Server</span></span>
*   <span data-ttu-id="3286a-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="3286a-123">Teradata</span></span>

<span data-ttu-id="3286a-124">Deze stappen laten zien hoe toofirst installeren Hallo lokale gegevensgateway voordat u [instellen van een verbinding tussen Hallo-gateway en uw logische apps](./logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="3286a-124">These steps show how toofirst install hello on-premises data gateway before you [set up a connection between hello gateway and your logic apps](./logic-apps-gateway-connection.md).</span></span> <span data-ttu-id="3286a-125">Zie voor meer informatie over ondersteunde connectors [Connectors voor Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="3286a-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span> 

<span data-ttu-id="3286a-126">Zie voor informatie over hoe toouse Hallo gateway met andere services, deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="3286a-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="3286a-127">Microsoft Power BI lokale gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="3286a-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="3286a-128">Azure Analysis Services op locatie gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="3286a-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="3286a-129">Microsoft-Flow lokale gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="3286a-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="3286a-130">Microsoft PowerApps lokale gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="3286a-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a><span data-ttu-id="3286a-131">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3286a-131">Requirements</span></span>

<span data-ttu-id="3286a-132">**Minimale**:</span><span class="sxs-lookup"><span data-stu-id="3286a-132">**Minimum**:</span></span>

* <span data-ttu-id="3286a-133">.NET 4.5 framework</span><span class="sxs-lookup"><span data-stu-id="3286a-133">.NET 4.5 Framework</span></span>
* <span data-ttu-id="3286a-134">64-bits versie van Windows 7 of Windows Server 2008 R2 (of hoger)</span><span class="sxs-lookup"><span data-stu-id="3286a-134">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="3286a-135">**Aanbevolen**:</span><span class="sxs-lookup"><span data-stu-id="3286a-135">**Recommended**:</span></span>

* <span data-ttu-id="3286a-136">8-core CPU</span><span class="sxs-lookup"><span data-stu-id="3286a-136">8 Core CPU</span></span>
* <span data-ttu-id="3286a-137">8 GB geheugen</span><span class="sxs-lookup"><span data-stu-id="3286a-137">8 GB Memory</span></span>
* <span data-ttu-id="3286a-138">64-bits versie van Windows 2012 R2 (of hoger)</span><span class="sxs-lookup"><span data-stu-id="3286a-138">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="3286a-139">**Belangrijke overwegingen**:</span><span class="sxs-lookup"><span data-stu-id="3286a-139">**Important considerations**:</span></span>

* <span data-ttu-id="3286a-140">Hallo lokale gegevensgateway alleen op een lokale computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3286a-140">Install hello on-premises data gateway only on a local computer.</span></span>
<span data-ttu-id="3286a-141">U kunt Hallo gateway niet installeren op een domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="3286a-141">You can't install hello gateway on a domain controller.</span></span>

   > [!TIP]
   > <span data-ttu-id="3286a-142">U hebt geen tooinstall Hallo gateway op Hallo dezelfde computer als uw gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="3286a-142">You don't have tooinstall hello gateway on hello same computer as your data source.</span></span> <span data-ttu-id="3286a-143">toominimize latentie, kunt u Hallo gateway zo dicht als mogelijke tooyour gegevensbron, of op Hallo dezelfde installeren computer, ervan uitgaande dat u machtigingen hebt.</span><span class="sxs-lookup"><span data-stu-id="3286a-143">toominimize latency, you can install hello gateway as close as possible tooyour data source, or on hello same computer, assuming that you have permissions.</span></span>

* <span data-ttu-id="3286a-144">Installeer geen Hallo-gateway op een computer die wordt uitgeschakeld, gaat toosleep of toohello Internet geen verbinding worden gemaakt omdat het Hallo-gateway kan niet worden uitgevoerd in deze omstandigheden.</span><span class="sxs-lookup"><span data-stu-id="3286a-144">Don't install hello gateway on a computer that turns off, goes toosleep, or doesn't connect toohello Internet because hello gateway can't run under those circumstances.</span></span> <span data-ttu-id="3286a-145">Ook de prestaties van de gateway via een draadloos netwerk kan afnemen.</span><span class="sxs-lookup"><span data-stu-id="3286a-145">Also, gateway performance might suffer over a wireless network.</span></span>

* <span data-ttu-id="3286a-146">Tijdens de installatie, moet u zich aanmelden met een [werk- of schoolaccount](https://docs.microsoft.com/azure/active-directory/sign-up-organization) die wordt beheerd door Azure Active Directory (Azure AD), niet in een Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="3286a-146">During installation, you must sign in with a [work or school account](https://docs.microsoft.com/azure/active-directory/sign-up-organization) that's managed by Azure Active Directory (Azure AD), not a Microsoft account.</span></span> 

  <span data-ttu-id="3286a-147">U hebt toouse Hallo hetzelfde werk of school account later in hello Azure portal maken en koppelen van een gateway-resource met de gateway-installatie.</span><span class="sxs-lookup"><span data-stu-id="3286a-147">You have toouse hello same work or school account later in hello Azure portal when you create and associate a gateway resource with your gateway installation.</span></span> <span data-ttu-id="3286a-148">U selecteert deze gateway resource vervolgens wanneer u Hallo verbinding tussen uw logica app en Hallo on-premises gegevensbron maken.</span><span class="sxs-lookup"><span data-stu-id="3286a-148">You then select this gateway resource when you create hello connection between your logic app and hello on-premises data source.</span></span> [<span data-ttu-id="3286a-149">Waarom moet ik een Azure AD werk- of schoolaccount?</span><span class="sxs-lookup"><span data-stu-id="3286a-149">Why must I use an Azure AD work or school account?</span></span>](#why-azure-work-school-account)

  > [!TIP]
  > <span data-ttu-id="3286a-150">Als u zich registreerde voor een Office 365-aanbieding en uw werkelijke Werke-mailadres niet opgeven, uw adres aanmelden als volgt uitzien jeff@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="3286a-150">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span></span> 

* <span data-ttu-id="3286a-151">Als u een bestaande gateway die u hebt ingesteld met een installatieprogramma dat ouder is dan versie 14.16.6317.4 hebt, kunt u uw gateway locatie door actieve Hallo nieuwste installer niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3286a-151">If you have an existing gateway that you set up with an installer that's earlier than version 14.16.6317.4, you can't change your gateway's location by running hello latest installer.</span></span> <span data-ttu-id="3286a-152">U kunt echter Hallo nieuwste installatieprogramma tooset van een nieuwe gateway met Hallo in plaats daarvan de gewenste locatie.</span><span class="sxs-lookup"><span data-stu-id="3286a-152">However, you can use hello latest installer tooset up a new gateway with hello location that you want instead.</span></span>
  
  <span data-ttu-id="3286a-153">Als u een gateway-installatieprogramma dat ouder is dan versie 14.16.6317.4 hebben, maar u kunt uw gateway nog niet geïnstalleerd nog, kunt u downloaden en de meest recente installatieprogramma hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3286a-153">If you have a gateway installer that's earlier than version 14.16.6317.4, but you haven't installed your gateway yet, you can download and use hello latest installer.</span></span>

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a><span data-ttu-id="3286a-154">Hallo gegevensgateway installeren</span><span class="sxs-lookup"><span data-stu-id="3286a-154">Install hello data gateway</span></span>

1.  <span data-ttu-id="3286a-155">[Downloaden en uitvoeren van het installatieprogramma van Hallo gateway op een lokale computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="3286a-155">[Download and run hello gateway installer on a local computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span></span>

2. <span data-ttu-id="3286a-156">Lees en accepteer de gebruiksvoorwaarden en de privacyverklaring Hallo.</span><span class="sxs-lookup"><span data-stu-id="3286a-156">Review and accept hello terms of use and privacy statement.</span></span>

3. <span data-ttu-id="3286a-157">Hallo-pad op de lokale computer waar u tooinstall Hallo gateway wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="3286a-157">Specify hello path on your local computer where you want tooinstall hello gateway.</span></span>

4. <span data-ttu-id="3286a-158">Wanneer u wordt gevraagd, meld u aan met uw Azure werk- of schoolaccount, niet in een Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="3286a-158">When prompted, sign in with your Azure work or school account, not a Microsoft account.</span></span>

   ![Meld u aan met Azure werk- of schoolaccount](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. <span data-ttu-id="3286a-160">Nu uw geïnstalleerde gateway registreren met Hallo [gateway-cloudservice](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="3286a-160">Now register your installed gateway with hello [gateway cloud service](#gateway-cloud-service).</span></span> <span data-ttu-id="3286a-161">Kies **registreren van een nieuwe gateway op deze computer**.</span><span class="sxs-lookup"><span data-stu-id="3286a-161">Choose **Register a new gateway on this computer**.</span></span>

   <span data-ttu-id="3286a-162">gateway-cloudservice Hallo versleutelt en slaat de referenties van de gegevensbron en de details van de gateway.</span><span class="sxs-lookup"><span data-stu-id="3286a-162">hello gateway cloud service encrypts and stores your data source credentials and gateway details.</span></span> 
   <span data-ttu-id="3286a-163">Hallo-service stuurt ook query's en de bijbehorende resultaten tussen uw logische app, Hallo lokale gegevensgateway en uw gegevensbron on-premises.</span><span class="sxs-lookup"><span data-stu-id="3286a-163">hello service also routes queries and their results between your logic app, hello on-premises data gateway, and your data source on premises.</span></span>

6. <span data-ttu-id="3286a-164">Geef een naam voor uw gateway-installatie.</span><span class="sxs-lookup"><span data-stu-id="3286a-164">Provide a name for your gateway installation.</span></span> <span data-ttu-id="3286a-165">Een herstelsleutel maken en bevestig vervolgens uw herstelsleutel.</span><span class="sxs-lookup"><span data-stu-id="3286a-165">Create a recovery key, then confirm your recovery key.</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="3286a-166">De herstelsleutel moet ten minste acht tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="3286a-166">Your recovery key must contain at least eight characters.</span></span> <span data-ttu-id="3286a-167">Zorg ervoor dat u opslaat en Hallo-sleutel in een veilige plaats bewaren.</span><span class="sxs-lookup"><span data-stu-id="3286a-167">Make sure that you save and keep hello key in a safe place.</span></span> <span data-ttu-id="3286a-168">Ook moet u deze sleutel als u wilt dat toomigrate, herstellen of overnemen van een bestaande gateway.</span><span class="sxs-lookup"><span data-stu-id="3286a-168">You also need this key when you want toomigrate, restore, or take over an existing gateway.</span></span>

   1. <span data-ttu-id="3286a-169">toochange hello standaard regio voor Hallo gateway-cloudservice en de Azure Service Bus gebruikt door de installatie van de gateway, kiezen **wijziging regio**.</span><span class="sxs-lookup"><span data-stu-id="3286a-169">toochange hello default region for hello gateway cloud service and Azure Service Bus used by your gateway installation, choose **Change Region**.</span></span>

      ![Wijziging regio](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      <span data-ttu-id="3286a-171">Hallo standaard regio is Hallo regio die aan uw Azure AD-tenant zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="3286a-171">hello default region is hello region associated with your Azure AD tenant.</span></span>

   2. <span data-ttu-id="3286a-172">Open op de volgende deelvenster Hallo Hallo **regio selecteren** een andere regio te kiezen.</span><span class="sxs-lookup"><span data-stu-id="3286a-172">On hello next pane, open hello **Select Region** too choose a different region.</span></span>

      ![Selecteer een andere regio](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      <span data-ttu-id="3286a-174">Bijvoorbeeld: u selecteert Hallo mogelijk dezelfde regio bevinden als uw logische app, of selecteer Hallo regio dichtstbijzijnde tooyour lokale gegevensbron zodat de latentie te verminderen.</span><span class="sxs-lookup"><span data-stu-id="3286a-174">For example, you might select hello same region as your logic app, or select hello region closest tooyour on-premises data source so you can reduce latency.</span></span> <span data-ttu-id="3286a-175">Uw gateway en logica voor resource app hebben verschillende locaties.</span><span class="sxs-lookup"><span data-stu-id="3286a-175">Your gateway resource and logic app can have different locations.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="3286a-176">U kunt deze regio niet wijzigen na de installatie.</span><span class="sxs-lookup"><span data-stu-id="3286a-176">You can't change this region after installation.</span></span> <span data-ttu-id="3286a-177">Dit gebied wordt ook bepaalt en Hallo locatie hier u hello Azure-resource voor uw gateway maken kunt worden beperkt.</span><span class="sxs-lookup"><span data-stu-id="3286a-177">This region also determines and restricts hello location where you can create hello Azure resource for your gateway.</span></span> <span data-ttu-id="3286a-178">Wanneer u uw gateway-resource in Azure maakt, zorg er dus Hallo Resourcelocatie komt overeen met Hallo regio die u hebt geselecteerd tijdens de installatie van de gateway.</span><span class="sxs-lookup"><span data-stu-id="3286a-178">So when you create your gateway resource in Azure, make sure that hello resource location matches hello region that you selected during gateway installation.</span></span>
      > 
      > <span data-ttu-id="3286a-179">Als u een andere regio toouse voor uw gateway later wilt, moet u een nieuwe gateway instellen.</span><span class="sxs-lookup"><span data-stu-id="3286a-179">If you want toouse a different region for your gateway later, you must set up a new gateway.</span></span>

   3. <span data-ttu-id="3286a-180">Als u klaar bent, kiest u **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="3286a-180">When you're ready, choose **Done**.</span></span>

7. <span data-ttu-id="3286a-181">Nu als volgt te werk in Azure-portal Hallo zodat u kunt [maken van een Azure-resource voor uw gateway](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="3286a-181">Now follow these steps in hello Azure portal so you can [create an Azure resource for your gateway](../logic-apps/logic-apps-gateway-connection.md).</span></span> 

<span data-ttu-id="3286a-182">Meer informatie over [de werking van de gegevensgateway Hallo](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="3286a-182">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a><span data-ttu-id="3286a-183">Migreren, herstellen of overnemen van een bestaande gateway</span><span class="sxs-lookup"><span data-stu-id="3286a-183">Migrate, restore, or take over an existing gateway</span></span>

<span data-ttu-id="3286a-184">tooperform u deze taken, moet u de herstelsleutel Hallo die is opgegeven tijdens het Hallo-gateway is geïnstalleerd hebben.</span><span class="sxs-lookup"><span data-stu-id="3286a-184">tooperform these tasks, you must have hello recovery key that was specified when hello gateway was installed.</span></span>

1. <span data-ttu-id="3286a-185">Kies in het menu Start uw computer **On-premises gegevensgateway**.</span><span class="sxs-lookup"><span data-stu-id="3286a-185">From your computer's Start menu, choose **On-premises data gateway**.</span></span>

2. <span data-ttu-id="3286a-186">Nadat hello installatieprogramma wordt geopend Meld u aan met hello dezelfde Azure werk- of schoolaccount dat eerder tooinstall Hallo gateway gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3286a-186">After hello installer opens, sign in with hello same Azure work or school account that was previously used tooinstall hello gateway.</span></span>

3. <span data-ttu-id="3286a-187">Kies **migreren, herstellen of overnemen van een bestaande gateway**.</span><span class="sxs-lookup"><span data-stu-id="3286a-187">Choose **Migrate, restore, or take over an existing gateway**.</span></span>

4. <span data-ttu-id="3286a-188">De naam en herstel sleutel Hallo voor Hallo-gateway die u toomigrate, herstellen of nemen via wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="3286a-188">Provide hello name and recovery key for hello gateway that you want toomigrate, restore, or take over.</span></span>

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a><span data-ttu-id="3286a-189">Hallo-gateway opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="3286a-189">Restart hello gateway</span></span>

<span data-ttu-id="3286a-190">Hallo-gateway als een Windows-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3286a-190">hello gateway runs as a Windows service.</span></span> <span data-ttu-id="3286a-191">Net als elke andere Windows-service, kunt u starten en stoppen van service Hallo op verschillende manieren.</span><span class="sxs-lookup"><span data-stu-id="3286a-191">Like any other Windows service, you can start and stop hello service in multiple ways.</span></span> <span data-ttu-id="3286a-192">U kunt bijvoorbeeld open een opdrachtprompt met verhoogde machtigingen op Hallo-computer waarop het Hallo-gateway wordt uitgevoerd, en beide deze opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3286a-192">For example, you can open a command prompt with elevated permissions on hello computer where hello gateway is running, and run either these commands:</span></span>

* <span data-ttu-id="3286a-193">toostop hello service, die deze opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3286a-193">toostop hello service, run this command:</span></span>
  
    `net stop PBIEgwService`

* <span data-ttu-id="3286a-194">toostart hello service, die deze opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3286a-194">toostart hello service, run this command:</span></span>
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a><span data-ttu-id="3286a-195">Windows-serviceaccount</span><span class="sxs-lookup"><span data-stu-id="3286a-195">Windows service account</span></span>

<span data-ttu-id="3286a-196">Hallo lokale gegevensgateway is ingesteld op toouse `NT SERVICE\PBIEgwService` voor Windows hello service aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="3286a-196">hello on-premises data gateway is set up toouse `NT SERVICE\PBIEgwService` for hello Windows service logon credentials.</span></span> <span data-ttu-id="3286a-197">Hallo gateway heeft standaard Hallo 'Aanmelden als service' rechts voor Hallo machine waarop u Hallo-gateway installeert.</span><span class="sxs-lookup"><span data-stu-id="3286a-197">By default, hello gateway has hello "Log on as a service" right for hello machine where you install hello gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="3286a-198">Hallo Windows-service-account verschilt van Hallo account dat wordt gebruikt voor het verbinden van tooon-premises gegevensbronnen en van hello Azure werk of schoolaccount gebruikt toosign in toocloud services.</span><span class="sxs-lookup"><span data-stu-id="3286a-198">hello Windows service account differs from hello account used for connecting tooon-premises data sources, and from hello Azure work or school account used toosign in toocloud services.</span></span>

## <a name="configure-a-firewall-or-proxy"></a><span data-ttu-id="3286a-199">Een firewall of proxy configureren</span><span class="sxs-lookup"><span data-stu-id="3286a-199">Configure a firewall or proxy</span></span>

<span data-ttu-id="3286a-200">Hallo-gateway maakt een uitgaande verbinding te [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="3286a-200">hello gateway creates an outbound connection too [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="3286a-201">proxy-informatie voor uw gateway tooprovide Zie [proxy-instellingen configureren](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span><span class="sxs-lookup"><span data-stu-id="3286a-201">tooprovide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span></span>

<span data-ttu-id="3286a-202">toocheck of uw firewall of proxy, kan verbindingen blokkeren, Controleer of uw machine daadwerkelijk verbinding kunt maken van toohello internet en Hallo [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="3286a-202">toocheck whether your firewall, or proxy, might block connections, confirm whether your machine can actually connect toohello internet and hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="3286a-203">Vanuit een PowerShell-prompt, moet u deze opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3286a-203">From a PowerShell prompt, run this command:</span></span>

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> <span data-ttu-id="3286a-204">Met deze opdracht wordt enkel tests netwerkverbinding en connectiviteit toohello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3286a-204">This command only tests network connectivity and connectivity toohello Azure Service Bus.</span></span> <span data-ttu-id="3286a-205">Zodat het Hallo-opdracht heeft niets toodo met Hallo gateway of Hallo gateway-cloudservice die versleutelt en slaat uw referenties en de details van de gateway.</span><span class="sxs-lookup"><span data-stu-id="3286a-205">So hello command doesn't have anything toodo with hello gateway or hello gateway cloud service that encrypts and stores your credentials and gateway details.</span></span> 
>
> <span data-ttu-id="3286a-206">Ook deze opdracht is alleen beschikbaar op Windows Server 2012 R2 of hoger, en Windows 8.1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="3286a-206">Also, this command is only available on Windows Server 2012 R2 or later, and Windows 8.1 or later.</span></span> <span data-ttu-id="3286a-207">In eerdere versies van het besturingssysteem, kunt u Telnet-connectiviteit te testen.</span><span class="sxs-lookup"><span data-stu-id="3286a-207">On earlier OS versions, you can use Telnet too test connectivity.</span></span> <span data-ttu-id="3286a-208">Meer informatie over [Azure Service Bus- en hybride oplossingen](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="3286a-208">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

<span data-ttu-id="3286a-209">Uw resultaten ziet vergelijkbaar toothis voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3286a-209">Your results should look similar toothis example:</span></span>

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

<span data-ttu-id="3286a-210">Als **TcpTestSucceeded** is niet ingesteld te**True**, u mogelijk geblokkeerd door een firewall.</span><span class="sxs-lookup"><span data-stu-id="3286a-210">If **TcpTestSucceeded** is not set too**True**, you might be blocked by a firewall.</span></span> <span data-ttu-id="3286a-211">Als u wilt dat uitgebreide toobe, vervangende Hallo **ComputerName** en **poort** waarden met Hallo waarden die worden vermeld onder [poorten configureren](#configure-ports) in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="3286a-211">If you want toobe comprehensive, substitute hello **ComputerName** and **Port** values with hello values listed under [Configure ports](#configure-ports) in this topic.</span></span>

<span data-ttu-id="3286a-212">Hallo firewall blokkeren mogelijk de ook verbindingen die hello die Azure Service Bus toohello Azure-datacenters maakt.</span><span class="sxs-lookup"><span data-stu-id="3286a-212">hello firewall might also block connections that hello Azure Service Bus makes toohello Azure datacenters.</span></span> <span data-ttu-id="3286a-213">Als u dit scenario gebeurt, goedkeuren (deblokkeren) alle Hallo IP-adressen voor deze datacentra in uw regio.</span><span class="sxs-lookup"><span data-stu-id="3286a-213">If this scenario happens, approve (unblock) all hello IP addresses for those datacenters in your region.</span></span> <span data-ttu-id="3286a-214">Voor deze IP-adressen [get hello Azure lijst IP-adressen hier](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="3286a-214">For those IP addresses, [get hello Azure IP addresses list here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

## <a name="configure-ports"></a><span data-ttu-id="3286a-215">Poorten configureren</span><span class="sxs-lookup"><span data-stu-id="3286a-215">Configure ports</span></span>

<span data-ttu-id="3286a-216">Hallo-gateway maakt een uitgaande verbinding te[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) en op uitgaande poorten communiceert: TCP 443 (standaard), 5671, 5672, 9350 via 9354.</span><span class="sxs-lookup"><span data-stu-id="3286a-216">hello gateway creates an outbound connection too[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span> <span data-ttu-id="3286a-217">Hallo-gateway nodig niet poorten voor inkomend verkeer.</span><span class="sxs-lookup"><span data-stu-id="3286a-217">hello gateway doesn't require inbound ports.</span></span> <span data-ttu-id="3286a-218">Meer informatie over [Azure Service Bus- en hybride oplossingen](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="3286a-218">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

| <span data-ttu-id="3286a-219">DOMEINNAMEN</span><span class="sxs-lookup"><span data-stu-id="3286a-219">DOMAIN NAMES</span></span> | <span data-ttu-id="3286a-220">UITGAANDE POORTEN</span><span class="sxs-lookup"><span data-stu-id="3286a-220">OUTBOUND PORTS</span></span> | <span data-ttu-id="3286a-221">BESCHRIJVING</span><span class="sxs-lookup"><span data-stu-id="3286a-221">DESCRIPTION</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3286a-222">*. analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="3286a-222">*.analysis.windows.net</span></span> | <span data-ttu-id="3286a-223">443</span><span class="sxs-lookup"><span data-stu-id="3286a-223">443</span></span> | <span data-ttu-id="3286a-224">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3286a-224">HTTPS</span></span> | 
| <span data-ttu-id="3286a-225">*. login.windows.net</span><span class="sxs-lookup"><span data-stu-id="3286a-225">*.login.windows.net</span></span> | <span data-ttu-id="3286a-226">443</span><span class="sxs-lookup"><span data-stu-id="3286a-226">443</span></span> | <span data-ttu-id="3286a-227">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3286a-227">HTTPS</span></span> | 
| <span data-ttu-id="3286a-228">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="3286a-228">*.servicebus.windows.net</span></span> | <span data-ttu-id="3286a-229">5671-5672</span><span class="sxs-lookup"><span data-stu-id="3286a-229">5671-5672</span></span> | <span data-ttu-id="3286a-230">Geavanceerde Message Queuing-Protocol (AMQP)</span><span class="sxs-lookup"><span data-stu-id="3286a-230">Advanced Message Queuing Protocol (AMQP)</span></span> | 
| <span data-ttu-id="3286a-231">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="3286a-231">*.servicebus.windows.net</span></span> | <span data-ttu-id="3286a-232">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="3286a-232">443, 9350-9354</span></span> | <span data-ttu-id="3286a-233">Listeners op Service Bus Relay via TCP (443 voor toegangsbeheer token aanschaf vereist)</span><span class="sxs-lookup"><span data-stu-id="3286a-233">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> | 
| <span data-ttu-id="3286a-234">*. frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="3286a-234">*.frontend.clouddatahub.net</span></span> | <span data-ttu-id="3286a-235">443</span><span class="sxs-lookup"><span data-stu-id="3286a-235">443</span></span> | <span data-ttu-id="3286a-236">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3286a-236">HTTPS</span></span> | 
| <span data-ttu-id="3286a-237">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="3286a-237">*.core.windows.net</span></span> | <span data-ttu-id="3286a-238">443</span><span class="sxs-lookup"><span data-stu-id="3286a-238">443</span></span> | <span data-ttu-id="3286a-239">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3286a-239">HTTPS</span></span> | 
| <span data-ttu-id="3286a-240">Login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="3286a-240">login.microsoftonline.com</span></span> | <span data-ttu-id="3286a-241">443</span><span class="sxs-lookup"><span data-stu-id="3286a-241">443</span></span> | <span data-ttu-id="3286a-242">HTTPS</span><span class="sxs-lookup"><span data-stu-id="3286a-242">HTTPS</span></span> | 
| <span data-ttu-id="3286a-243">*. msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="3286a-243">*.msftncsi.com</span></span> | <span data-ttu-id="3286a-244">443</span><span class="sxs-lookup"><span data-stu-id="3286a-244">443</span></span> | <span data-ttu-id="3286a-245">Verbinding met internet tootest gebruikt wanneer Hallo gateway onbereikbaar via Hallo Power BI-service is.</span><span class="sxs-lookup"><span data-stu-id="3286a-245">Used tootest internet connectivity when hello gateway is unreachable by hello Power BI service.</span></span> | 

<span data-ttu-id="3286a-246">Als u tooapprove IP-adressen in plaats van Hallo domeinen hebt, kunt u downloaden en gebruiken van Hallo [Microsoft Azure Datacenter IP-adresbereiken lijst](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="3286a-246">If you have tooapprove IP addresses instead of hello domains, you can download and use hello [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="3286a-247">In sommige gevallen bestaan hello Azure Service Bus-verbindingen met IP-adres in plaats van een volledig gekwalificeerde domeinnamen.</span><span class="sxs-lookup"><span data-stu-id="3286a-247">In some cases, hello Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span></span>

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a><span data-ttu-id="3286a-248">Hoe werkt de gegevensgateway Hallo?</span><span class="sxs-lookup"><span data-stu-id="3286a-248">How does hello data gateway work?</span></span>

<span data-ttu-id="3286a-249">Hallo gegevensgateway vergemakkelijkt de snel en veilig communicatie tussen uw logische app, Hallo gateway-cloudservice en uw on-premises gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="3286a-249">hello data gateway facilitates quick and secure communication between your logic app, hello gateway cloud service, and your on-premises data source.</span></span> 

![diagram-for-on-premises-Data-gateway-flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

<span data-ttu-id="3286a-251">Dus als gebruiker in de cloud Hallo Hallo communiceert met een element dat is verbonden tooyour lokale gegevensbron:</span><span class="sxs-lookup"><span data-stu-id="3286a-251">So when hello user in hello cloud interacts with an element that's connected tooyour on-premises data source:</span></span>

1. <span data-ttu-id="3286a-252">Hallo gateway-cloudservice maakt van een query, samen met de Hallo versleuteld referenties voor gegevensbron hello, en stuurt Hallo query toohello wachtrij voor Hallo gateway tooprocess.</span><span class="sxs-lookup"><span data-stu-id="3286a-252">hello gateway cloud service creates a query, along with hello encrypted credentials for hello data source, and sends hello query toohello queue for hello gateway tooprocess.</span></span>

2. <span data-ttu-id="3286a-253">gateway-cloudservice Hallo Hallo query analyseert en pushes Hallo aanvraag toohello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3286a-253">hello gateway cloud service analyzes hello query and pushes hello request toohello Azure Service Bus.</span></span>

3. <span data-ttu-id="3286a-254">Hallo lokale gegevensgateway hello Azure Service Bus voor aanvragen in behandeling worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="3286a-254">hello on-premises data gateway polls hello Azure Service Bus for pending requests.</span></span>

4. <span data-ttu-id="3286a-255">Hallo gateway Hallo query opgehaald, ontsleutelt Hallo referenties en toohello-gegevensbron is verbonden met deze referenties.</span><span class="sxs-lookup"><span data-stu-id="3286a-255">hello gateway gets hello query, decrypts hello credentials, and connects toohello data source with those credentials.</span></span>

5. <span data-ttu-id="3286a-256">Hallo gateway verzendt Hallo toohello querygegevensbron voor uitvoering.</span><span class="sxs-lookup"><span data-stu-id="3286a-256">hello gateway sends hello query toohello data source for execution.</span></span>

6. <span data-ttu-id="3286a-257">Hallo resultaten worden van de gegevensbron hello, toohello back-gateway en toohello gateway-cloudservice verzonden.</span><span class="sxs-lookup"><span data-stu-id="3286a-257">hello results are sent from hello data source, back toohello gateway, and then toohello gateway cloud service.</span></span> <span data-ttu-id="3286a-258">Hallo gateway-cloudservice gebruikt vervolgens Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="3286a-258">hello gateway cloud service then uses hello results.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="3286a-259">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="3286a-259">Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="3286a-260">Algemeen</span><span class="sxs-lookup"><span data-stu-id="3286a-260">General</span></span>

<span data-ttu-id="3286a-261">**Q**: moet ik een gateway voor gegevensbronnen in de cloud hello, zoals SQL Azure?</span><span class="sxs-lookup"><span data-stu-id="3286a-261">**Q**: Do I need a gateway for data sources in hello cloud, such as SQL Azure?</span></span> <br/><span data-ttu-id="3286a-262">
**Een**: Nee.</span><span class="sxs-lookup"><span data-stu-id="3286a-262">
**A**: No.</span></span> <span data-ttu-id="3286a-263">Een gateway maakt verbinding alleen tooon-premises gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="3286a-263">A gateway connects tooon-premises data sources only.</span></span>

<span data-ttu-id="3286a-264">**Q**: heeft Hallo gateway geïnstalleerd op dezelfde computer als de gegevensbron Hallo Hallo toobe?</span><span class="sxs-lookup"><span data-stu-id="3286a-264">**Q**: Does hello gateway have toobe installed on hello same machine as hello data source?</span></span> <br/><span data-ttu-id="3286a-265">
**Een**: Nee.</span><span class="sxs-lookup"><span data-stu-id="3286a-265">
**A**: No.</span></span> <span data-ttu-id="3286a-266">Hallo-gateway wordt verbonden toohello-gegevensbron Hallo verbindingsgegevens die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3286a-266">hello gateway connects toohello data source using hello connection information that was provided.</span></span> <span data-ttu-id="3286a-267">Hallo gateway beschouwen als een client-toepassing in deze zin.</span><span class="sxs-lookup"><span data-stu-id="3286a-267">Consider hello gateway as a client application in this sense.</span></span> <span data-ttu-id="3286a-268">Hallo-gateway moet net Hallo mogelijkheid tooconnect toohello servernaam die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3286a-268">hello gateway just needs hello capability tooconnect toohello server name that was provided.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="3286a-269">**Q**: Waarom moet ik een Azure werk- of schoolaccount account toosign in?</span><span class="sxs-lookup"><span data-stu-id="3286a-269">**Q**: Why must I use an Azure work or school account toosign in?</span></span> <br/><span data-ttu-id="3286a-270">
**Een**: U kunt alleen een Azure werk- of schoolaccount wanneer u Hallo lokale gegevensgateway installeert.</span><span class="sxs-lookup"><span data-stu-id="3286a-270">
**A**: You can only use an Azure work or school account when you install hello on-premises data gateway.</span></span> <span data-ttu-id="3286a-271">Uw account wordt opgeslagen in een tenant die wordt beheerd door Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3286a-271">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="3286a-272">Uw Azure AD-account UPN (user Principal name) normaal gesproken komt overeen met Hallo e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="3286a-272">Usually, your Azure AD account's user principal name (UPN) matches hello email address.</span></span>

<span data-ttu-id="3286a-273">**Q**: waar mijn referenties worden opgeslagen?</span><span class="sxs-lookup"><span data-stu-id="3286a-273">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="3286a-274">
**Een**: Hallo-referenties die u voor een gegevensbron opgeeft zijn versleuteld en opgeslagen in Hallo gateway-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="3286a-274">
**A**: hello credentials that you enter for a data source are encrypted and stored in hello gateway cloud service.</span></span> <span data-ttu-id="3286a-275">Hallo-referenties worden op Hallo lokale gegevensgateway ontsleuteld.</span><span class="sxs-lookup"><span data-stu-id="3286a-275">hello credentials are decrypted at hello on-premises data gateway.</span></span>

<span data-ttu-id="3286a-276">**Q**: zijn er vereisten voor de bandbreedte van het netwerk?</span><span class="sxs-lookup"><span data-stu-id="3286a-276">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="3286a-277">
**Een**: het is raadzaam dat de netwerkverbinding goed doorvoer heeft.</span><span class="sxs-lookup"><span data-stu-id="3286a-277">
**A**: We recommend that your network connection has good throughput.</span></span> <span data-ttu-id="3286a-278">Elke omgeving is verschillend en Hallo hoeveelheid verzonden gegevens heeft op Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="3286a-278">Every environment is different, and hello amount of data being sent affects hello results.</span></span> <span data-ttu-id="3286a-279">Met behulp van ExpressRoute kan helpen bij het tooguarantee een mate van doorvoer tussen on-premises en hello Azure-datacenters.</span><span class="sxs-lookup"><span data-stu-id="3286a-279">Using ExpressRoute could help tooguarantee a level of throughput between on-premises and hello Azure datacenters.</span></span>
<span data-ttu-id="3286a-280">U kunt uw doorvoer Hallo hulpprogramma van derden Azure snelheid testen app toohelp meter.</span><span class="sxs-lookup"><span data-stu-id="3286a-280">You can use hello third-party tool Azure Speed Test app toohelp gauge your throughput.</span></span>

<span data-ttu-id="3286a-281">**Q**: Wat is er Hallo latentie voor actieve query's tooa gegevensbron van Hallo gateway?</span><span class="sxs-lookup"><span data-stu-id="3286a-281">**Q**: What is hello latency for running queries tooa data source from hello gateway?</span></span> <span data-ttu-id="3286a-282">Wat is de beste architectuur Hallo?</span><span class="sxs-lookup"><span data-stu-id="3286a-282">What is hello best architecture?</span></span> <br/><span data-ttu-id="3286a-283">
**Een**: tooreduce netwerklatentie, Hallo-gateway installeren als de gegevensbron sluiten toohello mogelijk.</span><span class="sxs-lookup"><span data-stu-id="3286a-283">
**A**: tooreduce network latency, install hello gateway as close toohello data source as possible.</span></span> <span data-ttu-id="3286a-284">Als u Hallo gateway op de werkelijke gegevensbron hello installeren kunt, minimaliseert deze nabijheid Hallo latentie geïntroduceerd.</span><span class="sxs-lookup"><span data-stu-id="3286a-284">If you can install hello gateway on hello actual data source, this proximity minimizes hello latency introduced.</span></span> <span data-ttu-id="3286a-285">Hallo datacenters te overwegen.</span><span class="sxs-lookup"><span data-stu-id="3286a-285">Consider hello datacenters too.</span></span> <span data-ttu-id="3286a-286">Bijvoorbeeld, als Hallo VS-West datacenter maakt gebruik van uw service en u SQL Server gehost in een virtuele machine in Azure hebt, moet uw virtuele Azure-machine Hallo VS-West te.</span><span class="sxs-lookup"><span data-stu-id="3286a-286">For example, if your service uses hello West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in hello West US too.</span></span> <span data-ttu-id="3286a-287">Deze nabijheid minimaliseert latentie en vermijdt u kosten voor uitgaande op Hallo Azure VM.</span><span class="sxs-lookup"><span data-stu-id="3286a-287">This proximity minimizes latency and avoids egress charges on hello Azure VM.</span></span>

<span data-ttu-id="3286a-288">**Q**: hoe worden resultaten verzonden back toohello cloud?</span><span class="sxs-lookup"><span data-stu-id="3286a-288">**Q**: How are results sent back toohello cloud?</span></span> <br/><span data-ttu-id="3286a-289">
**Een**: resultaten worden verzonden via hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3286a-289">
**A**: Results are sent through hello Azure Service Bus.</span></span>

<span data-ttu-id="3286a-290">**Q**: zijn er inkomende verbindingen toohello gateway vanuit de cloud Hallo?</span><span class="sxs-lookup"><span data-stu-id="3286a-290">**Q**: Are there any inbound connections toohello gateway from hello cloud?</span></span> <br/><span data-ttu-id="3286a-291">
**Een**: Nee.</span><span class="sxs-lookup"><span data-stu-id="3286a-291">
**A**: No.</span></span> <span data-ttu-id="3286a-292">Hallo-gateway gebruikt uitgaande verbindingen tooAzure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3286a-292">hello gateway uses outbound connections tooAzure Service Bus.</span></span>

<span data-ttu-id="3286a-293">**Q**: Wat gebeurt er als ik uitgaande verbindingen blokkeren?</span><span class="sxs-lookup"><span data-stu-id="3286a-293">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="3286a-294">Wat kan ik tooopen nodig?</span><span class="sxs-lookup"><span data-stu-id="3286a-294">What do I need tooopen?</span></span> <br/><span data-ttu-id="3286a-295">
**Een**: Zie Hallo poorten en hosts die Hallo gateway gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3286a-295">
**A**: See hello ports and hosts that hello gateway uses.</span></span>

<span data-ttu-id="3286a-296">**Q**: de werkelijke Windows-service Hallo zogenaamd?</span><span class="sxs-lookup"><span data-stu-id="3286a-296">**Q**: What is hello actual Windows service called?</span></span><br/><span data-ttu-id="3286a-297">
**Een**: In de Services Hallo gateway Power BI Enterprise Gateway-Service wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3286a-297">
**A**: In Services, hello gateway is called Power BI Enterprise Gateway Service.</span></span>

<span data-ttu-id="3286a-298">**Q**: kunt Hallo gateway Windows-service uitvoert met een Azure Active Directory-account?</span><span class="sxs-lookup"><span data-stu-id="3286a-298">**Q**: Can hello gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="3286a-299">
**Een**: Nee.</span><span class="sxs-lookup"><span data-stu-id="3286a-299">
**A**: No.</span></span> <span data-ttu-id="3286a-300">Hallo Windows-service moet een geldige Windows-account hebben.</span><span class="sxs-lookup"><span data-stu-id="3286a-300">hello Windows service must have a valid Windows account.</span></span> <span data-ttu-id="3286a-301">Standaard is Hallo-service wordt uitgevoerd met Hallo Service-SID NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="3286a-301">By default, hello service runs with hello Service SID, NT SERVICE\PBIEgwService.</span></span>

### <a name="high-availability-and-disaster-recovery"></a><span data-ttu-id="3286a-302">Hoge beschikbaarheid en herstel na noodgevallen</span><span class="sxs-lookup"><span data-stu-id="3286a-302">High availability and disaster recovery</span></span>

<span data-ttu-id="3286a-303">**Q**: welke opties zijn beschikbaar voor herstel na noodgevallen?</span><span class="sxs-lookup"><span data-stu-id="3286a-303">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="3286a-304">
**Een**: U kunt gebruiken Hallo herstel sleutel toorestore of verplaatsen van een gateway.</span><span class="sxs-lookup"><span data-stu-id="3286a-304">
**A**: You can use hello recovery key toorestore or move a gateway.</span></span> <span data-ttu-id="3286a-305">Wanneer u Hallo-gateway installeert, geef Hallo herstelsleutel.</span><span class="sxs-lookup"><span data-stu-id="3286a-305">When you install hello gateway, specify hello recovery key.</span></span>

<span data-ttu-id="3286a-306">**Q**: Wat is Hallo voordeel van de herstelsleutel Hallo?</span><span class="sxs-lookup"><span data-stu-id="3286a-306">**Q**: What is hello benefit of hello recovery key?</span></span> <br/><span data-ttu-id="3286a-307">
**Een**: Hallo herstelsleutel biedt een manier toomigrate of de gateway-instellingen herstellen na een noodgeval.</span><span class="sxs-lookup"><span data-stu-id="3286a-307">
**A**: hello recovery key provides a way toomigrate or recover your gateway settings after a disaster.</span></span>

<span data-ttu-id="3286a-308">**Q**: zijn er plannen voor het inschakelen van scenario's voor hoge beschikbaarheid met Hallo gateway?</span><span class="sxs-lookup"><span data-stu-id="3286a-308">**Q**: Are there any plans for enabling high availability scenarios with hello gateway?</span></span> <br/><span data-ttu-id="3286a-309">
**Een**: de volgende scenario's op Hallo roadmap, maar we een tijdlijn nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="3286a-309">
**A**: These scenarios are on hello roadmap, but we don't have a timeline yet.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3286a-310">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="3286a-310">Troubleshooting</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

<span data-ttu-id="3286a-311">**Q**: hoe kan ik zien welke query toohello on-premises gegevensbron worden verzonden?</span><span class="sxs-lookup"><span data-stu-id="3286a-311">**Q**: How can I see what queries are being sent toohello on-premises data source?</span></span> <br/><span data-ttu-id="3286a-312">
**Een**: U kunt inschakelen querytracering, waaronder het Hallo-query's die worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="3286a-312">
**A**: You can enable query tracing, which includes hello queries that are sent.</span></span> <span data-ttu-id="3286a-313">Houd er rekening mee toochange query tracering van de oorspronkelijke waarde toohello gedaan bij het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="3286a-313">Remember toochange query tracing back toohello original value when done troubleshooting.</span></span> <span data-ttu-id="3286a-314">Querytracering ingeschakeld verlaten maakt grotere Logboeken.</span><span class="sxs-lookup"><span data-stu-id="3286a-314">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="3286a-315">U kunt ook hulpprogramma's die de gegevensbron voor tracering van query's heeft bekijken.</span><span class="sxs-lookup"><span data-stu-id="3286a-315">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="3286a-316">U kunt bijvoorbeeld de Extended Events of SQL Profiler gebruiken voor SQL Server en Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="3286a-316">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="3286a-317">**Q**: waar zich de gateway-logboeken Hallo?</span><span class="sxs-lookup"><span data-stu-id="3286a-317">**Q**: Where are hello gateway logs?</span></span> <br/><span data-ttu-id="3286a-318">
**Een**: Zie's verderop in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="3286a-318">
**A**: See Tools later in this topic.</span></span>

### <a name="update-toohello-latest-version"></a><span data-ttu-id="3286a-319">Meest recente versie van de update toohello</span><span class="sxs-lookup"><span data-stu-id="3286a-319">Update toohello latest version</span></span>

<span data-ttu-id="3286a-320">Veel problemen kunnen surface wanneer Hallo gatewayversie verouderd.</span><span class="sxs-lookup"><span data-stu-id="3286a-320">Many issues can surface when hello gateway version becomes outdated.</span></span> <span data-ttu-id="3286a-321">Zorg ervoor dat u met de meest recente versie Hallo als goed over het algemeen.</span><span class="sxs-lookup"><span data-stu-id="3286a-321">As good general practice, make sure that you use hello latest version.</span></span> <span data-ttu-id="3286a-322">Als u dit nog niet hebt Hallo gateway voor een maand of langer bijgewerkt, kunt u Overweeg de installatie van de meest recente versie van gateway Hallo Hallo en zien als u Hallo probleem kan reproduceren.</span><span class="sxs-lookup"><span data-stu-id="3286a-322">If you haven't updated hello gateway for a month or longer, you might consider installing hello latest version of hello gateway, and see if you can reproduce hello issue.</span></span>

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="3286a-323">Fout: Kan tooadd gebruiker toogroup.</span><span class="sxs-lookup"><span data-stu-id="3286a-323">Error: Failed tooadd user toogroup.</span></span> <span data-ttu-id="3286a-324">(-2147463168 PBIEgwService Prestatielogboekgebruikers)</span><span class="sxs-lookup"><span data-stu-id="3286a-324">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="3286a-325">U kunt deze fout kan ophalen, als u probeert tooinstall Hallo gateway op een domeincontroller wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="3286a-325">You might get this error if you try tooinstall hello gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="3286a-326">Zorg ervoor dat u Hallo-gateway op een computer die een domeincontroller niet implementeert.</span><span class="sxs-lookup"><span data-stu-id="3286a-326">Make sure that you deploy hello gateway on a machine that isn't a domain controller.</span></span>

## <a name="tools"></a><span data-ttu-id="3286a-327">Hulpprogramma's</span><span class="sxs-lookup"><span data-stu-id="3286a-327">Tools</span></span>

### <a name="collect-logs-from-hello-gateway-configurer"></a><span data-ttu-id="3286a-328">Verzamelen van Logboeken van Hallo gateway configurer</span><span class="sxs-lookup"><span data-stu-id="3286a-328">Collect logs from hello gateway configurer</span></span>

<span data-ttu-id="3286a-329">U kunt verschillende logboeken voor Hallo gateway verzamelen.</span><span class="sxs-lookup"><span data-stu-id="3286a-329">You can collect several logs for hello gateway.</span></span> <span data-ttu-id="3286a-330">Begin altijd met Hallo Logboeken!</span><span class="sxs-lookup"><span data-stu-id="3286a-330">Always start with hello logs!</span></span>

#### <a name="installer-logs"></a><span data-ttu-id="3286a-331">Installatieprogramma Logboeken</span><span class="sxs-lookup"><span data-stu-id="3286a-331">Installer logs</span></span>

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a><span data-ttu-id="3286a-332">Configuratielogboeken</span><span class="sxs-lookup"><span data-stu-id="3286a-332">Configuration logs</span></span>

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="3286a-333">Enterprise gateway-service-Logboeken</span><span class="sxs-lookup"><span data-stu-id="3286a-333">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a><span data-ttu-id="3286a-334">Gebeurtenislogboeken</span><span class="sxs-lookup"><span data-stu-id="3286a-334">Event logs</span></span>

<span data-ttu-id="3286a-335">U vindt Hallo Data Management Gateway en PowerBIGateway Logboeken onder **servicelogboeken voor toepassingen en**.</span><span class="sxs-lookup"><span data-stu-id="3286a-335">You can find hello Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>

### <a name="fiddler-trace"></a><span data-ttu-id="3286a-336">Fiddler traceren</span><span class="sxs-lookup"><span data-stu-id="3286a-336">Fiddler Trace</span></span>

<span data-ttu-id="3286a-337">[Fiddler](http://www.telerik.com/fiddler) is een gratis hulpprogramma uit Telerik die HTTP-verkeer wordt bewaakt.</span><span class="sxs-lookup"><span data-stu-id="3286a-337">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span></span> <span data-ttu-id="3286a-338">U kunt dit verkeer met Power BI-service vanaf de clientcomputer Hallo Hallo zien.</span><span class="sxs-lookup"><span data-stu-id="3286a-338">You can see this traffic with hello Power BI service from hello client machine.</span></span> <span data-ttu-id="3286a-339">Deze service mogelijk fouten en andere gerelateerde informatie weergeven.</span><span class="sxs-lookup"><span data-stu-id="3286a-339">This service might show errors and other related information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3286a-340">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3286a-340">Next steps</span></span>
    
* [<span data-ttu-id="3286a-341">Verbinding maken met tooon-premises gegevens vanuit logic apps</span><span class="sxs-lookup"><span data-stu-id="3286a-341">Connect tooon-premises data from logic apps</span></span>](../logic-apps/logic-apps-gateway-connection.md)
* [<span data-ttu-id="3286a-342">Enterprise integration-functies</span><span class="sxs-lookup"><span data-stu-id="3286a-342">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="3286a-343">Connectors voor Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="3286a-343">Connectors for Azure Logic Apps</span></span>](../connectors/apis-list.md)
