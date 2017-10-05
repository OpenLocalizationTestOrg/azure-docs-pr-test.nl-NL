---
title: Runtime-installatie van Azure Functions | Microsoft Docs
description: Het installeren van de Azure Functions-Runtime
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 1e4188313a87d07f396e5f8edc8969dd5da2c436
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="05e42-103">Installeer de Azure Functions-Runtime-Preview</span><span class="sxs-lookup"><span data-stu-id="05e42-103">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="05e42-104">Als u installeren van de preview van Azure Functions-Runtime wilt, moet u deze stappen volgen:</span><span class="sxs-lookup"><span data-stu-id="05e42-104">If you would like to install the Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="05e42-105">Zorg ervoor dat uw machine voldoet aan de minimale vereisten</span><span class="sxs-lookup"><span data-stu-id="05e42-105">Ensure your machine passes the minimum requirements</span></span>
1. <span data-ttu-id="05e42-106">Download de [Runtime Preview installatieprogramma van Azure Functions](https://aka.ms/azafr).</span><span class="sxs-lookup"><span data-stu-id="05e42-106">Download the [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="05e42-107">Installeer de Azure Functions-Runtime-preview</span><span class="sxs-lookup"><span data-stu-id="05e42-107">Install the Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="05e42-108">Voltooi de configuratie van de Azure Functions-Runtime-preview</span><span class="sxs-lookup"><span data-stu-id="05e42-108">Complete the configuration of the Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05e42-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="05e42-109">Prerequisites</span></span>

<span data-ttu-id="05e42-110">Voordat u de Azure Functions-Runtime-preview installeert, moet u het volgende hebben:</span><span class="sxs-lookup"><span data-stu-id="05e42-110">Before you install the Azure Functions Runtime preview, you must have the following:</span></span>

1. <span data-ttu-id="05e42-111">Een computer waarop Microsoft Windows Server 2016 of Microsoft Windows 10 auteurs Update (Professional of Enterprise Edition) wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="05e42-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="05e42-112">Een exemplaar van SQL Server die in uw netwerk worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="05e42-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="05e42-113">Minimale versie vereiste is SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="05e42-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="05e42-114">Installeer de Azure Functions-Runtime-Preview</span><span class="sxs-lookup"><span data-stu-id="05e42-114">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="05e42-115">Het installatieprogramma van Azure Functions-Runtime preview begeleidt u bij de installatie van de Azure Functions-Runtime preview beheer- en werkrollen.</span><span class="sxs-lookup"><span data-stu-id="05e42-115">The Azure Functions Runtime preview installer guides you through the installation of the Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="05e42-116">Het is mogelijk de beheer- en werkrollen-functie installeren op dezelfde machine.</span><span class="sxs-lookup"><span data-stu-id="05e42-116">It is possible to install the Management and Worker role on the same machine.</span></span>  <span data-ttu-id="05e42-117">Als u meer functies toevoegt, moet u echter meer werkrollen op extra computers te schalen van uw functies naar meerdere werknemers kunnen implementeren.</span><span class="sxs-lookup"><span data-stu-id="05e42-117">However, as you add more Functions, you must deploy more worker roles on additional machines to be able to scale your functions onto multiple workers.</span></span>

## <a name="install-the-management-and-worker-role-on-the-same-machine"></a><span data-ttu-id="05e42-118">Het beheer en de Werkrol op dezelfde computer installeren</span><span class="sxs-lookup"><span data-stu-id="05e42-118">Install the Management and Worker Role on the same machine</span></span>

1. <span data-ttu-id="05e42-119">Start het installatieprogramma van Azure Functions-Runtime Preview.</span><span class="sxs-lookup"><span data-stu-id="05e42-119">Run the Azure Functions Runtime Preview Installer.</span></span>

    ![Azure Functions-Runtime Preview-installatieprogramma][1]

1. <span data-ttu-id="05e42-121">**Klik op volgende** vooraf voorbij de eerste fase van het installatieprogramma</span><span class="sxs-lookup"><span data-stu-id="05e42-121">**Click Next** advance past the first stage of the installer</span></span>
1. <span data-ttu-id="05e42-122">Zodra u lees de voorwaarden van de **overeenkomst**, **het selectievakje** de voorwaarden accepteren en **Klik op volgende** om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="05e42-122">Once you have read the terms of the **EULA**, **check the box** to accept the terms and **click Next** to advance.</span></span>
1. <span data-ttu-id="05e42-123">Nu selecteren de rollen die u wilt installeren op deze machine **functies Beheerrol** en/of **functies Werkrol** en **Klik op volgende**</span><span class="sxs-lookup"><span data-stu-id="05e42-123">Now select the roles you want to install on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Azure Functions-Runtime Preview Installer - selectie van Systeemrol][3]

    > [!NOTE]
    > <span data-ttu-id="05e42-125">U kunt installeren de **functies Werkrol** op veel andere computers om dit te doen, volgt u deze instructies en selecteer alleen de **functies Werkrol** in het installatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="05e42-125">You can install the **Functions Worker Role** on many other machines to do so, follow these instructions, and only select **Functions Worker Role** in the installer.</span></span>

1. <span data-ttu-id="05e42-126">**Klik op volgende** hebben de **Azure Functions-Runtime-installatieprogramma** installeren op uw computer.</span><span class="sxs-lookup"><span data-stu-id="05e42-126">**Click Next** to have the **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="05e42-127">Nadat het installatieprogramma start de **Azure Functions-Runtime configuratiehulpprogramma**.</span><span class="sxs-lookup"><span data-stu-id="05e42-127">Once complete the installer will launch the **Azure Functions Runtime Configuration tool**.</span></span>

    ![Azure Functions-Runtime Preview installatieprogramma voltooid][5]

    > [!NOTE]
    > <span data-ttu-id="05e42-129">Als u wilt installeren op **Windows 10** en de **Container** functie heeft niet eerder is ingeschakeld, de **Azure Functions-Runtime** installatieprogramma vraagt u te starten om uw de machine om de installatie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="05e42-129">If you are installing on **Windows 10** and the **Container** feature has not been previously enabled, the **Azure Functions Runtime** Installer prompts you to reboot your machine to complete the install.</span></span>

## <a name="configure-the-azure-functions-runtime"></a><span data-ttu-id="05e42-130">Configureren van de Azure Functions-Runtime</span><span class="sxs-lookup"><span data-stu-id="05e42-130">Configure the Azure Functions Runtime</span></span>

<span data-ttu-id="05e42-131">U moet de configuratie te voltooien om de Azure Functions-Runtime-installatie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="05e42-131">To complete the Azure Functions Runtime installation you must complete the configuration.</span></span>

1. <span data-ttu-id="05e42-132">De **Azure Functions-Runtime-configuratieprogramma** ziet u welke functies op uw computer zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="05e42-132">The **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Azure Functions-Runtime Preview Configuration Tool][6]

1. <span data-ttu-id="05e42-134">Klik op de **Database** tabblad, voert u de **Verbindingsdetails voor uw SQL Server-exemplaar** en **Klik op toepassen**.</span><span class="sxs-lookup"><span data-stu-id="05e42-134">Click the **Database** tab, enter the **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="05e42-135">Dit is vereist in volgorde van de Azure Functions-Runtime voor het maken van een database voor de ondersteuning van de Runtime.</span><span class="sxs-lookup"><span data-stu-id="05e42-135">This is required in order to the Azure Functions Runtime to create a database to support the Runtime.</span></span>
    
    ![Azure Functions-Runtime Preview databaseconfiguratie][7]

1. <span data-ttu-id="05e42-137">Klik op de **referenties** tabblad.</span><span class="sxs-lookup"><span data-stu-id="05e42-137">Click the **Credentials** tab.</span></span>  <span data-ttu-id="05e42-138">In dit scherm moet u twee nieuwe referenties voor gebruik met een bestandsshare maken voor het hosten van uw Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="05e42-138">On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="05e42-139">**Geef een gebruikersnaam en wachtwoord** combinaties voor de **Share bestandseigenaar** en voor de **File Share gebruiker** en klik op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="05e42-139">**Specify Username and Password** combinations for the **File Share Owner** and for the **File Share User** and click **Apply**.</span></span>

    ![Azure Functions-Runtime Preview referenties][8]

1. <span data-ttu-id="05e42-141">Klik op de **bestandsshare** tabblad.</span><span class="sxs-lookup"><span data-stu-id="05e42-141">Click the **File Share** tab.</span></span>  <span data-ttu-id="05e42-142">In dit scherm moet u de details van de **bestandsshare-locatie**.</span><span class="sxs-lookup"><span data-stu-id="05e42-142">In this screen you must specify the details of the **File Share location**.</span></span>  <span data-ttu-id="05e42-143">Dit kan worden gemaakt voor u of u kunt een bestaande bestandsshare gebruiken en klik op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="05e42-143">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="05e42-144">Als u een nieuwe bestandsshare-locatie selecteert, moet u een map voor gebruik door de Azure Functions-Runtime.</span><span class="sxs-lookup"><span data-stu-id="05e42-144">If you select a new File Share location, you must specify a directory for use by the Azure Functions Runtime.</span></span>
    
    ![Azure Functions-Runtime Preview-bestandsshare][9]

1. <span data-ttu-id="05e42-146">Klik op de **IIS** tabblad.</span><span class="sxs-lookup"><span data-stu-id="05e42-146">Click the **IIS** tab.</span></span>  <span data-ttu-id="05e42-147">Op dit tabblad ziet de details van de websites in IIS die de Azure Functions-Runtime-installatie maakt.</span><span class="sxs-lookup"><span data-stu-id="05e42-147">This tab shows the details of the websites in IIS that the Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="05e42-148">**Klik op toepassen** te voltooien.</span><span class="sxs-lookup"><span data-stu-id="05e42-148">**Click Apply** to complete.</span></span>

    ![Preview van Azure Functions-Runtime IIS][10]

1. <span data-ttu-id="05e42-150">Klik op de **Services** tabblad.</span><span class="sxs-lookup"><span data-stu-id="05e42-150">Click the **Services** tab.</span></span>  <span data-ttu-id="05e42-151">Op dit tabblad toont de status van de services in uw Azure Functions-Runtime-installatie.</span><span class="sxs-lookup"><span data-stu-id="05e42-151">This tab shows the status of the services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="05e42-152">Als na de initiële configuratie de **Activation-Service van Azure Functions Host** wordt niet uitgevoerd Klik **Service starten**</span><span class="sxs-lookup"><span data-stu-id="05e42-152">If after initial configuration the **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Azure Functions-Runtime Preview Configruation voltooid][11]

1. <span data-ttu-id="05e42-154">Ten slotte bladert u naar de **Azure Functions-Runtime Portal** als`https://<machinename>/`</span><span class="sxs-lookup"><span data-stu-id="05e42-154">Finally browse to the **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

    ![Preview-Portal voor Azure Functions-Runtime][12]


<!--Image references-->
[1]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer1.png
[2]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer2-EULA.png
[3]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer3-ChooseRoles.png
[4]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer4-Install.png
[5]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer5-InstallComplete.png
[6]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration1.png
[7]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration2_SQL.png
[8]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration3_Credentials.png
[9]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration4_Fileshare.png
[10]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration5_IIS.png
[11]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration6_Services.png
[12]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal.png