---
title: aaaUse PowerShell tooCreate een virtuele machine met een Native modus rapportserver | Microsoft Docs
description: 'In dit onderwerp wordt beschreven en wordt u begeleid bij Hallo-implementatie en configuratie van een SQL Server Reporting Services native modus rapportserver in een virtuele Machine van Azure. '
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a><span data-ttu-id="d5321-103">Gebruik PowerShell tooCreate een Azure VM met een Native modus Report Server</span><span class="sxs-lookup"><span data-stu-id="d5321-103">Use PowerShell tooCreate an Azure VM With a Native Mode Report Server</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="d5321-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d5321-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d5321-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="d5321-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="d5321-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d5321-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="d5321-107">In dit onderwerp wordt beschreven en wordt u begeleid bij Hallo-implementatie en configuratie van een SQL Server Reporting Services native modus rapportserver in een virtuele Machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="d5321-107">This topic describes and walks you through hello deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span></span> <span data-ttu-id="d5321-108">Hallo stappen in dit document een combinatie van handmatige stappen toocreate Hallo virtuele machine en een Windows PowerShell-script voor tooconfigure Reporting Services op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="d5321-108">hello steps in this document use a combination of manual steps toocreate hello virtual machine and a Windows PowerShell script tooconfigure Reporting Services on hello VM.</span></span> <span data-ttu-id="d5321-109">Hallo-configuratiescript bevat een firewallpoort worden geopend voor HTTP of HTTPs.</span><span class="sxs-lookup"><span data-stu-id="d5321-109">hello configuration script includes opening a firewall port for HTTP or HTTPs.</span></span>

> [!NOTE]
> <span data-ttu-id="d5321-110">Als u geen vereist **HTTPS** op Hallo rapportserver **slaat u stap 2**.</span><span class="sxs-lookup"><span data-stu-id="d5321-110">If you do not require **HTTPS** on hello report server, **skip step 2**.</span></span>
> 
> <span data-ttu-id="d5321-111">Ga nadat Hallo VM is gemaakt in stap 1, toohello sectie gebruik script tooconfigure Hallo report server- en HTTP.</span><span class="sxs-lookup"><span data-stu-id="d5321-111">After creating hello VM in step 1, go toohello section Use script tooconfigure hello report server and HTTP.</span></span> <span data-ttu-id="d5321-112">Nadat u Hallo script uitvoert, is de rapportserver Hallo gereed toouse.</span><span class="sxs-lookup"><span data-stu-id="d5321-112">After you run hello script, hello report server is ready toouse.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="d5321-113">Vereisten en veronderstellingen</span><span class="sxs-lookup"><span data-stu-id="d5321-113">Prerequisites and Assumptions</span></span>
* <span data-ttu-id="d5321-114">**Azure-abonnement**: Controleer of het aantal kernen dat beschikbaar is in uw Azure-abonnement Hallo.</span><span class="sxs-lookup"><span data-stu-id="d5321-114">**Azure Subscription**: Verify hello number of cores available in your Azure Subscription.</span></span> <span data-ttu-id="d5321-115">Als u VM-grootte van aanbevolen Hallo maakt **A3**, moet u **4** beschikbaar kernen.</span><span class="sxs-lookup"><span data-stu-id="d5321-115">If you create hello recommended VM size of **A3**, you need **4** available cores.</span></span> <span data-ttu-id="d5321-116">Als u een VM-grootte van **A2**, moet u **2** beschikbaar kernen.</span><span class="sxs-lookup"><span data-stu-id="d5321-116">If you use a VM size of **A2**, you need **2** available cores.</span></span>
  
  * <span data-ttu-id="d5321-117">tooverify hello core limiet van uw abonnement op Hallo klassieke Azure-portal, klik op instellingen in het linkerdeelvenster Hallo en vervolgens klikt u op informatie over het gebruik in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="d5321-117">tooverify hello core limit of your subscription, in hello Azure classic portal, click SETTINGS in hello left pane and then Click USAGE in hello top menu.</span></span>
  * <span data-ttu-id="d5321-118">tooincrease hello quotum voor kernen, neem contact op met [ondersteuning van Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="d5321-118">tooincrease hello core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span></span> <span data-ttu-id="d5321-119">Zie voor informatie over de grootte van virtuele machine [grootten van virtuele machines voor Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d5321-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="d5321-120">**Windows PowerShell-scripts**: Hallo onderwerp wordt ervan uitgegaan dat u een werkende basiskennis hebben van Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d5321-120">**Windows PowerShell Scripting**: hello topic assumes that you have a basic working knowledge of Windows PowerShell.</span></span> <span data-ttu-id="d5321-121">Zie voor meer informatie over het gebruik van Windows PowerShell Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="d5321-121">For more information about using Windows PowerShell, see hello following:</span></span>
  
  * [<span data-ttu-id="d5321-122">Windows PowerShell op WindowsServer wordt gestart</span><span class="sxs-lookup"><span data-stu-id="d5321-122">Starting Windows PowerShell on Windows Server</span></span>](https://technet.microsoft.com/library/hh847814.aspx)
  * [<span data-ttu-id="d5321-123">Aan de slag met Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5321-123">Getting Started with Windows PowerShell</span></span>](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a><span data-ttu-id="d5321-124">Stap 1: Een Azure-Machine inrichten</span><span class="sxs-lookup"><span data-stu-id="d5321-124">Step 1: Provision an Azure Virtual Machine</span></span>
1. <span data-ttu-id="d5321-125">Blader toohello klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d5321-125">Browse toohello Azure classic portal.</span></span>
2. <span data-ttu-id="d5321-126">Klik op **virtuele Machines** in het linkerdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="d5321-126">Click **Virtual Machines** in hello left pane.</span></span>
   
    ![Microsoft azure virtuele machines](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. <span data-ttu-id="d5321-128">Klik op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="d5321-128">Click **New**.</span></span>
   
    ![Knop Nieuw](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. <span data-ttu-id="d5321-130">Klik op **vanuit galerie**.</span><span class="sxs-lookup"><span data-stu-id="d5321-130">Click **From Gallery**.</span></span>
   
    ![nieuwe virtuele machine vanuit galerie](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. <span data-ttu-id="d5321-132">Klik op **SQL Server 2014 RTM Standard – Windows Server 2012 R2** en klik vervolgens op Hallo pijl toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d5321-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click hello arrow toocontinue.</span></span>
   
    ![Volgende](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    <span data-ttu-id="d5321-134">Als u Hallo Reporting Services gegevensgestuurde abonnementen functie nodig hebt, kiest u **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span><span class="sxs-lookup"><span data-stu-id="d5321-134">If you need hello Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span></span> <span data-ttu-id="d5321-135">Zie voor meer informatie over SQL Server-edities en functieondersteuning [functies ondersteund door het Hallo-edities van SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span><span class="sxs-lookup"><span data-stu-id="d5321-135">For more information on SQL Server editions and feature support, see [Features Supported by hello Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span></span>
6. <span data-ttu-id="d5321-136">Op Hallo **Virtuele-machineconfiguratie** pagina, Hallo volgende velden te bewerken:</span><span class="sxs-lookup"><span data-stu-id="d5321-136">On hello **Virtual machine configuration** page, edit hello following fields:</span></span>
   
   * <span data-ttu-id="d5321-137">Als er meer dan één **versie RELEASEDATUM**, selecteer Hallo meest recente versie.</span><span class="sxs-lookup"><span data-stu-id="d5321-137">If there is more than one **VERSION RELEASE DATE**, select hello most recent version.</span></span>
   * <span data-ttu-id="d5321-138">**Naam van virtuele Machine**: naam van de machine Hallo wordt ook gebruikt op de volgende configuratiepagina Hallo als Hallo standaard Cloud Service DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="d5321-138">**Virtual Machine Name**: hello machine name is also used on hello next configuration page as hello default Cloud Service DNS name.</span></span> <span data-ttu-id="d5321-139">Hallo DNS-naam moet uniek zijn in hello Azure-service.</span><span class="sxs-lookup"><span data-stu-id="d5321-139">hello DNS name must be unique across hello Azure service.</span></span> <span data-ttu-id="d5321-140">Overweeg het Hallo VM configureren met de computernaam van een die wordt beschreven welke Hallo VM wordt gebruikt voor.</span><span class="sxs-lookup"><span data-stu-id="d5321-140">Consider configuring hello VM with a computer name that describes what hello VM is used for.</span></span> <span data-ttu-id="d5321-141">Bijvoorbeeld ssrsnativecloud.</span><span class="sxs-lookup"><span data-stu-id="d5321-141">For example ssrsnativecloud.</span></span>
   * <span data-ttu-id="d5321-142">**Laag**: standaard</span><span class="sxs-lookup"><span data-stu-id="d5321-142">**Tier**: Standard</span></span>
   * <span data-ttu-id="d5321-143">**Grootte: A3** wordt aanbevolen Hallo VM-grootte voor SQL Server-werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="d5321-143">**Size:A3** is hello recommended VM size for SQL Server workloads.</span></span> <span data-ttu-id="d5321-144">Als een virtuele machine alleen als een rapportserver gebruikt wordt, is een VM-grootte van A2 voldoende tenzij Hallo rapportserver optreedt in een grote werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="d5321-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless hello report server experiences a large workload.</span></span> <span data-ttu-id="d5321-145">Zie voor een VM prijsgegevens, [prijzen van virtuele Machines](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="d5321-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
   * <span data-ttu-id="d5321-146">**Nieuwe gebruikersnaam**: Hallo die u opgeeft als een beheerder op Hallo VM wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d5321-146">**New User Name**: hello name you provide is created as an administrator on hello VM.</span></span>
   * <span data-ttu-id="d5321-147">**Nieuw wachtwoord** en **bevestigen**.</span><span class="sxs-lookup"><span data-stu-id="d5321-147">**New Password** and **confirm**.</span></span> <span data-ttu-id="d5321-148">Dit wachtwoord wordt gebruikt voor nieuwe Hallo-administrator-account en het wordt aanbevolen dat een sterk wachtwoord te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d5321-148">This password is used for hello new administrator account and it is recommended you use a strong password.</span></span>
   * <span data-ttu-id="d5321-149">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="d5321-149">Click **Next**.</span></span> <span data-ttu-id="d5321-150">![volgende](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span><span class="sxs-lookup"><span data-stu-id="d5321-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span></span>
7. <span data-ttu-id="d5321-151">Op de volgende pagina Hallo Hallo volgende velden te bewerken:</span><span class="sxs-lookup"><span data-stu-id="d5321-151">On hello next page, edit hello following fields:</span></span>
   
   * <span data-ttu-id="d5321-152">**Cloudservice**: Selecteer **Maak een nieuwe Cloudservice**.</span><span class="sxs-lookup"><span data-stu-id="d5321-152">**Cloud Service**: select **Create a new Cloud Service**.</span></span>
   * <span data-ttu-id="d5321-153">**Cloud-Service DNS-naam**: dit Hallo openbare DNS-naam van Hallo Cloudservice die is gekoppeld aan Hallo VM is.</span><span class="sxs-lookup"><span data-stu-id="d5321-153">**Cloud Service DNS Name**: This is hello public DNS name of hello Cloud Service that is associated with hello VM.</span></span> <span data-ttu-id="d5321-154">Hallo is standaard Hallo naam die u hebt getypt voor Hallo VM-naam.</span><span class="sxs-lookup"><span data-stu-id="d5321-154">hello default name is hello name you typed in for hello VM name.</span></span> <span data-ttu-id="d5321-155">Als in latere stappen van Hallo onderwerp u een vertrouwd certificaat voor SSL maakt en vervolgens Hallo DNS-naam wordt gebruikt voor de waarde Hallo Hallo '**verleend aan**' hello certificaat.</span><span class="sxs-lookup"><span data-stu-id="d5321-155">If in later steps of hello topic, you create a trusted SSL certificate and then hello DNS name is used for hello value of hello “**Issued to**” of hello certificate.</span></span>
   * <span data-ttu-id="d5321-156">**Regio/affiniteit groep/virtueel netwerk**: Kies Hallo regio dichtstbijzijnde tooyour eindgebruikers.</span><span class="sxs-lookup"><span data-stu-id="d5321-156">**Region/Affinity Group/Virtual Network**: Choose hello region closest tooyour end users.</span></span>
   * <span data-ttu-id="d5321-157">**Storage-Account**: een automatisch gegenereerde opslagaccount gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d5321-157">**Storage Account**: Use an automatically generated storage account.</span></span>
   * <span data-ttu-id="d5321-158">**Beschikbaarheidsset**: geen.</span><span class="sxs-lookup"><span data-stu-id="d5321-158">**Availability Set**: None.</span></span>
   * <span data-ttu-id="d5321-159">**EINDPUNTEN** behouden Hallo **extern bureaublad** en **PowerShell** eindpunten en voeg vervolgens een HTTP- of HTTPS-eindpunt, afhankelijk van uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="d5321-159">**ENDPOINTS** Keep hello **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span></span>
     
     * <span data-ttu-id="d5321-160">**HTTP**: openbare en particuliere poorten zijn standaard Hallo **80**.</span><span class="sxs-lookup"><span data-stu-id="d5321-160">**HTTP**: hello default public and private ports are **80**.</span></span> <span data-ttu-id="d5321-161">Let op: als u een particuliere poort dan 80, wijzigt u **$HTTPport = 80** in Hallo HTTP-script.</span><span class="sxs-lookup"><span data-stu-id="d5321-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in hello http script.</span></span>
     * <span data-ttu-id="d5321-162">**HTTPS**: openbare en particuliere poorten zijn standaard Hallo **443**.</span><span class="sxs-lookup"><span data-stu-id="d5321-162">**HTTPS**: hello default public and private ports are **443**.</span></span> <span data-ttu-id="d5321-163">Een best practice bij beveiliging wordt toochange Hallo particuliere poort en uw firewall en Hallo report server toouse Hallo particuliere poort configureren.</span><span class="sxs-lookup"><span data-stu-id="d5321-163">A security best practice is toochange hello private port and configure your firewall and hello report server toouse hello private port.</span></span> <span data-ttu-id="d5321-164">Zie voor meer informatie over eindpunten [hoe tooSet van communicatie met een virtuele Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d5321-164">For more information on endpoints, see [How tooSet Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="d5321-165">Let op: als u een andere poort dan 443, wijzigt u de parameter Hallo **$HTTPsport = 443** in Hallo HTTPS-script.</span><span class="sxs-lookup"><span data-stu-id="d5321-165">Note that if you use a port other than 443, change hello parameter **$HTTPsport = 443** in hello HTTPS script.</span></span>
   * <span data-ttu-id="d5321-166">Klik op volgende.</span><span class="sxs-lookup"><span data-stu-id="d5321-166">Click next .</span></span> ![Volgende](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. <span data-ttu-id="d5321-168">Op de laatste pagina van wizard Hallo Hallo houden Hallo standaard **Hallo VM-agent installeren** geselecteerde.</span><span class="sxs-lookup"><span data-stu-id="d5321-168">On hello last page of hello wizard, keep hello default **Install hello VM agent** selected.</span></span> <span data-ttu-id="d5321-169">Hallo stappen in dit onderwerp, maken geen gebruik Hallo VM-agent, maar als u van plan tookeep deze virtuele machine bent, VM-agent Hallo en -extensies kunt u tooenhance hij CM.</span><span class="sxs-lookup"><span data-stu-id="d5321-169">hello steps in this topic do not utilize hello VM agent but if you plan tookeep this VM, hello VM agent and extensions will allow you tooenhance he CM.</span></span>  <span data-ttu-id="d5321-170">Zie voor meer informatie over de VM-agent Hallo [VM-Agent en -extensies – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span><span class="sxs-lookup"><span data-stu-id="d5321-170">For more information on hello VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span></span> <span data-ttu-id="d5321-171">Een Hallo standaard extensies geïnstalleerd ad met Hallo 'BGINFO'-extensie die wordt weergegeven op de VM-bureaublad hello, systeemgegevens zoals intern IP-adres en de vrije ruimte station.</span><span class="sxs-lookup"><span data-stu-id="d5321-171">One of hello default extensions installed ad running is hello “BGINFO” extension that displays on hello VM desktop, system information such as internal IP and free drive space.</span></span>
9. <span data-ttu-id="d5321-172">Klik op voltooien.</span><span class="sxs-lookup"><span data-stu-id="d5321-172">Click complete .</span></span> ![OK](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. <span data-ttu-id="d5321-174">Hallo **Status** Hallo VM wordt weergegeven als **starten (inrichten)** tijdens Hallo inrichten proces en vervolgens wordt weergegeven, **met** wanneer Hallo VM is ingericht en gereed toouse.</span><span class="sxs-lookup"><span data-stu-id="d5321-174">hello **Status** of hello VM displays as **Starting (Provisioning)** during hello provision process and then displays as **Running** when hello VM is provisioned and ready toouse.</span></span>

## <a name="step-2-create-a-server-certificate"></a><span data-ttu-id="d5321-175">Stap 2: Een servercertificaat maken</span><span class="sxs-lookup"><span data-stu-id="d5321-175">Step 2: Create a Server Certificate</span></span>
> [!NOTE]
> <span data-ttu-id="d5321-176">Als u HTTPS niet op de rapportserver hello vereist, kunt u **slaat u stap 2** en ga toohello sectie **script tooconfigure Hallo report server- en HTTP gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="d5321-176">If you do not require HTTPS on hello report server, you can **skip step 2** and go toohello section **Use script tooconfigure hello report server and HTTP**.</span></span> <span data-ttu-id="d5321-177">Gebruik Hallo HTTP script tooquickly Hallo rapportserver en Hallo report server bevindt zich nu toouse configureren.</span><span class="sxs-lookup"><span data-stu-id="d5321-177">Use hello HTTP script tooquickly configure hello report server and hello report server will be ready toouse.</span></span>

<span data-ttu-id="d5321-178">In de volgorde toouse HTTPS op Hallo VM moet u een vertrouwd certificaat voor SSL.</span><span class="sxs-lookup"><span data-stu-id="d5321-178">In order toouse HTTPS on hello VM, you need a trusted SSL certificate.</span></span> <span data-ttu-id="d5321-179">Afhankelijk van uw scenario kunt u een van de volgende twee methoden hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d5321-179">Depending on your scenario, you can use one of hello following two methods:</span></span>

* <span data-ttu-id="d5321-180">Een geldig SSL-certificaat uitgegeven door een certificeringsinstantie (CA) en wordt vertrouwd door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d5321-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span></span> <span data-ttu-id="d5321-181">Hallo CA-basiscertificaten zijn vereiste toobe gedistribueerd via Hallo Microsoft Root Certificate Program.</span><span class="sxs-lookup"><span data-stu-id="d5321-181">hello CA root certificates are required toobe distributed via hello Microsoft Root Certificate Program.</span></span> <span data-ttu-id="d5321-182">Zie voor meer informatie over dit programma [Windows en Windows Phone 8 SSL Root Certificate Program (lid CA's)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) en [inleiding toohello Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5321-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction toohello Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span></span>
* <span data-ttu-id="d5321-183">Een zelfondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="d5321-183">A self-signed certificate.</span></span> <span data-ttu-id="d5321-184">Zelfondertekende certificaten worden niet aanbevolen voor productieomgevingen.</span><span class="sxs-lookup"><span data-stu-id="d5321-184">Self-signed certificates are not recommended for production environments.</span></span>

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a><span data-ttu-id="d5321-185">toouse een certificaat gemaakt door een vertrouwde certificeringsinstantie (CA)</span><span class="sxs-lookup"><span data-stu-id="d5321-185">toouse a certificate created by a trusted Certificate Authority (CA)</span></span>
1. <span data-ttu-id="d5321-186">**Vraag een servercertificaat voor de website van de Hallo van een certificeringsinstantie**.</span><span class="sxs-lookup"><span data-stu-id="d5321-186">**Request a server certificate for hello website from a certification authority**.</span></span> 
   
    <span data-ttu-id="d5321-187">U kunt beide toogenerate een certificaataanvraagbestand (Certreq.txt) te sturen tooa certificeringsinstantie (CA) of toogenerate een aanvraag voor een online-certificeringsinstantie Hallo Wizard Webservercertificaat.</span><span class="sxs-lookup"><span data-stu-id="d5321-187">You can use hello Web Server Certificate Wizard either toogenerate a certificate request file (Certreq.txt) that you send tooa certification authority, or toogenerate a request for an online certification authority.</span></span> <span data-ttu-id="d5321-188">Bijvoorbeeld: Microsoft Certificate Services in Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="d5321-188">For example, Microsoft Certificate Services in Windows Server 2012.</span></span> <span data-ttu-id="d5321-189">Afhankelijk van Hallo identificatie zekerheidsniveau die worden aangeboden door uw servercertificaat, is enkele dagen tooseveral maanden voor Hallo certification authority tooapprove uw aanvraag en verzendt u een certificaatbestand.</span><span class="sxs-lookup"><span data-stu-id="d5321-189">Depending on hello level of identification assurance offered by your server certificate, it is several days tooseveral months for hello certification authority tooapprove your request and send you a certificate file.</span></span> 
   
    <span data-ttu-id="d5321-190">Zie voor meer informatie over het aanvragen van een servercertificaten Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="d5321-190">For more information about requesting a server certificates, see hello following:</span></span> 
   
   * <span data-ttu-id="d5321-191">Gebruik [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5321-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span></span>
   * <span data-ttu-id="d5321-192">Security Tools tooAdminister Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="d5321-192">Security Tools tooAdminister Windows Server 2012.</span></span>
     
     [<span data-ttu-id="d5321-193">Security Tools tooAdminister Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d5321-193">Security Tools tooAdminister Windows Server 2012</span></span>](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > <span data-ttu-id="d5321-194">Hallo **verleend aan** veld Hallo vertrouwde SSL-certificaat moet worden Hallo dezelfde als Hallo **Cloud Service DNS-naam** u hebt gebruikt voor nieuwe VM Hallo.</span><span class="sxs-lookup"><span data-stu-id="d5321-194">hello **issued to** field of hello trusted SSL certificate should be hello same as hello **Cloud Service DNS NAME** you used for hello new VM.</span></span>

2. <span data-ttu-id="d5321-195">**Hallo-servercertificaat installeren op de webserver Hallo**.</span><span class="sxs-lookup"><span data-stu-id="d5321-195">**Install hello server certificate on hello Web server**.</span></span> <span data-ttu-id="d5321-196">Hallo-webserver is in dit geval Hallo VM dat hosts Hallo rapportserver en Hallo-website is gemaakt in latere stappen bij het configureren van Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="d5321-196">hello Web server in this case is hello VM that hosts hello report server and hello website is created in later steps when you configure Reporting Services.</span></span> <span data-ttu-id="d5321-197">Zie voor meer informatie over het Hallo-servercertificaat installeren op Hallo-webserver met behulp van Hallo MMC-module certificaat [een servercertificaat installeren](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="d5321-197">For more information about installing hello server certificate on hello Web server by using hello Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
    <span data-ttu-id="d5321-198">Als u wilt dat toouse Hallo script is opgenomen in dit onderwerp, rapportserver tooconfigure hello, waarde van de certificaten Hallo Hallo **vingerafdruk** is vereist als een parameter van het Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="d5321-198">If you want toouse hello script included with this topic, tooconfigure hello report server, hello value of hello certificates **Thumbprint** is required as a parameter of hello script.</span></span> <span data-ttu-id="d5321-199">Zie Hallo volgende sectie voor meer informatie over hoe tooobtain vingerafdruk van certificaat Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="d5321-199">See hello next section for details on how tooobtain hello thumbprint of hello certificate.</span></span>
3. <span data-ttu-id="d5321-200">Hallo server certificaat toohello-rapportserver toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d5321-200">Assign hello server certificate toohello report server.</span></span> <span data-ttu-id="d5321-201">Hallo-toewijzing is voltooid in de volgende sectie Hallo bij het configureren van Hallo-rapportserver.</span><span class="sxs-lookup"><span data-stu-id="d5321-201">hello assignment is completed in hello next section when you configure hello report server.</span></span>

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a><span data-ttu-id="d5321-202">toouse hello zelfondertekende certificaten voor virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="d5321-202">toouse hello Virtual Machines Self-signed Certificate</span></span>
<span data-ttu-id="d5321-203">Een zelfondertekend certificaat is gemaakt op Hallo VM wanneer Hallo VM is ingericht.</span><span class="sxs-lookup"><span data-stu-id="d5321-203">A self-signed certificate was created on hello VM when hello VM was provisioned.</span></span> <span data-ttu-id="d5321-204">Hallo-certificaat heeft dezelfde naam als Hallo VM DNS-naam Hallo.</span><span class="sxs-lookup"><span data-stu-id="d5321-204">hello certificate has hello same name as hello VM DNS name.</span></span> <span data-ttu-id="d5321-205">In de volgorde tooavoid certificaatfouten, is het vereist dat Hallo-certificaat wordt vertrouwd op Hallo VM zichzelf en voor alle gebruikers van Hallo-site.</span><span class="sxs-lookup"><span data-stu-id="d5321-205">In order tooavoid certificate errors, it is required that hello certificate is trusted on hello VM itself, and also by all users of hello site.</span></span>

1. <span data-ttu-id="d5321-206">tootrust hello basis-CA van Hallo-certificaat op Hallo lokale VM toevoegen Hallo certificaat toohello **Trusted Root Certification Authorities**.</span><span class="sxs-lookup"><span data-stu-id="d5321-206">tootrust hello root CA of hello certificate on hello Local VM, add hello certificate toohello **Trusted Root Certification Authorities**.</span></span> <span data-ttu-id="d5321-207">Hallo Hieronder volgt een samenvatting van Hallo stappen vereist.</span><span class="sxs-lookup"><span data-stu-id="d5321-207">hello following is a summary of hello steps required.</span></span> <span data-ttu-id="d5321-208">Zie voor gedetailleerde stappen op hoe tootrust CA Hallo [een servercertificaat installeren](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="d5321-208">For detailed steps on how tootrust hello CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
   1. <span data-ttu-id="d5321-209">Selecteer in de klassieke Azure-portal hello, Hallo VM en klik op verbinden.</span><span class="sxs-lookup"><span data-stu-id="d5321-209">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="d5321-210">Afhankelijk van de browserconfiguratie van uw, hebt u mogelijk na vragen aan gebruiker toosave een RDP-bestand voor het verbinden van toohello VM.</span><span class="sxs-lookup"><span data-stu-id="d5321-210">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
      
       ![verbinding maken met tooazure virtuele machine](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="d5321-212">Hallo VM gebruikersnaam, gebruikersnaam en wachtwoord die u hebt geconfigureerd tijdens het maken van VM hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d5321-212">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
      
       <span data-ttu-id="d5321-213">In Hallo installatiekopie te volgen, Hallo VM-naam is bijvoorbeeld **ssrsnativecloud** en gebruikersnaam Hallo **testgebruiker**.</span><span class="sxs-lookup"><span data-stu-id="d5321-213">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
      
       ![aanmeldingsnaam opgenomen vm](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. <span data-ttu-id="d5321-215">Mmc.exe worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d5321-215">Run mmc.exe.</span></span> <span data-ttu-id="d5321-216">Zie voor meer informatie [hoe: certificaten weergeven met Hallo MMC-module](https://msdn.microsoft.com/library/ms788967.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5321-216">For more information, see [How to: View Certificates with hello MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span></span>
   3. <span data-ttu-id="d5321-217">In de consoletoepassing Hallo **bestand** menu toevoegen Hallo **certificaten** -module, selecteer **computeraccount** wanneer u wordt gevraagd en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d5321-217">In hello console application **File** menu, add hello **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span></span>
   4. <span data-ttu-id="d5321-218">Selecteer **lokale Computer** toomanage en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="d5321-218">Select **Local Computer** toomanage and then click **Finish**.</span></span>
   5. <span data-ttu-id="d5321-219">Klik op **Ok** en vouw vervolgens Hallo **certificaten - persoonlijke** knooppunten en klik vervolgens op **certificaten**.</span><span class="sxs-lookup"><span data-stu-id="d5321-219">Click **Ok** and then expand hello **Certificates -Personal** nodes and then click **Certificates**.</span></span> <span data-ttu-id="d5321-220">Hallo certificaat Hallo DNS-naam van Hallo VM heeft de naam en eindigt op **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="d5321-220">hello certificate is named after hello DNS name of hello VM and ends with **cloudapp.net**.</span></span> <span data-ttu-id="d5321-221">Met de rechtermuisknop op de certificaatnaam Hallo en klik op **kopie**.</span><span class="sxs-lookup"><span data-stu-id="d5321-221">Right-click hello certificate name and click **Copy**.</span></span>
   6. <span data-ttu-id="d5321-222">Vouw Hallo **Trusted Root Certification Authorities** knooppunt en klik met de rechtermuisknop **certificaten** en klik vervolgens op **plakken**.</span><span class="sxs-lookup"><span data-stu-id="d5321-222">Expand hello **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span></span>
   7. <span data-ttu-id="d5321-223">toovalidate dubbele klikt u op de certificaatnaam Hallo onder **Trusted Root Certification Authorities** en controleer of er zijn geen fouten ziet u uw certificaat.</span><span class="sxs-lookup"><span data-stu-id="d5321-223">toovalidate, double click on hello certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span></span> <span data-ttu-id="d5321-224">Als u wilt dat toouse Hallo HTTPS script is opgenomen in dit onderwerp, rapportserver tooconfigure hello, waarde van de certificaten Hallo Hallo **vingerafdruk** is vereist als een parameter van het Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="d5321-224">If you want toouse hello HTTPS script included with this topic, tooconfigure hello report server, hello value of hello certificates **Thumbprint** is required as a parameter of hello script.</span></span> <span data-ttu-id="d5321-225">**tooget hello vingerafdrukwaarde**, Hallo volgende voltooien.</span><span class="sxs-lookup"><span data-stu-id="d5321-225">**tooget hello thumbprint value**, complete hello following.</span></span> <span data-ttu-id="d5321-226">Er is ook een PowerShell-voorbeeld tooretrieve Hallo vingerafdruk in sectie [script tooconfigure Hallo report server- en HTTPS gebruiken](#use-script-to-configure-the-report-server-and-HTTPS).</span><span class="sxs-lookup"><span data-stu-id="d5321-226">There is also a PowerShell sample tooretrieve hello thumbprint in section [Use script tooconfigure hello report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span></span>
      
      1. <span data-ttu-id="d5321-227">Dubbelklik op Hallo van Hallo certificaat, bijvoorbeeld ssrsnativecloud.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="d5321-227">Double-click hello name of hello certificate, for example ssrsnativecloud.cloudapp.net.</span></span>
      2. <span data-ttu-id="d5321-228">Klik op Hallo **Details** tabblad.</span><span class="sxs-lookup"><span data-stu-id="d5321-228">Click hello **Details** tab.</span></span>
      3. <span data-ttu-id="d5321-229">Klik op **vingerafdruk**.</span><span class="sxs-lookup"><span data-stu-id="d5321-229">Click **Thumbprint**.</span></span> <span data-ttu-id="d5321-230">Hallo-waarde van de vingerafdruk van het Hallo wordt weergegeven in het veld Hallo details, bijvoorbeeld a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span><span class="sxs-lookup"><span data-stu-id="d5321-230">hello value of hello thumbprint is displayed in hello details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span></span>
      4. <span data-ttu-id="d5321-231">Kopieer de vingerafdruk Hallo en Hallo waarde opslaan voor later of Hallo script nu bewerken.</span><span class="sxs-lookup"><span data-stu-id="d5321-231">Copy hello thumbprint and save hello value for later or edit hello script now.</span></span>
      5. <span data-ttu-id="d5321-232">(*) Voordat u Hallo script uitvoert, verwijdert u Hallo spaties tussen Hallo-waardeparen.</span><span class="sxs-lookup"><span data-stu-id="d5321-232">(*) Before you run hello script, remove hello spaces in between hello pairs of values.</span></span> <span data-ttu-id="d5321-233">Hallo-vingerafdruk die al eerder is vermeld zou bijvoorbeeld nu a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f zijn.</span><span class="sxs-lookup"><span data-stu-id="d5321-233">For example hello thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span></span>
      6. <span data-ttu-id="d5321-234">Hallo server certificaat toohello-rapportserver toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d5321-234">Assign hello server certificate toohello report server.</span></span> <span data-ttu-id="d5321-235">Hallo-toewijzing is voltooid in de volgende sectie Hallo bij het configureren van Hallo-rapportserver.</span><span class="sxs-lookup"><span data-stu-id="d5321-235">hello assignment is completed in hello next section when you configure hello report server.</span></span>

<span data-ttu-id="d5321-236">Als u een zelfondertekend SSL-certificaat gebruikt, overeenkomt met met Hallo-naam op Hallo certificaat al Hallo-hostnaam van Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="d5321-236">If you are using a self-signed SSL certificate, hello name on hello certificate already matches hello hostname of hello VM.</span></span> <span data-ttu-id="d5321-237">Daarom Hallo Hallo machine DNS is al geregistreerd globaal en toegankelijk zijn vanaf elke client.</span><span class="sxs-lookup"><span data-stu-id="d5321-237">Therefore, hello DNS of hello machine is already registered globally and can be accessed from any client.</span></span>

## <a name="step-3-configure-hello-report-server"></a><span data-ttu-id="d5321-238">Stap 3: Hallo Report Server configureren</span><span class="sxs-lookup"><span data-stu-id="d5321-238">Step 3: Configure hello Report Server</span></span>
<span data-ttu-id="d5321-239">Deze sectie helpt u bij het Hallo VM als een rapportserver voor native-modus van Reporting Services configureren.</span><span class="sxs-lookup"><span data-stu-id="d5321-239">This section walks you through configuring hello VM as a Reporting Services native mode report server.</span></span> <span data-ttu-id="d5321-240">U kunt een Hallo methoden tooconfigure Hallo rapportserver volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d5321-240">You can use one of hello following methods tooconfigure hello report server:</span></span>

* <span data-ttu-id="d5321-241">Hallo script tooconfigure Hallo-rapportserver gebruiken</span><span class="sxs-lookup"><span data-stu-id="d5321-241">Use hello script tooconfigure hello report server</span></span>
* <span data-ttu-id="d5321-242">Gebruik Configuration Manager tooConfigure hello Report Server.</span><span class="sxs-lookup"><span data-stu-id="d5321-242">Use Configuration Manager tooConfigure hello Report Server.</span></span>

<span data-ttu-id="d5321-243">Zie voor meer stappen gedetailleerde, Hallo sectie [toohello verbinding maken met virtuele Machine en Start de Reporting Services Configuration Manager Hallo](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="d5321-243">For more detailed steps, see hello section [Connect toohello Virtual Machine and Start hello Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span></span>

<span data-ttu-id="d5321-244">**Verificatie-Opmerking:** Windows-verificatie is de aanbevolen methode voor netwerkverificatie Hallo en het Hallo-standaardverificatie Reporting Services is.</span><span class="sxs-lookup"><span data-stu-id="d5321-244">**Authentication Note:** Windows authentication is hello recommended authentication method and it is hello default Reporting Services authentication.</span></span> <span data-ttu-id="d5321-245">Alleen gebruikers die zijn geconfigureerd op Hallo VM toegankelijk Reporting Services en toegewezen tooReporting Services-functies.</span><span class="sxs-lookup"><span data-stu-id="d5321-245">Only users that are configured on hello VM can access Reporting Services and assigned tooReporting Services roles.</span></span>

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a><span data-ttu-id="d5321-246">Script tooconfigure Hallo report server- en HTTP gebruiken</span><span class="sxs-lookup"><span data-stu-id="d5321-246">Use script tooconfigure hello report server and HTTP</span></span>
<span data-ttu-id="d5321-247">toouse hello Windows PowerShell-script tooconfigure Hallo rapportserver, volledige Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="d5321-247">toouse hello Windows PowerShell script tooconfigure hello report server, complete hello following steps.</span></span> <span data-ttu-id="d5321-248">Hallo-configuratie bevat HTTP, niet HTTPS:</span><span class="sxs-lookup"><span data-stu-id="d5321-248">hello configuration includes HTTP, not HTTPS:</span></span>

1. <span data-ttu-id="d5321-249">Selecteer in de klassieke Azure-portal hello, Hallo VM en klik op verbinden.</span><span class="sxs-lookup"><span data-stu-id="d5321-249">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="d5321-250">Afhankelijk van de browserconfiguratie van uw, hebt u mogelijk na vragen aan gebruiker toosave een RDP-bestand voor het verbinden van toohello VM.</span><span class="sxs-lookup"><span data-stu-id="d5321-250">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
   
    ![verbinding maken met tooazure virtuele machine](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="d5321-252">Hallo VM gebruikersnaam, gebruikersnaam en wachtwoord die u hebt geconfigureerd tijdens het maken van VM hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d5321-252">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
   
    <span data-ttu-id="d5321-253">In Hallo installatiekopie te volgen, Hallo VM-naam is bijvoorbeeld **ssrsnativecloud** en gebruikersnaam Hallo **testgebruiker**.</span><span class="sxs-lookup"><span data-stu-id="d5321-253">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
   
    ![aanmeldingsnaam opgenomen vm](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="d5321-255">Open op Hallo VM, **Windows PowerShell ISE** met beheerdersbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="d5321-255">On hello VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="d5321-256">Hallo PowerShell ISE is standaard geïnstalleerd op WindowsServer 2012.</span><span class="sxs-lookup"><span data-stu-id="d5321-256">hello PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="d5321-257">Het verdient aanbeveling dat u Hallo ISE gebruiken in plaats van een standaard Windows PowerShell-venster zodat Hallo script in Hallo ISE te plakken, Hallo script wijzigen en vervolgens Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d5321-257">It is recommended you use hello ISE instead of a standard Windows PowerShell window so that you can paste hello script into hello ISE, modify hello script, and then run hello script.</span></span>
3. <span data-ttu-id="d5321-258">Klik in Windows PowerShell ISE op Hallo **weergave** menu en klik vervolgens op **scriptvenster weergeven**.</span><span class="sxs-lookup"><span data-stu-id="d5321-258">In Windows PowerShell ISE, click hello **View** menu and then click **Show Script Pane**.</span></span>
4. <span data-ttu-id="d5321-259">Hallo volgende script kopiëren en plakken van Hallo script in Windows PowerShell ISE-scriptvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="d5321-259">Copy hello following script, and paste hello script into hello Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. <span data-ttu-id="d5321-260">Als u Hallo VM met een HTTP-poort 80 gemaakt, wijzigt u Hallo parameter $HTTPport = 80.</span><span class="sxs-lookup"><span data-stu-id="d5321-260">If you created hello VM with an HTTP port other than 80, modify hello parameter $HTTPport = 80.</span></span>
6. <span data-ttu-id="d5321-261">Hallo-script is momenteel geconfigureerd voor Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="d5321-261">hello script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="d5321-262">Als u toorun Hallo script voor Reporting Services wilt, wijzigt u Hallo versie gedeelte van Hallo pad toohello naamruimte te 'v11' op Hallo Get-WmiObject-instructie.</span><span class="sxs-lookup"><span data-stu-id="d5321-262">If you want toorun hello script for  Reporting Services, modify hello version portion of hello path toohello namespace too“v11”, on hello Get-WmiObject statement.</span></span>
7. <span data-ttu-id="d5321-263">Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d5321-263">Run hello script.</span></span>

<span data-ttu-id="d5321-264">**Validatie**: tooverify die Hallo standaardrapport serverfunctionaliteit werkt, Zie Hallo [controleren Hallo configuratie](#verify-the-configuration) verderop in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="d5321-264">**Validation**: tooverify that hello basic report server functionality is working, see hello [Verify hello configuration](#verify-the-configuration) section later in this topic.</span></span>

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a><span data-ttu-id="d5321-265">Script tooconfigure Hallo report server- en HTTPS gebruiken</span><span class="sxs-lookup"><span data-stu-id="d5321-265">Use script tooconfigure hello report server and HTTPS</span></span>
<span data-ttu-id="d5321-266">toouse Windows PowerShell tooconfigure Hallo rapportserver, volledige Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="d5321-266">toouse Windows PowerShell tooconfigure hello report server, complete hello following steps.</span></span> <span data-ttu-id="d5321-267">Hallo configuratie omvat HTTPS, niet HTTP.</span><span class="sxs-lookup"><span data-stu-id="d5321-267">hello configuration includes HTTPS, not HTTP.</span></span>

1. <span data-ttu-id="d5321-268">Selecteer in de klassieke Azure-portal hello, Hallo VM en klik op verbinden.</span><span class="sxs-lookup"><span data-stu-id="d5321-268">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="d5321-269">Afhankelijk van de browserconfiguratie van uw, hebt u mogelijk na vragen aan gebruiker toosave een RDP-bestand voor het verbinden van toohello VM.</span><span class="sxs-lookup"><span data-stu-id="d5321-269">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
   
    ![verbinding maken met tooazure virtuele machine](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="d5321-271">Hallo VM gebruikersnaam, gebruikersnaam en wachtwoord die u hebt geconfigureerd tijdens het maken van VM hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d5321-271">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
   
    <span data-ttu-id="d5321-272">In Hallo installatiekopie te volgen, Hallo VM-naam is bijvoorbeeld **ssrsnativecloud** en gebruikersnaam Hallo **testgebruiker**.</span><span class="sxs-lookup"><span data-stu-id="d5321-272">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
   
    ![aanmeldingsnaam opgenomen vm](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="d5321-274">Open op Hallo VM, **Windows PowerShell ISE** met beheerdersbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="d5321-274">On hello VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="d5321-275">Hallo PowerShell ISE is standaard geïnstalleerd op WindowsServer 2012.</span><span class="sxs-lookup"><span data-stu-id="d5321-275">hello PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="d5321-276">Het verdient aanbeveling dat u Hallo ISE gebruiken in plaats van een standaard Windows PowerShell-venster zodat Hallo script in Hallo ISE te plakken, Hallo script wijzigen en vervolgens Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d5321-276">It is recommended you use hello ISE instead of a standard Windows PowerShell window so that you can paste hello script into hello ISE, modify hello script, and then run hello script.</span></span>
3. <span data-ttu-id="d5321-277">tooenable uitvoeren van scripts, Hallo volgende Windows PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d5321-277">tooenable running scripts, run hello following Windows PowerShell command:</span></span>
   
        Set-ExecutionPolicy RemoteSigned
   
    <span data-ttu-id="d5321-278">Vervolgens kunt u de volgende tooverify Hallo beleid Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d5321-278">You can then run hello following tooverify hello policy:</span></span>
   
        Get-ExecutionPolicy
4. <span data-ttu-id="d5321-279">In **Windows PowerShell ISE**, klikt u op Hallo **weergave** menu en klik vervolgens op **scriptvenster weergeven**.</span><span class="sxs-lookup"><span data-stu-id="d5321-279">In **Windows PowerShell ISE**, click hello **View** menu and then click **Show Script Pane**.</span></span>
5. <span data-ttu-id="d5321-280">Hallo volgende script en plak deze in Windows PowerShell ISE-scriptvenster Hallo kopiëren.</span><span class="sxs-lookup"><span data-stu-id="d5321-280">Copy hello following script and paste it into hello Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. <span data-ttu-id="d5321-281">Hallo wijzigen **$certificatehash** parameter in Hallo script:</span><span class="sxs-lookup"><span data-stu-id="d5321-281">Modify hello **$certificatehash** parameter in hello script:</span></span>
   
   * <span data-ttu-id="d5321-282">Dit is een **vereist** parameter.</span><span class="sxs-lookup"><span data-stu-id="d5321-282">This is a **required** parameter.</span></span> <span data-ttu-id="d5321-283">Als u de waarde van de Hallo-certificaat niet uit de vorige stappen Hallo hebt opgeslagen, gebruikt u een van de volgende methoden toocopy Hallo certificaat-hash-waarde uit Hallo certificaten vingerafdruk Hallo.:</span><span class="sxs-lookup"><span data-stu-id="d5321-283">If you did not save hello certificate value from hello previous steps, use one of hello following methods toocopy hello certificate hash value from hello certificates thumbprint.:</span></span>
     
       <span data-ttu-id="d5321-284">Open Windows PowerShell ISE op Hallo VM, en Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d5321-284">On hello VM, open Windows PowerShell ISE and run hello following command:</span></span>
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       <span data-ttu-id="d5321-285">Hallo-uitvoer ziet er vergelijkbare toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="d5321-285">hello output will look similar toohello following.</span></span> <span data-ttu-id="d5321-286">Als het Hallo-script retourneert een lege regel, Hallo VM heeft geen een certificaat dat zo is geconfigureerd, Zie de sectie Hallo [toouse Hallo virtuele Machines zelfondertekende certificaten](#to-use-the-virtual-machines-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="d5321-286">If hello script returns a blank line, hello VM does not have a certificate configured for example, see hello section [toouse hello Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span></span>
     
     <span data-ttu-id="d5321-287">OF</span><span class="sxs-lookup"><span data-stu-id="d5321-287">OR</span></span>
   * <span data-ttu-id="d5321-288">Op Hallo van mmc.exe VM worden uitgevoerd en voeg vervolgens Hallo **certificaten** -module.</span><span class="sxs-lookup"><span data-stu-id="d5321-288">On hello VM Run mmc.exe and then add hello **Certificates** snap-in.</span></span>
   * <span data-ttu-id="d5321-289">Onder Hallo **vertrouwde basiscertificeringsinstanties** knooppunt dubbelklikt u op de certificaatnaam van uw.</span><span class="sxs-lookup"><span data-stu-id="d5321-289">Under hello **Trusted Root Certificate Authorities** node double-click your certificate name.</span></span> <span data-ttu-id="d5321-290">Als u zelf-ondertekend certificaat Hallo Hallo VM Hallo certificaat Hallo DNS-naam van Hallo VM heeft de naam en eindigt op **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="d5321-290">If you are using hello self-signed certificate of hello VM, hello certificate is named after hello DNS name of hello VM and ends with **cloudapp.net**.</span></span>
   * <span data-ttu-id="d5321-291">Klik op Hallo **Details** tabblad.</span><span class="sxs-lookup"><span data-stu-id="d5321-291">Click hello **Details** tab.</span></span>
   * <span data-ttu-id="d5321-292">Klik op **vingerafdruk**.</span><span class="sxs-lookup"><span data-stu-id="d5321-292">Click **Thumbprint**.</span></span> <span data-ttu-id="d5321-293">Hallo-waarde van de vingerafdruk van het Hallo wordt weergegeven in het veld Hallo details, bijvoorbeeld af 11 60 b6 4b 28 8 d 89 0a 82 12 ff 6 ter a9 c3 66 4f 31 90 48</span><span class="sxs-lookup"><span data-stu-id="d5321-293">hello value of hello thumbprint is displayed in hello details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span></span>
   * <span data-ttu-id="d5321-294">**Voordat u Hallo-script uitvoeren**, Hallo spaties tussen Hallo-waardeparen verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d5321-294">**Before you run hello script**, remove hello spaces in between hello pairs of values.</span></span> <span data-ttu-id="d5321-295">Bijvoorbeeld af1160b64b288d890a8212ff6ba9c3664f319048</span><span class="sxs-lookup"><span data-stu-id="d5321-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span></span>
7. <span data-ttu-id="d5321-296">Hallo wijzigen **$httpsport** parameter:</span><span class="sxs-lookup"><span data-stu-id="d5321-296">Modify hello **$httpsport** parameter:</span></span> 
   
   * <span data-ttu-id="d5321-297">Als u poort 443 voor HTTPS-eindpunt Hallo gebruikt, hoeft niet u tooupdate deze parameter in Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="d5321-297">If you used port 443 for hello HTTPS endpoint, then you do not need tooupdate this parameter in hello script.</span></span> <span data-ttu-id="d5321-298">Anders gebruiken Hallo poortwaarde die u hebt geselecteerd toen u persoonlijke Hallo HTTPS-eindpunt op Hallo VM geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d5321-298">Otherwise use hello port value you selected when you configured hello HTTPS private endpoint on hello VM.</span></span>
8. <span data-ttu-id="d5321-299">Hallo wijzigen **$DNSName** parameter:</span><span class="sxs-lookup"><span data-stu-id="d5321-299">Modify hello **$DNSName** parameter:</span></span> 
   
   * <span data-ttu-id="d5321-300">Hallo-script is geconfigureerd voor een certificaat met wild card $DNSName = '+'.</span><span class="sxs-lookup"><span data-stu-id="d5321-300">hello script is configured for a wild card certificate $DNSName="+".</span></span> <span data-ttu-id="d5321-301">Als u geen tooconfigure wilt voor een jokerteken certificaatbinding doen, uitcommentariëren $DNSName = ' + 'en inschakelen van de volgende regel, Hallo volledige $DNSNAme referentie, ## $DNSName="$server.cloudapp.net Hallo'.</span><span class="sxs-lookup"><span data-stu-id="d5321-301">If you do no want tooconfigure for a wildcard certificate binding, comment out $DNSName="+" and enable hello following line, hello full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span></span>
     
       <span data-ttu-id="d5321-302">Hallo $DNSName waarde wijzigen als u niet dat de DNS-naam toouse Hallo van virtuele machine voor Reporting Services wilt.</span><span class="sxs-lookup"><span data-stu-id="d5321-302">Change hello $DNSName value if you do not want toouse hello virtual machine’s DNS name for Reporting Services.</span></span> <span data-ttu-id="d5321-303">Als u Hallo-parameter gebruikt, Hallo certificaat moet ook gebruiken voor deze naam en de naam van de Hallo globaal op een DNS-server te registreren.</span><span class="sxs-lookup"><span data-stu-id="d5321-303">If you use hello parameter, hello certificate must also use this name and you register hello name globally on a DNS server.</span></span>
9. <span data-ttu-id="d5321-304">Hallo-script is momenteel geconfigureerd voor Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="d5321-304">hello script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="d5321-305">Als u toorun Hallo script voor Reporting Services wilt, wijzigt u Hallo versie gedeelte van Hallo pad toohello naamruimte te 'v11' op Hallo Get-WmiObject-instructie.</span><span class="sxs-lookup"><span data-stu-id="d5321-305">If you want toorun hello script for  Reporting Services, modify hello version portion of hello path toohello namespace too“v11”, on hello Get-WmiObject statement.</span></span>
10. <span data-ttu-id="d5321-306">Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d5321-306">Run hello script.</span></span>

<span data-ttu-id="d5321-307">**Validatie**: tooverify die Hallo standaardrapport serverfunctionaliteit werkt, Zie Hallo [controleren Hallo configuratie](#verify-the-connection) verderop in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="d5321-307">**Validation**: tooverify that hello basic report server functionality is working, see hello [Verify hello configuration](#verify-the-connection) section later in this topic.</span></span> <span data-ttu-id="d5321-308">tooverify hello certificaatbinding open een opdrachtprompt met beheerdersbevoegdheden en Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d5321-308">tooverify hello certificate binding open a command prompt with administrative privileges, and then run hello following command:</span></span>

    netsh http show sslcert

<span data-ttu-id="d5321-309">Hallo resultaat wordt Hallo volgende zijn:</span><span class="sxs-lookup"><span data-stu-id="d5321-309">hello result will include hello following:</span></span>

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a><span data-ttu-id="d5321-310">Gebruik Configuration Manager tooConfigure Hallo Report Server</span><span class="sxs-lookup"><span data-stu-id="d5321-310">Use Configuration Manager tooConfigure hello Report Server</span></span>
<span data-ttu-id="d5321-311">Als u geen toorun Hallo PowerShell script tooconfigure Hallo report server, volgt u de Hallo stappen in deze sectie toouse Hallo Reporting Services native modus configuration manager tooconfigure Hallo rapportserver.</span><span class="sxs-lookup"><span data-stu-id="d5321-311">If you do not want toorun hello PowerShell script tooconfigure hello report server, follow hello steps in this section toouse hello Reporting Services native mode configuration manager tooconfigure hello report server.</span></span>

1. <span data-ttu-id="d5321-312">Selecteer in de klassieke Azure-portal hello, Hallo VM en klik op verbinden.</span><span class="sxs-lookup"><span data-stu-id="d5321-312">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="d5321-313">Hallo-gebruikersnaam en wachtwoord die u hebt geconfigureerd tijdens het maken van VM hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d5321-313">Use hello user name and password you configured when you created hello VM.</span></span>
   
    ![verbinding maken met tooazure virtuele machine](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. <span data-ttu-id="d5321-315">Voer Windows update en installeer updates toohello VM.</span><span class="sxs-lookup"><span data-stu-id="d5321-315">Run Windows update and install updates toohello VM.</span></span> <span data-ttu-id="d5321-316">Als een herstart van Hallo VM vereist is, Hallo VM starten en verbinding toohello VM van Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d5321-316">If a restart of hello VM is required, restart hello VM and reconnect toohello VM from hello Azure classic portal.</span></span>
3. <span data-ttu-id="d5321-317">Typ vanuit het startmenu Hallo op Hallo VM, **Reporting Services** en open **Reporting Services Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="d5321-317">From hello Start menu on hello VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span></span>
4. <span data-ttu-id="d5321-318">Laat de standaardwaarden Hallo voor **servernaam** en **rapportserverexemplaar**.</span><span class="sxs-lookup"><span data-stu-id="d5321-318">Leave hello default values for **Server Name** and **Report Server Instance**.</span></span> <span data-ttu-id="d5321-319">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="d5321-319">Click **Connect**.</span></span>
5. <span data-ttu-id="d5321-320">Klik in het linkerdeelvenster Hallo **URL van webservice**.</span><span class="sxs-lookup"><span data-stu-id="d5321-320">In hello left pane, click **Web Service URL**.</span></span>
6. <span data-ttu-id="d5321-321">RS is standaard geconfigureerd voor HTTP poort 80 met IP-adres 'Alle toegewezen'.</span><span class="sxs-lookup"><span data-stu-id="d5321-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span></span> <span data-ttu-id="d5321-322">tooadd HTTPS:</span><span class="sxs-lookup"><span data-stu-id="d5321-322">tooadd HTTPS:</span></span>
   
   1. <span data-ttu-id="d5321-323">In **SSL-certificaat**: Selecteer Hallo certificaat dat u toouse, bijvoorbeeld [VM name]. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="d5321-323">In **SSL Certificate**: select hello certificate you want toouse, for example [VM name].cloudapp.net.</span></span> <span data-ttu-id="d5321-324">Als er geen certificaten worden vermeld, raadpleegt u Hallo sectie **stap 2: Maak een servercertificaat** voor meer informatie over hoe Hallo certificaat op Hallo VM tooinstall en vertrouwt.</span><span class="sxs-lookup"><span data-stu-id="d5321-324">If no certificates are listed, see hello section **Step 2: Create a Server Certificate** for information on how tooinstall and trust hello certificate on hello VM.</span></span>
   2. <span data-ttu-id="d5321-325">Onder **SSL-poort**: 443 kiezen.</span><span class="sxs-lookup"><span data-stu-id="d5321-325">Under **SSL Port**: choose 443.</span></span> <span data-ttu-id="d5321-326">Als u persoonlijke Hallo HTTPS-eindpunt geconfigureerd in Hallo VM met een andere particuliere poort, hier die waarde gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d5321-326">If you configured hello HTTPS private endpoint in hello VM with a different private port, use that value here.</span></span>
   3. <span data-ttu-id="d5321-327">Klik op **toepassen** en wachten op Hallo bewerking toocomplete.</span><span class="sxs-lookup"><span data-stu-id="d5321-327">Click **Apply** and wait for hello operation toocomplete.</span></span>
7. <span data-ttu-id="d5321-328">Klik in het linkerdeelvenster Hallo **Database**.</span><span class="sxs-lookup"><span data-stu-id="d5321-328">In hello left pane, click **Database**.</span></span>
   
   1. <span data-ttu-id="d5321-329">Klik op **wijzigen Databas**e.</span><span class="sxs-lookup"><span data-stu-id="d5321-329">Click **Change Databas**e.</span></span>
   2. <span data-ttu-id="d5321-330">Klik op **maken van een nieuw report server-database** en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d5321-330">Click **Create a new report server database** and then click **Next**.</span></span>
   3. <span data-ttu-id="d5321-331">Laat de standaardwaarde Hallo **servernaam**: Hallo VM de naam en laat de standaardwaarde Hallo **verificatietype** als **huidige gebruiker** – **geïntegreerde beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="d5321-331">Leave hello default **Server Name**: as hello VM name and leave hello default **Authentication Type** as **Current User** – **Integrated Security**.</span></span> <span data-ttu-id="d5321-332">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="d5321-332">Click **Next**.</span></span>
   4. <span data-ttu-id="d5321-333">Laat de standaardwaarde Hallo **databasenaam** als **ReportServer** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d5321-333">Leave hello default **Database Name** as **ReportServer** and click **Next**.</span></span>
   5. <span data-ttu-id="d5321-334">Laat de standaardwaarde Hallo **verificatietype** als **Servicereferenties** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d5321-334">Leave hello default **Authentication Type** as **Service Credentials** and click **Next**.</span></span>
   6. <span data-ttu-id="d5321-335">Klik op **volgende** op Hallo **samenvatting** pagina.</span><span class="sxs-lookup"><span data-stu-id="d5321-335">Click **Next** on hello **Summary** page.</span></span>
   7. <span data-ttu-id="d5321-336">Wanneer het Hallo-configuratie is voltooid, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="d5321-336">When hello configuration is complete, click **Finish**.</span></span>
8. <span data-ttu-id="d5321-337">Klik in het linkerdeelvenster Hallo **URL van Report Manager**.</span><span class="sxs-lookup"><span data-stu-id="d5321-337">In hello left pane, click **Report Manager URL**.</span></span> <span data-ttu-id="d5321-338">Laat de standaardwaarde Hallo **virtuele map** als **rapporten** en klik op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="d5321-338">Leave hello default **Virtual Directory** as **Reports** and click **Apply**.</span></span>
9. <span data-ttu-id="d5321-339">Klik op **afsluiten** tooclose Hallo Reporting Services Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="d5321-339">Click **Exit** tooclose hello Reporting Services Configuration Manager.</span></span>

## <a name="step-4-open-windows-firewall-port"></a><span data-ttu-id="d5321-340">Stap 4: Open Windows Firewall-poort</span><span class="sxs-lookup"><span data-stu-id="d5321-340">Step 4: Open Windows Firewall Port</span></span>
> [!NOTE]
> <span data-ttu-id="d5321-341">Als u een van de rapportserver voor Hallo scripts tooconfigure Hallo gebruikt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="d5321-341">If you used one of hello scripts tooconfigure hello report server, you can skip this section.</span></span> <span data-ttu-id="d5321-342">Hallo script een firewallpoort stap tooopen Hallo opgenomen.</span><span class="sxs-lookup"><span data-stu-id="d5321-342">hello script included a step tooopen hello firewall port.</span></span> <span data-ttu-id="d5321-343">Hallo standaardwaarde is poort 80 voor HTTP en poort 443 voor HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d5321-343">hello default was port 80 for HTTP and port 443 for HTTPS.</span></span>
> 
> 

<span data-ttu-id="d5321-344">tooconnect op afstand tooReport Manager of Hallo melden Server op Hallo virtuele machine, een TCP-eindpunt is vereist op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="d5321-344">tooconnect remotely tooReport Manager or hello Report Server on hello virtual machine, a TCP Endpoint is required on hello VM.</span></span> <span data-ttu-id="d5321-345">Het is vereiste tooopen Hallo dezelfde in de firewall Hallo van de virtuele machine poort.</span><span class="sxs-lookup"><span data-stu-id="d5321-345">It is required tooopen hello same port in hello VM’s firewall.</span></span> <span data-ttu-id="d5321-346">Hallo-eindpunt is gemaakt toen Hallo VM is ingericht.</span><span class="sxs-lookup"><span data-stu-id="d5321-346">hello endpoint was created when hello VM was provisioned.</span></span>

<span data-ttu-id="d5321-347">In deze sectie bevat algemene informatie over hoe tooopen firewallpoort Hallo.</span><span class="sxs-lookup"><span data-stu-id="d5321-347">This section provides basic information on how tooopen hello firewall port.</span></span> <span data-ttu-id="d5321-348">Zie voor meer informatie [een Firewall configureren voor toegang tot de Server van rapporten](https://technet.microsoft.com/library/bb934283.aspx)</span><span class="sxs-lookup"><span data-stu-id="d5321-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="d5321-349">Als u Hallo script tooconfigure Hallo-rapportserver gebruikt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="d5321-349">If you used hello script tooconfigure hello report server, you can skip this section.</span></span> <span data-ttu-id="d5321-350">Hallo script een firewallpoort stap tooopen Hallo opgenomen.</span><span class="sxs-lookup"><span data-stu-id="d5321-350">hello script included a step tooopen hello firewall port.</span></span>
> 
> 

<span data-ttu-id="d5321-351">Als u een particuliere poort geconfigureerd voor HTTPS dan 443, wijzig Hallo script op de juiste wijze te volgen.</span><span class="sxs-lookup"><span data-stu-id="d5321-351">If you configured a private port for HTTPS other than 443, modify hello following script appropriately.</span></span> <span data-ttu-id="d5321-352">poort tooopen **443** op Hallo Windows Firewall, Hallo volgende voltooien:</span><span class="sxs-lookup"><span data-stu-id="d5321-352">tooopen port **443** on hello Windows Firewall, complete hello following:</span></span>

1. <span data-ttu-id="d5321-353">Open een Windows PowerShell-venster met beheerdersbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="d5321-353">Open a Windows PowerShell window with administrative privileges.</span></span>
2. <span data-ttu-id="d5321-354">Als u een andere poort dan 443 gebruikt wanneer u HTTPS-eindpunt Hallo geconfigureerd op Hallo VM, werk de poort in de volgende opdracht Hallo Hallo en Voer Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="d5321-354">If you used a port other than 443 when you configured hello HTTPS endpoint on hello VM, update hello port in hello following command and then run hello command:</span></span>
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. <span data-ttu-id="d5321-355">Wanneer het Hallo-opdracht is voltooid, **Ok** wordt weergegeven in het Hallo-opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="d5321-355">When hello command completes, **Ok** is displayed in hello command prompt.</span></span>

<span data-ttu-id="d5321-356">tooverify dat Hallo-poort is geopend, open een Windows PowerShell-venster en Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d5321-356">tooverify that hello port is opened, open a Windows PowerShell window and run hello following command:</span></span>

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a><span data-ttu-id="d5321-357">Hallo-configuratie verifiëren</span><span class="sxs-lookup"><span data-stu-id="d5321-357">Verify hello configuration</span></span>
<span data-ttu-id="d5321-358">tooverify die Hallo standaardrapport serverfunctionaliteit nu werkt, open uw browser met beheerdersbevoegdheden en vervolgens de server ad-Rapportbeheer URL's voor het rapporteren van bladeren toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="d5321-358">tooverify that hello basic report server functionality is now working, open your browser with administrative privileges and then browse toohello following report server ad report manager URLS:</span></span>

* <span data-ttu-id="d5321-359">Blader op Hallo VM, toohello report server-URL:</span><span class="sxs-lookup"><span data-stu-id="d5321-359">On hello VM, browse toohello report server URL:</span></span>
  
        http://localhost/reportserver
* <span data-ttu-id="d5321-360">Blader op Hallo VM, toohello report Manager-URL:</span><span class="sxs-lookup"><span data-stu-id="d5321-360">On hello VM, browse toohello report manger URL:</span></span>
  
        http://localhost/Reports
* <span data-ttu-id="d5321-361">Bladeren naar uw lokale computer toohello **externe** report Manager op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="d5321-361">From your local computer, browse toohello **remote** report Manager on hello VM.</span></span> <span data-ttu-id="d5321-362">Hallo DNS-naam in het volgende voorbeeld naar gelang van toepassing hello bijwerken.</span><span class="sxs-lookup"><span data-stu-id="d5321-362">Update hello DNS name in hello following example as appropriate.</span></span> <span data-ttu-id="d5321-363">Als u wordt gevraagd om een wachtwoord, gebruik Hallo-beheerdersreferenties die u hebt gemaakt tijdens het Hallo VM is ingericht.</span><span class="sxs-lookup"><span data-stu-id="d5321-363">When prompted for a password, use hello administrator credentials you created when hello VM was provisioned.</span></span> <span data-ttu-id="d5321-364">Hallo-gebruikersnaam is in Hallo [domein]\[gebruikersnaam]-indeling, waarbij Hallo domein Hallo VM computernaam, bijvoorbeeld ssrsnativecloud\testuser is.</span><span class="sxs-lookup"><span data-stu-id="d5321-364">hello user name is in hello [Domain]\[user name] format, where hello domain is hello VM computer name, for example ssrsnativecloud\testuser.</span></span> <span data-ttu-id="d5321-365">Als u geen van HTTP gebruikmaakt**S**, verwijder Hallo **s** in Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="d5321-365">If you are not using HTTP**S**, remove hello **s** in hello URL.</span></span> <span data-ttu-id="d5321-366">Zie Hallo volgende sectie voor informatie over het maken van extra gebruikers op virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d5321-366">See hello next section for information on creating additional users on VM.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/Reports
* <span data-ttu-id="d5321-367">Blader toohello externe report server-URL van de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="d5321-367">From your local computer, browse toohello remote report server URL.</span></span> <span data-ttu-id="d5321-368">Hallo DNS-naam in het volgende voorbeeld naar gelang van toepassing hello bijwerken.</span><span class="sxs-lookup"><span data-stu-id="d5321-368">Update hello DNS name in hello following example as appropriate.</span></span> <span data-ttu-id="d5321-369">Als u HTTPS niet gebruikt, verwijdert u Hallo s in Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="d5321-369">If you are not using HTTPS, remove hello s in hello URL.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a><span data-ttu-id="d5321-370">Gebruikers maken en toewijzen van rollen</span><span class="sxs-lookup"><span data-stu-id="d5321-370">Create Users and Assign Roles</span></span>
<span data-ttu-id="d5321-371">Nadat rapporteren server configureren en controleren van hello, wordt een algemene beheertaak toocreate is een of meer gebruikers en gebruikers tooReporting Services rollen toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d5321-371">After configuring and verifying hello report server, a common administrative task is toocreate one or more users and assign users tooReporting Services roles.</span></span> <span data-ttu-id="d5321-372">Zie voor meer informatie de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="d5321-372">For more information, see hello following:</span></span>

* [<span data-ttu-id="d5321-373">Een lokale gebruikersaccount maken</span><span class="sxs-lookup"><span data-stu-id="d5321-373">Create a local user account</span></span>](https://technet.microsoft.com/library/cc770642.aspx)
* <span data-ttu-id="d5321-374">[Toegang van de gebruiker verlenen tooa Report Server (Rapportbeheer)](https://msdn.microsoft.com/library/ms156034.aspx))</span><span class="sxs-lookup"><span data-stu-id="d5321-374">[Grant User Access tooa Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span></span>
* [<span data-ttu-id="d5321-375">Maken en beheren van roltoewijzingen</span><span class="sxs-lookup"><span data-stu-id="d5321-375">Create and Manage Role Assignments</span></span>](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a><span data-ttu-id="d5321-376">tooCreate en rapporten publiceren toohello Azure virtuele Machine</span><span class="sxs-lookup"><span data-stu-id="d5321-376">tooCreate and Publish Reports toohello Azure Virtual Machine</span></span>
<span data-ttu-id="d5321-377">Hallo volgende tabel ziet u enkele Hallo opties beschikbaar toopublish bestaande rapporten uit een on-premises computer toohello rapportserver gehost op Hallo van Microsoft Azure Virtual Machine:</span><span class="sxs-lookup"><span data-stu-id="d5321-377">hello following table summarizes some of hello options available toopublish existing reports from an on-premises computer toohello report server hosted on hello Microsoft Azure Virtual Machine:</span></span>

* <span data-ttu-id="d5321-378">**RS.exe script**: gebruik RS.exe script toocopy rapportitems uit en bestaande report server tooyour Microsoft Azure virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="d5321-378">**RS.exe script**: Use RS.exe script toocopy report items from and existing report server tooyour Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="d5321-379">Zie voor meer informatie Hallo sectie 'Native modus tooNative Mode – Microsoft Azure virtuele Machine' in [voorbeeld Reporting Services rs.exe Script tooMigrate inhoud tussen rapportservers](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5321-379">For more information, see hello section “Native mode tooNative Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>
* <span data-ttu-id="d5321-380">**Report Builder**: Hallo virtuele machine bevat Hallo Klik-eenmaal versie van Microsoft SQL Server Report Builder.</span><span class="sxs-lookup"><span data-stu-id="d5321-380">**Report Builder**: hello virtual machine includes hello click-once version of Microsoft SQL Server Report Builder.</span></span> <span data-ttu-id="d5321-381">toostart Report builder Hallo eerst op Hallo virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="d5321-381">toostart Report builder hello first time on hello virtual machine:</span></span>
  
  1. <span data-ttu-id="d5321-382">Start uw browser met beheerdersbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="d5321-382">Start your browser with administrative privileges.</span></span>
  2. <span data-ttu-id="d5321-383">Blader tooreport manager op Hallo virtuele machine en klik op **Report Builder** in Hallo-lint.</span><span class="sxs-lookup"><span data-stu-id="d5321-383">Browse tooreport manager on hello virtual machine and click **Report Builder**  in hello ribbon.</span></span>
     
     <span data-ttu-id="d5321-384">Zie voor meer informatie [installeren, verwijderen en ondersteunende Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5321-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span></span>
* <span data-ttu-id="d5321-385">**SQL Server Data Tools: VM**: als u Hallo VM met SQL Server 2012 gemaakt, wordt SQL Server Data Tools op Hallo virtuele machine is geïnstalleerd en kan worden gebruikt toocreate **Report Server-projecten** en rapporten op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d5321-385">**SQL Server Data Tools: VM**:  If you created hello VM with SQL Server 2012, then SQL Server Data Tools is installed on hello virtual machine and can be used toocreate **Report Server Projects** and reports on hello virtual machine.</span></span> <span data-ttu-id="d5321-386">SQL Server Data Tools kunt publiceren Hallo rapporten toohello-rapportserver op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d5321-386">SQL Server Data Tools can publish hello reports toohello report server on hello virtual machine.</span></span>
  
    <span data-ttu-id="d5321-387">Als u met SQL server 2014 Hallo VM hebt gemaakt, kunt u SQL Server Data Tools - BI voor visual Studio installeren.</span><span class="sxs-lookup"><span data-stu-id="d5321-387">If you created hello VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span></span> <span data-ttu-id="d5321-388">Zie voor meer informatie de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="d5321-388">For more information, see hello following:</span></span>
  
  * [<span data-ttu-id="d5321-389">Microsoft SQL Server Data Tools - Business Intelligence voor Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d5321-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span></span>](https://www.microsoft.com/download/details.aspx?id=42313)
  * [<span data-ttu-id="d5321-390">Microsoft SQL Server Data Tools - Business Intelligence voor Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="d5321-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=36843)
  * [<span data-ttu-id="d5321-391">SQL Server Data Tools en SQL Server Business Intelligence (BI SSDT)</span><span class="sxs-lookup"><span data-stu-id="d5321-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span></span>](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* <span data-ttu-id="d5321-392">**SQL Server Data Tools: Extern**: op uw lokale computer, kunt u een Reporting Services-project maken in SQL Server Data Tools met Reporting Services-rapporten.</span><span class="sxs-lookup"><span data-stu-id="d5321-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span></span> <span data-ttu-id="d5321-393">Hallo project tooconnect toohello URL van webservice configureren.</span><span class="sxs-lookup"><span data-stu-id="d5321-393">Configure hello project tooconnect toohello web service URL.</span></span>
  
    ![de Projecteigenschappen SSDT voor SQL Server Reporting Services-project](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* <span data-ttu-id="d5321-395">**Script gebruiken**: script toocopy rapportinhoud server gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d5321-395">**Use script**: Use script toocopy report server content.</span></span> <span data-ttu-id="d5321-396">Zie voor meer informatie [voorbeeld Reporting Services rs.exe Script tooMigrate inhoud tussen rapportservers](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5321-396">For more information, see [Sample Reporting Services rs.exe Script tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a><span data-ttu-id="d5321-397">Als u geen van Hallo VM gebruikmaakt kosten minimaliseren</span><span class="sxs-lookup"><span data-stu-id="d5321-397">Minimize cost if you are not using hello VM</span></span>
> [!NOTE]
> <span data-ttu-id="d5321-398">toominimize kosten voor uw Azure Virtual Machines als deze niet in gebruik is, sluit de Hallo VM van Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d5321-398">toominimize charges for your Azure Virtual Machines when not in use, shut down hello VM from hello Azure classic portal.</span></span> <span data-ttu-id="d5321-399">Als u Energiebeheer van Windows hello binnen een VM-tooshut omlaag Hallo VM gebruikt, er zijn nog steeds in rekening gebracht Hallo dezelfde bedrag voor Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="d5321-399">If you use hello Windows power options inside a VM tooshut down hello VM, you are still charged hello same amount for hello VM.</span></span> <span data-ttu-id="d5321-400">tooreduce kosten, moet u tooshut omlaag Hallo VM in Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d5321-400">tooreduce charges, you need tooshut down hello VM in hello Azure classic portal.</span></span> <span data-ttu-id="d5321-401">Als u niet langer Hallo VM, toodelete Hallo VM onthouden en Hallo gekoppelde VHD-bestanden tooavoid opslagkosten. Zie voor meer informatie, veelgestelde vragen over het Hallo-sectie op [prijsinformatie voor virtuele Machines](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="d5321-401">If you no longer need hello VM, remember toodelete hello VM and hello associated .vhd files tooavoid storage charges.For more information, see hello FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>

## <a name="more-information"></a><span data-ttu-id="d5321-402">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="d5321-402">More Information</span></span>
### <a name="resources"></a><span data-ttu-id="d5321-403">Resources</span><span class="sxs-lookup"><span data-stu-id="d5321-403">Resources</span></span>
* <span data-ttu-id="d5321-404">Voor vergelijkbare inhoud gerelateerde tooa single server-implementatie van SQL Server Business Intelligence en SharePoint 2013, Zie [tooCreate gebruik Windows PowerShell een Azure virtuele machine met SQL Server BI en SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5321-404">For similar content related tooa single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell tooCreate an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span></span>
* <span data-ttu-id="d5321-405">Zie voor vergelijkbare inhoud gerelateerde tooa implementatie met meerdere servers van SQL Server Business Intelligence en SharePoint 2013 [implementeren SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5321-405">For similar content related tooa multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span></span>
* <span data-ttu-id="d5321-406">Raadpleeg voor algemene informatie gerelateerde toodeployments van SQL Server Business Intelligence in Azure Virtual Machines [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span><span class="sxs-lookup"><span data-stu-id="d5321-406">For General information related toodeployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span></span>
* <span data-ttu-id="d5321-407">Zie voor meer informatie over Hallo kosten van Azure compute-kosten, tabblad van de virtuele Machines Hallo van [Azure prijscategorie Rekenmachine](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="d5321-407">For more information about hello cost of Azure compute charges, see hello Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span></span>

### <a name="community-content"></a><span data-ttu-id="d5321-408">Inhoud van de community</span><span class="sxs-lookup"><span data-stu-id="d5321-408">Community Content</span></span>
* <span data-ttu-id="d5321-409">Zie voor stapsgewijze instructies voor het hoe een Reporting Services Native modus toocreate server melden zonder script te gebruiken, [hosten van SQL Reporting Service op Azure virtuele Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span><span class="sxs-lookup"><span data-stu-id="d5321-409">For step by step instructions on how toocreate a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span></span>

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a><span data-ttu-id="d5321-410">Koppelingen tooother resources voor SQL Server in Azure VM 's</span><span class="sxs-lookup"><span data-stu-id="d5321-410">Links tooother resources for SQL Server in Azure VMs</span></span>
[<span data-ttu-id="d5321-411">SQL Server op Azure Virtual Machines-overzicht</span><span class="sxs-lookup"><span data-stu-id="d5321-411">SQL Server on Azure Virtual Machines Overview</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

