---
title: 'Azure Data Lake Tools: Gebruik Azure Data Lake Tools voor Visual Studio Code | Microsoft Docs'
description: 'Ontdek hoe toouse Azure Data Lake Tools voor Visual Studio Code toocreate, testen en U-SQL-scripts uitvoeren. '
Keywords: VScode, Azure Data Lake Tools, lokaal uitvoeren, lokale foutopsporing, lokale Debug preview opslagbestand uploaden toostorage pad
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 77771c5d5dae3bfce4ad2df240ea6c6ef848f288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="7690e-104">Azure Data Lake Tools voor Visual Studio Code gebruiken</span><span class="sxs-lookup"><span data-stu-id="7690e-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="7690e-105">Ontdek hoe toouse Azure Data Lake Tools voor Visual Studio Code (VS-Code) toocreate, testen en U-SQL-scripts uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7690e-105">Learn how toouse Azure Data Lake Tools for Visual Studio Code (VS Code) toocreate, test, and run U-SQL scripts.</span></span> <span data-ttu-id="7690e-106">Hallo-informatie wordt ook beschreven in Hallo video te volgen:</span><span class="sxs-lookup"><span data-stu-id="7690e-106">hello information is also covered in hello following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="7690e-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7690e-107">Prerequisites</span></span>

<span data-ttu-id="7690e-108">Data Lake Tools kan worden geïnstalleerd op Hallo platforms die worden ondersteund door VS-Code.</span><span class="sxs-lookup"><span data-stu-id="7690e-108">Data Lake Tools can be installed on hello platforms supported by VS Code.</span></span> <span data-ttu-id="7690e-109">Hallo ondersteunde platforms zijn Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="7690e-109">hello supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="7690e-110">Hallo verschillende platforms hebben Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="7690e-110">hello different platforms have hello following prerequisites:</span></span>

- <span data-ttu-id="7690e-111">Windows</span><span class="sxs-lookup"><span data-stu-id="7690e-111">Windows</span></span>

    - <span data-ttu-id="7690e-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="7690e-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="7690e-113">[Java Runtime Environment voor SE versie 8 update 77 of hoger](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="7690e-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="7690e-114">Hallo java.exe pad toohello system omgeving variabele pad toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7690e-114">Add hello java.exe path toohello system environment variable path.</span></span> <span data-ttu-id="7690e-115">Zie voor configuratie-instructies [hoe instellen of wijzigen van de padvariabele system Hallo ik?]( https://www.java.com/download/help/path.xml).</span><span class="sxs-lookup"><span data-stu-id="7690e-115">For configuration instructions, see [How do I set or change hello Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="7690e-116">Hallo-pad is vergelijkbaar tooC:\Program Files\Java\jdk1.8.0_77\jre\bin.</span><span class="sxs-lookup"><span data-stu-id="7690e-116">hello path is similar tooC:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="7690e-117">[.NET core SDK 1.0.3 of .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="7690e-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="7690e-118">Linux (We raden u aan Ubuntu 14.04 TNS)</span><span class="sxs-lookup"><span data-stu-id="7690e-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="7690e-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="7690e-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="7690e-120">tooinstall Hallo code, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7690e-120">tooinstall hello code, enter hello following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="7690e-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span><span class="sxs-lookup"><span data-stu-id="7690e-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="7690e-122">tooupdate hello deb pakket bron, Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="7690e-122">tooupdate hello deb package source, enter hello following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="7690e-123">tooinstall Mono, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7690e-123">tooinstall Mono, enter hello following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="7690e-124">Mono 4.6 wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7690e-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="7690e-125">Versie 4.6 verwijderen volledig voordat u 4.2.x installeert.</span><span class="sxs-lookup"><span data-stu-id="7690e-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="7690e-126">[Java Runtime Environment voor SE versie 8 update 77 of hoger](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="7690e-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="7690e-127">Zie voor instructies voor installatie, Hallo [Linux 64-bits installatie-instructies voor Java]( https://java.com/en/download/help/linux_x64_install.xml) pagina.</span><span class="sxs-lookup"><span data-stu-id="7690e-127">For instructions on installation, see hello [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="7690e-128">[.NET core SDK 1.0.3 of .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="7690e-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="7690e-129">MacOS</span><span class="sxs-lookup"><span data-stu-id="7690e-129">MacOS</span></span>

    - <span data-ttu-id="7690e-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="7690e-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="7690e-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span><span class="sxs-lookup"><span data-stu-id="7690e-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="7690e-132">[Java Runtime Environment voor SE versie 8 update 77 of hoger](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="7690e-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="7690e-133">Zie voor instructies voor installatie, Hallo [Linux 64-bits installatie-instructies voor Java](https://java.com/en/download/help/mac_install.xml) pagina.</span><span class="sxs-lookup"><span data-stu-id="7690e-133">For instructions on installation, see hello [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="7690e-134">[.NET core SDK 1.0.3 of .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="7690e-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="7690e-135">Installeren van Data Lake Tools</span><span class="sxs-lookup"><span data-stu-id="7690e-135">Install Data Lake Tools</span></span>

<span data-ttu-id="7690e-136">Nadat u Hallo vereisten hebt geïnstalleerd, kunt u Data Lake Tools voor VS-Code installeren.</span><span class="sxs-lookup"><span data-stu-id="7690e-136">After you install hello prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="7690e-137">**tooinstall Data Lake Tools**</span><span class="sxs-lookup"><span data-stu-id="7690e-137">**tooinstall Data Lake Tools**</span></span>

1. <span data-ttu-id="7690e-138">Open Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7690e-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="7690e-139">Ctrl + P selecteren en voer vervolgens Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7690e-139">Select Ctrl+P, and then enter hello following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="7690e-140">Hier ziet u een lijst met Visual Studio code-uitbreidingen.</span><span class="sxs-lookup"><span data-stu-id="7690e-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="7690e-141">Een van beide is **Azure Data Lake Tools**.</span><span class="sxs-lookup"><span data-stu-id="7690e-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="7690e-142">Selecteer **installeren** volgende te**Azure Data Lake Tools**.</span><span class="sxs-lookup"><span data-stu-id="7690e-142">Select **Install** next too**Azure Data Lake Tools**.</span></span> <span data-ttu-id="7690e-143">Na enkele seconden Hallo **installeren** wijzigingen te knop**opnieuw laden**.</span><span class="sxs-lookup"><span data-stu-id="7690e-143">After a few seconds, hello **Install** button changes too**Reload**.</span></span>
4. <span data-ttu-id="7690e-144">Selecteer **opnieuw laden** tooactivate Hallo-extensie.</span><span class="sxs-lookup"><span data-stu-id="7690e-144">Select **Reload** tooactivate hello extension.</span></span>
5. <span data-ttu-id="7690e-145">Selecteer **OK** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="7690e-145">Select **OK** tooconfirm.</span></span> <span data-ttu-id="7690e-146">U kunt Azure Data Lake Tools zien in Hallo **extensies** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="7690e-146">You can see Azure Data Lake Tools in hello **Extensions** pane.</span></span>
    <span data-ttu-id="7690e-147">![Data Lake Tools voor Visual Studio Code Extensions deelvenster](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="7690e-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="7690e-148">Azure Data Lake Tools activeren</span><span class="sxs-lookup"><span data-stu-id="7690e-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="7690e-149">Maak een nieuw .usql-bestand of open een bestaande .usql tooactivate Hallo bestandsextensie.</span><span class="sxs-lookup"><span data-stu-id="7690e-149">Create a new .usql file or open an existing .usql file tooactivate hello extension.</span></span> 

## <a name="connect-tooazure"></a><span data-ttu-id="7690e-150">Verbinding maken met tooAzure</span><span class="sxs-lookup"><span data-stu-id="7690e-150">Connect tooAzure</span></span>

<span data-ttu-id="7690e-151">Voordat u kunt compileren en U-SQL-scripts in Data Lake Analytics uitvoeren, moet u verbinding maken met tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="7690e-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect tooyour Azure account.</span></span>

<span data-ttu-id="7690e-152">**tooconnect tooAzure**</span><span class="sxs-lookup"><span data-stu-id="7690e-152">**tooconnect tooAzure**</span></span>

1.  <span data-ttu-id="7690e-153">Selecteer Ctrl + Shift + P tooopen Hallo opdracht palet.</span><span class="sxs-lookup"><span data-stu-id="7690e-153">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2.  <span data-ttu-id="7690e-154">Voer **ADL: aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="7690e-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="7690e-155">Hallo-aanmeldingsgegevens wordt weergegeven in Hallo **uitvoer** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="7690e-155">hello login information appears in hello **Output** pane.</span></span>

    <span data-ttu-id="7690e-156">![Data Lake Tools voor Visual Studio Code opdracht palet](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Data Lake Tools voor Visual Studio Code aanmelding apparaatgegevens](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="7690e-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="7690e-157">Selecteer Ctrl + klikken op Hallo aanmeldings-URL: https://aka.ms/devicelogin tooopen Hallo aanmelding webpagina.</span><span class="sxs-lookup"><span data-stu-id="7690e-157">Select Ctrl+click on hello login URL: https://aka.ms/devicelogin tooopen hello login webpage.</span></span> <span data-ttu-id="7690e-158">Voer de code Hallo **G567LX42V** in het tekstvak Hallo en selecteer vervolgens **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="7690e-158">Enter hello code **G567LX42V** into hello text box, and then select **Continue**.</span></span>

   ![Data Lake Tools voor Visual Studio Code aanmelding plakken code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="7690e-160">Volg Hallo instructies toosign in van Hallo webpagina.</span><span class="sxs-lookup"><span data-stu-id="7690e-160">Follow hello instructions toosign in from hello webpage.</span></span> <span data-ttu-id="7690e-161">Wanneer u verbonden bent, de naam van uw Azure-account wordt weergegeven op de statusbalk Hallo in Hallo linkerbenedenhoek Hallo **tegenover Code** venster.</span><span class="sxs-lookup"><span data-stu-id="7690e-161">When you're connected, your Azure account name appears on hello status bar in hello lower-left corner of hello **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="7690e-162">Als uw account twee factoren is ingeschakeld heeft, wordt u aangeraden phone verificatie in plaats van met een PINCODE te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7690e-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="7690e-163">toosign, Voer Hallo opdracht **ADL: afmelding**.</span><span class="sxs-lookup"><span data-stu-id="7690e-163">toosign out, enter hello command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="7690e-164">Lijst van uw Data Lake Analytics-accounts</span><span class="sxs-lookup"><span data-stu-id="7690e-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="7690e-165">tootest hello verbinding get een lijst van uw Data Lake Analytics-accounts.</span><span class="sxs-lookup"><span data-stu-id="7690e-165">tootest hello connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="7690e-166">**toolist hello Data Lake Analytics-accounts onder uw Azure-abonnement**</span><span class="sxs-lookup"><span data-stu-id="7690e-166">**toolist hello Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="7690e-167">Selecteer Ctrl + Shift + P tooopen Hallo opdracht palet.</span><span class="sxs-lookup"><span data-stu-id="7690e-167">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="7690e-168">Voer **ADL: lijst van Accounts**.</span><span class="sxs-lookup"><span data-stu-id="7690e-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="7690e-169">Hallo-accounts worden weergegeven in Hallo **uitvoer** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="7690e-169">hello accounts appear in hello **Output** pane.</span></span>

## <a name="open-hello-sample-script"></a><span data-ttu-id="7690e-170">Open Hallo-voorbeeldscript</span><span class="sxs-lookup"><span data-stu-id="7690e-170">Open hello sample script</span></span>
<span data-ttu-id="7690e-171">Open Hallo opdracht palet (Ctrl + Shift + P) en voer de **ADL: Open voorbeeldscript**.</span><span class="sxs-lookup"><span data-stu-id="7690e-171">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="7690e-172">Hiermee opent u een ander exemplaar van dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7690e-172">This opens another instance of this sample.</span></span> <span data-ttu-id="7690e-173">U kunt bewerken, configureren en verzenden van script op basis van dit exemplaar.</span><span class="sxs-lookup"><span data-stu-id="7690e-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="7690e-174">Werken met U-SQL</span><span class="sxs-lookup"><span data-stu-id="7690e-174">Work with U-SQL</span></span>

<span data-ttu-id="7690e-175">U moet een U-SQL-bestand of een map toowork openen met U-SQL.</span><span class="sxs-lookup"><span data-stu-id="7690e-175">You need open either a U-SQL file or a folder toowork with U-SQL.</span></span>

<span data-ttu-id="7690e-176">**tooopen een map voor uw project U-SQL**</span><span class="sxs-lookup"><span data-stu-id="7690e-176">**tooopen a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="7690e-177">Selecteer in Visual Studio Code Hallo **bestand** menu en selecteer vervolgens **map openen**.</span><span class="sxs-lookup"><span data-stu-id="7690e-177">From Visual Studio Code, select hello **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="7690e-178">Geef een map op en selecteer vervolgens **map selecteren**.</span><span class="sxs-lookup"><span data-stu-id="7690e-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="7690e-179">Selecteer Hallo **bestand** menu en selecteer vervolgens **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="7690e-179">Select hello **File** menu, and then select **New**.</span></span> <span data-ttu-id="7690e-180">Een naamloos-1-bestand wordt toohello project toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7690e-180">An Untitled-1 file is added toohello project.</span></span>
4. <span data-ttu-id="7690e-181">Voer Hallo code in Hallo naamloos-1-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="7690e-181">Enter hello following code into hello Untitled-1 file:</span></span>

        @departments  = 
            SELECT * FROM 
                (VALUES
                    (31,    "Sales"),
                    (33,    "Engineering"), 
                    (34,    "Clerical"),
                    (35,    "Marketing")
                ) AS 
                      D( DepID, DepName );
         
        OUTPUT @departments
            TO “/Output/departments.csv”

    <span data-ttu-id="7690e-182">Hallo script maakt een bestand departments.csv met enkele gegevens die zijn opgenomen in Hallo/output-map.</span><span class="sxs-lookup"><span data-stu-id="7690e-182">hello script creates a departments.csv file with some data included in hello /output folder.</span></span>

5. <span data-ttu-id="7690e-183">Hallo bestand opslaan als **myUSQL.usql** in Hallo map geopend.</span><span class="sxs-lookup"><span data-stu-id="7690e-183">Save hello file as **myUSQL.usql** in hello opened folder.</span></span> <span data-ttu-id="7690e-184">Een configuratiebestand adltools_settings.json is ook toohello project toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7690e-184">A adltools_settings.json configuration file is also added toohello project.</span></span>
4. <span data-ttu-id="7690e-185">Open en adltools_settings.json configureren met Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="7690e-185">Open and configure adltools_settings.json with hello following properties:</span></span>

    - <span data-ttu-id="7690e-186">Account: Een Data Lake Analytics-account onder uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7690e-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="7690e-187">Database: Een database onder uw account.</span><span class="sxs-lookup"><span data-stu-id="7690e-187">Database: A database under your account.</span></span> <span data-ttu-id="7690e-188">Hallo standaardwaarde is **master**.</span><span class="sxs-lookup"><span data-stu-id="7690e-188">hello default is **master**.</span></span>
    - <span data-ttu-id="7690e-189">Schema: Een schema op uw database.</span><span class="sxs-lookup"><span data-stu-id="7690e-189">Schema: A schema under your database.</span></span> <span data-ttu-id="7690e-190">Hallo standaardwaarde is **dbo**.</span><span class="sxs-lookup"><span data-stu-id="7690e-190">hello default is **dbo**.</span></span>
    - <span data-ttu-id="7690e-191">Optionele instellingen:</span><span class="sxs-lookup"><span data-stu-id="7690e-191">Optional settings:</span></span>
        - <span data-ttu-id="7690e-192">Prioriteit: Hallo prioriteitsbereik is 1 too1000 met 1 Hallo hoogste prioriteit.</span><span class="sxs-lookup"><span data-stu-id="7690e-192">Priority: hello priority range is from 1 too1000 with 1 as hello highest priority.</span></span> <span data-ttu-id="7690e-193">de standaardwaarde Hallo is **1000**.</span><span class="sxs-lookup"><span data-stu-id="7690e-193">hello default value is **1000**.</span></span>
        - <span data-ttu-id="7690e-194">Parallelle uitvoering: Hallo parallelle uitvoering bereik is 1 too150.</span><span class="sxs-lookup"><span data-stu-id="7690e-194">Parallelism: hello parallelism range is from 1 too150.</span></span> <span data-ttu-id="7690e-195">de standaardwaarde Hallo is Hallo maximale parallelle uitvoering toegestaan in uw Azure Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="7690e-195">hello default value is hello maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="7690e-196">Als Hallo-instellingen ongeldige zijn, worden Hallo standaardwaarden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7690e-196">If hello settings are invalid, hello default values are used.</span></span>

    ![Data Lake Tools voor Visual Studio Code-configuratiebestand](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="7690e-198">Een compute Data Lake Analytics-account is nodig toocompile en voer U-SQL-taken.</span><span class="sxs-lookup"><span data-stu-id="7690e-198">A compute Data Lake Analytics account is needed toocompile and run U-SQL jobs.</span></span> <span data-ttu-id="7690e-199">Voordat u deze kunt compileren en U-SQL-taken uitvoeren, moet u de computeraccount Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="7690e-199">You must configure hello computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="7690e-200">Nadat het Hallo-configuratie is opgeslagen, wordt op Hallo statusbalk Hallo linkerbenedenhoek van het bijbehorende .usql bestand Hallo Hallo-account, database en schema-informatie weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7690e-200">After hello configuration is saved, hello account, database, and schema information appears on hello status bar at hello bottom-left corner of hello corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="7690e-201">Vergeleken tooopening een bestand, wanneer u een map die u kunt openen:</span><span class="sxs-lookup"><span data-stu-id="7690e-201">Compared tooopening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="7690e-202">Gebruik een code-behind-bestand.</span><span class="sxs-lookup"><span data-stu-id="7690e-202">Use a code-behind file.</span></span> <span data-ttu-id="7690e-203">Code-behind wordt niet ondersteund in de modus Hallo één bestand.</span><span class="sxs-lookup"><span data-stu-id="7690e-203">In hello single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="7690e-204">Gebruik een configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="7690e-204">Use a configuration file.</span></span> <span data-ttu-id="7690e-205">Wanneer u een map opent, delen Hallo-scripts in Hallo werkdirectory een enkel configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="7690e-205">When you open a folder, hello scripts in hello working folder share a single configuration file.</span></span>


<span data-ttu-id="7690e-206">Hallo U-SQL-script wordt gecompileerd op afstand via Hallo Data Lake Analytics-service.</span><span class="sxs-lookup"><span data-stu-id="7690e-206">hello U-SQL script compiles remotely through hello Data Lake Analytics service.</span></span> <span data-ttu-id="7690e-207">Wanneer u de opdracht Hallo **compileren** opdracht Hallo U-SQL-script tooyour Data Lake Analytics-account wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="7690e-207">When you issue hello **compile** command, hello U-SQL script is sent tooyour Data Lake Analytics account.</span></span> <span data-ttu-id="7690e-208">Visual Studio Code ontvangt later Hallo compilatieresultaat.</span><span class="sxs-lookup"><span data-stu-id="7690e-208">Later, Visual Studio Code receives hello compilation result.</span></span> <span data-ttu-id="7690e-209">Vervaldatum toohello externe compilatie vereist Visual Studio Code dat u gegevens weer te geven Hallo tooconnect tooyour Data Lake Analytics-account in het Hallo-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="7690e-209">Due toohello remote compilation, Visual Studio Code requires that you list hello information tooconnect tooyour Data Lake Analytics account in hello configuration file.</span></span>

<span data-ttu-id="7690e-210">**toocompile een U-SQL-script**</span><span class="sxs-lookup"><span data-stu-id="7690e-210">**toocompile a U-SQL script**</span></span>

1. <span data-ttu-id="7690e-211">Selecteer Ctrl + Shift + P tooopen Hallo opdracht palet.</span><span class="sxs-lookup"><span data-stu-id="7690e-211">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="7690e-212">Voer **ADL: compileren van Script**.</span><span class="sxs-lookup"><span data-stu-id="7690e-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="7690e-213">Hallo compileren resultaten worden weergegeven in Hallo **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="7690e-213">hello compile results appear in hello **Output** window.</span></span> <span data-ttu-id="7690e-214">U kunt ook met de rechtermuisknop op een scriptbestand en selecteer vervolgens **ADL: compileren Script** toocompile een U-SQL-taak.</span><span class="sxs-lookup"><span data-stu-id="7690e-214">You can also right-click a script file, and then select **ADL: Compile Script** toocompile a U-SQL job.</span></span> <span data-ttu-id="7690e-215">Hallo compilatieresultaat wordt weergegeven in Hallo **uitvoer** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="7690e-215">hello compilation result appears in hello **Output** pane.</span></span>
 

<span data-ttu-id="7690e-216">**toosubmit een U-SQL-script**</span><span class="sxs-lookup"><span data-stu-id="7690e-216">**toosubmit a U-SQL script**</span></span>

1. <span data-ttu-id="7690e-217">Selecteer Ctrl + Shift + P tooopen Hallo opdracht palet.</span><span class="sxs-lookup"><span data-stu-id="7690e-217">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="7690e-218">Voer **ADL: verzenden van taak**.</span><span class="sxs-lookup"><span data-stu-id="7690e-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="7690e-219">U kunt ook met de rechtermuisknop op een scriptbestand en selecteer vervolgens **ADL: Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="7690e-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="7690e-220">Nadat u een U-SQL-taak hebt ingediend, Hallo verzending van Logboeken worden weergegeven in Hallo **uitvoer** venster in VS-Code.</span><span class="sxs-lookup"><span data-stu-id="7690e-220">After you submit a U-SQL job, hello submission logs appear in hello **Output** window in VS Code.</span></span> <span data-ttu-id="7690e-221">Hallo taak URL wordt ook weergegeven als Hallo verzending geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="7690e-221">If hello submission is successful, hello job URL appears as well.</span></span> <span data-ttu-id="7690e-222">U kunt Hallo taak URL openen in een web browser tootrack Hallo realtime taakstatus.</span><span class="sxs-lookup"><span data-stu-id="7690e-222">You can open hello job URL in a web browser tootrack hello real-time job status.</span></span>

<span data-ttu-id="7690e-223">tooenable hello uitvoer van de taakdetails hello, stel **jobInformationOutputPath** in Hallo **tegenover code voor u Hallo-sql_settings.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="7690e-223">tooenable hello output of hello job details, set **jobInformationOutputPath** in hello **vs code for hello u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="7690e-224">Een code-behind-bestand gebruiken</span><span class="sxs-lookup"><span data-stu-id="7690e-224">Use a code-behind file</span></span>

<span data-ttu-id="7690e-225">Een code-behind-bestand is een C#-bestanden die zijn gekoppeld aan een enkel U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="7690e-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="7690e-226">U kunt een specifiek script tooUDO, UDA, UDT en UDF definiëren in Hallo code-behind-bestand.</span><span class="sxs-lookup"><span data-stu-id="7690e-226">You can define a script dedicated tooUDO, UDA, UDT, and UDF in hello code-behind file.</span></span> <span data-ttu-id="7690e-227">Hallo kunnen UDO, UDA, UDT en UDF worden gebruikt rechtstreeks in Hallo script zonder Hallo assembly eerst registreren.</span><span class="sxs-lookup"><span data-stu-id="7690e-227">hello UDO, UDA, UDT, and UDF can be used directly in hello script without registering hello assembly first.</span></span> <span data-ttu-id="7690e-228">Hallo code-behind-bestand wordt geplaatst in Hallo dezelfde map als de peering U-SQL-scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="7690e-228">hello code-behind file is put in hello same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="7690e-229">Hallo script heet xxx.usql, heet Hallo code-behind als xxx.usql.cs.</span><span class="sxs-lookup"><span data-stu-id="7690e-229">If hello script is named xxx.usql, hello code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="7690e-230">Als u Hallo code-behind-bestand voor het handmatig verwijdert, worden Hallo code-behind functie is uitgeschakeld voor de bijbehorende U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="7690e-230">If you manually delete hello code-behind file, hello code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="7690e-231">Zie voor meer informatie over het schrijven van code voor de U-SQL-script klant [schrijven en met behulp van aangepaste Code in de U-SQL: door de gebruiker gedefinieerde functies]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span><span class="sxs-lookup"><span data-stu-id="7690e-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="7690e-232">toosupport code-behind, moet u een werkmap openen.</span><span class="sxs-lookup"><span data-stu-id="7690e-232">toosupport code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="7690e-233">**toogenerate een code-behind-bestand**</span><span class="sxs-lookup"><span data-stu-id="7690e-233">**toogenerate a code-behind file**</span></span>

1. <span data-ttu-id="7690e-234">Open een bronbestand.</span><span class="sxs-lookup"><span data-stu-id="7690e-234">Open a source file.</span></span> 
2. <span data-ttu-id="7690e-235">Selecteer Ctrl + Shift + P tooopen Hallo opdracht palet.</span><span class="sxs-lookup"><span data-stu-id="7690e-235">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
3. <span data-ttu-id="7690e-236">Voer **ADL: genereren van Code achter**.</span><span class="sxs-lookup"><span data-stu-id="7690e-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="7690e-237">Een code-behind-bestand wordt gemaakt in Hallo dezelfde map.</span><span class="sxs-lookup"><span data-stu-id="7690e-237">A code-behind file is created in hello same folder.</span></span> 

<span data-ttu-id="7690e-238">U kunt ook met de rechtermuisknop op een scriptbestand en selecteer vervolgens **ADL: Code genereren achter**.</span><span class="sxs-lookup"><span data-stu-id="7690e-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="7690e-239">toocompile en het verzenden van een U-SQL-script met een code-behind-bestand is hetzelfde als het script bestand met de Hallo zelfstandige U-SQL Hallo.</span><span class="sxs-lookup"><span data-stu-id="7690e-239">toocompile and submit a U-SQL script with a code-behind file is hello same as with hello standalone U-SQL script file.</span></span>

<span data-ttu-id="7690e-240">Hallo na twee schermafbeeldingen weergeven een code-behind-bestand en het bijbehorende bestand van de U-SQL-script:</span><span class="sxs-lookup"><span data-stu-id="7690e-240">hello following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Data Lake Tools voor Visual Studio Code code-behind](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Data Lake Tools voor Visual Studio Code code-behind scriptbestand](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="7690e-243">Assembly's gebruiken</span><span class="sxs-lookup"><span data-stu-id="7690e-243">Use assemblies</span></span>

<span data-ttu-id="7690e-244">Zie voor meer informatie over het ontwikkelen van assembly's [ontwikkelen van U-SQL-assembly's voor Azure Data Lake Analytics-taken](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="7690e-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="7690e-245">U kunt Data Lake Tools tooregister aangepaste code assembly's in Hallo Data Lake Analytics-catalogus.</span><span class="sxs-lookup"><span data-stu-id="7690e-245">You can use Data Lake Tools tooregister custom code assemblies in hello Data Lake Analytics catalog.</span></span>

<span data-ttu-id="7690e-246">**tooregister een assembly**</span><span class="sxs-lookup"><span data-stu-id="7690e-246">**tooregister an assembly**</span></span>

<span data-ttu-id="7690e-247">U kunt registreren assembly via Hallo Hallo **ADL: registreren Assembly** of **ADL: Assembly registreren via configuratie** opdrachten.</span><span class="sxs-lookup"><span data-stu-id="7690e-247">You can register hello assembly through hello **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="7690e-248">**tooregister via Hallo ADL: registreren Assembly-opdracht**</span><span class="sxs-lookup"><span data-stu-id="7690e-248">**tooregister through hello ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="7690e-249">Selecteer Ctrl + Shift + P tooopen Hallo opdracht palet.</span><span class="sxs-lookup"><span data-stu-id="7690e-249">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="7690e-250">Voer **ADL: Assembly registreren**.</span><span class="sxs-lookup"><span data-stu-id="7690e-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="7690e-251">Hallo lokale assembly-pad opgeven.</span><span class="sxs-lookup"><span data-stu-id="7690e-251">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="7690e-252">Selecteer een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="7690e-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="7690e-253">Selecteer een database.</span><span class="sxs-lookup"><span data-stu-id="7690e-253">Select a database.</span></span>

<span data-ttu-id="7690e-254">Resultaten: Hallo portal wordt geopend in een browser en Hallo assembly registratieproces wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7690e-254">Results: hello portal is opened in a browser and displays hello assembly registration process.</span></span>  

<span data-ttu-id="7690e-255">Een andere handige manier tootrigger hello **ADL: registreren Assembly** opdracht is tooright en klik op Hallo dll-bestand in Verkenner.</span><span class="sxs-lookup"><span data-stu-id="7690e-255">Another convenient way tootrigger hello **ADL: Register Assembly** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="7690e-256">**tooregister Hallo echter ADL: Assembly registreren via de opdracht configuratie**</span><span class="sxs-lookup"><span data-stu-id="7690e-256">**tooregister though hello ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="7690e-257">Selecteer Ctrl + Shift + P tooopen Hallo opdracht palet.</span><span class="sxs-lookup"><span data-stu-id="7690e-257">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="7690e-258">Voer **ADL: Assembly via configuratie registreren**.</span><span class="sxs-lookup"><span data-stu-id="7690e-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="7690e-259">Hallo lokale assembly-pad opgeven.</span><span class="sxs-lookup"><span data-stu-id="7690e-259">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="7690e-260">Hallo JSON-bestand wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7690e-260">hello JSON file is displayed.</span></span> <span data-ttu-id="7690e-261">Bekijk en bewerk Hallo assembly-afhankelijkheden en Resourceparameters, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="7690e-261">Review and edit hello assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="7690e-262">Instructies worden weergegeven in Hallo **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="7690e-262">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="7690e-263">tooproceed toohello assembly-registratie, sla Hallo JSON-bestand (Ctrl + S).</span><span class="sxs-lookup"><span data-stu-id="7690e-263">tooproceed toohello assembly registration, save (Ctrl+S) hello JSON file.</span></span>

![Data Lake Tools voor Visual Studio Code code-behind](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="7690e-265">Assembly-afhankelijkheden: een Azure Data Lake Tools of Hallo DLL eventuele afhankelijkheden heeft.</span><span class="sxs-lookup"><span data-stu-id="7690e-265">Assembly dependencies: Azure Data Lake Tools autodetects whether hello DLL has any dependencies.</span></span> <span data-ttu-id="7690e-266">Hallo afhankelijkheden worden weergegeven in de JSON-bestand Hallo nadat ze zijn gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="7690e-266">hello dependencies are displayed in hello JSON file after they are detected.</span></span> 
>- <span data-ttu-id="7690e-267">Resources: U kunt uw resources dll-bestand (bijvoorbeeld, txt, PNG en CSV) als onderdeel van de registratie van assembly Hallo uploaden.</span><span class="sxs-lookup"><span data-stu-id="7690e-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of hello assembly registration.</span></span> 

<span data-ttu-id="7690e-268">Een andere manier tootrigger hello **ADL: Assembly registreren via configuratie** opdracht is tooright en klik op Hallo dll-bestand in Verkenner.</span><span class="sxs-lookup"><span data-stu-id="7690e-268">Another way tootrigger hello **ADL: Register Assembly through Configuration** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="7690e-269">Hallo volgende U-SQL-code laat zien hoe toocall een assembly.</span><span class="sxs-lookup"><span data-stu-id="7690e-269">hello following U-SQL code demonstrates how toocall an assembly.</span></span> <span data-ttu-id="7690e-270">In voorbeeld Hallo Hallo assembly-naam is *testen*.</span><span class="sxs-lookup"><span data-stu-id="7690e-270">In hello sample, hello assembly name is *test*.</span></span>

```
REFERENCE ASSEMBLY [test];

@a = 
    EXTRACT 
        Iid int,
    Starts DateTime,
    Region string,
    Query string,
    DwellTime int,
    Results string,
    ClickedUrls string 
    FROM @"Sample/SearchLog.txt" 
    USING Extractors.Tsv();

@d =
    SELECT DISTINCT Region 
    FROM @a;

@d1 = 
    PROCESS @d
    PRODUCE 
        Region string,
    Mkt string
    USING new USQLApplication_codebehind.MyProcessor();

OUTPUT @d1 
    too@"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-hello-data-lake-analytics-catalog"></a><span data-ttu-id="7690e-271">Toegang tot Hallo Data Lake Analytics-catalogus</span><span class="sxs-lookup"><span data-stu-id="7690e-271">Access hello Data Lake Analytics catalog</span></span>

<span data-ttu-id="7690e-272">Wanneer u tooAzure hebt gekoppeld, kunt u Hallo stappen tooaccess Hallo U-SQL-catalogus te volgen.</span><span class="sxs-lookup"><span data-stu-id="7690e-272">After you have connected tooAzure, you can use hello following steps tooaccess hello U-SQL catalog.</span></span>

<span data-ttu-id="7690e-273">**tooaccess hello Azure Data Lake Analytics-metagegevens**</span><span class="sxs-lookup"><span data-stu-id="7690e-273">**tooaccess hello Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="7690e-274">Ctrl + Shift + P selecteren en voer vervolgens **ADL: lijst met tabellen**.</span><span class="sxs-lookup"><span data-stu-id="7690e-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="7690e-275">Selecteer een van de Hallo Data Lake Analytics-accounts.</span><span class="sxs-lookup"><span data-stu-id="7690e-275">Select one of hello Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="7690e-276">Selecteer een van de Hallo Data Lake Analytics-databases.</span><span class="sxs-lookup"><span data-stu-id="7690e-276">Select one of hello Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="7690e-277">Selecteer een van de Hallo schema's.</span><span class="sxs-lookup"><span data-stu-id="7690e-277">Select one of hello schemas.</span></span> <span data-ttu-id="7690e-278">Hier ziet u Hallo lijst met tabellen.</span><span class="sxs-lookup"><span data-stu-id="7690e-278">You can see hello list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="7690e-279">Weergave Data Lake Analytics-taken</span><span class="sxs-lookup"><span data-stu-id="7690e-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="7690e-280">**tooview Data Lake Analytics-taken**</span><span class="sxs-lookup"><span data-stu-id="7690e-280">**tooview Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="7690e-281">Open Hallo opdracht palet (Ctrl + Shift + P) en selecteer **ADL: taak weergeven**.</span><span class="sxs-lookup"><span data-stu-id="7690e-281">Open hello command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="7690e-282">Selecteer een Data Lake Analytics of lokale account.</span><span class="sxs-lookup"><span data-stu-id="7690e-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="7690e-283">Wacht totdat de lijst met de Hallo taken voor Hallo account tooappear.</span><span class="sxs-lookup"><span data-stu-id="7690e-283">Wait for hello jobs list for hello account tooappear.</span></span>
4.  <span data-ttu-id="7690e-284">Selecteer een taak in de lijst om de taak, Data Lake Tools taakdetails Hallo in hello Azure-portal wordt geopend en toont Hallo Taakinfo-bestand in VS-Code.</span><span class="sxs-lookup"><span data-stu-id="7690e-284">Select a job from job list, Data Lake Tools opens hello job details in hello Azure portal and displays hello JobInfo file in VS Code.</span></span>

![Data Lake Tools voor Visual Studio Code IntelliSense objecttypen](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="7690e-286">Azure Data Lake Storage-integratie</span><span class="sxs-lookup"><span data-stu-id="7690e-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="7690e-287">U kunt Azure Data Lake Storage-gerelateerde opdrachten te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7690e-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="7690e-288">Blader door hello Azure Data Lake Storage-resources.</span><span class="sxs-lookup"><span data-stu-id="7690e-288">Browse through hello Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="7690e-289">Preview hello Azure Data Lake Storage-bestand.</span><span class="sxs-lookup"><span data-stu-id="7690e-289">Preview hello Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="7690e-290">Hallo uploaden bestand rechtstreeks tooAzure Data Lake Storage in VS-Code.</span><span class="sxs-lookup"><span data-stu-id="7690e-290">Upload hello file directly tooAzure Data Lake Storage in VS Code.</span></span> 

### <a name="list-hello-storage-path"></a><span data-ttu-id="7690e-291">Lijst Hallo opslagpad</span><span class="sxs-lookup"><span data-stu-id="7690e-291">List hello storage path</span></span> 
<span data-ttu-id="7690e-292">Hallo opslagpad via Hallo opdracht palet of met de rechtermuisknop klikt, kunt u weergeven.</span><span class="sxs-lookup"><span data-stu-id="7690e-292">You can list hello storage path through hello command palette or through right-click.</span></span>

<span data-ttu-id="7690e-293">**toolist hello opslagpad via Hallo opdracht palet**</span><span class="sxs-lookup"><span data-stu-id="7690e-293">**toolist hello storage path through hello command palette**</span></span>

1.  <span data-ttu-id="7690e-294">Open Hallo opdracht palet (Ctrl + Shift + P) en voer de **ADL: lijst opslagpad**.</span><span class="sxs-lookup"><span data-stu-id="7690e-294">Open hello command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Data Lake Tools voor Visual Studio Code lijst opslagpad](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="7690e-296">Selecteer uw favoriete methode voor het Hallo-opslagpad aanbieden.</span><span class="sxs-lookup"><span data-stu-id="7690e-296">Select your preferred way for listing hello storage path.</span></span> <span data-ttu-id="7690e-297">Maakt gebruik van deze overgang **Geef een pad** als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7690e-297">This passage uses **Enter a path** as an example.</span></span>

    ![Data Lake Tools voor Visual Studio Code eenrichtingssessie toolist Hallo opslagpad](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="7690e-299">VS-Code, blijft Hallo laatst bezochte pad in elke Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="7690e-299">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="7690e-300">Bijvoorbeeld: ss tt /.</span><span class="sxs-lookup"><span data-stu-id="7690e-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="7690e-301">Hoofdpad naar browser: pad naar de hoofdmap Hallo lijst van de geselecteerde Data Lake Analytics-account of een lokaal pad.</span><span class="sxs-lookup"><span data-stu-id="7690e-301">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="7690e-302">Geef een pad op: een opgegeven pad van de geselecteerde Data Lake Analytics-account of een lokaal pad.</span><span class="sxs-lookup"><span data-stu-id="7690e-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="7690e-303">Selecteer een account in Hallo lokaal pad of een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="7690e-303">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Data Lake Tools voor Visual Studio Code selecteren meer](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="7690e-305">Selecteer **meer** toolist meer Data Lake Analytics-accounts en selecteer vervolgens een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="7690e-305">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Data Lake Tools voor Visual Studio Code selecteren een account](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="7690e-307">Geef het pad van een Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="7690e-307">Enter an Azure storage path.</span></span> <span data-ttu-id="7690e-308">Bijvoorbeeld: / uitvoer.</span><span class="sxs-lookup"><span data-stu-id="7690e-308">For example, /output.</span></span>

    ![Data Lake Tools voor Visual Studio Code invoeren opslagpad](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="7690e-310">Resultaten: Hallo opdracht palet bevat Hallo padinformatie op basis van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="7690e-310">Results: hello command palette lists hello path information based on your entries.</span></span>

    ![Data Lake Tools voor Visual Studio Code weergeven opslag pad resultaten](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="7690e-312">Een handige methode toolist Hallo relatief pad wordt via Hallo met de rechtermuisknop op contextmenu.</span><span class="sxs-lookup"><span data-stu-id="7690e-312">A more convenient way toolist hello relative path is through hello right-click context menu.</span></span>

<span data-ttu-id="7690e-313">**toolist hello opslagpad via met de rechtermuisknop op**</span><span class="sxs-lookup"><span data-stu-id="7690e-313">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="7690e-314">Met de rechtermuisknop op Hallo pad tekenreeks tooselect **lijst opslagpad**.</span><span class="sxs-lookup"><span data-stu-id="7690e-314">Right-click hello path string tooselect **List Storage Path**.</span></span>

       ![Data Lake Tools voor Visual Studio Code met de rechtermuisknop op contextmenu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="7690e-316">Hallo geselecteerde relatief pad wordt weergegeven in Hallo opdracht palet.</span><span class="sxs-lookup"><span data-stu-id="7690e-316">hello selected relative path appears in hello command palette.</span></span>

   ![Data Lake Tools voor Visual Studio Code relatief pad zijn geselecteerd](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="7690e-318">Selecteer een account in Hallo lokaal pad of een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="7690e-318">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools voor Visual Studio Code selecteren een account](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="7690e-320">Resultaten: Hallo opdracht palet bevat Hallo mappen en bestanden voor de huidige pad Hallo.</span><span class="sxs-lookup"><span data-stu-id="7690e-320">Results: hello command palette lists hello folders and files for hello current path.</span></span>

       ![Data Lake Tools voor Visual Studio Code lijst van de huidige pad Hallo](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a><span data-ttu-id="7690e-322">Hallo-opslagbestand Preview</span><span class="sxs-lookup"><span data-stu-id="7690e-322">Preview hello storage file</span></span>
<span data-ttu-id="7690e-323">Hallo opslagbestand via Hallo opdracht palet of met de rechtermuisknop klikt, kunt u bekijken.</span><span class="sxs-lookup"><span data-stu-id="7690e-323">You can preview hello storage file through hello command palette or through right-click.</span></span>

<span data-ttu-id="7690e-324">**toopreview hello opslagbestand via Hallo opdracht palet**</span><span class="sxs-lookup"><span data-stu-id="7690e-324">**toopreview hello storage file through hello command palette**</span></span>

1.  <span data-ttu-id="7690e-325">Open Hallo opdracht palet (Ctrl + Shift + P) en voer de **ADL: Preview opslagbestand**.</span><span class="sxs-lookup"><span data-stu-id="7690e-325">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Data Lake Tools voor Visual Studio Code preview opslagbestand](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="7690e-327">Selecteer een account in Hallo lokaal pad of een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="7690e-327">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools voor Visual Studio Code lijst account](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="7690e-329">Selecteer **meer** toolist meer Data Lake Analytics-accounts en selecteer vervolgens een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="7690e-329">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Data Lake Tools voor Visual Studio Code selecteren een account](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="7690e-331">Voer een pad van de Azure-opslag of het bestand.</span><span class="sxs-lookup"><span data-stu-id="7690e-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="7690e-332">Bijvoorbeeld: /output/SearchLog.txt.</span><span class="sxs-lookup"><span data-stu-id="7690e-332">For example, /output/SearchLog.txt.</span></span>

       ![Data Lake Tools voor Visual Studio Code invoeren opslagpad en bestandsnaam](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="7690e-334">Resultaten: Hallo opdracht palet bevat Hallo padinformatie op basis van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="7690e-334">Results: hello command palette lists hello path information based on your entries.</span></span>

       ![Data Lake Tools voor Visual Studio Code voorbeeld bestandsresultaat](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="7690e-336">**toolist hello opslagpad via met de rechtermuisknop op**</span><span class="sxs-lookup"><span data-stu-id="7690e-336">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="7690e-337">toopreview een bestand met de rechtermuisknop op Hallo bestandspad.</span><span class="sxs-lookup"><span data-stu-id="7690e-337">toopreview a file, right-click hello file path.</span></span>

   ![Data Lake Tools voor Visual Studio Code met de rechtermuisknop op contextmenu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="7690e-339">Selecteer een account in Hallo lokaal pad of een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="7690e-339">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools voor Visual Studio Code selecteren een account](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="7690e-341">Resultaten: VS-Code weergegeven Hallo voorbeeldresultaten van Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="7690e-341">Results: VS Code displays hello preview results of hello file.</span></span>

       ![Data Lake Tools voor Visual Studio Code voorbeeld bestandsresultaat](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="7690e-343">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="7690e-343">Upload a file</span></span> 

<span data-ttu-id="7690e-344">U kunt bestanden uploaden door te voeren Hallo opdrachten **ADL: uploaden** of **ADL:-bestand uploaden via configuratie**.</span><span class="sxs-lookup"><span data-stu-id="7690e-344">You can upload files by entering hello commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="7690e-345">**tooupload bestanden echter Hallo ADL: de opdracht-bestand uploaden**</span><span class="sxs-lookup"><span data-stu-id="7690e-345">**tooupload files though hello ADL: Upload File command**</span></span>
1. <span data-ttu-id="7690e-346">Ctrl + Shift + P tooopen Hallo opdracht palet selecteren of met de rechtermuisknop op Hallo scripteditor en voer vervolgens **-bestand uploaden**.</span><span class="sxs-lookup"><span data-stu-id="7690e-346">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="7690e-347">Hallo tooupload bestand, voert u een lokaal pad.</span><span class="sxs-lookup"><span data-stu-id="7690e-347">tooupload hello file, enter a local path.</span></span>

    ![Data Lake Tools voor Visual Studio Code opgeven lokaal pad](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="7690e-349">Selecteer een van de aanbieding Hallo opslagpad Hallo manieren.</span><span class="sxs-lookup"><span data-stu-id="7690e-349">Select one of hello ways of listing hello storage path.</span></span> <span data-ttu-id="7690e-350">Maakt gebruik van deze overgang **Geef een pad** als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7690e-350">This passage uses **Enter a path** as an example.</span></span>

    ![Data Lake Tools voor Visual Studio Code lijst opslagpad](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="7690e-352">VS-Code, blijft Hallo laatst bezochte pad in elke Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="7690e-352">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="7690e-353">Bijvoorbeeld: ss tt /.</span><span class="sxs-lookup"><span data-stu-id="7690e-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="7690e-354">Hoofdpad naar browser: pad naar de hoofdmap Hallo lijst van de geselecteerde Data Lake Analytics-account of een lokaal pad.</span><span class="sxs-lookup"><span data-stu-id="7690e-354">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="7690e-355">Geef een pad op: een opgegeven pad van de geselecteerde Data Lake Analytics-account of een lokaal pad.</span><span class="sxs-lookup"><span data-stu-id="7690e-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="7690e-356">Selecteer een account in Hallo lokaal pad of een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="7690e-356">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Data Lake Tools voor Visual Studio Code met de rechtermuisknop op de opslag](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="7690e-358">Geef het pad van een Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="7690e-358">Enter an Azure storage path.</span></span> <span data-ttu-id="7690e-359">Bijvoorbeeld: / uitvoer.</span><span class="sxs-lookup"><span data-stu-id="7690e-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="7690e-360">Uw Azure-opslag-pad vinden.</span><span class="sxs-lookup"><span data-stu-id="7690e-360">Find your Azure storage path.</span></span> <span data-ttu-id="7690e-361">Selecteer **de huidige map kiezen**.</span><span class="sxs-lookup"><span data-stu-id="7690e-361">Select **Choose current folder**.</span></span>

    ![Selecteer een map van Data Lake Tools voor Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="7690e-363">Resultaten: Hallo **uitvoer** venster Hallo-bestand Uploadstatus wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7690e-363">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Data Lake Tools voor Visual Studio Code Uploadstatus](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="7690e-365">**Hoewel Hallo ADL tooupload bestanden: configuratie opdracht-bestand uploaden**</span><span class="sxs-lookup"><span data-stu-id="7690e-365">**tooupload files though hello ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="7690e-366">Ctrl + Shift + P tooopen Hallo opdracht palet selecteren of met de rechtermuisknop op Hallo scripteditor en voer vervolgens **-bestand uploaden via configuratie**.</span><span class="sxs-lookup"><span data-stu-id="7690e-366">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="7690e-367">VS-Code wordt een JSON-bestand weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7690e-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="7690e-368">U kunt invoeren bestandspaden en meerdere bestanden op Hallo uploaden hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="7690e-368">You can enter file paths and upload multiple files at hello same time.</span></span> <span data-ttu-id="7690e-369">Instructies worden weergegeven in Hallo **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="7690e-369">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="7690e-370">tooproceed tooupload Hallo-bestand, sla Hallo JSON-bestand (Ctrl + S).</span><span class="sxs-lookup"><span data-stu-id="7690e-370">tooproceed tooupload hello file, save (Ctrl+S) hello JSON file.</span></span>

       ![Data Lake Tools voor Visual Studio Code bestandspad](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="7690e-372">Resultaten: Hallo **uitvoer** venster Hallo-bestand Uploadstatus wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7690e-372">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Data Lake Tools voor Visual Studio Code Uploadstatus](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="7690e-374">Een andere manier tooupload een bestand toostorage via Hallo is met de rechtermuisknop te klikken op het volledige pad van het bestand Hallo of relatief pad in de script-editor Hallo Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="7690e-374">Another way tooupload a file toostorage is through hello right-click menu on hello file's full path or hello file's relative path in hello script editor.</span></span> <span data-ttu-id="7690e-375">Geef het lokale bestandspad Hallo en selecteer vervolgens Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="7690e-375">Enter hello local file path, and then select hello account.</span></span> <span data-ttu-id="7690e-376">Hallo **uitvoer** venster Hallo Uploadstatus weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7690e-376">hello **Output** window displays hello upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="7690e-377">Open Azure Opslagverkenner</span><span class="sxs-lookup"><span data-stu-id="7690e-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="7690e-378">U kunt openen **Azure Opslagverkenner** door te voeren opdracht Hallo **ADL: Open Web Azure Storage Explorer** of door deze te selecteren in de context contextmenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="7690e-378">You can open **Azure Storage Explorer** by entering hello command **ADL: Open Web Azure Storage Explorer** or by selecting it from hello right-click context menu.</span></span>

<span data-ttu-id="7690e-379">**tooopen Azure Opslagverkenner**</span><span class="sxs-lookup"><span data-stu-id="7690e-379">**tooopen Azure Storage Explorer**</span></span>

1. <span data-ttu-id="7690e-380">Selecteer Ctrl + Shift + P tooopen Hallo opdracht palet.</span><span class="sxs-lookup"><span data-stu-id="7690e-380">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="7690e-381">Voer **Open Web Azure Storage Explorer** of met de rechtermuisknop op een relatief pad of een volledig pad in de script-editor Hallo Hallo en selecteer vervolgens **Open Web Azure Storage Explorer**.</span><span class="sxs-lookup"><span data-stu-id="7690e-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or hello full path in hello script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="7690e-382">Selecteer een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="7690e-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="7690e-383">Data Lake Tools geopend hello Azure opslagpad in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7690e-383">Data Lake Tools opens hello Azure storage path in hello Azure portal.</span></span> <span data-ttu-id="7690e-384">Pad en de preview-Hallo bestand Hallo van Hallo web, kunt u vinden.</span><span class="sxs-lookup"><span data-stu-id="7690e-384">You can find hello path and preview hello file from hello web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="7690e-385">Lokaal uitvoeren en lokaal fouten opsporen voor Windows gebruikers</span><span class="sxs-lookup"><span data-stu-id="7690e-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="7690e-386">U-SQL lokaal uitvoeren Test uw lokale gegevens en uw script lokaal, valideert voordat je code gepubliceerde tooData Lake Analytics is.</span><span class="sxs-lookup"><span data-stu-id="7690e-386">U-SQL local run tests your local data and validates your script locally, before your code is published tooData Lake Analytics.</span></span> <span data-ttu-id="7690e-387">Hallo lokale foutopsporing met het onderdeel kunt u toocomplete Hallo taken te volgen voordat uw code is tooData Lake Analytics verzonden:</span><span class="sxs-lookup"><span data-stu-id="7690e-387">hello local debug feature enables you toocomplete hello following tasks before your code is submitted tooData Lake Analytics:</span></span> 
- <span data-ttu-id="7690e-388">Uw C# code-behind voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="7690e-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="7690e-389">Doorloop Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="7690e-389">Step through hello code.</span></span> 
- <span data-ttu-id="7690e-390">Het script lokaal valideren.</span><span class="sxs-lookup"><span data-stu-id="7690e-390">Validate your script locally.</span></span>

<span data-ttu-id="7690e-391">Zie voor instructies voor lokale uitvoering en lokale foutopsporing, [U-SQL lokaal uitvoeren en lokale foutopsporing met Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="7690e-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="7690e-392">Aanvullende functies</span><span class="sxs-lookup"><span data-stu-id="7690e-392">Additional features</span></span>

<span data-ttu-id="7690e-393">Data Lake Tools voor VS Code ondersteunt Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="7690e-393">Data Lake Tools for VS Code supports hello following features:</span></span>

-   <span data-ttu-id="7690e-394">IntelliSense automatisch aanvullen: suggesties worden weergegeven in het pop-upvensters rond items, zoals trefwoorden, methoden en variabelen.</span><span class="sxs-lookup"><span data-stu-id="7690e-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="7690e-395">Verschillende pictogrammen verschillende typen Hallo objecten:</span><span class="sxs-lookup"><span data-stu-id="7690e-395">Different icons represent different types of hello objects:</span></span>

    - <span data-ttu-id="7690e-396">Het gegevenstype scala</span><span class="sxs-lookup"><span data-stu-id="7690e-396">Scala data type</span></span>
    - <span data-ttu-id="7690e-397">complex gegevenstype</span><span class="sxs-lookup"><span data-stu-id="7690e-397">Complex data type</span></span>
    - <span data-ttu-id="7690e-398">Ingebouwde UDT 's</span><span class="sxs-lookup"><span data-stu-id="7690e-398">Built-in UDTs</span></span>
    - <span data-ttu-id="7690e-399">.NET-verzameling en -klassen</span><span class="sxs-lookup"><span data-stu-id="7690e-399">.NET collection and classes</span></span>
    - <span data-ttu-id="7690e-400">C#-expressies</span><span class="sxs-lookup"><span data-stu-id="7690e-400">C# expressions</span></span>
    - <span data-ttu-id="7690e-401">Ingebouwde C# UDF's, UDO's en UDAAGs</span><span class="sxs-lookup"><span data-stu-id="7690e-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="7690e-402">U-SQL-functies</span><span class="sxs-lookup"><span data-stu-id="7690e-402">U-SQL functions</span></span>
    - <span data-ttu-id="7690e-403">U-SQL-windowingfunctie</span><span class="sxs-lookup"><span data-stu-id="7690e-403">U-SQL windowing function</span></span>
 
    ![Data Lake Tools voor Visual Studio Code IntelliSense objecttypen](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="7690e-405">IntelliSense automatisch aanvullen van Data Lake Analytics-metagegevens: Data Lake Tools Hallo Data Lake Analytics metagegevens lokaal downloadt.</span><span class="sxs-lookup"><span data-stu-id="7690e-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads hello Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="7690e-406">Hallo IntelliSense functie wordt automatisch gevuld objecten, inclusief Hallo-database, schema, tabel, weergave, tabelwaardefunctie, procedures en C#-assembly's, uit Hallo Data Lake Analytics-metagegevens.</span><span class="sxs-lookup"><span data-stu-id="7690e-406">hello IntelliSense feature automatically populates objects, including hello database, schema, table, view, table-valued function, procedures, and C# assemblies, from hello Data Lake Analytics metadata.</span></span>
 
    ![Data Lake Tools voor Visual Studio Code IntelliSense metagegevens](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="7690e-408">IntelliSense fout markering: Data Lake Tools onderstreept Hallo fouten voor de U-SQL en C# bewerken.</span><span class="sxs-lookup"><span data-stu-id="7690e-408">IntelliSense error marker: Data Lake Tools underlines hello editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="7690e-409">Syntaxis licht: Data Lake Tools maakt gebruik van verschillende kleuren toodifferentiate items, zoals variabelen, trefwoorden, gegevenstype en functies.</span><span class="sxs-lookup"><span data-stu-id="7690e-409">Syntax highlights: Data Lake Tools uses different colors toodifferentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Data Lake Tools voor Visual Studio Code syntaxis highlights](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="7690e-411">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7690e-411">Next steps</span></span>

- <span data-ttu-id="7690e-412">Zie voor U-SQL lokaal uitvoeren en lokale foutopsporing met Visual Studio Code [U-SQL lokaal uitvoeren en lokale foutopsporing met Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="7690e-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="7690e-413">Zie voor informatie over Data Lake Analytics aan de slag [zelfstudie: aan de slag met Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7690e-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="7690e-414">Zie voor meer informatie over Data Lake Tools voor Visual Studio [zelfstudie: U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7690e-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="7690e-415">Zie voor meer informatie over het ontwikkelen van assembly's [ontwikkelen van U-SQL-assembly's voor Azure Data Lake Analytics-taken](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="7690e-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



