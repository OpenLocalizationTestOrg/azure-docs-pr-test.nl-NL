## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="d05bf-101">Uw Raspberry Pi voorbereiden</span><span class="sxs-lookup"><span data-stu-id="d05bf-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="d05bf-102">Raspbian installeren</span><span class="sxs-lookup"><span data-stu-id="d05bf-102">Install Raspbian</span></span>

<span data-ttu-id="d05bf-103">Als dit de eerste keer dat u uw Pi frambozen gebruikt, moet u het Raspbian-besturingssysteem met behulp van NOOBS op de SD-kaart die is opgenomen in de kit installeren.</span><span class="sxs-lookup"><span data-stu-id="d05bf-103">If this is the first time you are using your Raspberry Pi, you need to install the Raspbian operating system using NOOBS on the SD card included in the kit.</span></span> <span data-ttu-id="d05bf-104">De [frambozen Pi Software handleiding] [ lnk-install-raspbian] wordt beschreven hoe u een besturingssysteem installeren op uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="d05bf-104">The [Raspberry Pi Software Guide][lnk-install-raspbian] describes how to install an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="d05bf-105">Deze zelfstudie wordt ervan uitgegaan dat u het besturingssysteem Raspbian op uw Pi frambozen hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="d05bf-105">This tutorial assumes you have installed the Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="d05bf-106">De SD-kaart die is opgenomen in de [Microsoft Azure IoT Starter Kit voor frambozen Pi 3] [ lnk-starter-kits] al NOOBS geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="d05bf-106">The SD card included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="d05bf-107">U kunt de Pi frambozen van deze kaart opstart en installeren van het besturingssysteem Raspbian.</span><span class="sxs-lookup"><span data-stu-id="d05bf-107">You can boot the Raspberry Pi from this card and choose to install the Raspbian OS.</span></span>

### <a name="set-up-the-hardware"></a><span data-ttu-id="d05bf-108">De hardware instellen</span><span class="sxs-lookup"><span data-stu-id="d05bf-108">Set up the hardware</span></span>

<span data-ttu-id="d05bf-109">Deze zelfstudie wordt gebruikgemaakt van de sensor BME280 is opgenomen in de [Microsoft Azure IoT Starter Kit voor frambozen Pi 3] [ lnk-starter-kits] telemetrische gegevens genereren.</span><span class="sxs-lookup"><span data-stu-id="d05bf-109">This tutorial uses the BME280 sensor included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] to generate telemetry data.</span></span> <span data-ttu-id="d05bf-110">Een LED wordt gebruikt om aan te geven wanneer de Pi frambozen verwerkt een methodeaanroep vanuit het dashboard van oplossing.</span><span class="sxs-lookup"><span data-stu-id="d05bf-110">It uses an LED to indicate when the Raspberry Pi processes a method invocation from the solution dashboard.</span></span>

<span data-ttu-id="d05bf-111">De onderdelen op het mededelingenbord brood zijn:</span><span class="sxs-lookup"><span data-stu-id="d05bf-111">The components on the bread board are:</span></span>

- <span data-ttu-id="d05bf-112">Rode LED</span><span class="sxs-lookup"><span data-stu-id="d05bf-112">Red LED</span></span>
- <span data-ttu-id="d05bf-113">220 Ohm weerstand (rood, rood, bruine)</span><span class="sxs-lookup"><span data-stu-id="d05bf-113">220-Ohm resistor (red, red, brown)</span></span>
- <span data-ttu-id="d05bf-114">BME280-temperatuursensor</span><span class="sxs-lookup"><span data-stu-id="d05bf-114">BME280 sensor</span></span>

<span data-ttu-id="d05bf-115">Het volgende diagram toont hoe u verbinding maakt van uw hardware:</span><span class="sxs-lookup"><span data-stu-id="d05bf-115">The following diagram shows how to connect your hardware:</span></span>

![Hardware-instellingen voor frambozen Pi][img-connection-diagram]

<span data-ttu-id="d05bf-117">De volgende tabel geeft een overzicht van de verbindingen van de Pi frambozen aan de onderdelen op de breadboard:</span><span class="sxs-lookup"><span data-stu-id="d05bf-117">The following table summarizes the connections from the Raspberry Pi to the components on the breadboard:</span></span>

| <span data-ttu-id="d05bf-118">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="d05bf-118">Raspberry Pi</span></span>            | <span data-ttu-id="d05bf-119">Breadboard</span><span class="sxs-lookup"><span data-stu-id="d05bf-119">Breadboard</span></span>             |<span data-ttu-id="d05bf-120">Kleur</span><span class="sxs-lookup"><span data-stu-id="d05bf-120">Color</span></span>         |
| ----------------------- | ---------------------- | ------------- |
| <span data-ttu-id="d05bf-121">GND (Pin 14)</span><span class="sxs-lookup"><span data-stu-id="d05bf-121">GND (Pin 14)</span></span>            | <span data-ttu-id="d05bf-122">LED - ve pincode (18 bis)</span><span class="sxs-lookup"><span data-stu-id="d05bf-122">LED -ve pin (18A)</span></span>      | <span data-ttu-id="d05bf-123">Paars</span><span class="sxs-lookup"><span data-stu-id="d05bf-123">Purple</span></span>          |
| <span data-ttu-id="d05bf-124">GPCLK0 (pincode 7)</span><span class="sxs-lookup"><span data-stu-id="d05bf-124">GPCLK0 (Pin 7)</span></span>          | <span data-ttu-id="d05bf-125">Weerstand (25 bis)</span><span class="sxs-lookup"><span data-stu-id="d05bf-125">Resistor (25A)</span></span>         | <span data-ttu-id="d05bf-126">Orange</span><span class="sxs-lookup"><span data-stu-id="d05bf-126">Orange</span></span>          |
| <span data-ttu-id="d05bf-127">SPI_CE0 (Pin 24)</span><span class="sxs-lookup"><span data-stu-id="d05bf-127">SPI_CE0 (Pin 24)</span></span>        | <span data-ttu-id="d05bf-128">CS (39A)</span><span class="sxs-lookup"><span data-stu-id="d05bf-128">CS (39A)</span></span>               | <span data-ttu-id="d05bf-129">Blauw</span><span class="sxs-lookup"><span data-stu-id="d05bf-129">Blue</span></span>          |
| <span data-ttu-id="d05bf-130">SPI_SCLK (Pin 23)</span><span class="sxs-lookup"><span data-stu-id="d05bf-130">SPI_SCLK (Pin 23)</span></span>       | <span data-ttu-id="d05bf-131">SCK (36A)</span><span class="sxs-lookup"><span data-stu-id="d05bf-131">SCK (36A)</span></span>              | <span data-ttu-id="d05bf-132">Geel</span><span class="sxs-lookup"><span data-stu-id="d05bf-132">Yellow</span></span>        |
| <span data-ttu-id="d05bf-133">SPI_MISO (Pin 21)</span><span class="sxs-lookup"><span data-stu-id="d05bf-133">SPI_MISO (Pin 21)</span></span>       | <span data-ttu-id="d05bf-134">SDO (37 BIS)</span><span class="sxs-lookup"><span data-stu-id="d05bf-134">SDO (37A)</span></span>              | <span data-ttu-id="d05bf-135">Wit</span><span class="sxs-lookup"><span data-stu-id="d05bf-135">White</span></span>         |
| <span data-ttu-id="d05bf-136">SPI_MOSI (Pin 19)</span><span class="sxs-lookup"><span data-stu-id="d05bf-136">SPI_MOSI (Pin 19)</span></span>       | <span data-ttu-id="d05bf-137">SDI (38 BIS)</span><span class="sxs-lookup"><span data-stu-id="d05bf-137">SDI (38A)</span></span>              | <span data-ttu-id="d05bf-138">Groen</span><span class="sxs-lookup"><span data-stu-id="d05bf-138">Green</span></span>         |
| <span data-ttu-id="d05bf-139">GND (pincode 6)</span><span class="sxs-lookup"><span data-stu-id="d05bf-139">GND (Pin 6)</span></span>             | <span data-ttu-id="d05bf-140">GND (35A)</span><span class="sxs-lookup"><span data-stu-id="d05bf-140">GND (35A)</span></span>              | <span data-ttu-id="d05bf-141">Zwart</span><span class="sxs-lookup"><span data-stu-id="d05bf-141">Black</span></span>         |
| <span data-ttu-id="d05bf-142">3.3 V (pincode 1)</span><span class="sxs-lookup"><span data-stu-id="d05bf-142">3.3 V (Pin 1)</span></span>           | <span data-ttu-id="d05bf-143">3Vo (34 bis)</span><span class="sxs-lookup"><span data-stu-id="d05bf-143">3Vo (34A)</span></span>              | <span data-ttu-id="d05bf-144">Rood</span><span class="sxs-lookup"><span data-stu-id="d05bf-144">Red</span></span>           |

<span data-ttu-id="d05bf-145">U voltooit de installatie van de hardware, moet u:</span><span class="sxs-lookup"><span data-stu-id="d05bf-145">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="d05bf-146">Verbinding maken met uw frambozen-Pi de voeding die is opgenomen in het pakket.</span><span class="sxs-lookup"><span data-stu-id="d05bf-146">Connect your Raspberry Pi to the power supply included in the kit.</span></span>
- <span data-ttu-id="d05bf-147">Verbinding maken met uw Pi frambozen via de Ethernet-kabel in uw kit opgenomen met het netwerk.</span><span class="sxs-lookup"><span data-stu-id="d05bf-147">Connect your Raspberry Pi to your network using the Ethernet cable included in your kit.</span></span> <span data-ttu-id="d05bf-148">U kunt ook kunt u instellen [draadloze netwerkverbinding] [ lnk-pi-wireless] voor uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="d05bf-148">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="d05bf-149">U hebt nu de hardware-instellingen van uw Pi frambozen voltooid.</span><span class="sxs-lookup"><span data-stu-id="d05bf-149">You have now completed the hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="d05bf-150">Aanmelden en toegang tot de terminal</span><span class="sxs-lookup"><span data-stu-id="d05bf-150">Sign in and access the terminal</span></span>

<span data-ttu-id="d05bf-151">U hebt twee opties voor toegang tot een terminal omgeving op uw Pi frambozen:</span><span class="sxs-lookup"><span data-stu-id="d05bf-151">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="d05bf-152">Als u een toetsenbord en de monitor die zijn verbonden met uw Pi frambozen hebt, kunt u de gebruikersinterface van Raspbian voor toegang tot een terminalvenster.</span><span class="sxs-lookup"><span data-stu-id="d05bf-152">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

- <span data-ttu-id="d05bf-153">Toegang tot de opdrachtregel op uw frambozen Pi gebruik van SSH op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d05bf-153">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="d05bf-154">Gebruik een terminalvenster in de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="d05bf-154">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="d05bf-155">De standaardreferenties voor Raspbian zijn gebruikersnaam **pi** en het wachtwoord **frambozen**.</span><span class="sxs-lookup"><span data-stu-id="d05bf-155">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="d05bf-156">U kunt starten in de taakbalk in de gebruikersinterface van de **Terminal** hulpprogramma met het pictogram dat op een monitor lijkt.</span><span class="sxs-lookup"><span data-stu-id="d05bf-156">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="d05bf-157">Meld u aan met SSH</span><span class="sxs-lookup"><span data-stu-id="d05bf-157">Sign in with SSH</span></span>

<span data-ttu-id="d05bf-158">U kunt SSH gebruiken voor vanaf de opdrachtregel toegang tot uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="d05bf-158">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="d05bf-159">Het artikel [SSH (Secure Shell)] [ lnk-pi-ssh] wordt beschreven hoe SSH configureren op uw Pi frambozen en verbinding maken van [Windows] [ lnk-ssh-windows] of [Linux en Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="d05bf-159">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="d05bf-160">Aanmelden met gebruikersnaam **pi** en het wachtwoord **frambozen**.</span><span class="sxs-lookup"><span data-stu-id="d05bf-160">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="d05bf-161">Optioneel: Een map op uw Pi frambozen delen</span><span class="sxs-lookup"><span data-stu-id="d05bf-161">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="d05bf-162">U kunt desgewenst een map op uw Pi frambozen delen met uw bureaublad omgeving.</span><span class="sxs-lookup"><span data-stu-id="d05bf-162">Optionally, you may want to share a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="d05bf-163">Delen van een map, kunt u gebruikmaken van uw voorkeur bureaublad teksteditor (zoals [Visual Studio Code](https://code.visualstudio.com/) of [Sublime Text](http://www.sublimetext.com/)) voor het bewerken van bestanden op uw Pi frambozen in plaats van `nano` of `vi`.</span><span class="sxs-lookup"><span data-stu-id="d05bf-163">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="d05bf-164">Als u wilt delen een map met Windows, configureert u een Samba-server op de frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="d05bf-164">To share a folder with Windows, configure a Samba server on the Raspberry Pi.</span></span> <span data-ttu-id="d05bf-165">U kunt ook gebruik van de ingebouwde [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server met een SFTP-client op het bureaublad.</span><span class="sxs-lookup"><span data-stu-id="d05bf-165">Alternatively, use the built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

### <a name="enable-spi"></a><span data-ttu-id="d05bf-166">SPI inschakelen</span><span class="sxs-lookup"><span data-stu-id="d05bf-166">Enable SPI</span></span>

<span data-ttu-id="d05bf-167">Voordat u de voorbeeldtoepassing uitvoeren kunt, moet u de seriële randapparatuur Interface (SPI)-bus van de Pi frambozen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d05bf-167">Before you can run the sample application, you must enable the Serial Peripheral Interface (SPI) bus on the Raspberry Pi.</span></span> <span data-ttu-id="d05bf-168">De Pi frambozen communiceert met het apparaat van de sensor BME280 via de SPI-bus.</span><span class="sxs-lookup"><span data-stu-id="d05bf-168">The Raspberry Pi communicates with the BME280 sensor device over the SPI bus.</span></span> <span data-ttu-id="d05bf-169">Gebruik de volgende opdracht in het configuratiebestand bewerken:</span><span class="sxs-lookup"><span data-stu-id="d05bf-169">Use the following command to edit the configuration file:</span></span>

```sh
sudo nano /boot/config.txt
```

<span data-ttu-id="d05bf-170">Zoek de regel:</span><span class="sxs-lookup"><span data-stu-id="d05bf-170">Find the line:</span></span>

`#dtparam=spi=on`

- <span data-ttu-id="d05bf-171">Om de opmerkingen bij de regel, verwijder de `#` aan het begin.</span><span class="sxs-lookup"><span data-stu-id="d05bf-171">To uncomment the line, delete the `#` at the start.</span></span>
- <span data-ttu-id="d05bf-172">Sla de wijzigingen (**Ctrl-O**, **Enter**) en sluit de editor af (**Ctrl X**).</span><span class="sxs-lookup"><span data-stu-id="d05bf-172">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>
- <span data-ttu-id="d05bf-173">Start opnieuw op de frambozen Pi zodat SPI.</span><span class="sxs-lookup"><span data-stu-id="d05bf-173">To enable SPI, reboot the Raspberry Pi.</span></span> <span data-ttu-id="d05bf-174">Opnieuw wordt opgestart nadat de verbinding verbreekt de terminal, moet u aan te melden opnieuw wanneer de Pi frambozen opnieuw wordt gestart:</span><span class="sxs-lookup"><span data-stu-id="d05bf-174">Rebooting disconnects the terminal, you need to sign in again when the Raspberry Pi restarts:</span></span>

  ```sh
  sudo reboot
  ```


[img-connection-diagram]: media/iot-suite-raspberry-pi-kit-prepare-pi/rpi2_remote_monitoring.png

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/