---
title: Azure Access Configuratiescherm extensie voor IE met behulp van een groepsbeleidsobject implementeren | Microsoft Docs
description: Het gebruik van Groepsbeleid voor het implementeren van de invoegtoepassing Internet Explorer voor de portal mijn Apps.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b402ae326ab34ec71ad9de966e22be00045fee3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-deploy-the-access-panel-extension-for-internet-explorer-using-group-policy"></a><span data-ttu-id="47fcf-103">De extensie van het Configuratiescherm toegang voor Internet Explorer met behulp van Groepsbeleid implementeren</span><span class="sxs-lookup"><span data-stu-id="47fcf-103">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>
<span data-ttu-id="47fcf-104">Deze zelfstudie laat zien hoe het gebruik van Groepsbeleid op afstand installeren van de extensie Toegangspaneel voor Internet Explorer op uw gebruikers-machines.</span><span class="sxs-lookup"><span data-stu-id="47fcf-104">This tutorial shows how to use group policy to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span> <span data-ttu-id="47fcf-105">Deze uitbreiding is vereist voor Internet Explorer-gebruikers hoeven zich aanmeldt bij apps die zijn geconfigureerd met [op basis van wachtwoorden eenmalige aanmelding](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="47fcf-105">This extension is required for Internet Explorer users who need to sign into apps that are configured using [password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

<span data-ttu-id="47fcf-106">Het is raadzaam dat beheerders de implementatie van deze extensie automatiseren.</span><span class="sxs-lookup"><span data-stu-id="47fcf-106">It is recommended that admins automate the deployment of this extension.</span></span> <span data-ttu-id="47fcf-107">Gebruikers hebben anders downloaden en installeren van de extensie zelf, die is kwetsbaar voor gebruikersfouten en zijn beheerdersrechten vereist.</span><span class="sxs-lookup"><span data-stu-id="47fcf-107">Otherwise, users have to download and install the extension themselves, which is prone to user error and requires administrator permissions.</span></span> <span data-ttu-id="47fcf-108">Deze zelfstudie bevat één methode voor het software-implementaties automatiseren met behulp van Groepsbeleid.</span><span class="sxs-lookup"><span data-stu-id="47fcf-108">This tutorial covers one method of automating software deployments by using group policy.</span></span> [<span data-ttu-id="47fcf-109">Meer informatie over Groepsbeleid.</span><span class="sxs-lookup"><span data-stu-id="47fcf-109">Learn more about group policy.</span></span>](https://technet.microsoft.com/windowsserver/bb310732.aspx)

<span data-ttu-id="47fcf-110">De extensie Toegangspaneel is ook beschikbaar voor [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) en [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), geen van beide vereist beheerdersmachtigingen om te installeren.</span><span class="sxs-lookup"><span data-stu-id="47fcf-110">The Access Panel extension is also available for [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) and [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), neither of which require administrator permissions to install.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47fcf-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="47fcf-111">Prerequisites</span></span>
* <span data-ttu-id="47fcf-112">U hebt ingesteld [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), en u hebt uw gebruikers machines toegevoegd aan uw domein.</span><span class="sxs-lookup"><span data-stu-id="47fcf-112">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>
* <span data-ttu-id="47fcf-113">U moet de machtiging 'Instellingen bewerken' voor het bewerken van het groepsbeleidsobject (GPO) hebben.</span><span class="sxs-lookup"><span data-stu-id="47fcf-113">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="47fcf-114">Standaard hebben leden van de volgende beveiligingsgroepen deze machtiging: Domeinadministrators, Ondernemingsadministrators en Maker Eigenaar Groepsbeleid.</span><span class="sxs-lookup"><span data-stu-id="47fcf-114">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> [<span data-ttu-id="47fcf-115">Meer informatie.</span><span class="sxs-lookup"><span data-stu-id="47fcf-115">Learn more.</span></span>](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-the-distribution-point"></a><span data-ttu-id="47fcf-116">Stap 1: Het distributiepunt maken</span><span class="sxs-lookup"><span data-stu-id="47fcf-116">Step 1: Create the Distribution Point</span></span>
<span data-ttu-id="47fcf-117">Eerst moet u het installer-pakket plaatsen op een netwerklocatie die toegankelijk zijn voor de machines die u de extensie wilt op afstand te installeren.</span><span class="sxs-lookup"><span data-stu-id="47fcf-117">First, you must place the installer package on a network location that can be accessed by the machines that you wish to remotely install the extension on.</span></span> <span data-ttu-id="47fcf-118">U doet dit door de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="47fcf-118">To do this, follow these steps:</span></span>

1. <span data-ttu-id="47fcf-119">Meld u aan bij de server als een beheerder</span><span class="sxs-lookup"><span data-stu-id="47fcf-119">Log on to the server as an administrator</span></span>
2. <span data-ttu-id="47fcf-120">In de **Serverbeheer** venster, gaat u naar **bestanden- en opslagservices**.</span><span class="sxs-lookup"><span data-stu-id="47fcf-120">In the **Server Manager** window, go to **Files and Storage Services**.</span></span>
   
    ![Geopende bestanden- en opslagservices](./media/active-directory-saas-ie-group-policy/files-services.png)
3. <span data-ttu-id="47fcf-122">Ga naar de **Shares** tabblad. Klik vervolgens op **taken** > **nieuwe Share...**</span><span class="sxs-lookup"><span data-stu-id="47fcf-122">Go to the **Shares** tab. Then click **Tasks** > **New Share...**</span></span>
   
    ![Geopende bestanden- en opslagservices](./media/active-directory-saas-ie-group-policy/shares.png)
4. <span data-ttu-id="47fcf-124">Voltooi de **Wizard Nieuwe Share** en stel de machtigingen om ervoor te zorgen dat deze kan worden geopend op uw gebruikers-machines.</span><span class="sxs-lookup"><span data-stu-id="47fcf-124">Complete the **New Share Wizard** and set permissions to ensure that it can be accessed from your users' machines.</span></span> [<span data-ttu-id="47fcf-125">Meer informatie over shares.</span><span class="sxs-lookup"><span data-stu-id="47fcf-125">Learn more about shares.</span></span>](https://technet.microsoft.com/library/cc753175.aspx)
5. <span data-ttu-id="47fcf-126">De volgende Microsoft Windows Installer-pakket (MSI-bestand) te downloaden: [toegang Configuratiescherm Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span><span class="sxs-lookup"><span data-stu-id="47fcf-126">Download the following Microsoft Windows Installer package (.msi file): [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span></span>
6. <span data-ttu-id="47fcf-127">Kopieer het installatiepakket op de gewenste locatie op de share.</span><span class="sxs-lookup"><span data-stu-id="47fcf-127">Copy the installer package to a desired location on the share.</span></span>
   
    ![Kopieer het MSI-bestand naar de share.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. <span data-ttu-id="47fcf-129">Controleer of uw clientcomputers toegang kunnen krijgen tot het installatiepakket van de share.</span><span class="sxs-lookup"><span data-stu-id="47fcf-129">Verify that your client machines are able to access the installer package from the share.</span></span> 

## <a name="step-2-create-the-group-policy-object"></a><span data-ttu-id="47fcf-130">Stap 2: Het groepsbeleidsobject maken</span><span class="sxs-lookup"><span data-stu-id="47fcf-130">Step 2: Create the Group Policy Object</span></span>
1. <span data-ttu-id="47fcf-131">Meld u bij de server die als host fungeert voor de installatie van Active Directory Domain Services (AD DS).</span><span class="sxs-lookup"><span data-stu-id="47fcf-131">Log on to the server that hosts your Active Directory Domain Services (AD DS) installation.</span></span>
2. <span data-ttu-id="47fcf-132">In Serverbeheer gaat u naar **extra** > **Group Policy Management**.</span><span class="sxs-lookup"><span data-stu-id="47fcf-132">In the Server Manager, go to **Tools** > **Group Policy Management**.</span></span>
   
    ![Ga naar Extra > beleid Management groep](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. <span data-ttu-id="47fcf-134">Klik in het linkerdeelvenster van de **Group Policy Management** venster weergeven van uw hiërarchie van organisatie-eenheid (OE) en bepalen bij welke bereik wilt u het groepsbeleid van toepassing.</span><span class="sxs-lookup"><span data-stu-id="47fcf-134">In the left pane of the **Group Policy Management** window, view your Organizational Unit (OU) hierarchy and determine at which scope you would like to apply the group policy.</span></span> <span data-ttu-id="47fcf-135">Bijvoorbeeld, u kiest een kleine organisatie-eenheid voor het implementeren van een paar gebruikers voor het testen van besluiten of kiest u een site op het hoogste organisatie-eenheid om te implementeren voor uw hele organisatie.</span><span class="sxs-lookup"><span data-stu-id="47fcf-135">For instance, you may decide to pick a small OU to deploy to a few users for testing, or you may pick a top-level OU to deploy to your entire organization.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="47fcf-136">Als u wilt maken of bewerken van uw organisatie-eenheden (OE's), Ga terug naar de Server Manager en gaat u naar **extra** > **Active Directory: gebruikers en Computers**.</span><span class="sxs-lookup"><span data-stu-id="47fcf-136">If you would like to create or edit your Organization Units (OUs), switch back to the Server Manager and go to **Tools** > **Active Directory Users and Computers**.</span></span>
   > 
   > 
4. <span data-ttu-id="47fcf-137">Nadat u een organisatie-eenheid hebt geselecteerd, met de rechtermuisknop en selecteer **een groepsbeleidsobject in dit domein maken en hier een koppeling...**</span><span class="sxs-lookup"><span data-stu-id="47fcf-137">Once you have selected an OU, right-click it and select **Create a GPO in this domain, and Link it here...**</span></span>
   
    ![Een nieuw groepsbeleidsobject maken](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. <span data-ttu-id="47fcf-139">In de **nieuw groepsbeleidsobject** modus, typt u een naam voor het nieuwe groepsbeleidsobject.</span><span class="sxs-lookup"><span data-stu-id="47fcf-139">In the **New GPO** prompt, type in a name for the new Group Policy Object.</span></span>
   
    ![De naam van het nieuwe groepsbeleidsobject](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. <span data-ttu-id="47fcf-141">Met de rechtermuisknop op het groepsbeleidsobject dat u maakte en selecteer **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="47fcf-141">Right-click the Group Policy Object that you created, and select **Edit**.</span></span>
   
    ![Het nieuwe groepsbeleidsobject bewerken](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-the-installation-package"></a><span data-ttu-id="47fcf-143">Stap 3: Het installatiepakket toewijzen</span><span class="sxs-lookup"><span data-stu-id="47fcf-143">Step 3: Assign the Installation Package</span></span>
1. <span data-ttu-id="47fcf-144">Bepalen of u dat wilt voor het implementeren van de extensie op basis van **Computerconfiguratie** of **Gebruikersconfiguratie**.</span><span class="sxs-lookup"><span data-stu-id="47fcf-144">Determine whether you would like to deploy the extension based on **Computer Configuration** or **User Configuration**.</span></span> <span data-ttu-id="47fcf-145">Wanneer u [Computerconfiguratie](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), de extensie wordt geïnstalleerd op de computer ongeacht welke gebruikers zich aanmelden bij deze.</span><span class="sxs-lookup"><span data-stu-id="47fcf-145">When using [computer configuration](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), the extension is installed on the computer regardless of which users log on to it.</span></span> <span data-ttu-id="47fcf-146">Met [Gebruikersconfiguratie](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), gebruikers hebben de extensie die is geïnstalleerd voor deze ongeacht welke computers ze zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="47fcf-146">With [user configuration](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), users have the extension installed for them regardless of which computers they log on to.</span></span>
2. <span data-ttu-id="47fcf-147">Klik in het linkerdeelvenster van de **Editor voor Groepsbeleidsbeheer** venster, gaat u naar een van de volgende paden voor mappen, afhankelijk van welk type van de configuratie die u hebt gekozen:</span><span class="sxs-lookup"><span data-stu-id="47fcf-147">In the left pane of the **Group Policy Management Editor** window, go to either of the following folder paths, depending on which type of configuration you chose:</span></span>
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. <span data-ttu-id="47fcf-148">Met de rechtermuisknop op **Software-installatie**, selecteer daarna **nieuw** > **pakket...**</span><span class="sxs-lookup"><span data-stu-id="47fcf-148">Right-click **Software installation**, then select **New** > **Package...**</span></span>
   
    ![Maak een nieuw pakket van de software-installatie](./media/active-directory-saas-ie-group-policy/new-package.png)
4. <span data-ttu-id="47fcf-150">Ga naar de gedeelde map met het installer-pakket van [stap 1: maken van het distributiepunt](#step-1-create-the-distribution-point), selecteert u het .msi-bestand en klik op **Open**.</span><span class="sxs-lookup"><span data-stu-id="47fcf-150">Go to the shared folder that contains the installer package from [Step 1: Create the Distribution Point](#step-1-create-the-distribution-point), select the .msi file, and click **Open**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="47fcf-151">Als de share bevindt zich op deze server, controleert u of u de .msi opent via het netwerk-bestandspad in plaats van het lokale bestandspad.</span><span class="sxs-lookup"><span data-stu-id="47fcf-151">If the share is located on this same server, verify that you are accessing the .msi through the network file path, rather than the local file path.</span></span>
   > 
   > 
   
    ![Selecteer het installatiepakket uit de gedeelde map.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. <span data-ttu-id="47fcf-153">In de **Software distribueren** vragen, selecteer **toegewezen** voor uw implementatiemethode.</span><span class="sxs-lookup"><span data-stu-id="47fcf-153">In the **Deploy Software** prompt, select **Assigned** for your deployment method.</span></span> <span data-ttu-id="47fcf-154">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="47fcf-154">Then click **OK**.</span></span>
   
    ![Selecteer toegewezen en klik op OK.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

<span data-ttu-id="47fcf-156">De extensie is nu geïmplementeerd op de organisatie-eenheid die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="47fcf-156">The extension is now deployed to the OU that you selected.</span></span> [<span data-ttu-id="47fcf-157">Meer informatie over Software-installatie.</span><span class="sxs-lookup"><span data-stu-id="47fcf-157">Learn more about Group Policy Software Installation.</span></span>](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-the-extension-for-internet-explorer"></a><span data-ttu-id="47fcf-158">Stap 4: Automatisch inschakelen voor de uitbreiding voor Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="47fcf-158">Step 4: Auto-Enable the Extension for Internet Explorer</span></span>
<span data-ttu-id="47fcf-159">Naast het installatieprogramma wordt uitgevoerd, moet alle uitbreidingen voor Internet Explorer ingeschakeld zijn voordat deze kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="47fcf-159">In addition to running the installer, every extension for Internet Explorer must be explicitly enabled before it can be used.</span></span> <span data-ttu-id="47fcf-160">Volg onderstaande stappen voor het inschakelen van de uitbreiding van het Configuratiescherm toegang met behulp van Groepsbeleid:</span><span class="sxs-lookup"><span data-stu-id="47fcf-160">Follow the steps below to enable the Access Panel Extension using group policy:</span></span>

1. <span data-ttu-id="47fcf-161">In de **Editor voor Groepsbeleidsbeheer** venster, gaat u naar een van de volgende paden, afhankelijk van welk type van de configuratie die u kiest in [stap 3: het installatiepakket toewijzen](#step-3-assign-the-installation-package):</span><span class="sxs-lookup"><span data-stu-id="47fcf-161">In the **Group Policy Management Editor** window, go to either of the following paths, depending on which type of configuration you chose in [Step 3: Assign the Installation Package](#step-3-assign-the-installation-package):</span></span>
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. <span data-ttu-id="47fcf-162">Met de rechtermuisknop op **lijst met invoegtoepassingen**, en selecteer **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="47fcf-162">Right-click **Add-on List**, and select **Edit**.</span></span>
    <span data-ttu-id="47fcf-163">![Invoegtoepassing lijst niet bewerken.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span><span class="sxs-lookup"><span data-stu-id="47fcf-163">![Edit Add-on List.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span></span>
3. <span data-ttu-id="47fcf-164">In de **lijst met invoegtoepassingen** Selecteer **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="47fcf-164">In the **Add-on List** window, select **Enabled**.</span></span> <span data-ttu-id="47fcf-165">Klik vervolgens onder de **opties** sectie, klikt u op **weergeven...** .</span><span class="sxs-lookup"><span data-stu-id="47fcf-165">Then, under the **Options** section, click **Show...**.</span></span>
   
    ![Klik op inschakelen en klik vervolgens op weergeven...](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. <span data-ttu-id="47fcf-167">In de **inhoud weergeven** venster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="47fcf-167">In the **Show Contents** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="47fcf-168">Voor de eerste kolom (de **waardenaam** veld), kopiëren en plakken van de volgende klasse-ID:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span><span class="sxs-lookup"><span data-stu-id="47fcf-168">For the first column (the **Value Name** field), copy and paste the following Class ID: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span></span>
   2. <span data-ttu-id="47fcf-169">Voor de tweede kolom (de **waarde** veld), typt u de volgende waarde:`1`</span><span class="sxs-lookup"><span data-stu-id="47fcf-169">For the second column (the **Value** field), type in the following value: `1`</span></span>
   3. <span data-ttu-id="47fcf-170">Klik op **OK** sluiten de **inhoud weergeven** venster.</span><span class="sxs-lookup"><span data-stu-id="47fcf-170">Click **OK** to close the **Show Contents** window.</span></span>
      
      ![Vul de parameterwaarden als is beschreven.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. <span data-ttu-id="47fcf-172">Klik op **OK** naar uw wijzigingen toepassen op en sluit de **lijst met invoegtoepassingen** venster.</span><span class="sxs-lookup"><span data-stu-id="47fcf-172">Click **OK** to apply your changes and close the **Add-on List** window.</span></span>

<span data-ttu-id="47fcf-173">De extensie moet nu worden ingeschakeld voor de machines in de geselecteerde OE.</span><span class="sxs-lookup"><span data-stu-id="47fcf-173">The extension should now be enabled for the machines in the selected OU.</span></span> [<span data-ttu-id="47fcf-174">Meer informatie over het gebruik van Groepsbeleid inschakelen of uitschakelen van invoegtoepassingen voor Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="47fcf-174">Learn more about using group policy to enable or disable Internet Explorer add-ons.</span></span>](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a><span data-ttu-id="47fcf-175">Stap 5 (optioneel): 'Wachtwoord onthouden' Prompt uitschakelen</span><span class="sxs-lookup"><span data-stu-id="47fcf-175">Step 5 (Optional): Disable "Remember Password" Prompt</span></span>
<span data-ttu-id="47fcf-176">Wanneer gebruikers aanmelden naar websites met de extensie van het Configuratiescherm toegang, Internet Explorer op de volgende gevraagd 'Wilt u uw wachtwoord opslaan?' kan tonen</span><span class="sxs-lookup"><span data-stu-id="47fcf-176">When users sign-in to websites using the Access Panel Extension, Internet Explorer may show the following prompt asking "Would you like to store your password?"</span></span>

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

<span data-ttu-id="47fcf-177">Als u voorkomen dat uw gebruikers deze vraag te zien wilt, klikt u vervolgens de stappen hieronder om te voorkomen dat automatisch aanvullen van onthouden wachtwoorden:</span><span class="sxs-lookup"><span data-stu-id="47fcf-177">If you wish to prevent your users from seeing this prompt, then follow the steps below to prevent auto-complete from remembering passwords:</span></span>

1. <span data-ttu-id="47fcf-178">In de **Editor voor Groepsbeleidsbeheer** venster, gaat u naar het pad hieronder vermeld.</span><span class="sxs-lookup"><span data-stu-id="47fcf-178">In the **Group Policy Management Editor** window, go to the path listed below.</span></span> <span data-ttu-id="47fcf-179">Deze configuratieinstelling is alleen beschikbaar onder **Gebruikersconfiguratie**.</span><span class="sxs-lookup"><span data-stu-id="47fcf-179">This configuration setting is only available under **User Configuration**.</span></span>
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. <span data-ttu-id="47fcf-180">De instelling met de naam vinden **Schakel de functie voor automatisch aanvullen voor gebruikersnamen en wachtwoorden op formulieren**.</span><span class="sxs-lookup"><span data-stu-id="47fcf-180">Find the setting named **Turn on the auto-complete feature for user names and passwords on forms**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="47fcf-181">Eerdere versies van Active Directory kunnen deze instellingen met de naam van de lijst **niet toestaan dat wachtwoorden op te slaan automatisch aanvullen**.</span><span class="sxs-lookup"><span data-stu-id="47fcf-181">Previous versions of Active Directory may list this setting with the name **Do not allow auto-complete to save passwords**.</span></span> <span data-ttu-id="47fcf-182">De configuratie voor de instelling verschilt van de instelling die wordt beschreven in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="47fcf-182">The configuration for that setting differs from the setting described in this tutorial.</span></span>
   > 
   > 
   
    ![Vergeet niet om te zoeken voor dit onder gebruikersinstellingen.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. <span data-ttu-id="47fcf-184">Klik met de rechtermuisknop op de instelling hierboven en selecteer **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="47fcf-184">Right click the above setting, and select **Edit**.</span></span>
4. <span data-ttu-id="47fcf-185">In het venster met de titel **Schakel de functie voor automatisch aanvullen voor gebruikersnamen en wachtwoorden op formulieren**, selecteer **uitgeschakelde**.</span><span class="sxs-lookup"><span data-stu-id="47fcf-185">In the window titled **Turn on the auto-complete feature for user names and passwords on forms**, select **Disabled**.</span></span>
   
    ![Selecteer uitschakelen](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. <span data-ttu-id="47fcf-187">Klik op **OK** deze wijzigingen toepassen en sluit het venster.</span><span class="sxs-lookup"><span data-stu-id="47fcf-187">Click **OK** to apply these changes and close the window.</span></span>

<span data-ttu-id="47fcf-188">Gebruikers wordt niet langer hun referenties of automatisch aanvullen gebruiken voor toegang tot de eerder opgeslagen referenties op te slaan.</span><span class="sxs-lookup"><span data-stu-id="47fcf-188">Users will no longer be able to store their credentials or use auto-complete to access previously stored credentials.</span></span> <span data-ttu-id="47fcf-189">Dit beleid echter dat gebruikers om te blijven gebruiken automatisch aanvullen voor andere soorten formuliervelden, zoals zoeken.</span><span class="sxs-lookup"><span data-stu-id="47fcf-189">However, this policy does allow users to continue to use auto-complete for other types of form fields, such as search fields.</span></span>

> [!WARNING]
> <span data-ttu-id="47fcf-190">Als dit beleid is ingeschakeld, nadat gebruikers hebt gekozen voor het opslaan van sommige referenties, dit beleid wordt *niet* schakelt u de referenties die al zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="47fcf-190">If this policy is enabled after users have chosen to store some credentials, this policy will *not* clear the credentials that have already been stored.</span></span>
> 
> 

## <a name="step-6-testing-the-deployment"></a><span data-ttu-id="47fcf-191">Stap 6: De implementatie testen</span><span class="sxs-lookup"><span data-stu-id="47fcf-191">Step 6: Testing the Deployment</span></span>
<span data-ttu-id="47fcf-192">De volgende stappen om te controleren of de implementatie van de uitbreiding geslaagd is:</span><span class="sxs-lookup"><span data-stu-id="47fcf-192">Follow the steps below to verify if the extension deployment was successful:</span></span>

1. <span data-ttu-id="47fcf-193">Als u hebt geïmplementeerd met behulp van **Computerconfiguratie**, meld u aan bij een clientcomputer die deel uitmaakt van de organisatie-eenheid die u hebt geselecteerd in [stap 2: het groepsbeleidsobject maken](#step-2-create-the-group-policy-object).</span><span class="sxs-lookup"><span data-stu-id="47fcf-193">If you deployed using **Computer Configuration**, sign into a client machine that belongs to the OU that you selected in [Step 2: Create the Group Policy Object](#step-2-create-the-group-policy-object).</span></span> <span data-ttu-id="47fcf-194">Als u hebt geïmplementeerd met behulp van **Gebruikersconfiguratie**, zorg ervoor dat u zich aanmelden als een gebruiker die lid is van organisatie-eenheid.</span><span class="sxs-lookup"><span data-stu-id="47fcf-194">If you deployed using **User Configuration**, make sure to sign in as a user who belongs to that OU.</span></span>
2. <span data-ttu-id="47fcf-195">Het duurt een paar aanmelding modules voor het groepsbeleid wijzigt volledig bijwerken met deze machine.</span><span class="sxs-lookup"><span data-stu-id="47fcf-195">It may take a couple sign ins for the group policy changes to fully update with this machine.</span></span> <span data-ttu-id="47fcf-196">Als u wilt dat de update, opent u een **opdrachtprompt** venster en voer de volgende opdracht:`gpupdate /force`</span><span class="sxs-lookup"><span data-stu-id="47fcf-196">To force the update, open a **Command Prompt** window and run the following command: `gpupdate /force`</span></span>
3. <span data-ttu-id="47fcf-197">De computer voor de installatie te kunnen uitvoeren, moet u opnieuw.</span><span class="sxs-lookup"><span data-stu-id="47fcf-197">You must restart the machine for the installation to take place.</span></span> <span data-ttu-id="47fcf-198">Wanneer kan aanzienlijk langer duren dan normaal tijdens de uitbreiding wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="47fcf-198">Bootup may take significantly more time than usual while the extension installs.</span></span>
4. <span data-ttu-id="47fcf-199">Start opnieuw op en open **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="47fcf-199">After restarting, open **Internet Explorer**.</span></span> <span data-ttu-id="47fcf-200">Klik in de rechterbovenhoek van het venster op **extra** (het tandwielpictogram pictogram), en selecteer vervolgens **invoegtoepassingen beheren**.</span><span class="sxs-lookup"><span data-stu-id="47fcf-200">On the upper-right corner of the window, click **Tools** (the gear icon), and then select **Manage add-ons**.</span></span>
   
    ![Ga naar Extra > invoegtoepassingen beheren](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. <span data-ttu-id="47fcf-202">In de **invoegtoepassingen beheren** venster controleren of de **Configuratiescherm-uitbreiding voor toegang tot** is geïnstalleerd en dat de **Status** is ingesteld op **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="47fcf-202">In the **Manage Add-ons** window, verify that the **Access Panel Extension** has been installed and that its **Status** has been set to **Enabled**.</span></span>
   
    ![Controleer of de uitbreiding van het Configuratiescherm toegang is geïnstalleerd en is ingeschakeld.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a><span data-ttu-id="47fcf-204">Verwante artikelen</span><span class="sxs-lookup"><span data-stu-id="47fcf-204">Related Articles</span></span>
* <span data-ttu-id="47fcf-205">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="47fcf-205">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* [<span data-ttu-id="47fcf-206">Toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47fcf-206">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="47fcf-207">De uitbreiding van het deelvenster toegang tot het oplossen van problemen voor Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="47fcf-207">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>](active-directory-saas-ie-troubleshooting.md)

