---
title: 'Azure Data Lake Tools: Gebruik Azure Data Lake Tools voor Visual Studio Code | Microsoft Docs'
description: 'Informatie over het gebruik van Azure Data Lake Tools voor Visual Studio Code maken, testen en U-SQL-scripts uitvoeren. '
Keywords: VScode, Azure Data Lake Tools, lokaal uitvoeren, lokale foutopsporing, lokale Debug preview opslagbestand uploaden naar opslagpad
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
ms.openlocfilehash: 833d14af47454a01fa3c97ffa854d688dd35871f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="d6e65-104">Azure Data Lake Tools voor Visual Studio Code gebruiken</span><span class="sxs-lookup"><span data-stu-id="d6e65-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="d6e65-105">Informatie over het gebruik van Azure Data Lake Tools voor Visual Studio Code (VS-Code) voor het maken, testen en U-SQL-scripts uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d6e65-105">Learn how to use Azure Data Lake Tools for Visual Studio Code (VS Code) to create, test, and run U-SQL scripts.</span></span> <span data-ttu-id="d6e65-106">De informatie wordt ook beschreven in de volgende video:</span><span class="sxs-lookup"><span data-stu-id="d6e65-106">The information is also covered in the following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="d6e65-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d6e65-107">Prerequisites</span></span>

<span data-ttu-id="d6e65-108">Data Lake Tools kan worden geïnstalleerd op de platformen die worden ondersteund door VS-Code.</span><span class="sxs-lookup"><span data-stu-id="d6e65-108">Data Lake Tools can be installed on the platforms supported by VS Code.</span></span> <span data-ttu-id="d6e65-109">De ondersteunde platforms zijn Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="d6e65-109">The supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="d6e65-110">De verschillende platforms zijn de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="d6e65-110">The different platforms have the following prerequisites:</span></span>

- <span data-ttu-id="d6e65-111">Windows</span><span class="sxs-lookup"><span data-stu-id="d6e65-111">Windows</span></span>

    - <span data-ttu-id="d6e65-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6e65-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="d6e65-113">[Java Runtime Environment voor SE versie 8 update 77 of hoger](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="d6e65-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="d6e65-114">Het pad java.exe toevoegen aan het systeempad omgeving variabele bevindt.</span><span class="sxs-lookup"><span data-stu-id="d6e65-114">Add the java.exe path to the system environment variable path.</span></span> <span data-ttu-id="d6e65-115">Zie voor configuratie-instructies [hoe instellen of wijzigen van de variabele Path system ik?]( https://www.java.com/download/help/path.xml).</span><span class="sxs-lookup"><span data-stu-id="d6e65-115">For configuration instructions, see [How do I set or change the Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="d6e65-116">Het pad is vergelijkbaar met C:\Program Files\Java\jdk1.8.0_77\jre\bin.</span><span class="sxs-lookup"><span data-stu-id="d6e65-116">The path is similar to C:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="d6e65-117">[.NET core SDK 1.0.3 of .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="d6e65-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="d6e65-118">Linux (We raden u aan Ubuntu 14.04 TNS)</span><span class="sxs-lookup"><span data-stu-id="d6e65-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="d6e65-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6e65-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="d6e65-120">Voer de volgende opdracht voor het installeren van de code:</span><span class="sxs-lookup"><span data-stu-id="d6e65-120">To install the code, enter the following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="d6e65-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span><span class="sxs-lookup"><span data-stu-id="d6e65-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="d6e65-122">Voor het bijwerken van de pakketbron deb, voert u de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="d6e65-122">To update the deb package source, enter the following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="d6e65-123">Als u wilt installeren Mono, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d6e65-123">To install Mono, enter the following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="d6e65-124">Mono 4.6 wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="d6e65-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="d6e65-125">Versie 4.6 verwijderen volledig voordat u 4.2.x installeert.</span><span class="sxs-lookup"><span data-stu-id="d6e65-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="d6e65-126">[Java Runtime Environment voor SE versie 8 update 77 of hoger](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="d6e65-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="d6e65-127">Zie voor instructies voor installatie, de [Linux 64-bits installatie-instructies voor Java]( https://java.com/en/download/help/linux_x64_install.xml) pagina.</span><span class="sxs-lookup"><span data-stu-id="d6e65-127">For instructions on installation, see the [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="d6e65-128">[.NET core SDK 1.0.3 of .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="d6e65-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="d6e65-129">MacOS</span><span class="sxs-lookup"><span data-stu-id="d6e65-129">MacOS</span></span>

    - <span data-ttu-id="d6e65-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6e65-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="d6e65-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span><span class="sxs-lookup"><span data-stu-id="d6e65-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="d6e65-132">[Java Runtime Environment voor SE versie 8 update 77 of hoger](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="d6e65-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="d6e65-133">Zie voor instructies voor installatie, de [Linux 64-bits installatie-instructies voor Java](https://java.com/en/download/help/mac_install.xml) pagina.</span><span class="sxs-lookup"><span data-stu-id="d6e65-133">For instructions on installation, see the [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="d6e65-134">[.NET core SDK 1.0.3 of .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="d6e65-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="d6e65-135">Installeren van Data Lake Tools</span><span class="sxs-lookup"><span data-stu-id="d6e65-135">Install Data Lake Tools</span></span>

<span data-ttu-id="d6e65-136">Nadat u de vereiste onderdelen hebt geïnstalleerd, kunt u Data Lake Tools voor VS-Code installeren.</span><span class="sxs-lookup"><span data-stu-id="d6e65-136">After you install the prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="d6e65-137">**Voor het installeren van Data Lake Tools**</span><span class="sxs-lookup"><span data-stu-id="d6e65-137">**To install Data Lake Tools**</span></span>

1. <span data-ttu-id="d6e65-138">Open Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d6e65-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="d6e65-139">Ctrl + P selecteren en voer vervolgens de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d6e65-139">Select Ctrl+P, and then enter the following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="d6e65-140">Hier ziet u een lijst met Visual Studio code-uitbreidingen.</span><span class="sxs-lookup"><span data-stu-id="d6e65-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="d6e65-141">Een van beide is **Azure Data Lake Tools**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="d6e65-142">Selecteer **installeren** naast **Azure Data Lake Tools**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-142">Select **Install** next to **Azure Data Lake Tools**.</span></span> <span data-ttu-id="d6e65-143">Na enkele seconden, de **installeren** knop verandert **opnieuw laden**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-143">After a few seconds, the **Install** button changes to **Reload**.</span></span>
4. <span data-ttu-id="d6e65-144">Selecteer **opnieuw laden** voor het activeren van de extensie.</span><span class="sxs-lookup"><span data-stu-id="d6e65-144">Select **Reload** to activate the extension.</span></span>
5. <span data-ttu-id="d6e65-145">Selecteer **OK** om te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="d6e65-145">Select **OK** to confirm.</span></span> <span data-ttu-id="d6e65-146">U kunt zien Azure Data Lake Tools in de **extensies** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="d6e65-146">You can see Azure Data Lake Tools in the **Extensions** pane.</span></span>
    <span data-ttu-id="d6e65-147">![Data Lake Tools voor Visual Studio Code Extensions deelvenster](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="d6e65-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="d6e65-148">Azure Data Lake Tools activeren</span><span class="sxs-lookup"><span data-stu-id="d6e65-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="d6e65-149">Maak een nieuw .usql-bestand of open een bestaande .usql-bestand voor het activeren van de extensie.</span><span class="sxs-lookup"><span data-stu-id="d6e65-149">Create a new .usql file or open an existing .usql file to activate the extension.</span></span> 

## <a name="connect-to-azure"></a><span data-ttu-id="d6e65-150">Verbinding maken met Azure</span><span class="sxs-lookup"><span data-stu-id="d6e65-150">Connect to Azure</span></span>

<span data-ttu-id="d6e65-151">Voordat u kunt compileren en U-SQL-scripts in Data Lake Analytics uitvoeren, moet u verbinding met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="d6e65-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect to your Azure account.</span></span>

<span data-ttu-id="d6e65-152">**Verbinding maken met Azure**</span><span class="sxs-lookup"><span data-stu-id="d6e65-152">**To connect to Azure**</span></span>

1.  <span data-ttu-id="d6e65-153">Selecteer Ctrl + Shift + P om de opdracht palet te openen.</span><span class="sxs-lookup"><span data-stu-id="d6e65-153">Select Ctrl+Shift+P to open the command palette.</span></span> 
2.  <span data-ttu-id="d6e65-154">Voer **ADL: aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="d6e65-155">De aanmeldingsgegevens wordt weergegeven in de **uitvoer** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="d6e65-155">The login information appears in the **Output** pane.</span></span>

    <span data-ttu-id="d6e65-156">![Data Lake Tools voor Visual Studio Code opdracht palet](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Data Lake Tools voor Visual Studio Code aanmelding apparaatgegevens](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="d6e65-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="d6e65-157">Selecteer Ctrl + klik op de aanmeldings-URL: https://aka.ms/devicelogin de webpagina van de aanmelding te openen.</span><span class="sxs-lookup"><span data-stu-id="d6e65-157">Select Ctrl+click on the login URL: https://aka.ms/devicelogin to open the login webpage.</span></span> <span data-ttu-id="d6e65-158">Voer de code **G567LX42V** in het tekstvak in en selecteer vervolgens **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-158">Enter the code **G567LX42V** into the text box, and then select **Continue**.</span></span>

   ![Data Lake Tools voor Visual Studio Code aanmelding plakken code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="d6e65-160">Volg de instructies voor het aanmelden van de webpagina.</span><span class="sxs-lookup"><span data-stu-id="d6e65-160">Follow the instructions to sign in from the webpage.</span></span> <span data-ttu-id="d6e65-161">Wanneer u verbonden bent, de naam van uw Azure-account wordt weergegeven op de statusbalk in de linkerbenedenhoek van het **tegenover Code** venster.</span><span class="sxs-lookup"><span data-stu-id="d6e65-161">When you're connected, your Azure account name appears on the status bar in the lower-left corner of the **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="d6e65-162">Als uw account twee factoren is ingeschakeld heeft, wordt u aangeraden phone verificatie in plaats van met een PINCODE te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d6e65-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="d6e65-163">Als u wilt afmelden, voer de opdracht **ADL: afmelding**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-163">To sign out, enter the command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="d6e65-164">Lijst van uw Data Lake Analytics-accounts</span><span class="sxs-lookup"><span data-stu-id="d6e65-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="d6e65-165">De om verbinding te testen, moet u een lijst van uw Data Lake Analytics-accounts ophalen.</span><span class="sxs-lookup"><span data-stu-id="d6e65-165">To test the connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="d6e65-166">**Voor een lijst met de Data Lake Analytics-accounts onder uw Azure-abonnement**</span><span class="sxs-lookup"><span data-stu-id="d6e65-166">**To list the Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="d6e65-167">Selecteer Ctrl + Shift + P om de opdracht palet te openen.</span><span class="sxs-lookup"><span data-stu-id="d6e65-167">Select Ctrl+Shift+P to open the command palette.</span></span>
2. <span data-ttu-id="d6e65-168">Voer **ADL: lijst van Accounts**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="d6e65-169">De accounts die worden weergegeven in de **uitvoer** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="d6e65-169">The accounts appear in the **Output** pane.</span></span>

## <a name="open-the-sample-script"></a><span data-ttu-id="d6e65-170">Het voorbeeldscript openen</span><span class="sxs-lookup"><span data-stu-id="d6e65-170">Open the sample script</span></span>
<span data-ttu-id="d6e65-171">Open het palet opdracht (Ctrl + Shift + P) en voer de **ADL: Open voorbeeldscript**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-171">Open the command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="d6e65-172">Hiermee opent u een ander exemplaar van dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d6e65-172">This opens another instance of this sample.</span></span> <span data-ttu-id="d6e65-173">U kunt bewerken, configureren en verzenden van script op basis van dit exemplaar.</span><span class="sxs-lookup"><span data-stu-id="d6e65-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="d6e65-174">Werken met U-SQL</span><span class="sxs-lookup"><span data-stu-id="d6e65-174">Work with U-SQL</span></span>

<span data-ttu-id="d6e65-175">U moet een U-SQL-bestand of een map voor het werken met U-SQL openen.</span><span class="sxs-lookup"><span data-stu-id="d6e65-175">You need open either a U-SQL file or a folder to work with U-SQL.</span></span>

<span data-ttu-id="d6e65-176">**Een map voor uw U-SQL project openen**</span><span class="sxs-lookup"><span data-stu-id="d6e65-176">**To open a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="d6e65-177">Selecteer in Visual Studio Code, de **bestand** menu en selecteer vervolgens **map openen**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-177">From Visual Studio Code, select the **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="d6e65-178">Geef een map op en selecteer vervolgens **map selecteren**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="d6e65-179">Selecteer de **bestand** menu en selecteer vervolgens **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-179">Select the **File** menu, and then select **New**.</span></span> <span data-ttu-id="d6e65-180">Een naamloos-1-bestand wordt toegevoegd aan het project.</span><span class="sxs-lookup"><span data-stu-id="d6e65-180">An Untitled-1 file is added to the project.</span></span>
4. <span data-ttu-id="d6e65-181">Voer de volgende code in het bestand naamloos 1:</span><span class="sxs-lookup"><span data-stu-id="d6e65-181">Enter the following code into the Untitled-1 file:</span></span>

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

    <span data-ttu-id="d6e65-182">Het script maakt een bestand departments.csv met enkele gegevens die zijn opgenomen in de map/Output.</span><span class="sxs-lookup"><span data-stu-id="d6e65-182">The script creates a departments.csv file with some data included in the /output folder.</span></span>

5. <span data-ttu-id="d6e65-183">Sla het bestand als **myUSQL.usql** in de map is geopend.</span><span class="sxs-lookup"><span data-stu-id="d6e65-183">Save the file as **myUSQL.usql** in the opened folder.</span></span> <span data-ttu-id="d6e65-184">Een configuratiebestand adltools_settings.json wordt ook toegevoegd aan het project.</span><span class="sxs-lookup"><span data-stu-id="d6e65-184">A adltools_settings.json configuration file is also added to the project.</span></span>
4. <span data-ttu-id="d6e65-185">Open en adltools_settings.json configureren met de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="d6e65-185">Open and configure adltools_settings.json with the following properties:</span></span>

    - <span data-ttu-id="d6e65-186">Account: Een Data Lake Analytics-account onder uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="d6e65-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="d6e65-187">Database: Een database onder uw account.</span><span class="sxs-lookup"><span data-stu-id="d6e65-187">Database: A database under your account.</span></span> <span data-ttu-id="d6e65-188">De standaardwaarde is **master**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-188">The default is **master**.</span></span>
    - <span data-ttu-id="d6e65-189">Schema: Een schema op uw database.</span><span class="sxs-lookup"><span data-stu-id="d6e65-189">Schema: A schema under your database.</span></span> <span data-ttu-id="d6e65-190">De standaardwaarde is **dbo**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-190">The default is **dbo**.</span></span>
    - <span data-ttu-id="d6e65-191">Optionele instellingen:</span><span class="sxs-lookup"><span data-stu-id="d6e65-191">Optional settings:</span></span>
        - <span data-ttu-id="d6e65-192">Prioriteit: De prioriteitsbereik loopt van 1 tot en met 1000 met 1 als de hoogste prioriteit.</span><span class="sxs-lookup"><span data-stu-id="d6e65-192">Priority: The priority range is from 1 to 1000 with 1 as the highest priority.</span></span> <span data-ttu-id="d6e65-193">De standaardwaarde is **1000**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-193">The default value is **1000**.</span></span>
        - <span data-ttu-id="d6e65-194">Parallelle uitvoering: De parallelle uitvoering bereik is 1 op 150.</span><span class="sxs-lookup"><span data-stu-id="d6e65-194">Parallelism: The parallelism range is from 1 to 150.</span></span> <span data-ttu-id="d6e65-195">De standaardwaarde is de maximale parallelle uitvoering zijn toegestaan in uw Azure Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="d6e65-195">The default value is the maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="d6e65-196">Als de instellingen ongeldige zijn, worden de standaardwaarden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d6e65-196">If the settings are invalid, the default values are used.</span></span>

    ![Data Lake Tools voor Visual Studio Code-configuratiebestand](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="d6e65-198">Een compute Data Lake Analytics-account is nodig voor het compileren en U-SQL-taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d6e65-198">A compute Data Lake Analytics account is needed to compile and run U-SQL jobs.</span></span> <span data-ttu-id="d6e65-199">Voordat u deze kunt compileren en U-SQL-taken uitvoeren, moet u het computeraccount configureren.</span><span class="sxs-lookup"><span data-stu-id="d6e65-199">You must configure the computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="d6e65-200">Nadat de configuratie is opgeslagen, is de account, database en schema-informatie wordt weergegeven op de statusbalk in de linkerbenedenhoek van het bijbehorende .usql-bestand.</span><span class="sxs-lookup"><span data-stu-id="d6e65-200">After the configuration is saved, the account, database, and schema information appears on the status bar at the bottom-left corner of the corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="d6e65-201">Vergeleken met het openen van een bestand, wanneer u een map die u kunt openen:</span><span class="sxs-lookup"><span data-stu-id="d6e65-201">Compared to opening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="d6e65-202">Gebruik een code-behind-bestand.</span><span class="sxs-lookup"><span data-stu-id="d6e65-202">Use a code-behind file.</span></span> <span data-ttu-id="d6e65-203">Code-behind wordt niet ondersteund in de modus met één bestand.</span><span class="sxs-lookup"><span data-stu-id="d6e65-203">In the single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="d6e65-204">Gebruik een configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="d6e65-204">Use a configuration file.</span></span> <span data-ttu-id="d6e65-205">Wanneer u een map opent, delen de scripts in de werkmap in een enkel configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="d6e65-205">When you open a folder, the scripts in the working folder share a single configuration file.</span></span>


<span data-ttu-id="d6e65-206">De U-SQL-script wordt gecompileerd op afstand via de Data Lake Analytics-service.</span><span class="sxs-lookup"><span data-stu-id="d6e65-206">The U-SQL script compiles remotely through the Data Lake Analytics service.</span></span> <span data-ttu-id="d6e65-207">Wanneer u de opdracht de **compileren** opdracht, de U-SQL-script wordt verzonden naar uw Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="d6e65-207">When you issue the **compile** command, the U-SQL script is sent to your Data Lake Analytics account.</span></span> <span data-ttu-id="d6e65-208">Visual Studio Code ontvangt later, het compilatieresultaat.</span><span class="sxs-lookup"><span data-stu-id="d6e65-208">Later, Visual Studio Code receives the compilation result.</span></span> <span data-ttu-id="d6e65-209">Als gevolg van het externe compileren vereist Visual Studio Code weer te geven die de gegevens voor verbinding met uw Data Lake Analytics-account in het configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="d6e65-209">Due to the remote compilation, Visual Studio Code requires that you list the information to connect to your Data Lake Analytics account in the configuration file.</span></span>

<span data-ttu-id="d6e65-210">**Voor het compileren van een U-SQL-script**</span><span class="sxs-lookup"><span data-stu-id="d6e65-210">**To compile a U-SQL script**</span></span>

1. <span data-ttu-id="d6e65-211">Selecteer Ctrl + Shift + P om de opdracht palet te openen.</span><span class="sxs-lookup"><span data-stu-id="d6e65-211">Select Ctrl+Shift+P to open the command palette.</span></span> 
2. <span data-ttu-id="d6e65-212">Voer **ADL: compileren van Script**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="d6e65-213">De compilatie-resultaten verschijnen in de **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="d6e65-213">The compile results appear in the **Output** window.</span></span> <span data-ttu-id="d6e65-214">U kunt ook met de rechtermuisknop op een scriptbestand en selecteer vervolgens **ADL: compileren Script** voor het compileren van een U-SQL-taak.</span><span class="sxs-lookup"><span data-stu-id="d6e65-214">You can also right-click a script file, and then select **ADL: Compile Script** to compile a U-SQL job.</span></span> <span data-ttu-id="d6e65-215">Het compilatieresultaat wordt weergegeven in de **uitvoer** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="d6e65-215">The compilation result appears in the **Output** pane.</span></span>
 

<span data-ttu-id="d6e65-216">**Verzenden van een U-SQL-script**</span><span class="sxs-lookup"><span data-stu-id="d6e65-216">**To submit a U-SQL script**</span></span>

1. <span data-ttu-id="d6e65-217">Selecteer Ctrl + Shift + P om de opdracht palet te openen.</span><span class="sxs-lookup"><span data-stu-id="d6e65-217">Select Ctrl+Shift+P to open the command palette.</span></span> 
2. <span data-ttu-id="d6e65-218">Voer **ADL: verzenden van taak**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="d6e65-219">U kunt ook met de rechtermuisknop op een scriptbestand en selecteer vervolgens **ADL: Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="d6e65-220">Nadat u een U-SQL-taak hebt ingediend, de verzending van Logboeken worden weergegeven in de **uitvoer** venster in VS-Code.</span><span class="sxs-lookup"><span data-stu-id="d6e65-220">After you submit a U-SQL job, the submission logs appear in the **Output** window in VS Code.</span></span> <span data-ttu-id="d6e65-221">Als de verzending geslaagd is, de taak URL wordt weergegeven ook.</span><span class="sxs-lookup"><span data-stu-id="d6e65-221">If the submission is successful, the job URL appears as well.</span></span> <span data-ttu-id="d6e65-222">U kunt de URL van de taak openen in een webbrowser om bij te houden van de status van de realtime.</span><span class="sxs-lookup"><span data-stu-id="d6e65-222">You can open the job URL in a web browser to track the real-time job status.</span></span>

<span data-ttu-id="d6e65-223">Instellen zodat de uitvoer van de taakdetails **jobInformationOutputPath** in de **tegenover code voor de u-sql_settings.json** bestand.</span><span class="sxs-lookup"><span data-stu-id="d6e65-223">To enable the output of the job details, set **jobInformationOutputPath** in the **vs code for the u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="d6e65-224">Een code-behind-bestand gebruiken</span><span class="sxs-lookup"><span data-stu-id="d6e65-224">Use a code-behind file</span></span>

<span data-ttu-id="d6e65-225">Een code-behind-bestand is een C#-bestanden die zijn gekoppeld aan een enkel U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="d6e65-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="d6e65-226">U kunt een speciale script definiëren UDO, UDA, UDT en UDF in het code-behind-bestand.</span><span class="sxs-lookup"><span data-stu-id="d6e65-226">You can define a script dedicated to UDO, UDA, UDT, and UDF in the code-behind file.</span></span> <span data-ttu-id="d6e65-227">De UDO, UDA, UDT en UDF kunnen rechtstreeks in het script zonder eerst registreren van de assembly worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d6e65-227">The UDO, UDA, UDT, and UDF can be used directly in the script without registering the assembly first.</span></span> <span data-ttu-id="d6e65-228">De code-behind-bestand is in dezelfde map als de peering U-SQL-scriptbestand geplaatst.</span><span class="sxs-lookup"><span data-stu-id="d6e65-228">The code-behind file is put in the same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="d6e65-229">Als het script de naam xxx.usql, is de code-behind xxx.usql.cs genoemd.</span><span class="sxs-lookup"><span data-stu-id="d6e65-229">If the script is named xxx.usql, the code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="d6e65-230">Als u de code-behind-bestand voor het handmatig verwijdert, wordt de code-behind-functie is uitgeschakeld voor de bijbehorende U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="d6e65-230">If you manually delete the code-behind file, the code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="d6e65-231">Zie voor meer informatie over het schrijven van code voor de U-SQL-script klant [schrijven en met behulp van aangepaste Code in de U-SQL: door de gebruiker gedefinieerde functies]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span><span class="sxs-lookup"><span data-stu-id="d6e65-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="d6e65-232">Ter ondersteuning van code-behind, moet u een werkmap te openen.</span><span class="sxs-lookup"><span data-stu-id="d6e65-232">To support code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="d6e65-233">**Een code-behind-bestand genereren**</span><span class="sxs-lookup"><span data-stu-id="d6e65-233">**To generate a code-behind file**</span></span>

1. <span data-ttu-id="d6e65-234">Open een bronbestand.</span><span class="sxs-lookup"><span data-stu-id="d6e65-234">Open a source file.</span></span> 
2. <span data-ttu-id="d6e65-235">Selecteer Ctrl + Shift + P om de opdracht palet te openen.</span><span class="sxs-lookup"><span data-stu-id="d6e65-235">Select Ctrl+Shift+P to open the command palette.</span></span>
3. <span data-ttu-id="d6e65-236">Voer **ADL: genereren van Code achter**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="d6e65-237">Een code-behind-bestand wordt gemaakt in dezelfde map.</span><span class="sxs-lookup"><span data-stu-id="d6e65-237">A code-behind file is created in the same folder.</span></span> 

<span data-ttu-id="d6e65-238">U kunt ook met de rechtermuisknop op een scriptbestand en selecteer vervolgens **ADL: Code genereren achter**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="d6e65-239">Is hetzelfde als met de zelfstandige U-SQL-scriptbestand om te compileren en verzenden van een U-SQL-script met een code-behind-bestand.</span><span class="sxs-lookup"><span data-stu-id="d6e65-239">To compile and submit a U-SQL script with a code-behind file is the same as with the standalone U-SQL script file.</span></span>

<span data-ttu-id="d6e65-240">De volgende twee schermafbeeldingen weergeven een code-behind-bestand en het bijbehorende bestand van de U-SQL-script:</span><span class="sxs-lookup"><span data-stu-id="d6e65-240">The following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Data Lake Tools voor Visual Studio Code code-behind](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Data Lake Tools voor Visual Studio Code code-behind scriptbestand](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="d6e65-243">Assembly's gebruiken</span><span class="sxs-lookup"><span data-stu-id="d6e65-243">Use assemblies</span></span>

<span data-ttu-id="d6e65-244">Zie voor meer informatie over het ontwikkelen van assembly's [ontwikkelen van U-SQL-assembly's voor Azure Data Lake Analytics-taken](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="d6e65-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="d6e65-245">Data Lake Tools kunt u aangepaste code-assembly's registreren in de Data Lake Analytics-catalogus.</span><span class="sxs-lookup"><span data-stu-id="d6e65-245">You can use Data Lake Tools to register custom code assemblies in the Data Lake Analytics catalog.</span></span>

<span data-ttu-id="d6e65-246">**Registreren van een assembly**</span><span class="sxs-lookup"><span data-stu-id="d6e65-246">**To register an assembly**</span></span>

<span data-ttu-id="d6e65-247">U kunt de assembly via registreren de **ADL: registreren Assembly** of **ADL: Assembly registreren via configuratie** opdrachten.</span><span class="sxs-lookup"><span data-stu-id="d6e65-247">You can register the assembly through the **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="d6e65-248">**Registreren via de ADL: registreren Assembly-opdracht**</span><span class="sxs-lookup"><span data-stu-id="d6e65-248">**To register through the ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="d6e65-249">Selecteer Ctrl + Shift + P om de opdracht palet te openen.</span><span class="sxs-lookup"><span data-stu-id="d6e65-249">Select Ctrl+Shift+P to open the command palette.</span></span>
2.  <span data-ttu-id="d6e65-250">Voer **ADL: Assembly registreren**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="d6e65-251">Geef het lokale assembly-pad.</span><span class="sxs-lookup"><span data-stu-id="d6e65-251">Specify the local assembly path.</span></span> 
4.  <span data-ttu-id="d6e65-252">Selecteer een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="d6e65-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="d6e65-253">Selecteer een database.</span><span class="sxs-lookup"><span data-stu-id="d6e65-253">Select a database.</span></span>

<span data-ttu-id="d6e65-254">Resultaten: De portal wordt geopend in een browser en geeft het registratieproces assembly.</span><span class="sxs-lookup"><span data-stu-id="d6e65-254">Results: The portal is opened in a browser and displays the assembly registration process.</span></span>  

<span data-ttu-id="d6e65-255">Een andere handige manier voor het activeren van de **ADL: registreren Assembly** opdracht is met de rechtermuisknop op het DLL-bestand in Verkenner.</span><span class="sxs-lookup"><span data-stu-id="d6e65-255">Another convenient way to trigger the **ADL: Register Assembly** command is to right-click the .dll file in File Explorer.</span></span> 

<span data-ttu-id="d6e65-256">**Registreren via de ADL: Assembly registreren via de opdracht configuratie**</span><span class="sxs-lookup"><span data-stu-id="d6e65-256">**To register though the ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="d6e65-257">Selecteer Ctrl + Shift + P om de opdracht palet te openen.</span><span class="sxs-lookup"><span data-stu-id="d6e65-257">Select Ctrl+Shift+P to open the command palette.</span></span>
2.  <span data-ttu-id="d6e65-258">Voer **ADL: Assembly via configuratie registreren**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="d6e65-259">Geef het lokale assembly-pad.</span><span class="sxs-lookup"><span data-stu-id="d6e65-259">Specify the local assembly path.</span></span> 
4.  <span data-ttu-id="d6e65-260">Het JSON-bestand wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d6e65-260">The JSON file is displayed.</span></span> <span data-ttu-id="d6e65-261">Bekijken en bewerken van de assembly-afhankelijkheden en de resourceparameters, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="d6e65-261">Review and edit the assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="d6e65-262">Instructies worden weergegeven in de **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="d6e65-262">Instructions are displayed in the **Output** window.</span></span> <span data-ttu-id="d6e65-263">Sla om door te gaan naar de assembly-registratie (Ctrl + S) het JSON-bestand.</span><span class="sxs-lookup"><span data-stu-id="d6e65-263">To proceed to the assembly registration, save (Ctrl+S) the JSON file.</span></span>

![Data Lake Tools voor Visual Studio Code code-behind](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="d6e65-265">Assembly-afhankelijkheden: een Azure Data Lake Tools of de DLL-bestand eventuele afhankelijkheden heeft.</span><span class="sxs-lookup"><span data-stu-id="d6e65-265">Assembly dependencies: Azure Data Lake Tools autodetects whether the DLL has any dependencies.</span></span> <span data-ttu-id="d6e65-266">De afhankelijkheden worden weergegeven in het JSON-bestand nadat ze zijn gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="d6e65-266">The dependencies are displayed in the JSON file after they are detected.</span></span> 
>- <span data-ttu-id="d6e65-267">Resources: U kunt uw resources dll-bestand (bijvoorbeeld, txt, PNG en .csv) uploaden als onderdeel van de registratie van de assembly.</span><span class="sxs-lookup"><span data-stu-id="d6e65-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of the assembly registration.</span></span> 

<span data-ttu-id="d6e65-268">Een andere manier voor het activeren van de **ADL: Assembly registreren via configuratie** opdracht is met de rechtermuisknop op het DLL-bestand in Verkenner.</span><span class="sxs-lookup"><span data-stu-id="d6e65-268">Another way to trigger the **ADL: Register Assembly through Configuration** command is to right-click the .dll file in File Explorer.</span></span> 

<span data-ttu-id="d6e65-269">De volgende U-SQL-code toont het aanroepen van een assembly.</span><span class="sxs-lookup"><span data-stu-id="d6e65-269">The following U-SQL code demonstrates how to call an assembly.</span></span> <span data-ttu-id="d6e65-270">In het voorbeeld de assemblynaam is *testen*.</span><span class="sxs-lookup"><span data-stu-id="d6e65-270">In the sample, the assembly name is *test*.</span></span>

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
    TO @"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-the-data-lake-analytics-catalog"></a><span data-ttu-id="d6e65-271">Toegang tot de Data Lake Analytics-catalogus</span><span class="sxs-lookup"><span data-stu-id="d6e65-271">Access the Data Lake Analytics catalog</span></span>

<span data-ttu-id="d6e65-272">Nadat u verbinding hebt gemaakt in Azure, kunt u de volgende stappen uit voor toegang tot de U-SQL-catalogus.</span><span class="sxs-lookup"><span data-stu-id="d6e65-272">After you have connected to Azure, you can use the following steps to access the U-SQL catalog.</span></span>

<span data-ttu-id="d6e65-273">**Toegang tot de Azure Data Lake Analytics-metagegevens**</span><span class="sxs-lookup"><span data-stu-id="d6e65-273">**To access the Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="d6e65-274">Ctrl + Shift + P selecteren en voer vervolgens **ADL: lijst met tabellen**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="d6e65-275">Selecteer een van de Data Lake Analytics-accounts.</span><span class="sxs-lookup"><span data-stu-id="d6e65-275">Select one of the Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="d6e65-276">Selecteer een van de Data Lake Analytics-databases.</span><span class="sxs-lookup"><span data-stu-id="d6e65-276">Select one of the Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="d6e65-277">Selecteer een van de schema's.</span><span class="sxs-lookup"><span data-stu-id="d6e65-277">Select one of the schemas.</span></span> <span data-ttu-id="d6e65-278">Hier ziet u de lijst met tabellen.</span><span class="sxs-lookup"><span data-stu-id="d6e65-278">You can see the list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="d6e65-279">Weergave Data Lake Analytics-taken</span><span class="sxs-lookup"><span data-stu-id="d6e65-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="d6e65-280">**Data Lake Analytics-taken weergeven**</span><span class="sxs-lookup"><span data-stu-id="d6e65-280">**To view Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="d6e65-281">Open het palet opdracht (Ctrl + Shift + P) en selecteer **ADL: taak weergeven**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-281">Open the command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="d6e65-282">Selecteer een Data Lake Analytics of lokale account.</span><span class="sxs-lookup"><span data-stu-id="d6e65-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="d6e65-283">Wacht totdat de takenlijst met voor het account dat moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d6e65-283">Wait for the jobs list for the account to appear.</span></span>
4.  <span data-ttu-id="d6e65-284">Selecteer een taak in de lijst om de taak, Data Lake Tools Hiermee opent u de taakdetails van de in de Azure portal en het bestand Taakinfo wordt weergegeven in de VS-Code.</span><span class="sxs-lookup"><span data-stu-id="d6e65-284">Select a job from job list, Data Lake Tools opens the job details in the Azure portal and displays the JobInfo file in VS Code.</span></span>

![Data Lake Tools voor Visual Studio Code IntelliSense objecttypen](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="d6e65-286">Azure Data Lake Storage-integratie</span><span class="sxs-lookup"><span data-stu-id="d6e65-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="d6e65-287">U kunt Azure Data Lake Storage-gerelateerde opdrachten te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d6e65-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="d6e65-288">Blader door de Azure Data Lake Storage-resources.</span><span class="sxs-lookup"><span data-stu-id="d6e65-288">Browse through the Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="d6e65-289">Voorbeeld bekijken van het Azure Data Lake Storage-bestand.</span><span class="sxs-lookup"><span data-stu-id="d6e65-289">Preview the Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="d6e65-290">Upload het bestand rechtstreeks naar Azure Data Lake Storage in VS-Code.</span><span class="sxs-lookup"><span data-stu-id="d6e65-290">Upload the file directly to Azure Data Lake Storage in VS Code.</span></span> 

### <a name="list-the-storage-path"></a><span data-ttu-id="d6e65-291">Het pad voor opslag weergeven</span><span class="sxs-lookup"><span data-stu-id="d6e65-291">List the storage path</span></span> 
<span data-ttu-id="d6e65-292">U kunt het pad voor de opslag via het palet opdracht of klik met de rechtermuisknop aanbieden.</span><span class="sxs-lookup"><span data-stu-id="d6e65-292">You can list the storage path through the command palette or through right-click.</span></span>

<span data-ttu-id="d6e65-293">**Voor een lijst met het pad voor opslag via het palet opdracht**</span><span class="sxs-lookup"><span data-stu-id="d6e65-293">**To list the storage path through the command palette**</span></span>

1.  <span data-ttu-id="d6e65-294">Open het palet opdracht (Ctrl + Shift + P) en voer de **ADL: lijst opslagpad**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-294">Open the command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Data Lake Tools voor Visual Studio Code lijst opslagpad](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="d6e65-296">Selecteer uw favoriete methode voor het aanbieden van het pad voor opslag.</span><span class="sxs-lookup"><span data-stu-id="d6e65-296">Select your preferred way for listing the storage path.</span></span> <span data-ttu-id="d6e65-297">Maakt gebruik van deze overgang **Geef een pad** als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d6e65-297">This passage uses **Enter a path** as an example.</span></span>

    ![Data Lake Tools voor Visual Studio Code een manier om de lijst met het pad voor opslag](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="d6e65-299">VS-Code, blijft de laatst bezochte pad in elke Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="d6e65-299">VS Code keeps the last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="d6e65-300">Bijvoorbeeld: ss tt /.</span><span class="sxs-lookup"><span data-stu-id="d6e65-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="d6e65-301">Hoofdpad naar browser: het hoofdpad lijst van de geselecteerde Data Lake Analytics-account of een lokaal pad.</span><span class="sxs-lookup"><span data-stu-id="d6e65-301">Browser from root path: The list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="d6e65-302">Geef een pad op: een opgegeven pad van de geselecteerde Data Lake Analytics-account of een lokaal pad.</span><span class="sxs-lookup"><span data-stu-id="d6e65-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="d6e65-303">Selecteer een account in het lokale pad of een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="d6e65-303">Select an account from the local path or a Data Lake Analytics account.</span></span>

    ![Data Lake Tools voor Visual Studio Code selecteren meer](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="d6e65-305">Selecteer **meer** lijst met meer Data Lake Analytics-accounts, en selecteer vervolgens een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="d6e65-305">Select **more** to list more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Data Lake Tools voor Visual Studio Code selecteren een account](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="d6e65-307">Geef het pad van een Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="d6e65-307">Enter an Azure storage path.</span></span> <span data-ttu-id="d6e65-308">Bijvoorbeeld: / uitvoer.</span><span class="sxs-lookup"><span data-stu-id="d6e65-308">For example, /output.</span></span>

    ![Data Lake Tools voor Visual Studio Code invoeren opslagpad](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="d6e65-310">Resultaten: Het palet opdracht bevat informatie over het pad op basis van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="d6e65-310">Results: The command palette lists the path information based on your entries.</span></span>

    ![Data Lake Tools voor Visual Studio Code weergeven opslag pad resultaten](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="d6e65-312">Er is een handige methode voor een lijst met het relatieve pad via het snelmenu.</span><span class="sxs-lookup"><span data-stu-id="d6e65-312">A more convenient way to list the relative path is through the right-click context menu.</span></span>

<span data-ttu-id="d6e65-313">**Aan de lijst door met de rechtermuisknop op het pad voor opslag**</span><span class="sxs-lookup"><span data-stu-id="d6e65-313">**To list the storage path through right-click**</span></span>

1.  <span data-ttu-id="d6e65-314">Met de rechtermuisknop op de padtekenreeks selecteren **lijst opslagpad**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-314">Right-click the path string to select **List Storage Path**.</span></span>

       ![Data Lake Tools voor Visual Studio Code met de rechtermuisknop op contextmenu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="d6e65-316">Het geselecteerde relatief pad wordt weergegeven in het palet opdracht.</span><span class="sxs-lookup"><span data-stu-id="d6e65-316">The selected relative path appears in the command palette.</span></span>

   ![Data Lake Tools voor Visual Studio Code relatief pad zijn geselecteerd](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="d6e65-318">Selecteer een account in het lokale pad of een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="d6e65-318">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools voor Visual Studio Code selecteren een account](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="d6e65-320">Resultaten: Het palet opdracht worden de mappen en bestanden voor het huidige pad.</span><span class="sxs-lookup"><span data-stu-id="d6e65-320">Results: The command palette lists the folders and files for the current path.</span></span>

       ![Data Lake Tools voor Visual Studio Code lijst van het huidige pad](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-the-storage-file"></a><span data-ttu-id="d6e65-322">Voorbeeld van het opslagbestand</span><span class="sxs-lookup"><span data-stu-id="d6e65-322">Preview the storage file</span></span>
<span data-ttu-id="d6e65-323">U kunt het opslagbestand via het palet opdracht of klik met de rechtermuisknop bekijken.</span><span class="sxs-lookup"><span data-stu-id="d6e65-323">You can preview the storage file through the command palette or through right-click.</span></span>

<span data-ttu-id="d6e65-324">**Voorbeeld van het opslagbestand via het palet opdracht**</span><span class="sxs-lookup"><span data-stu-id="d6e65-324">**To preview the storage file through the command palette**</span></span>

1.  <span data-ttu-id="d6e65-325">Open het palet opdracht (Ctrl + Shift + P) en voer de **ADL: Preview opslagbestand**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-325">Open the command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Data Lake Tools voor Visual Studio Code preview opslagbestand](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="d6e65-327">Selecteer een account in het lokale pad of een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="d6e65-327">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools voor Visual Studio Code lijst account](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="d6e65-329">Selecteer **meer** lijst met meer Data Lake Analytics-accounts, en selecteer vervolgens een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="d6e65-329">Select **more** to list more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Data Lake Tools voor Visual Studio Code selecteren een account](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="d6e65-331">Voer een pad van de Azure-opslag of het bestand.</span><span class="sxs-lookup"><span data-stu-id="d6e65-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="d6e65-332">Bijvoorbeeld: /output/SearchLog.txt.</span><span class="sxs-lookup"><span data-stu-id="d6e65-332">For example, /output/SearchLog.txt.</span></span>

       ![Data Lake Tools voor Visual Studio Code invoeren opslagpad en bestandsnaam](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="d6e65-334">Resultaten: Het palet opdracht bevat informatie over het pad op basis van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="d6e65-334">Results: The command palette lists the path information based on your entries.</span></span>

       ![Data Lake Tools voor Visual Studio Code voorbeeld bestandsresultaat](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="d6e65-336">**Aan de lijst door met de rechtermuisknop op het pad voor opslag**</span><span class="sxs-lookup"><span data-stu-id="d6e65-336">**To list the storage path through right-click**</span></span>

1.  <span data-ttu-id="d6e65-337">Voorbeeld van een bestand door met de rechtermuisknop op het bestandspad.</span><span class="sxs-lookup"><span data-stu-id="d6e65-337">To preview a file, right-click the file path.</span></span>

   ![Data Lake Tools voor Visual Studio Code met de rechtermuisknop op contextmenu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="d6e65-339">Selecteer een account in het lokale pad of een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="d6e65-339">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Data Lake Tools voor Visual Studio Code selecteren een account](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="d6e65-341">Resultaten: VS-Code weergegeven de voorbeeldresultaten van het bestand.</span><span class="sxs-lookup"><span data-stu-id="d6e65-341">Results: VS Code displays the preview results of the file.</span></span>

       ![Data Lake Tools voor Visual Studio Code voorbeeld bestandsresultaat](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="d6e65-343">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="d6e65-343">Upload a file</span></span> 

<span data-ttu-id="d6e65-344">U kunt bestanden uploaden door te voeren van de opdrachten **ADL: uploaden** of **ADL:-bestand uploaden via configuratie**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-344">You can upload files by entering the commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="d6e65-345">**Voor het uploaden van bestanden via het ADL: de opdracht-bestand uploaden**</span><span class="sxs-lookup"><span data-stu-id="d6e65-345">**To upload files though the ADL: Upload File command**</span></span>
1. <span data-ttu-id="d6e65-346">Selecteer Ctrl + Shift + P om het palet opdracht openen of met de rechtermuisknop op de scripteditor en voer vervolgens **-bestand uploaden**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-346">Select Ctrl+Shift+P to open the command palette or right-click the script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="d6e65-347">Voer voor het bestand uploadt, een lokaal pad.</span><span class="sxs-lookup"><span data-stu-id="d6e65-347">To upload the file, enter a local path.</span></span>

    ![Data Lake Tools voor Visual Studio Code opgeven lokaal pad](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="d6e65-349">Selecteer een van de manieren van het opsommen van het pad voor opslag.</span><span class="sxs-lookup"><span data-stu-id="d6e65-349">Select one of the ways of listing the storage path.</span></span> <span data-ttu-id="d6e65-350">Maakt gebruik van deze overgang **Geef een pad** als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d6e65-350">This passage uses **Enter a path** as an example.</span></span>

    ![Data Lake Tools voor Visual Studio Code lijst opslagpad](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="d6e65-352">VS-Code, blijft de laatst bezochte pad in elke Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="d6e65-352">VS Code keeps the last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="d6e65-353">Bijvoorbeeld: ss tt /.</span><span class="sxs-lookup"><span data-stu-id="d6e65-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="d6e65-354">Hoofdpad naar browser: het hoofdpad lijst van de geselecteerde Data Lake Analytics-account of een lokaal pad.</span><span class="sxs-lookup"><span data-stu-id="d6e65-354">Browser from root path: The list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="d6e65-355">Geef een pad op: een opgegeven pad van de geselecteerde Data Lake Analytics-account of een lokaal pad.</span><span class="sxs-lookup"><span data-stu-id="d6e65-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="d6e65-356">Selecteer een account in het lokale pad of een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="d6e65-356">Select an account from the local path or a Data Lake Analytics account.</span></span>

    ![Data Lake Tools voor Visual Studio Code met de rechtermuisknop op de opslag](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="d6e65-358">Geef het pad van een Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="d6e65-358">Enter an Azure storage path.</span></span> <span data-ttu-id="d6e65-359">Bijvoorbeeld: / uitvoer.</span><span class="sxs-lookup"><span data-stu-id="d6e65-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="d6e65-360">Uw Azure-opslag-pad vinden.</span><span class="sxs-lookup"><span data-stu-id="d6e65-360">Find your Azure storage path.</span></span> <span data-ttu-id="d6e65-361">Selecteer **de huidige map kiezen**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-361">Select **Choose current folder**.</span></span>

    ![Selecteer een map van Data Lake Tools voor Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="d6e65-363">Resultaten: De **uitvoer** venster wordt de status van bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="d6e65-363">Results: The **Output** window displays the file upload status.</span></span>

       ![Data Lake Tools voor Visual Studio Code Uploadstatus](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="d6e65-365">**Voor het uploaden van bestanden via het ADL:-bestand uploaden via configuratie-opdracht**</span><span class="sxs-lookup"><span data-stu-id="d6e65-365">**To upload files though the ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="d6e65-366">Selecteer Ctrl + Shift + P om het palet opdracht openen of met de rechtermuisknop op de scripteditor en voer vervolgens **-bestand uploaden via configuratie**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-366">Select Ctrl+Shift+P to open the command palette or right-click the script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="d6e65-367">VS-Code wordt een JSON-bestand weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d6e65-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="d6e65-368">U kunt bestandspaden invoeren en meerdere bestanden tegelijk uploaden.</span><span class="sxs-lookup"><span data-stu-id="d6e65-368">You can enter file paths and upload multiple files at the same time.</span></span> <span data-ttu-id="d6e65-369">Instructies worden weergegeven in de **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="d6e65-369">Instructions are displayed in the **Output** window.</span></span> <span data-ttu-id="d6e65-370">Sla (Ctrl + S) het JSON-bestand om door te gaan van het bestand te uploaden.</span><span class="sxs-lookup"><span data-stu-id="d6e65-370">To proceed to upload the file, save (Ctrl+S) the JSON file.</span></span>

       ![Data Lake Tools voor Visual Studio Code bestandspad](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="d6e65-372">Resultaten: De **uitvoer** venster wordt de status van bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="d6e65-372">Results: The **Output** window displays the file upload status.</span></span>

       ![Data Lake Tools voor Visual Studio Code Uploadstatus](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="d6e65-374">Een andere manier een bestand te uploaden naar de opslag is via het menu met de rechtermuisknop op het volledige pad van het bestand of het relatieve pad van het bestand in de scripteditor.</span><span class="sxs-lookup"><span data-stu-id="d6e65-374">Another way to upload a file to storage is through the right-click menu on the file's full path or the file's relative path in the script editor.</span></span> <span data-ttu-id="d6e65-375">Geef het lokale bestandspad en selecteer vervolgens het account.</span><span class="sxs-lookup"><span data-stu-id="d6e65-375">Enter the local file path, and then select the account.</span></span> <span data-ttu-id="d6e65-376">De **uitvoer** venster wordt de uploadstatus.</span><span class="sxs-lookup"><span data-stu-id="d6e65-376">The **Output** window displays the upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="d6e65-377">Open Azure Opslagverkenner</span><span class="sxs-lookup"><span data-stu-id="d6e65-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="d6e65-378">U kunt openen **Azure Opslagverkenner** met de opdracht **ADL: Open Web Azure Storage Explorer** of door deze te selecteren in het contextmenu van de context.</span><span class="sxs-lookup"><span data-stu-id="d6e65-378">You can open **Azure Storage Explorer** by entering the command **ADL: Open Web Azure Storage Explorer** or by selecting it from the right-click context menu.</span></span>

<span data-ttu-id="d6e65-379">**Azure Storage Explorer openen**</span><span class="sxs-lookup"><span data-stu-id="d6e65-379">**To open Azure Storage Explorer**</span></span>

1. <span data-ttu-id="d6e65-380">Selecteer Ctrl + Shift + P om de opdracht palet te openen.</span><span class="sxs-lookup"><span data-stu-id="d6e65-380">Select Ctrl+Shift+P to open the command palette.</span></span>
2. <span data-ttu-id="d6e65-381">Voer **Open Web Azure Storage Explorer** of met de rechtermuisknop op een relatief pad of het volledige pad in de scripteditor en selecteer vervolgens **Open Web Azure Storage Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d6e65-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or the full path in the script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="d6e65-382">Selecteer een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="d6e65-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="d6e65-383">Data Lake Tools Hiermee opent u het pad van de Azure-opslag in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d6e65-383">Data Lake Tools opens the Azure storage path in the Azure portal.</span></span> <span data-ttu-id="d6e65-384">U kunt het pad niet vinden en een voorbeeld bekijken van het bestand via het web.</span><span class="sxs-lookup"><span data-stu-id="d6e65-384">You can find the path and preview the file from the web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="d6e65-385">Lokaal uitvoeren en lokaal fouten opsporen voor Windows gebruikers</span><span class="sxs-lookup"><span data-stu-id="d6e65-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="d6e65-386">U-SQL lokaal uitvoeren Test uw lokale gegevens en uw script lokaal, valideert voordat uw code naar Data Lake Analytics is gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="d6e65-386">U-SQL local run tests your local data and validates your script locally, before your code is published to Data Lake Analytics.</span></span> <span data-ttu-id="d6e65-387">De functie lokale foutopsporing kunt u de volgende taken uitvoeren voordat u uw code wordt verzonden naar Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="d6e65-387">The local debug feature enables you to complete the following tasks before your code is submitted to Data Lake Analytics:</span></span> 
- <span data-ttu-id="d6e65-388">Uw C# code-behind voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="d6e65-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="d6e65-389">Analyseer de code in.</span><span class="sxs-lookup"><span data-stu-id="d6e65-389">Step through the code.</span></span> 
- <span data-ttu-id="d6e65-390">Het script lokaal valideren.</span><span class="sxs-lookup"><span data-stu-id="d6e65-390">Validate your script locally.</span></span>

<span data-ttu-id="d6e65-391">Zie voor instructies voor lokale uitvoering en lokale foutopsporing, [U-SQL lokaal uitvoeren en lokale foutopsporing met Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="d6e65-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="d6e65-392">Aanvullende functies</span><span class="sxs-lookup"><span data-stu-id="d6e65-392">Additional features</span></span>

<span data-ttu-id="d6e65-393">Data Lake Tools voor VS Code ondersteunt de volgende functies:</span><span class="sxs-lookup"><span data-stu-id="d6e65-393">Data Lake Tools for VS Code supports the following features:</span></span>

-   <span data-ttu-id="d6e65-394">IntelliSense automatisch aanvullen: suggesties worden weergegeven in het pop-upvensters rond items, zoals trefwoorden, methoden en variabelen.</span><span class="sxs-lookup"><span data-stu-id="d6e65-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="d6e65-395">Verschillende pictogrammen verschillende typen objecten:</span><span class="sxs-lookup"><span data-stu-id="d6e65-395">Different icons represent different types of the objects:</span></span>

    - <span data-ttu-id="d6e65-396">Het gegevenstype scala</span><span class="sxs-lookup"><span data-stu-id="d6e65-396">Scala data type</span></span>
    - <span data-ttu-id="d6e65-397">complex gegevenstype</span><span class="sxs-lookup"><span data-stu-id="d6e65-397">Complex data type</span></span>
    - <span data-ttu-id="d6e65-398">Ingebouwde UDT 's</span><span class="sxs-lookup"><span data-stu-id="d6e65-398">Built-in UDTs</span></span>
    - <span data-ttu-id="d6e65-399">.NET-verzameling en -klassen</span><span class="sxs-lookup"><span data-stu-id="d6e65-399">.NET collection and classes</span></span>
    - <span data-ttu-id="d6e65-400">C#-expressies</span><span class="sxs-lookup"><span data-stu-id="d6e65-400">C# expressions</span></span>
    - <span data-ttu-id="d6e65-401">Ingebouwde C# UDF's, UDO's en UDAAGs</span><span class="sxs-lookup"><span data-stu-id="d6e65-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="d6e65-402">U-SQL-functies</span><span class="sxs-lookup"><span data-stu-id="d6e65-402">U-SQL functions</span></span>
    - <span data-ttu-id="d6e65-403">U-SQL-windowingfunctie</span><span class="sxs-lookup"><span data-stu-id="d6e65-403">U-SQL windowing function</span></span>
 
    ![Data Lake Tools voor Visual Studio Code IntelliSense objecttypen](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="d6e65-405">IntelliSense automatisch aanvullen van Data Lake Analytics-metagegevens: Data Lake Tools downloadt de metagegevens van de Data Lake Analytics lokaal.</span><span class="sxs-lookup"><span data-stu-id="d6e65-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads the Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="d6e65-406">De functie IntelliSense wordt automatisch gevuld objecten, inclusief de database, schema, tabel, weergave, tabelwaardefunctie, procedures en C#-assembly's, uit de Data Lake Analytics-metagegevens.</span><span class="sxs-lookup"><span data-stu-id="d6e65-406">The IntelliSense feature automatically populates objects, including the database, schema, table, view, table-valued function, procedures, and C# assemblies, from the Data Lake Analytics metadata.</span></span>
 
    ![Data Lake Tools voor Visual Studio Code IntelliSense metagegevens](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="d6e65-408">IntelliSense fout markering: Data Lake Tools onderstreept de bewerken fouten voor de U-SQL en C#.</span><span class="sxs-lookup"><span data-stu-id="d6e65-408">IntelliSense error marker: Data Lake Tools underlines the editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="d6e65-409">Syntaxis licht: Data Lake Tools maakt gebruik van verschillende kleuren te onderscheiden van items, zoals variabelen, trefwoorden, gegevenstype en functies.</span><span class="sxs-lookup"><span data-stu-id="d6e65-409">Syntax highlights: Data Lake Tools uses different colors to differentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Data Lake Tools voor Visual Studio Code syntaxis highlights](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="d6e65-411">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d6e65-411">Next steps</span></span>

- <span data-ttu-id="d6e65-412">Zie voor U-SQL lokaal uitvoeren en lokale foutopsporing met Visual Studio Code [U-SQL lokaal uitvoeren en lokale foutopsporing met Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="d6e65-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="d6e65-413">Zie voor informatie over Data Lake Analytics aan de slag [zelfstudie: aan de slag met Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d6e65-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="d6e65-414">Zie voor meer informatie over Data Lake Tools voor Visual Studio [zelfstudie: U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d6e65-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="d6e65-415">Zie voor meer informatie over het ontwikkelen van assembly's [ontwikkelen van U-SQL-assembly's voor Azure Data Lake Analytics-taken](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="d6e65-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



