---
title: aaaConnect tooSQL Database met behulp van SQL Server Management Studio in Azure RemoteApp | Microsoft Docs
description: Gebruik deze zelfstudie toolearn hoe toouse SQL Server Management Studio in Azure RemoteApp voor beveiliging en prestaties bij het verbinden van tooSQL Database
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a><span data-ttu-id="43c60-103">SQL Server Management Studio in Azure RemoteApp tooconnect tooSQL Database gebruiken</span><span class="sxs-lookup"><span data-stu-id="43c60-103">Use SQL Server Management Studio in Azure RemoteApp tooconnect tooSQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43c60-104">Azure RemoteApp wordt buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="43c60-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="43c60-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="43c60-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="43c60-106">Inleiding</span><span class="sxs-lookup"><span data-stu-id="43c60-106">Introduction</span></span>
<span data-ttu-id="43c60-107">Deze zelfstudie leert u hoe toouse SQL Server Management Studio (SSMS) in Azure RemoteApp tooconnect tooSQL Database.</span><span class="sxs-lookup"><span data-stu-id="43c60-107">This tutorial shows you how toouse SQL Server Management Studio (SSMS) in Azure RemoteApp tooconnect tooSQL Database.</span></span> <span data-ttu-id="43c60-108">Deze begeleidt u bij Hallo-proces voor het instellen van SQL Server Management Studio in Azure RemoteApp, wordt uitgelegd Hallo voordelen en ziet u beveiligingsfuncties die u kunt gebruiken in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="43c60-108">It walks you through hello process of setting up SQL Server Management Studio in Azure RemoteApp, explains hello benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="43c60-109">**Geschatte tijd toocomplete:** 45 minuten</span><span class="sxs-lookup"><span data-stu-id="43c60-109">**Estimated time toocomplete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="43c60-110">SSMS in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="43c60-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="43c60-111">Azure RemoteApp is een RDS-service in Azure die toepassingen levert.</span><span class="sxs-lookup"><span data-stu-id="43c60-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="43c60-112">Meer informatie over deze hier: [wat is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="43c60-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="43c60-113">SSMS uitgevoerd in Azure RemoteApp biedt Hallo u dezelfde ervaring als SSMS lokaal uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="43c60-113">SSMS running in Azure RemoteApp gives you hello same experience as running SSMS locally.</span></span>

![Schermopname van SSMS uitgevoerd in Azure RemoteApp][1]

## <a name="benefits"></a><span data-ttu-id="43c60-115">Voordelen</span><span class="sxs-lookup"><span data-stu-id="43c60-115">Benefits</span></span>
<span data-ttu-id="43c60-116">Er zijn veel voordelen toousing SSMS in Azure RemoteApp, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="43c60-116">There are many benefits toousing SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="43c60-117">Poort 1433 op Azure SQL-server heeft geen toobe blootgesteld extern (buiten Azure).</span><span class="sxs-lookup"><span data-stu-id="43c60-117">Port 1433 on Azure SQL server does not have toobe exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="43c60-118">Er is geen noodzaak tookeep toevoegen en verwijderen van IP-adressen in de firewall hello Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="43c60-118">No need tookeep adding and removing IP addresses in hello Azure SQL server firewall.</span></span>
* <span data-ttu-id="43c60-119">Alle verbindingen met Azure RemoteApp vindt plaats via HTTPS over het gebruik van poort 443 versleuteld Remote Desktop protocol</span><span class="sxs-lookup"><span data-stu-id="43c60-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="43c60-120">Het is van meerdere gebruikers en kan worden geschaald.</span><span class="sxs-lookup"><span data-stu-id="43c60-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="43c60-121">Er is een prestatieverbetering van SSMS in Hallo hebben dezelfde regio bevinden als Hallo SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="43c60-121">There is a performance gain from having SSMS in hello same region as hello SQL Database.</span></span>
* <span data-ttu-id="43c60-122">U kunt gebruik van Azure RemoteApp met Hallo Premium-editie van Azure Active Directory, die gebruiker activiteit rapporten controleren.</span><span class="sxs-lookup"><span data-stu-id="43c60-122">You can audit use of Azure RemoteApp with hello Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="43c60-123">U kunt multi-factor authentication (MFA) inschakelen.</span><span class="sxs-lookup"><span data-stu-id="43c60-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="43c60-124">Toegang SSMS overal wanneer u een van de Hallo ondersteund Azure RemoteApp-clients, waaronder iOS, Android, Mac, Windows Phone en Windows-PC's.</span><span class="sxs-lookup"><span data-stu-id="43c60-124">Access SSMS anywhere when using any of hello supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-hello-azure-remoteapp-collection"></a><span data-ttu-id="43c60-125">Hello Azure RemoteApp-verzameling maken</span><span class="sxs-lookup"><span data-stu-id="43c60-125">Create hello Azure RemoteApp collection</span></span>
<span data-ttu-id="43c60-126">Hier volgen Hallo stappen toocreate uw Azure RemoteApp-collectie met SSMS:</span><span class="sxs-lookup"><span data-stu-id="43c60-126">Here are hello steps toocreate your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="43c60-127">1. Een nieuwe Windows VM vanaf installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="43c60-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="43c60-128">Gebruik Hallo 'Windows Server Remote Desktop Session Host Windows Server 2012 R2' installatiekopie van Hallo galerie toomake uw nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="43c60-128">Use hello "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from hello Gallery toomake your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="43c60-129">2. SSMS van SQL Express installeren</span><span class="sxs-lookup"><span data-stu-id="43c60-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="43c60-130">Ga op Hallo van nieuwe virtuele machine en ga toothis downloadpagina: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="43c60-130">Go onto hello new VM and navigate toothis download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="43c60-131">Er is een optie tooonly download SSMS.</span><span class="sxs-lookup"><span data-stu-id="43c60-131">There is an option tooonly download SSMS.</span></span> <span data-ttu-id="43c60-132">Na het downloaden, gaat u naar de installatiemap Hallo en voer Setup tooinstall SSMS.</span><span class="sxs-lookup"><span data-stu-id="43c60-132">After download, go into hello install directory and run Setup tooinstall SSMS.</span></span>

<span data-ttu-id="43c60-133">U moet ook tooinstall SQL Server 2014 Service Pack 1.</span><span class="sxs-lookup"><span data-stu-id="43c60-133">You also need tooinstall SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="43c60-134">U kunt dit hier downloaden: [Microsoft SQL Server 2014 met Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span><span class="sxs-lookup"><span data-stu-id="43c60-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="43c60-135">SQL Server 2014 Service Pack 1 bevat essentiële functionaliteit voor het werken met Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="43c60-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="43c60-136">3. Script uitvoeren valideren en Sysprep</span><span class="sxs-lookup"><span data-stu-id="43c60-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="43c60-137">Bureaublad Hallo VM is op Hallo een PowerShell-script valideren genoemd.</span><span class="sxs-lookup"><span data-stu-id="43c60-137">On hello desktop of hello VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="43c60-138">Deze door te dubbelklikken op uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="43c60-138">Run this by double-clicking.</span></span> <span data-ttu-id="43c60-139">Deze controleert dat die Hallo VM is gereed toobe gebruikt voor externe hosting van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="43c60-139">It will verify that hello VM is ready toobe used for remote hosting of applications.</span></span> <span data-ttu-id="43c60-140">Als verificatie voltooid is, wordt deze gevraagd toorun sysprep - toorun kiezen deze.</span><span class="sxs-lookup"><span data-stu-id="43c60-140">When verification is complete, it will ask toorun sysprep - choose toorun it.</span></span>

<span data-ttu-id="43c60-141">Als sysprep is voltooid, wordt het Hallo VM afsluiten.</span><span class="sxs-lookup"><span data-stu-id="43c60-141">When sysprep completes, it will shut down hello VM.</span></span>

<span data-ttu-id="43c60-142">toolearn meer informatie over het maken van een Azure RemoteApp-installatiekopie, Zie: [hoe toocreate een sjabloon voor RemoteApp-installatiekopie in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="43c60-142">toolearn more about creating a Azure RemoteApp image, see: [How toocreate a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="43c60-143">4. Installatiekopie vastleggen</span><span class="sxs-lookup"><span data-stu-id="43c60-143">4. Capture image</span></span>
<span data-ttu-id="43c60-144">Wanneer Hallo VM is gestopt, vinden in de huidige portal Hallo en vastlegt.</span><span class="sxs-lookup"><span data-stu-id="43c60-144">When hello VM has stopped running, find it in hello current portal and capture it.</span></span>

<span data-ttu-id="43c60-145">toolearn meer informatie over het vastleggen van een afbeelding Zie [een installatiekopie van een Windows Azure virtuele machine gemaakt met het klassieke implementatiemodel Hallo](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="43c60-145">toolearn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with hello classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-tooazure-remoteapp-template-images"></a><span data-ttu-id="43c60-146">5. RemoteApp-sjablooninstallatiekopieën tooAzure toevoegen</span><span class="sxs-lookup"><span data-stu-id="43c60-146">5. Add tooAzure RemoteApp Template images</span></span>
<span data-ttu-id="43c60-147">Hallo Azure RemoteApp-sectie van de huidige portal hello, gaat u toohello Sjablooninstallatiekopieën tabblad en klik op toevoegen.</span><span class="sxs-lookup"><span data-stu-id="43c60-147">In hello Azure RemoteApp section of hello current portal, go toohello Template Images tab and click Add.</span></span> <span data-ttu-id="43c60-148">In het pop-vak hello, selecteert u 'Een installatiekopie van het importeren van de bibliotheek van uw virtuele Machines' en kies vervolgens Hallo-installatiekopie die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="43c60-148">In hello pop-up box, select "Import an image from your Virtual Machines library" and then choose hello Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="43c60-149">6. Cloudverzameling maken</span><span class="sxs-lookup"><span data-stu-id="43c60-149">6. Create cloud collection</span></span>
<span data-ttu-id="43c60-150">In de huidige portal Hallo, maak een nieuwe Azure RemoteApp-Cloudverzameling.</span><span class="sxs-lookup"><span data-stu-id="43c60-150">In hello current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="43c60-151">Kies Hallo-Sjablooninstallatiekopie die u zojuist hebt geïmporteerd met SSMS is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="43c60-151">Choose hello Template Image that you just imported with SSMS installed on it.</span></span>

![Nieuwe cloudverzameling maken][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="43c60-153">7. Publiceren van SSMS</span><span class="sxs-lookup"><span data-stu-id="43c60-153">7. Publish SSMS</span></span>
<span data-ttu-id="43c60-154">Op het tabblad van de nieuwe cloudverzameling, selecteer publiceren een toepassing wordt publiceren Hallo Hallo Menu Start en kies vervolgens SSMS uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="43c60-154">On hello Publishing tab of your new cloud collection, select Publish an application from hello Start Menu and then choose SSMS from hello list.</span></span>

![App publiceren][5]

### <a name="8-add-users"></a><span data-ttu-id="43c60-156">8. Gebruikers toevoegen</span><span class="sxs-lookup"><span data-stu-id="43c60-156">8. Add users</span></span>
<span data-ttu-id="43c60-157">U kunt op Hallo gebruikerstoegang tabblad Hallo-gebruikers die toegang toothis Azure RemoteApp-verzameling waaronder alleen SSMS selecteren.</span><span class="sxs-lookup"><span data-stu-id="43c60-157">On hello User Access tab you can select hello users that will have access toothis Azure RemoteApp collection which only includes SSMS.</span></span>

![Gebruiker toevoegen][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a><span data-ttu-id="43c60-159">9. Toepassing hello Azure RemoteApp-client installeren</span><span class="sxs-lookup"><span data-stu-id="43c60-159">9. Install hello Azure RemoteApp client application</span></span>
<span data-ttu-id="43c60-160">U kunt downloaden en installeren van een Azure RemoteApp-client: [downloaden | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="43c60-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="43c60-161">Azure SQL-server configureren</span><span class="sxs-lookup"><span data-stu-id="43c60-161">Configure Azure SQL server</span></span>
<span data-ttu-id="43c60-162">Hallo is alleen configuratie is vereist is tooensure dat Azure Services voor Hallo firewall ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="43c60-162">hello only configuration needed is tooensure that Azure Services is enabled for hello firewall.</span></span> <span data-ttu-id="43c60-163">Als u deze oplossing gebruikt, hoeft niet u tooadd IP-adressen tooopen Hallo firewall.</span><span class="sxs-lookup"><span data-stu-id="43c60-163">If you use this solution, then you do not need tooadd any IP addresses tooopen hello firewall.</span></span> <span data-ttu-id="43c60-164">Hallo-netwerkverkeer dat is toegestaan toohello SQL Server is van andere Azure-services.</span><span class="sxs-lookup"><span data-stu-id="43c60-164">hello network traffic that is allowed toohello SQL Server is from other Azure services.</span></span>

![Azure toestaan][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="43c60-166">Multi-factor Authentication (MFA)</span><span class="sxs-lookup"><span data-stu-id="43c60-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="43c60-167">MFA kan specifiek voor deze toepassing worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="43c60-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="43c60-168">Ga toohello op het tabblad toepassingen van uw Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="43c60-168">Go toohello Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="43c60-169">U vindt een vermelding voor Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="43c60-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="43c60-170">Als u deze toepassing op en configureer vervolgens, ziet u Hallo pagina hieronder waar u MFA voor deze toepassing inschakelen kunt.</span><span class="sxs-lookup"><span data-stu-id="43c60-170">If you click that application and then configure, you will see hello page below where you can enable MFA for this application.</span></span>

![Schakel MFA in][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="43c60-172">Controle van gebruikersactiviteit met Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="43c60-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="43c60-173">Als u nog geen Azure AD Premium, hebt u tooturn Hallo deze op in de sectie licenties van uw directory.</span><span class="sxs-lookup"><span data-stu-id="43c60-173">If you do not have Azure AD Premium, then you have tooturn it on in hello Licenses section of your directory.</span></span> <span data-ttu-id="43c60-174">Met de Premium is ingeschakeld, kunt u gebruikers toewijzen toohello Premium niveau.</span><span class="sxs-lookup"><span data-stu-id="43c60-174">With Premium enabled, you can assign users toohello Premium level.</span></span>

<span data-ttu-id="43c60-175">Wanneer u tooa gebruiker in uw Azure Active Directory gaat, kunt u vervolgens toohello activiteit tabblad toosee aanmelding informatie tooAzure RemoteApp gaan.</span><span class="sxs-lookup"><span data-stu-id="43c60-175">When you go tooa user in your Azure Active Directory, you can then go toohello Activity tab toosee login information tooAzure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43c60-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="43c60-176">Next steps</span></span>
<span data-ttu-id="43c60-177">Na het voltooien van alle Hallo bovenstaande stappen u kunt toorun hello Azure RemoteApp-client en aanmelden met een toegewezen gebruiker.</span><span class="sxs-lookup"><span data-stu-id="43c60-177">After completing all hello above steps, you will be able toorun hello Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="43c60-178">U krijgt SSMS als een van uw toepassingen en u het kunt uitvoeren, zoals u zou doen als deze zijn geïnstalleerd op uw computer met toegang tooAzure SQL server.</span><span class="sxs-lookup"><span data-stu-id="43c60-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access tooAzure SQL server.</span></span>

<span data-ttu-id="43c60-179">Zie voor meer informatie over hoe toomake verbinding tooSQL Database hello, [tooSQL Database verbinding met SQL Server Management Studio en een voorbeeld T-SQL-query uitvoert](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="43c60-179">For more information on how toomake hello connection tooSQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="43c60-180">Dat is alles wat nu.</span><span class="sxs-lookup"><span data-stu-id="43c60-180">That's everything for now.</span></span> <span data-ttu-id="43c60-181">Veel plezier!</span><span class="sxs-lookup"><span data-stu-id="43c60-181">Enjoy!</span></span>

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png