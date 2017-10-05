---
title: Verbinding maken met SQL Database met SQL Server Management Studio in Azure RemoteApp | Microsoft Docs
description: Gebruik deze handleiding om meer informatie over het SQL Server Management Studio in Azure RemoteApp voor beveiliging en prestaties wordt gebruikt om verbinding te maken met SQL-Database
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
ms.openlocfilehash: ae1f2fa38d38fe6c10bc7960fddb07ae330d1eeb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-to-connect-to-sql-database"></a><span data-ttu-id="07969-103">SQL Server Management Studio in Azure RemoteApp gebruiken voor verbinding met SQL-Database</span><span class="sxs-lookup"><span data-stu-id="07969-103">Use SQL Server Management Studio in Azure RemoteApp to connect to SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07969-104">Azure RemoteApp wordt buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="07969-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="07969-105">Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="07969-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="07969-106">Inleiding</span><span class="sxs-lookup"><span data-stu-id="07969-106">Introduction</span></span>
<span data-ttu-id="07969-107">Deze zelfstudie laat zien hoe u verbinding maken met SQL Database met SQL Server Management Studio (SSMS) in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="07969-107">This tutorial shows you how to use SQL Server Management Studio (SSMS) in Azure RemoteApp to connect to SQL Database.</span></span> <span data-ttu-id="07969-108">Deze begeleidt u bij het proces voor het instellen van SQL Server Management Studio in Azure RemoteApp, worden de voordelen en toont beveiligingsfuncties die u kunt gebruiken in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07969-108">It walks you through the process of setting up SQL Server Management Studio in Azure RemoteApp, explains the benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="07969-109">**Geschatte duur:** 45 minuten</span><span class="sxs-lookup"><span data-stu-id="07969-109">**Estimated time to complete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="07969-110">SSMS in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="07969-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="07969-111">Azure RemoteApp is een RDS-service in Azure die toepassingen levert.</span><span class="sxs-lookup"><span data-stu-id="07969-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="07969-112">Meer informatie over deze hier: [wat is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="07969-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="07969-113">SSMS uitgevoerd in Azure RemoteApp biedt u dezelfde ervaring als SSMS lokaal uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="07969-113">SSMS running in Azure RemoteApp gives you the same experience as running SSMS locally.</span></span>

![Schermopname van SSMS uitgevoerd in Azure RemoteApp][1]

## <a name="benefits"></a><span data-ttu-id="07969-115">Voordelen</span><span class="sxs-lookup"><span data-stu-id="07969-115">Benefits</span></span>
<span data-ttu-id="07969-116">Er zijn veel voordelen voor het gebruik van SSMS in Azure RemoteApp, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="07969-116">There are many benefits to using SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="07969-117">Poort 1433 op Azure SQL-server heeft geen extern (buiten Azure) worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="07969-117">Port 1433 on Azure SQL server does not have to be exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="07969-118">U hoeft te houden toevoegen en verwijderen van IP-adressen in de Azure SQL server-firewall.</span><span class="sxs-lookup"><span data-stu-id="07969-118">No need to keep adding and removing IP addresses in the Azure SQL server firewall.</span></span>
* <span data-ttu-id="07969-119">Alle verbindingen met Azure RemoteApp vindt plaats via HTTPS over het gebruik van poort 443 versleuteld Remote Desktop protocol</span><span class="sxs-lookup"><span data-stu-id="07969-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="07969-120">Het is van meerdere gebruikers en kan worden geschaald.</span><span class="sxs-lookup"><span data-stu-id="07969-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="07969-121">Er is een prestatieverbetering van SSMS hebben in dezelfde regio bevinden als de SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="07969-121">There is a performance gain from having SSMS in the same region as the SQL Database.</span></span>
* <span data-ttu-id="07969-122">U kunt gebruik van Azure RemoteApp met de Premium-editie van Azure Active Directory, die gebruiker activiteit rapporten controleren.</span><span class="sxs-lookup"><span data-stu-id="07969-122">You can audit use of Azure RemoteApp with the Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="07969-123">U kunt multi-factor authentication (MFA) inschakelen.</span><span class="sxs-lookup"><span data-stu-id="07969-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="07969-124">Toegang SSMS overal wanneer u een van de ondersteunde Azure RemoteApp-clients, waaronder iOS, Android, Mac, Windows Phone en Windows-PC's.</span><span class="sxs-lookup"><span data-stu-id="07969-124">Access SSMS anywhere when using any of the supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-the-azure-remoteapp-collection"></a><span data-ttu-id="07969-125">De Azure RemoteApp-verzameling maken</span><span class="sxs-lookup"><span data-stu-id="07969-125">Create the Azure RemoteApp collection</span></span>
<span data-ttu-id="07969-126">Hier volgen de stappen voor het maken van uw Azure RemoteApp-collectie met SSMS:</span><span class="sxs-lookup"><span data-stu-id="07969-126">Here are the steps to create your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="07969-127">1. Een nieuwe Windows VM vanaf installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="07969-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="07969-128">De installatiekopie van het 'Windows Server Remote Desktop Session Host Windows Server 2012 R2' uit de galerie gebruiken om uw nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="07969-128">Use the "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from the Gallery to make your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="07969-129">2. SSMS van SQL Express installeren</span><span class="sxs-lookup"><span data-stu-id="07969-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="07969-130">Ga naar de nieuwe virtuele machine en navigeer naar deze downloadpagina: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="07969-130">Go onto the new VM and navigate to this download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="07969-131">Er is een optie voor het downloaden van alleen SSMS.</span><span class="sxs-lookup"><span data-stu-id="07969-131">There is an option to only download SSMS.</span></span> <span data-ttu-id="07969-132">Na het downloaden, gaat u naar de installatiemap en voer Setup voor de installatie van SSMS.</span><span class="sxs-lookup"><span data-stu-id="07969-132">After download, go into the install directory and run Setup to install SSMS.</span></span>

<span data-ttu-id="07969-133">U moet ook SQL Server 2014 Service Pack 1 installeert.</span><span class="sxs-lookup"><span data-stu-id="07969-133">You also need to install SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="07969-134">U kunt dit hier downloaden: [Microsoft SQL Server 2014 met Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span><span class="sxs-lookup"><span data-stu-id="07969-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="07969-135">SQL Server 2014 Service Pack 1 bevat essentiële functionaliteit voor het werken met Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="07969-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="07969-136">3. Script uitvoeren valideren en Sysprep</span><span class="sxs-lookup"><span data-stu-id="07969-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="07969-137">Op het bureaublad van de virtuele machine wordt een PowerShell-script valideren genoemd.</span><span class="sxs-lookup"><span data-stu-id="07969-137">On the desktop of the VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="07969-138">Deze door te dubbelklikken op uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="07969-138">Run this by double-clicking.</span></span> <span data-ttu-id="07969-139">Er wordt gecontroleerd dat de virtuele machine gereed om te worden gebruikt is voor externe hosting van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="07969-139">It will verify that the VM is ready to be used for remote hosting of applications.</span></span> <span data-ttu-id="07969-140">Als verificatie voltooid is, wordt u gevraagd naar voert u sysprep - kiezen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="07969-140">When verification is complete, it will ask to run sysprep - choose to run it.</span></span>

<span data-ttu-id="07969-141">Wanneer sysprep is voltooid, wordt deze de virtuele machine afgesloten.</span><span class="sxs-lookup"><span data-stu-id="07969-141">When sysprep completes, it will shut down the VM.</span></span>

<span data-ttu-id="07969-142">Zie voor meer informatie over het maken van een Azure RemoteApp-installatiekopie: [een RemoteApp-sjablooninstallatiekopie maken in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="07969-142">To learn more about creating a Azure RemoteApp image, see: [How to create a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="07969-143">4. Installatiekopie vastleggen</span><span class="sxs-lookup"><span data-stu-id="07969-143">4. Capture image</span></span>
<span data-ttu-id="07969-144">Wanneer de virtuele machine is gestopt, vindt het in de huidige portal en vastlegt.</span><span class="sxs-lookup"><span data-stu-id="07969-144">When the VM has stopped running, find it in the current portal and capture it.</span></span>

<span data-ttu-id="07969-145">Zie voor meer informatie over het vastleggen van een installatiekopie, [een installatiekopie van een Windows Azure virtuele machine gemaakt met het klassieke implementatiemodel](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="07969-145">To learn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with the classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-to-azure-remoteapp-template-images"></a><span data-ttu-id="07969-146">5. Toevoegen aan Azure RemoteApp-sjablooninstallatiekopieën</span><span class="sxs-lookup"><span data-stu-id="07969-146">5. Add to Azure RemoteApp Template images</span></span>
<span data-ttu-id="07969-147">In de Azure RemoteApp-sectie van de huidige portal, gaat u naar het tabblad installatiekopieën van de sjabloon en klikt u op toevoegen.</span><span class="sxs-lookup"><span data-stu-id="07969-147">In the Azure RemoteApp section of the current portal, go to the Template Images tab and click Add.</span></span> <span data-ttu-id="07969-148">Selecteer 'Een afbeelding van uw virtuele Machines bibliotheek importeren' in het pop- en kies vervolgens de installatiekopie die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="07969-148">In the pop-up box, select "Import an image from your Virtual Machines library" and then choose the Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="07969-149">6. Cloudverzameling maken</span><span class="sxs-lookup"><span data-stu-id="07969-149">6. Create cloud collection</span></span>
<span data-ttu-id="07969-150">Maak een nieuwe Azure RemoteApp-Cloudverzameling in de huidige portal.</span><span class="sxs-lookup"><span data-stu-id="07969-150">In the current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="07969-151">Kies de Sjablooninstallatiekopie die u zojuist hebt geïmporteerd met SSMS is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="07969-151">Choose the Template Image that you just imported with SSMS installed on it.</span></span>

![Nieuwe cloudverzameling maken][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="07969-153">7. Publiceren van SSMS</span><span class="sxs-lookup"><span data-stu-id="07969-153">7. Publish SSMS</span></span>
<span data-ttu-id="07969-154">Op de publicatie tabblad van uw nieuwe cloudverzameling, selecteer een toepassing in het Menu Start publiceren en kies vervolgens SSMS in de lijst.</span><span class="sxs-lookup"><span data-stu-id="07969-154">On the Publishing tab of your new cloud collection, select Publish an application from the Start Menu and then choose SSMS from the list.</span></span>

![App publiceren][5]

### <a name="8-add-users"></a><span data-ttu-id="07969-156">8. Gebruikers toevoegen</span><span class="sxs-lookup"><span data-stu-id="07969-156">8. Add users</span></span>
<span data-ttu-id="07969-157">U kunt de gebruikers die toegang hebben tot deze Azure RemoteApp-collectie waaronder alleen SSMS selecteren op het tabblad gebruikerstoegang.</span><span class="sxs-lookup"><span data-stu-id="07969-157">On the User Access tab you can select the users that will have access to this Azure RemoteApp collection which only includes SSMS.</span></span>

![Gebruiker toevoegen][6]

### <a name="9-install-the-azure-remoteapp-client-application"></a><span data-ttu-id="07969-159">9. De toepassing Azure RemoteApp-client installeren</span><span class="sxs-lookup"><span data-stu-id="07969-159">9. Install the Azure RemoteApp client application</span></span>
<span data-ttu-id="07969-160">U kunt downloaden en installeren van een Azure RemoteApp-client: [downloaden | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="07969-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="07969-161">Azure SQL-server configureren</span><span class="sxs-lookup"><span data-stu-id="07969-161">Configure Azure SQL server</span></span>
<span data-ttu-id="07969-162">De enige configuratie nodig is om ervoor te zorgen dat Azure Services voor de firewall is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="07969-162">The only configuration needed is to ensure that Azure Services is enabled for the firewall.</span></span> <span data-ttu-id="07969-163">Als u deze oplossing gebruikt, vervolgens hoeft niet u voor het toevoegen van IP-adressen om de firewall te openen.</span><span class="sxs-lookup"><span data-stu-id="07969-163">If you use this solution, then you do not need to add any IP addresses to open the firewall.</span></span> <span data-ttu-id="07969-164">Het netwerkverkeer dat is toegestaan voor de SQL Server is van andere Azure-services.</span><span class="sxs-lookup"><span data-stu-id="07969-164">The network traffic that is allowed to the SQL Server is from other Azure services.</span></span>

![Azure toestaan][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="07969-166">Multi-factor Authentication (MFA)</span><span class="sxs-lookup"><span data-stu-id="07969-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="07969-167">MFA kan specifiek voor deze toepassing worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="07969-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="07969-168">Ga naar het tabblad toepassingen van uw Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07969-168">Go to the Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="07969-169">U vindt een vermelding voor Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="07969-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="07969-170">Als u deze toepassing op en configureer vervolgens, ziet u de pagina waar u MFA voor deze toepassing inschakelen kunt.</span><span class="sxs-lookup"><span data-stu-id="07969-170">If you click that application and then configure, you will see the page below where you can enable MFA for this application.</span></span>

![Schakel MFA in][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="07969-172">Controle van gebruikersactiviteit met Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="07969-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="07969-173">Als u geen Azure AD Premium, hebt u inschakelen in de sectie licenties van uw directory.</span><span class="sxs-lookup"><span data-stu-id="07969-173">If you do not have Azure AD Premium, then you have to turn it on in the Licenses section of your directory.</span></span> <span data-ttu-id="07969-174">Met Premium is ingeschakeld, kunt u gebruikers toewijzen aan het Premium-niveau.</span><span class="sxs-lookup"><span data-stu-id="07969-174">With Premium enabled, you can assign users to the Premium level.</span></span>

<span data-ttu-id="07969-175">Wanneer u naar een gebruiker in uw Azure Active Directory gaat, kunt u vervolgens naar het tabblad activiteit om te zien van aanmeldingsgegevens naar Azure RemoteApp gaan.</span><span class="sxs-lookup"><span data-stu-id="07969-175">When you go to a user in your Azure Active Directory, you can then go to the Activity tab to see login information to Azure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07969-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="07969-176">Next steps</span></span>
<span data-ttu-id="07969-177">Na het voltooien van de bovenstaande stappen, zult u de Azure RemoteApp-client uitvoeren en het aanmelden met een toegewezen gebruiker.</span><span class="sxs-lookup"><span data-stu-id="07969-177">After completing all the above steps, you will be able to run the Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="07969-178">U krijgt SSMS als een van uw toepassingen en u het kunt uitvoeren, zoals u zou doen als deze zijn geïnstalleerd op uw computer met toegang tot Azure SQL-server.</span><span class="sxs-lookup"><span data-stu-id="07969-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access to Azure SQL server.</span></span>

<span data-ttu-id="07969-179">Zie voor meer informatie over het maken van de verbinding met SQL Database [verbinding maken met SQL Database met SQL Server Management Studio en een voorbeeld T-SQL-query uit te voeren](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="07969-179">For more information on how to make the connection to SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="07969-180">Dat is alles wat nu.</span><span class="sxs-lookup"><span data-stu-id="07969-180">That's everything for now.</span></span> <span data-ttu-id="07969-181">Veel plezier!</span><span class="sxs-lookup"><span data-stu-id="07969-181">Enjoy!</span></span>

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png