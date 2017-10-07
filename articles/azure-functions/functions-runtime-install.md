---
title: Runtime-installatie van functies aaaAzure | Microsoft Docs
description: Hoe tooInstall hello Azure Functions-Runtime
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
ms.openlocfilehash: 67c6d10b5c0ac43e880d29cff0ae7b099f82bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="f708c-103">Hello Azure Functions-Runtime Preview installeren</span><span class="sxs-lookup"><span data-stu-id="f708c-103">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="f708c-104">Als u tooinstall hello Azure Functions-Runtime preview wilt, moet u deze stappen volgen:</span><span class="sxs-lookup"><span data-stu-id="f708c-104">If you would like tooinstall hello Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="f708c-105">Zorg ervoor dat uw machine voldoet aan de minimumvereisten Hallo</span><span class="sxs-lookup"><span data-stu-id="f708c-105">Ensure your machine passes hello minimum requirements</span></span>
1. <span data-ttu-id="f708c-106">Hallo downloaden [Azure Functions-Runtime Preview Installer](https://aka.ms/azafr).</span><span class="sxs-lookup"><span data-stu-id="f708c-106">Download hello [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="f708c-107">Installeer hello Azure Functions-Runtime-preview</span><span class="sxs-lookup"><span data-stu-id="f708c-107">Install hello Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="f708c-108">Configuratie van de volledige Hallo van hello Azure Functions-Runtime-preview</span><span class="sxs-lookup"><span data-stu-id="f708c-108">Complete hello configuration of hello Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f708c-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f708c-109">Prerequisites</span></span>

<span data-ttu-id="f708c-110">Voordat u hello Azure Functions-Runtime preview installeert, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="f708c-110">Before you install hello Azure Functions Runtime preview, you must have hello following:</span></span>

1. <span data-ttu-id="f708c-111">Een computer waarop Microsoft Windows Server 2016 of Microsoft Windows 10 auteurs Update (Professional of Enterprise Edition) wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f708c-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="f708c-112">Een exemplaar van SQL Server die in uw netwerk worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f708c-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="f708c-113">Minimale versie vereiste is SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="f708c-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="f708c-114">Hello Azure Functions-Runtime Preview installeren</span><span class="sxs-lookup"><span data-stu-id="f708c-114">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="f708c-115">Hello Azure Functions-Runtime preview installatieprogramma leidt u door het Hallo-installatie van hello Azure Functions-Runtime preview beheer- en werkrollen.</span><span class="sxs-lookup"><span data-stu-id="f708c-115">hello Azure Functions Runtime preview installer guides you through hello installation of hello Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="f708c-116">Het is mogelijk tooinstall Hallo Management en een werkrol op Hallo dezelfde machine.</span><span class="sxs-lookup"><span data-stu-id="f708c-116">It is possible tooinstall hello Management and Worker role on hello same machine.</span></span>  <span data-ttu-id="f708c-117">Echter, als u meer functies toevoegt, moet u implementeren meer werkrollen op extra computers toobe kunnen tooscale uw functies naar meerdere werknemers.</span><span class="sxs-lookup"><span data-stu-id="f708c-117">However, as you add more Functions, you must deploy more worker roles on additional machines toobe able tooscale your functions onto multiple workers.</span></span>

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a><span data-ttu-id="f708c-118">Hallo Management en een Werkrol installeren op Hallo dezelfde machine</span><span class="sxs-lookup"><span data-stu-id="f708c-118">Install hello Management and Worker Role on hello same machine</span></span>

1. <span data-ttu-id="f708c-119">Hello Azure Functions-Runtime Preview installatieprogramma worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f708c-119">Run hello Azure Functions Runtime Preview Installer.</span></span>

    ![Azure Functions-Runtime Preview-installatieprogramma][1]

1. <span data-ttu-id="f708c-121">**Klik op volgende** vooraf voorbij de eerste fase Hallo van Hallo installer</span><span class="sxs-lookup"><span data-stu-id="f708c-121">**Click Next** advance past hello first stage of hello installer</span></span>
1. <span data-ttu-id="f708c-122">Zodra u Hallo Hallo gebruiksvoorwaarden hebt gelezen **overeenkomst**, **Hallo selectievakje** tooaccept Hallo voorwaarden en **Klik op volgende** tooadvance.</span><span class="sxs-lookup"><span data-stu-id="f708c-122">Once you have read hello terms of hello **EULA**, **check hello box** tooaccept hello terms and **click Next** tooadvance.</span></span>
1. <span data-ttu-id="f708c-123">Nu Selecteer rollen Hallo gewenste tooinstall op deze machine **functies Beheerrol** en/of **functies Werkrol** en **Klik op volgende**</span><span class="sxs-lookup"><span data-stu-id="f708c-123">Now select hello roles you want tooinstall on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Azure Functions-Runtime Preview Installer - selectie van Systeemrol][3]

    > [!NOTE]
    > <span data-ttu-id="f708c-125">Kunt u Hallo installeren **functies Werkrol** op veel andere machines toodo geval is, volg deze instructies en selecteer alleen de **functies Werkrol** in Hallo-installatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="f708c-125">You can install hello **Functions Worker Role** on many other machines toodo so, follow these instructions, and only select **Functions Worker Role** in hello installer.</span></span>

1. <span data-ttu-id="f708c-126">**Klik op volgende** toohave hello **Azure Functions-Runtime-installatieprogramma** installeren op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f708c-126">**Click Next** toohave hello **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="f708c-127">Zodra de volledige Hallo installatieprogramma start Hallo **Azure Functions-Runtime configuratiehulpprogramma**.</span><span class="sxs-lookup"><span data-stu-id="f708c-127">Once complete hello installer will launch hello **Azure Functions Runtime Configuration tool**.</span></span>

    ![Azure Functions-Runtime Preview installatieprogramma voltooid][5]

    > [!NOTE]
    > <span data-ttu-id="f708c-129">Als u wilt installeren op **Windows 10** en Hallo **Container** functie is niet eerder hebt ingeschakeld, hello **Azure Functions-Runtime** Installer vraagt u tooreboot uw machine toocomplete Hallo installeren.</span><span class="sxs-lookup"><span data-stu-id="f708c-129">If you are installing on **Windows 10** and hello **Container** feature has not been previously enabled, hello **Azure Functions Runtime** Installer prompts you tooreboot your machine toocomplete hello install.</span></span>

## <a name="configure-hello-azure-functions-runtime"></a><span data-ttu-id="f708c-130">Hello Azure Functions-Runtime configureren</span><span class="sxs-lookup"><span data-stu-id="f708c-130">Configure hello Azure Functions Runtime</span></span>

<span data-ttu-id="f708c-131">toocomplete hello Azure Functions-Runtime-installatie moet u Hallo-configuratie voltooien.</span><span class="sxs-lookup"><span data-stu-id="f708c-131">toocomplete hello Azure Functions Runtime installation you must complete hello configuration.</span></span>

1. <span data-ttu-id="f708c-132">Hallo **Azure Functions-Runtime-configuratieprogramma** ziet u welke functies op uw computer zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f708c-132">hello **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Azure Functions-Runtime Preview Configuration Tool][6]

1. <span data-ttu-id="f708c-134">Klik op Hallo **Database** tabblad, voert u Hallo **Verbindingsdetails voor uw SQL Server-exemplaar** en **Klik op toepassen**.</span><span class="sxs-lookup"><span data-stu-id="f708c-134">Click hello **Database** tab, enter hello **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="f708c-135">Dit is vereist in de volgorde toohello Azure Functions-Runtime toocreate een database toosupport Hallo Runtime.</span><span class="sxs-lookup"><span data-stu-id="f708c-135">This is required in order toohello Azure Functions Runtime toocreate a database toosupport hello Runtime.</span></span>
    
    ![Azure Functions-Runtime Preview databaseconfiguratie][7]

1. <span data-ttu-id="f708c-137">Klik op Hallo **referenties** tabblad.  In dit scherm moet u twee nieuwe referenties voor gebruik met een bestandsshare maken voor het hosten van uw Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="f708c-137">Click hello **Credentials** tab.  On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="f708c-138">**Geef een gebruikersnaam en wachtwoord** combinaties van Hallo **Share bestandseigenaar** en voor Hallo **File Share gebruiker** en klik op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="f708c-138">**Specify Username and Password** combinations for hello **File Share Owner** and for hello **File Share User** and click **Apply**.</span></span>

    ![Azure Functions-Runtime Preview referenties][8]

1. <span data-ttu-id="f708c-140">Klik op Hallo **bestandsshare** tabblad.  In dit scherm Geef details op Hallo van Hallo **bestandsshare-locatie**.</span><span class="sxs-lookup"><span data-stu-id="f708c-140">Click hello **File Share** tab.  In this screen you must specify hello details of hello **File Share location**.</span></span>  <span data-ttu-id="f708c-141">Dit kan worden gemaakt voor u of u kunt een bestaande bestandsshare gebruiken en klik op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="f708c-141">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="f708c-142">Als u een nieuwe bestandsshare-locatie selecteert, moet u een map voor gebruik door hello Azure Functions-Runtime.</span><span class="sxs-lookup"><span data-stu-id="f708c-142">If you select a new File Share location, you must specify a directory for use by hello Azure Functions Runtime.</span></span>
    
    ![Azure Functions-Runtime Preview-bestandsshare][9]

1. <span data-ttu-id="f708c-144">Klik op Hallo **IIS** tabblad.  Op dit tabblad Hallo worden details weergegeven van Hallo websites in IIS die hello Azure Functions-Runtime-installatie maakt.</span><span class="sxs-lookup"><span data-stu-id="f708c-144">Click hello **IIS** tab.  This tab shows hello details of hello websites in IIS that hello Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="f708c-145">**Klik op toepassen** toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f708c-145">**Click Apply** toocomplete.</span></span>

    ![Preview van Azure Functions-Runtime IIS][10]

1. <span data-ttu-id="f708c-147">Klik op Hallo **Services** tabblad.  Dit tabblad toont Hallo status van Hallo-services in uw Azure Functions-Runtime-installatie.</span><span class="sxs-lookup"><span data-stu-id="f708c-147">Click hello **Services** tab.  This tab shows hello status of hello services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="f708c-148">Als na de initiële configuratie Hallo **Activation-Service van Azure Functions Host** wordt niet uitgevoerd Klik **Service starten**</span><span class="sxs-lookup"><span data-stu-id="f708c-148">If after initial configuration hello **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Azure Functions-Runtime Preview Configruation voltooid][11]

1. <span data-ttu-id="f708c-150">Ten slotte bladeren toohello **Azure Functions-Runtime Portal** als`https://<machinename>/`</span><span class="sxs-lookup"><span data-stu-id="f708c-150">Finally browse toohello **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

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