---
title: aaaIntegrate Sleutelkluis met SQL Server op Windows-machines in Azure (Resource Manager) | Microsoft Docs
description: Meer informatie over hoe tooautomate Hallo configuratie van SQL Server-versleuteling voor gebruik met Azure Sleutelkluis. Dit onderwerp wordt uitgelegd hoe toouse Azure Sleutelkluis-integratie met SQL Server virtuele machines met Resource Manager gemaakt.
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: cd66dfb1-0e9b-4fb0-a471-9deaf4ab4ab8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: jroth
ms.openlocfilehash: 0d36d3d075d6538c18cd5ecb43c19a4b000a99e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a><span data-ttu-id="9b9be-104">Configureren van Azure Sleutelkluis-integratie voor SQL Server op Azure Virtual Machines (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="9b9be-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b9be-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9b9be-105">Resource Manager</span></span>](virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="9b9be-106">Klassiek</span><span class="sxs-lookup"><span data-stu-id="9b9be-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="9b9be-107">Overzicht</span><span class="sxs-lookup"><span data-stu-id="9b9be-107">Overview</span></span>
<span data-ttu-id="9b9be-108">Er zijn meerdere onderdelen van SQL Server-versleuteling, zoals [transparante gegevensversleuteling (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [kolom: versleuteling op bestandsniveau (wissen)](https://msdn.microsoft.com/library/ms173744.aspx), en [back-upversleuteling](https://msdn.microsoft.com/library/dn449489.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b9be-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="9b9be-109">Deze vormen van versleuteling vereisen dat u toomanage en slaan Hallo cryptografische sleutels die u voor versleuteling gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9b9be-109">These forms of encryption require you toomanage and store hello cryptographic keys you use for encryption.</span></span> <span data-ttu-id="9b9be-110">Hello Azure Key Vault (Azure Sleutelkluis)-service is ontworpen tooimprove Hallo beveiliging en beheer van deze sleutels op een locatie met veilige en maximaal beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="9b9be-110">hello Azure Key Vault (AKV) service is designed tooimprove hello security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="9b9be-111">Hallo [SQL Server-Connector](http://www.microsoft.com/download/details.aspx?id=45344) kunt SQL Server-toouse deze sleutels van Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="9b9be-111">hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server toouse these keys from Azure Key Vault.</span></span>

<span data-ttu-id="9b9be-112">Als u met SQL Server met on-premises machines, er zijn [stappen kunt u tooaccess Azure Key Vault volgen uit uw on-premises SQL Server-machine](https://msdn.microsoft.com/library/dn198405.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b9be-112">If you running SQL Server with on-premises machines, there are [steps you can follow tooaccess Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="9b9be-113">Maar voor SQL Server in Azure VM's, kunt u tijd besparen met behulp van Hallo *Azure Sleutelkluis-integratie* functie.</span><span class="sxs-lookup"><span data-stu-id="9b9be-113">But for SQL Server in Azure VMs, you can save time by using hello *Azure Key Vault Integration* feature.</span></span>

<span data-ttu-id="9b9be-114">Wanneer deze functie is ingeschakeld, installeert en deze automatisch Hallo SQL Server-Connector, configureert u Hallo EKM-provider tooaccess Azure Sleutelkluis, Hallo referentie tooallow maakt u tooaccess uw kluis.</span><span class="sxs-lookup"><span data-stu-id="9b9be-114">When this feature is enabled, it automatically installs hello SQL Server Connector, configures hello EKM provider tooaccess Azure Key Vault, and creates hello credential tooallow you tooaccess your vault.</span></span> <span data-ttu-id="9b9be-115">Als u het hebt bekeken Hallo stappen in Hallo genoemde lokale documentatie, ziet u dat deze functie automatiseert stap 2 en 3.</span><span class="sxs-lookup"><span data-stu-id="9b9be-115">If you looked at hello steps in hello previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="9b9be-116">Hallo enige dat u nog moet toodo handmatig is toocreate hello sleutelkluis en de sleutels.</span><span class="sxs-lookup"><span data-stu-id="9b9be-116">hello only thing you would still need toodo manually is toocreate hello key vault and keys.</span></span> <span data-ttu-id="9b9be-117">Van daaruit wordt Hallo volledige installatie van de SQL-VM geautomatiseerd.</span><span class="sxs-lookup"><span data-stu-id="9b9be-117">From there, hello entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="9b9be-118">Zodra deze functie kan voor deze installatie is voltooid, kunt u de T-SQL-instructies toobegin normaal versleutelen van uw databases of back-ups uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="9b9be-118">Once this feature has completed this setup, you can execute T-SQL statements toobegin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a><span data-ttu-id="9b9be-119">Inschakelen en configureren van Azure Sleutelkluis-integratie</span><span class="sxs-lookup"><span data-stu-id="9b9be-119">Enabling and configuring AKV integration</span></span>
<span data-ttu-id="9b9be-120">U kunt Azure Sleutelkluis-integratie tijdens het inrichten of configureren voor een bestaande virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="9b9be-120">You can enable AKV integration during provisioning or configure it for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="9b9be-121">Nieuwe virtuele machines</span><span class="sxs-lookup"><span data-stu-id="9b9be-121">New VMs</span></span>
<span data-ttu-id="9b9be-122">Als u een nieuwe virtuele SQL Server-machine met Resource Manager inricht, biedt hello Azure-portal een stap tooenable Azure Sleutelkluis-integratie.</span><span class="sxs-lookup"><span data-stu-id="9b9be-122">If you are provisioning a new SQL Server virtual machine with Resource Manager, hello Azure portal provides a step tooenable Azure Key Vault integration.</span></span> <span data-ttu-id="9b9be-123">Hello Azure Sleutelkluis-functie is alleen beschikbaar voor Hallo Enterprise, Developer, en evaluatie-editie van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9b9be-123">hello Azure Key Vault feature is available only for hello Enterprise, Developer and Evaluation Editions of SQL Server.</span></span>

![Integratie van Azure Sleutelkluis in SQL](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

<span data-ttu-id="9b9be-125">Zie voor een gedetailleerd overzicht van de inrichting [een SQL Server-machine inrichten in Azure Portal Hallo](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="9b9be-125">For a detailed walkthrough of provisioning, see [Provision a SQL Server virtual machine in hello Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="9b9be-126">Bestaande virtuele machines</span><span class="sxs-lookup"><span data-stu-id="9b9be-126">Existing VMs</span></span>
<span data-ttu-id="9b9be-127">Selecteer de virtuele machine van SQL Server voor een bestaande SQL Server-virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="9b9be-127">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="9b9be-128">Selecteer vervolgens Hallo **SQL Server-configuratiebestand** sectie Hallo **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="9b9be-128">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![SQL Azure Sleutelkluis-integratie voor bestaande virtuele machines](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

<span data-ttu-id="9b9be-130">In Hallo **SQL Server-configuratiebestand** blade, klikt u op Hallo **bewerken** knop in Hallo sectie geautomatiseerde Sleutelkluis-integratie.</span><span class="sxs-lookup"><span data-stu-id="9b9be-130">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated Key Vault integration section.</span></span>

![SQL Azure Sleutelkluis-integratie voor bestaande virtuele machines configureren](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

<span data-ttu-id="9b9be-132">Wanneer u klaar bent, klikt u op Hallo **OK** knop op Hallo Hallo onderaan **SQL Server-configuratiebestand** blade toosave uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="9b9be-132">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

> [!NOTE]
> <span data-ttu-id="9b9be-133">U kunt ook Azure Sleutelkluis-integratie met een sjabloon configureren.</span><span class="sxs-lookup"><span data-stu-id="9b9be-133">You can also configure AKV integration using a template.</span></span> <span data-ttu-id="9b9be-134">Zie voor meer informatie [Azure quickstart-sjabloon voor Azure Sleutelkluis-integratie](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span><span class="sxs-lookup"><span data-stu-id="9b9be-134">For more information, see [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span></span>
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

