---
title: Extern verbinding maken met uw StorSimple-apparaat | Microsoft Docs
description: Legt uit hoe u uw apparaat voor extern beheer configureren en verbinding maken met Windows PowerShell voor StorSimple via HTTP of HTTPS.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b916173e127394d3ea06eded36285bdbbf884b12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-remotely-to-your-storsimple-8000-series-device"></a><span data-ttu-id="d0b18-103">Extern verbinding maken met uw StorSimple 8000 series apparaat</span><span class="sxs-lookup"><span data-stu-id="d0b18-103">Connect remotely to your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="d0b18-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d0b18-104">Overview</span></span>
<span data-ttu-id="d0b18-105">U kunt Windows PowerShell op afstand verbinding maken met uw StorSimple-apparaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d0b18-105">You can use Windows PowerShell remoting to connect to your StorSimple device.</span></span> <span data-ttu-id="d0b18-106">Als u op deze manier verbinding, ziet u een menu.</span><span class="sxs-lookup"><span data-stu-id="d0b18-106">When you connect this way, you will not see a menu.</span></span> <span data-ttu-id="d0b18-107">(Ziet u een menu alleen als u de seriële console op het apparaat om verbinding te gebruiken.) Met Windows PowerShell op afstand verbinding u met een specifieke runspace.</span><span class="sxs-lookup"><span data-stu-id="d0b18-107">(You see a menu only if you use the serial console on the device to connect.) With Windows PowerShell remoting, you connect to a specific runspace.</span></span> <span data-ttu-id="d0b18-108">U kunt ook de weergavetaal opgeven.</span><span class="sxs-lookup"><span data-stu-id="d0b18-108">You can also specify the display language.</span></span> 

<span data-ttu-id="d0b18-109">Voor meer informatie over het beheren van uw apparaat met Windows PowerShell op afstand, gaat u naar [gebruik Windows PowerShell voor StorSimple voor het beheren van uw StorSimple-apparaat](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d0b18-109">For more information about using Windows PowerShell remoting to manage your device, go to [Use Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>

<span data-ttu-id="d0b18-110">Deze zelfstudie wordt uitgelegd hoe u uw apparaat voor extern beheer configureren en vervolgens verbinding maken met Windows PowerShell voor StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d0b18-110">This tutorial explains how to configure your device for remote management and then how to connect to Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="d0b18-111">U kunt HTTP of HTTPS gebruiken via Windows PowerShell op afstand te verbinden.</span><span class="sxs-lookup"><span data-stu-id="d0b18-111">You can use HTTP or HTTPS to connect via Windows PowerShell remoting.</span></span> <span data-ttu-id="d0b18-112">Echter, wanneer u verbinding maken met Windows PowerShell voor StorSimple beslist, het volgende overwegen:</span><span class="sxs-lookup"><span data-stu-id="d0b18-112">However, when you are deciding how to connect to Windows PowerShell for StorSimple, consider the following:</span></span> 

* <span data-ttu-id="d0b18-113">Rechtstreeks verbinding maken met de seriële console van het apparaat is beveiligd, maar geen verbinding maken met de seriële console via netwerkswitches is.</span><span class="sxs-lookup"><span data-stu-id="d0b18-113">Connecting directly to the device serial console is secure, but connecting to the serial console over network switches is not.</span></span> <span data-ttu-id="d0b18-114">Wees voorzichtig met over de beveiligingsrisico's het verbinding maken met de seriële console van het apparaat via netwerkswitches.</span><span class="sxs-lookup"><span data-stu-id="d0b18-114">Be cautious of the security risk when connecting to the device serial console over network switches.</span></span> 
* <span data-ttu-id="d0b18-115">Verbinding maken via een HTTP-sessie, is het mogelijk bieden meer beveiliging dan verbinding maken via de seriële console via het netwerk.</span><span class="sxs-lookup"><span data-stu-id="d0b18-115">Connecting through an HTTP session might offer more security than connecting through the serial console over the network.</span></span> <span data-ttu-id="d0b18-116">Hoewel dit niet de meest beveiligde methode, is het is acceptabel in vertrouwde netwerken.</span><span class="sxs-lookup"><span data-stu-id="d0b18-116">Although this is not the most secure method, it is acceptable on trusted networks.</span></span> 
* <span data-ttu-id="d0b18-117">Verbinding maken via een HTTPS-sessie met een zelfondertekend certificaat is de veiligste en de aanbevolen optie.</span><span class="sxs-lookup"><span data-stu-id="d0b18-117">Connecting through an HTTPS session with a self-signed certificate is the most secure and the recommended option.</span></span>

<span data-ttu-id="d0b18-118">U kunt op afstand verbinden met de Windows PowerShell-interface.</span><span class="sxs-lookup"><span data-stu-id="d0b18-118">You can connect remotely to the Windows PowerShell interface.</span></span> <span data-ttu-id="d0b18-119">Externe toegang tot uw StorSimple-apparaat via de Windows PowerShell-interface wordt echter niet standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d0b18-119">However, remote access to your StorSimple device via the Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="d0b18-120">U moet eerst extern beheer op het apparaat inschakelen en klik vervolgens op de client die wordt gebruikt voor toegang tot uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="d0b18-120">You need to enable remote management on the device first, and then on the client that is used to access your device.</span></span>

<span data-ttu-id="d0b18-121">De stappen in dit artikel zijn uitgevoerd op een hostsysteem met Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="d0b18-121">The steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="d0b18-122">Verbinding maken via HTTP</span><span class="sxs-lookup"><span data-stu-id="d0b18-122">Connect through HTTP</span></span>
<span data-ttu-id="d0b18-123">Verbinding maken met Windows PowerShell voor StorSimple via een HTTP-sessie, biedt betere beveiliging dan verbinding maken via de seriële console van uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="d0b18-123">Connecting to Windows PowerShell for StorSimple through an HTTP session offers more security than connecting through the serial console of your StorSimple device.</span></span> <span data-ttu-id="d0b18-124">Hoewel dit niet de meest beveiligde methode, is het is acceptabel in vertrouwde netwerken.</span><span class="sxs-lookup"><span data-stu-id="d0b18-124">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="d0b18-125">U kunt de klassieke Azure portal of de seriële console extern beheer configureren.</span><span class="sxs-lookup"><span data-stu-id="d0b18-125">You can use either the Azure classic portal or the serial console to configure remote management.</span></span> <span data-ttu-id="d0b18-126">Selecteer in de volgende procedures:</span><span class="sxs-lookup"><span data-stu-id="d0b18-126">Select from the following procedures:</span></span>

* [<span data-ttu-id="d0b18-127">Gebruik de klassieke Azure portal extern beheer inschakelen via HTTP</span><span class="sxs-lookup"><span data-stu-id="d0b18-127">Use the Azure classic portal to enable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="d0b18-128">Gebruik de seriële console extern beheer inschakelen via HTTP</span><span class="sxs-lookup"><span data-stu-id="d0b18-128">Use the serial console to enable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="d0b18-129">Nadat u extern beheer inschakelen, gebruik de volgende procedure voor het voorbereiden van de client voor een externe verbinding.</span><span class="sxs-lookup"><span data-stu-id="d0b18-129">After you enable remote management, use the following procedure to prepare the client for a remote connection.</span></span>

* [<span data-ttu-id="d0b18-130">De client voorbereiden voor externe verbinding</span><span class="sxs-lookup"><span data-stu-id="d0b18-130">Prepare the client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-the-azure-classic-portal-to-enable-remote-management-over-http"></a><span data-ttu-id="d0b18-131">Gebruik de klassieke Azure portal extern beheer inschakelen via HTTP</span><span class="sxs-lookup"><span data-stu-id="d0b18-131">Use the Azure classic portal to enable remote management over HTTP</span></span>
<span data-ttu-id="d0b18-132">Voer de volgende stappen uit in de klassieke Azure portal extern beheer inschakelen via HTTP.</span><span class="sxs-lookup"><span data-stu-id="d0b18-132">Perform the following steps in the Azure classic portal to enable remote management over HTTP.</span></span>

#### <a name="to-enable-remote-management-through-the-azure-classic-portal"></a><span data-ttu-id="d0b18-133">Extern beheer via de klassieke Azure portal inschakelen</span><span class="sxs-lookup"><span data-stu-id="d0b18-133">To enable remote management through the Azure classic portal</span></span>
1. <span data-ttu-id="d0b18-134">Toegang **apparaten** > **configureren** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="d0b18-134">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="d0b18-135">Schuif omlaag naar het gedeelte **Extern beheer**.</span><span class="sxs-lookup"><span data-stu-id="d0b18-135">Scroll down to the **Remote Management** section.</span></span>
3. <span data-ttu-id="d0b18-136">Stel **Extern beheer inschakelen** in op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="d0b18-136">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="d0b18-137">U kunt nu verbinding maken via HTTP.</span><span class="sxs-lookup"><span data-stu-id="d0b18-137">You can now choose to connect using HTTP.</span></span> <span data-ttu-id="d0b18-138">(De standaardinstelling is verbinding maken via HTTPS.) Zorg ervoor dat HTTP is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="d0b18-138">(The default is to connect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d0b18-139">Verbinding maken via HTTP is alleen acceptabel in vertrouwde netwerken.</span><span class="sxs-lookup"><span data-stu-id="d0b18-139">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   > 
   > 
5. <span data-ttu-id="d0b18-140">Klik op **Opslaan** onder aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="d0b18-140">Click **Save** at the bottom of the page.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-http"></a><span data-ttu-id="d0b18-141">Gebruik de seriële console extern beheer inschakelen via HTTP</span><span class="sxs-lookup"><span data-stu-id="d0b18-141">Use the serial console to enable remote management over HTTP</span></span>
<span data-ttu-id="d0b18-142">De volgende stappen uitvoeren op de seriële console van het apparaat extern beheer inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d0b18-142">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="d0b18-143">Extern beheer via de seriële console van het apparaat inschakelen</span><span class="sxs-lookup"><span data-stu-id="d0b18-143">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="d0b18-144">Selecteer in het menu seriële console optie 1.</span><span class="sxs-lookup"><span data-stu-id="d0b18-144">On the serial console menu, select option 1.</span></span> <span data-ttu-id="d0b18-145">Voor meer informatie over het gebruik van de seriële console op het apparaat, gaat u naar [verbinding maken met Windows PowerShell voor StorSimple via de seriële console apparaat](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d0b18-145">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="d0b18-146">Typ het volgende bij de opdrachtprompt:`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="d0b18-146">At the prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="d0b18-147">U ontvangt een melding over de beveiligingsproblemen van het gebruik van HTTP verbinding maken met het apparaat.</span><span class="sxs-lookup"><span data-stu-id="d0b18-147">You will be notified about the security vulnerabilities of using HTTP to connect to the device.</span></span> <span data-ttu-id="d0b18-148">Bevestig door op te geven wanneer u wordt gevraagd, **Y**.</span><span class="sxs-lookup"><span data-stu-id="d0b18-148">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="d0b18-149">Controleer of HTTP is ingeschakeld door te typen:`Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="d0b18-149">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="d0b18-150">Controleer de **RemoteManagementMode** veld bevat **HttpsAndHttpEnabled**. De volgende afbeelding ziet deze instellingen in de PuTTY.</span><span class="sxs-lookup"><span data-stu-id="d0b18-150">Verify that the **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![Seriële HTTPS en HTTP-ingeschakeld](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-the-client-for-remote-connection"></a><span data-ttu-id="d0b18-152">De client voorbereiden voor externe verbinding</span><span class="sxs-lookup"><span data-stu-id="d0b18-152">Prepare the client for remote connection</span></span>
<span data-ttu-id="d0b18-153">Voer de volgende stappen uit op de client extern beheer inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d0b18-153">Perform the following steps on the client to enable remote management.</span></span>

#### <a name="to-prepare-the-client-for-remote-connection"></a><span data-ttu-id="d0b18-154">De client voorbereiden voor externe verbinding</span><span class="sxs-lookup"><span data-stu-id="d0b18-154">To prepare the client for remote connection</span></span>
1. <span data-ttu-id="d0b18-155">Start een Windows PowerShell-sessie als administrator.</span><span class="sxs-lookup"><span data-stu-id="d0b18-155">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="d0b18-156">Typ de volgende opdracht het IP-adres van het StorSimple-apparaat toevoegen aan lijst met vertrouwde hosts van de client:</span><span class="sxs-lookup"><span data-stu-id="d0b18-156">Type the following command to add the IP address of the StorSimple device to the client’s trusted hosts list:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="d0b18-157">Vervang <*device_ip*> met het IP-adres van uw apparaat; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d0b18-157">Replace <*device_ip*> with the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="d0b18-158">Typ de volgende opdracht voor het opslaan van de referenties van het apparaat in een variabele:</span><span class="sxs-lookup"><span data-stu-id="d0b18-158">Type the following command to save the device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="d0b18-159">In het dialoogvenster dat wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="d0b18-159">In the dialog box that appears:</span></span>
   
   1. <span data-ttu-id="d0b18-160">Typ de gebruikersnaam in deze indeling: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="d0b18-160">Type the user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="d0b18-161">Typ het administrator-wachtwoord voor het apparaat dat is ingesteld wanneer het apparaat is geconfigureerd met de wizard setup.</span><span class="sxs-lookup"><span data-stu-id="d0b18-161">Type the device administrator password that was set when the device was configured with the setup wizard.</span></span> <span data-ttu-id="d0b18-162">Is het standaardwachtwoord *Wachtwoord1*.</span><span class="sxs-lookup"><span data-stu-id="d0b18-162">The default password is *Password1*.</span></span>
5. <span data-ttu-id="d0b18-163">Start een Windows PowerShell-sessie op het apparaat door deze opdracht te typen:</span><span class="sxs-lookup"><span data-stu-id="d0b18-163">Start a Windows PowerShell session on the device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="d0b18-164">Toevoegen als u wilt maken voor gebruik van een Windows PowerShell-sessie met het virtuele StorSimple-apparaat, de `–Port` parameter en geeft u de openbare poort die u hebt geconfigureerd in externe toegang voor virtueel StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="d0b18-164">To create a Windows PowerShell session for use with the StorSimple virtual device, append the `–Port` parameter and specify the public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   > 
   > 
   
     <span data-ttu-id="d0b18-165">U hebt op dit moment een actieve externe Windows PowerShell-sessie op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="d0b18-165">At this point, you should have an active remote Windows PowerShell session to the device.</span></span>
   
    ![Externe communicatie via HTTP met PowerShell](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="d0b18-167">Verbinding maken via HTTPS</span><span class="sxs-lookup"><span data-stu-id="d0b18-167">Connect through HTTPS</span></span>
<span data-ttu-id="d0b18-168">Verbinding maken met Windows PowerShell voor StorSimple via een HTTPS-sessie, is de veiligste en aanbevolen methode externe verbinding maken met uw Microsoft Azure StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="d0b18-168">Connecting to Windows PowerShell for StorSimple through an HTTPS session is the most secure and recommended method of remotely connecting to your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="d0b18-169">De volgende procedures wordt uitgelegd hoe voor het instellen van de seriële console en client-computers, zodat u HTTPS kunt verbinding maken met Windows PowerShell voor StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d0b18-169">The following procedures explain how to set up the serial console and client computers so that you can use HTTPS to connect to Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="d0b18-170">U kunt de klassieke Azure portal of de seriële console extern beheer configureren.</span><span class="sxs-lookup"><span data-stu-id="d0b18-170">You can use either the Azure classic portal or the serial console to configure remote management.</span></span> <span data-ttu-id="d0b18-171">Selecteer in de volgende procedures:</span><span class="sxs-lookup"><span data-stu-id="d0b18-171">Select from the following procedures:</span></span>

* [<span data-ttu-id="d0b18-172">Gebruik de klassieke Azure portal extern beheer inschakelen via HTTPS</span><span class="sxs-lookup"><span data-stu-id="d0b18-172">Use the Azure classic portal to enable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="d0b18-173">Gebruik de seriële console extern beheer inschakelen via HTTPS</span><span class="sxs-lookup"><span data-stu-id="d0b18-173">Use the serial console to enable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="d0b18-174">Nadat u extern beheer inschakelen, gebruikt u de volgende procedures voor het voorbereiden van de host voor een extern beheer en verbinding maken met het apparaat van de externe host.</span><span class="sxs-lookup"><span data-stu-id="d0b18-174">After you enable remote management, use the following procedures to prepare the host for a remote management and connect to the device from the remote host.</span></span>

* [<span data-ttu-id="d0b18-175">De host voorbereiden voor extern beheer</span><span class="sxs-lookup"><span data-stu-id="d0b18-175">Prepare the host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="d0b18-176">Verbinding maken met het apparaat van de externe host</span><span class="sxs-lookup"><span data-stu-id="d0b18-176">Connect to the device from the remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-the-azure-classic-portal-to-enable-remote-management-over-https"></a><span data-ttu-id="d0b18-177">Gebruik de klassieke Azure portal extern beheer inschakelen via HTTPS</span><span class="sxs-lookup"><span data-stu-id="d0b18-177">Use the Azure classic portal to enable remote management over HTTPS</span></span>
<span data-ttu-id="d0b18-178">Voer de volgende stappen uit in de klassieke Azure portal extern beheer inschakelen via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d0b18-178">Perform the following steps in the Azure classic portal to enable remote management over HTTPS.</span></span>

#### <a name="to-enable-remote-management-over-https-from-the-azure-classic-portal"></a><span data-ttu-id="d0b18-179">Extern beheer inschakelen via HTTPS vanaf de klassieke Azure portal</span><span class="sxs-lookup"><span data-stu-id="d0b18-179">To enable remote management over HTTPS from the Azure classic portal</span></span>
1. <span data-ttu-id="d0b18-180">Toegang **apparaten** > **configureren** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="d0b18-180">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="d0b18-181">Schuif omlaag naar het gedeelte **Extern beheer**.</span><span class="sxs-lookup"><span data-stu-id="d0b18-181">Scroll down to the **Remote Management** section.</span></span>
3. <span data-ttu-id="d0b18-182">Stel **Extern beheer inschakelen** in op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="d0b18-182">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="d0b18-183">U kunt nu verbinding maken via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d0b18-183">You can now choose to connect using HTTPS.</span></span> <span data-ttu-id="d0b18-184">(De standaardinstelling is verbinding maken via HTTPS.) Zorg ervoor dat HTTPS is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="d0b18-184">(The default is to connect over HTTPS.) Make sure that HTTPS is selected.</span></span> 
5. <span data-ttu-id="d0b18-185">Klik op **certificaat voor extern beheer downloaden**.</span><span class="sxs-lookup"><span data-stu-id="d0b18-185">Click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="d0b18-186">Geef een locatie voor dit bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="d0b18-186">Specify a location to save this file.</span></span> <span data-ttu-id="d0b18-187">U moet dit certificaat installeren op de client of hostcomputer computer die u gebruiken wilt voor het verbinding maken met het apparaat.</span><span class="sxs-lookup"><span data-stu-id="d0b18-187">You will need to install this certificate on the client or host computer that you will use to connect to the device.</span></span>
6. <span data-ttu-id="d0b18-188">Klik op **Opslaan** onder aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="d0b18-188">Click **Save** at the bottom of the page.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-https"></a><span data-ttu-id="d0b18-189">Gebruik de seriële console extern beheer inschakelen via HTTPS</span><span class="sxs-lookup"><span data-stu-id="d0b18-189">Use the serial console to enable remote management over HTTPS</span></span>
<span data-ttu-id="d0b18-190">De volgende stappen uitvoeren op de seriële console van het apparaat extern beheer inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d0b18-190">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="d0b18-191">Extern beheer via de seriële console van het apparaat inschakelen</span><span class="sxs-lookup"><span data-stu-id="d0b18-191">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="d0b18-192">Selecteer in het menu seriële console optie 1.</span><span class="sxs-lookup"><span data-stu-id="d0b18-192">On the serial console menu, select option 1.</span></span> <span data-ttu-id="d0b18-193">Voor meer informatie over het gebruik van de seriële console op het apparaat, gaat u naar [verbinding maken met Windows PowerShell voor StorSimple via de seriële console apparaat](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d0b18-193">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="d0b18-194">Typ het volgende bij de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="d0b18-194">At the prompt, type:</span></span> 
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="d0b18-195">Dit moet HTTPS inschakelen op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="d0b18-195">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="d0b18-196">Controleer of HTTPS is ingeschakeld door te typen:</span><span class="sxs-lookup"><span data-stu-id="d0b18-196">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="d0b18-197">Zorg ervoor dat de **RemoteManagementMode** veld bevat **HttpsEnabled**. De volgende afbeelding ziet deze instellingen in de PuTTY.</span><span class="sxs-lookup"><span data-stu-id="d0b18-197">Make sure that the **RemoteManagementMode** field shows **HttpsEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![Seriële HTTPS-functionaliteit](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="d0b18-199">Vanuit de uitvoer van `Get-HcsSystem`, Kopieer het serienummer van het apparaat en opslaan voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="d0b18-199">From the output of `Get-HcsSystem`, copy the serial number of the device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d0b18-200">Het serienummer wordt toegewezen aan de CN-naam in het certificaat.</span><span class="sxs-lookup"><span data-stu-id="d0b18-200">The serial number maps to the CN name in the certificate.</span></span>
   > 
   > 
5. <span data-ttu-id="d0b18-201">Een certificaat voor extern beheer verkrijgen door te typen:</span><span class="sxs-lookup"><span data-stu-id="d0b18-201">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="d0b18-202">Een certificaat voor de volgende strekking weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d0b18-202">A certificate similar to the following will appear.</span></span>
   
    ![Extern beheercertificaat ophalen](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="d0b18-204">Kopieer de gegevens in het certificaat van **---BEGIN CERTIFICATE---** naar **---EINDCERTIFICAAT---** in een teksteditor zoals Kladblok en sla deze op te geven als een .cer-bestand.</span><span class="sxs-lookup"><span data-stu-id="d0b18-204">Copy the information in the certificate from **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="d0b18-205">(Kopieert u dit bestand met de externe host bij het voorbereiden van de host.)</span><span class="sxs-lookup"><span data-stu-id="d0b18-205">(You will copy this file to your remote host when you prepare the host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d0b18-206">Als een nieuw certificaat worden gegenereerd, gebruiken de `Set-HcsRemoteManagementCert` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d0b18-206">To generate a new certificate, use the `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   > 
   > 

### <a name="prepare-the-host-for-remote-management"></a><span data-ttu-id="d0b18-207">De host voorbereiden voor extern beheer</span><span class="sxs-lookup"><span data-stu-id="d0b18-207">Prepare the host for remote management</span></span>
<span data-ttu-id="d0b18-208">Als u de computer voorbereiden voor een externe verbinding die gebruikmaakt van een HTTPS-sessie, kunt u de volgende procedures uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d0b18-208">To prepare the host computer for a remote connection that uses an HTTPS session, perform the following procedures:</span></span>

* <span data-ttu-id="d0b18-209">[Het cer-bestand importeren in het basisarchief van de client of de externe host](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="d0b18-209">[Import the .cer file into the root store of the client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="d0b18-210">[De serienummers van het apparaat toevoegen aan het hosts-bestand op de externe host](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="d0b18-210">[Add the device serial numbers to the hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="d0b18-211">Elk van deze procedures wordt hieronder beschreven.</span><span class="sxs-lookup"><span data-stu-id="d0b18-211">Each of these procedures is described below.</span></span>

#### <a name="to-import-the-certificate-on-the-remote-host"></a><span data-ttu-id="d0b18-212">Het certificaat op de externe host importeren</span><span class="sxs-lookup"><span data-stu-id="d0b18-212">To import the certificate on the remote host</span></span>
1. <span data-ttu-id="d0b18-213">Met de rechtermuisknop op het cer-bestand en selecteer **installeren certificaat**.</span><span class="sxs-lookup"><span data-stu-id="d0b18-213">Right-click the .cer file and select **Install certificate**.</span></span> <span data-ttu-id="d0b18-214">Hiermee wordt de Wizard Certificaat importeren gestart.</span><span class="sxs-lookup"><span data-stu-id="d0b18-214">This will start the Certificate Import Wizard.</span></span>
   
    ![Wizard Certificaat importeren 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="d0b18-216">Voor **archieflocatie**, selecteer **lokale Machine**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d0b18-216">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="d0b18-217">Selecteer **alle certificaten in het onderstaande archief plaatsen**, en klik vervolgens op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="d0b18-217">Select **Place all certificates in the following store**, and then click **Browse**.</span></span> <span data-ttu-id="d0b18-218">Navigeer naar het basisarchief van de externe host, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d0b18-218">Navigate to the root store of your remote host, and then click **Next**.</span></span>
   
    ![Wizard Certificaat importeren 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="d0b18-220">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="d0b18-220">Click **Finish**.</span></span> <span data-ttu-id="d0b18-221">Er verschijnt een bericht dat u het importeren is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="d0b18-221">A message that tells you that the import was successful appears.</span></span>
   
    ![Wizard Certificaat importeren 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="to-add-device-serial-numbers-to-the-remote-host"></a><span data-ttu-id="d0b18-223">Serienummers toevoegen aan de externe host</span><span class="sxs-lookup"><span data-stu-id="d0b18-223">To add device serial numbers to the remote host</span></span>
1. <span data-ttu-id="d0b18-224">Kladblok start als beheerder en open vervolgens het hosts-bestand dat zich bevindt op \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="d0b18-224">Start Notepad as an administrator, and then open the hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="d0b18-225">De volgende drie items toevoegen aan het hosts-bestand: **DATA 0-IP-adres**, **Controller 0 vast IP-adres**, en **Controller 1 vast IP-adres**.</span><span class="sxs-lookup"><span data-stu-id="d0b18-225">Add the following three entries to your hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="d0b18-226">Voer het serienummer van het apparaat dat u eerder hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d0b18-226">Enter the device serial number that you saved earlier.</span></span> <span data-ttu-id="d0b18-227">Toewijzing van het IP-adres zoals in de volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="d0b18-227">Map this to the IP address as shown in the following image.</span></span> <span data-ttu-id="d0b18-228">Voor Controller 0 en Controller 1 toevoegen **Controller0** en **Controller1** aan het einde van het serienummer (CN-naam).</span><span class="sxs-lookup"><span data-stu-id="d0b18-228">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at the end of the serial number (CN name).</span></span>
   
    ![CN-naam aan het hosts-bestand toe te voegen](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="d0b18-230">Sla het hosts-bestand.</span><span class="sxs-lookup"><span data-stu-id="d0b18-230">Save the hosts file.</span></span>

### <a name="connect-to-the-device-from-the-remote-host"></a><span data-ttu-id="d0b18-231">Verbinding maken met het apparaat van de externe host</span><span class="sxs-lookup"><span data-stu-id="d0b18-231">Connect to the device from the remote host</span></span>
<span data-ttu-id="d0b18-232">Gebruik Windows PowerShell- en SSL voor een sessie SSAdmin op uw apparaat vanaf een externe host of de client.</span><span class="sxs-lookup"><span data-stu-id="d0b18-232">Use Windows PowerShell and SSL to enter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="d0b18-233">De sessie SSAdmin wordt toegewezen aan de optie 1 in de [seriële console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu van uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="d0b18-233">The SSAdmin session maps to option 1 in the [serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="d0b18-234">De volgende procedure uitvoeren op de computer van waaruit u wilt maken van de externe verbinding met Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d0b18-234">Perform the following procedure on the computer from which you want to make the remote Windows PowerShell connection.</span></span>

#### <a name="to-enter-an-ssadmin-session-on-the-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="d0b18-235">Een sessie SSAdmin invoeren op het apparaat met behulp van Windows PowerShell- en SSL</span><span class="sxs-lookup"><span data-stu-id="d0b18-235">To enter an SSAdmin session on the device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="d0b18-236">Start een Windows PowerShell-sessie als administrator.</span><span class="sxs-lookup"><span data-stu-id="d0b18-236">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="d0b18-237">Het IP-adres van het apparaat toevoegen aan de vertrouwde hosts van de client door te typen:</span><span class="sxs-lookup"><span data-stu-id="d0b18-237">Add the device IP address to the client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="d0b18-238">Waarbij <*device_ip*> het IP-adres van uw apparaat is; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d0b18-238">Where <*device_ip*> is the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="d0b18-239">Een nieuwe referentie maken door te typen:</span><span class="sxs-lookup"><span data-stu-id="d0b18-239">Create a new credential by typing:</span></span> 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="d0b18-240">Waarbij <*IP-adres van het doelapparaat*> het IP-adres van de DATA 0 voor uw apparaat; bijvoorbeeld **10.126.173.90** zoals weergegeven in de voorgaande afbeelding van het hosts-bestand.</span><span class="sxs-lookup"><span data-stu-id="d0b18-240">Where <*IP of target device*> is the IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in the preceding image of the hosts file.</span></span> <span data-ttu-id="d0b18-241">Geef ook het administrator-wachtwoord voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="d0b18-241">Also, supply the administrator password for your device.</span></span>
4. <span data-ttu-id="d0b18-242">Een sessie maken door te typen:</span><span class="sxs-lookup"><span data-stu-id="d0b18-242">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="d0b18-243">Voor de parameter - ComputerName in de cmdlet, geeft u de <*serienummer van het doelapparaat*>.</span><span class="sxs-lookup"><span data-stu-id="d0b18-243">For the -ComputerName parameter in the cmdlet, provide the <*serial number of target device*>.</span></span> <span data-ttu-id="d0b18-244">Dit serienummer is toegewezen aan het IP-adres van de DATA 0 in het bestand hosts op de externe host; bijvoorbeeld: **SHX0991003G44MT** zoals weergegeven in de volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="d0b18-244">This serial number was mapped to the IP address of DATA 0 in the hosts file on your remote host; for example, **SHX0991003G44MT** as shown in the following image.</span></span>
5. <span data-ttu-id="d0b18-245">Type:</span><span class="sxs-lookup"><span data-stu-id="d0b18-245">Type:</span></span> 
   
     `Enter-PSSession $session`
6. <span data-ttu-id="d0b18-246">U moet wacht een paar minuten en vervolgens u worden verbonden met uw apparaat via HTTPS via SSL.</span><span class="sxs-lookup"><span data-stu-id="d0b18-246">You will need to wait a few minutes, and then you will be connected to your device via HTTPS over SSL.</span></span> <span data-ttu-id="d0b18-247">U ziet een bericht dat u bent verbonden met uw apparaat aangeeft.</span><span class="sxs-lookup"><span data-stu-id="d0b18-247">You will see a message that indicates you are connected to your device.</span></span>
   
    ![PowerShell voor externe toegang met behulp van HTTPS- en SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="d0b18-249">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d0b18-249">Next steps</span></span>
* <span data-ttu-id="d0b18-250">Meer informatie over [Windows PowerShell gebruiken voor het beheer van uw StorSimple-apparaat](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d0b18-250">Learn more about [using Windows PowerShell to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="d0b18-251">Meer informatie over [de StorSimple Manager-service gebruiken voor het beheer van uw StorSimple-apparaat](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d0b18-251">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

