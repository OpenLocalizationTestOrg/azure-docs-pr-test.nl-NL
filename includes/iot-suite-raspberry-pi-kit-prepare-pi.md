## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="6aae6-101">Uw Raspberry Pi voorbereiden</span><span class="sxs-lookup"><span data-stu-id="6aae6-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="6aae6-102">Raspbian installeren</span><span class="sxs-lookup"><span data-stu-id="6aae6-102">Install Raspbian</span></span>

<span data-ttu-id="6aae6-103">Als dit Hallo eerste keer dat u uw Pi frambozen gebruikt, moet u tooinstall hello Raspbian besturingssysteem via NOOBS op Hallo SD-kaart is opgenomen in het Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="6aae6-103">If this is hello first time you are using your Raspberry Pi, you need tooinstall hello Raspbian operating system using NOOBS on hello SD card included in hello kit.</span></span> <span data-ttu-id="6aae6-104">Hallo [frambozen Pi Software handleiding] [ lnk-install-raspbian] beschrijft hoe een besturingssysteem op uw Pi frambozen tooinstall.</span><span class="sxs-lookup"><span data-stu-id="6aae6-104">hello [Raspberry Pi Software Guide][lnk-install-raspbian] describes how tooinstall an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="6aae6-105">Deze zelfstudie wordt ervan uitgegaan dat u hebt Hallo Raspbian-besturingssysteem geïnstalleerd op uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="6aae6-105">This tutorial assumes you have installed hello Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="6aae6-106">Hallo SD-kaart is opgenomen in Hallo [Microsoft Azure IoT Starter Kit voor frambozen Pi 3] [ lnk-starter-kits] al NOOBS geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6aae6-106">hello SD card included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="6aae6-107">U kunt opstarten Hallo frambozen Pi van deze kaart en tooinstall hello Raspbian OS kiezen.</span><span class="sxs-lookup"><span data-stu-id="6aae6-107">You can boot hello Raspberry Pi from this card and choose tooinstall hello Raspbian OS.</span></span>

### <a name="set-up-hello-hardware"></a><span data-ttu-id="6aae6-108">Hallo hardware instellen</span><span class="sxs-lookup"><span data-stu-id="6aae6-108">Set up hello hardware</span></span>

<span data-ttu-id="6aae6-109">Deze zelfstudie wordt gebruikgemaakt van Hallo BME280 sensor opgenomen in Hallo [Microsoft Azure IoT Starter Kit voor frambozen Pi 3] [ lnk-starter-kits] toogenerate telemetrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="6aae6-109">This tutorial uses hello BME280 sensor included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] toogenerate telemetry data.</span></span> <span data-ttu-id="6aae6-110">Een tooindicate LED wordt gebruikt wanneer Hallo frambozen Pi een methodeaanroep vanuit Hallo oplossing dashboard verwerkt.</span><span class="sxs-lookup"><span data-stu-id="6aae6-110">It uses an LED tooindicate when hello Raspberry Pi processes a method invocation from hello solution dashboard.</span></span>

<span data-ttu-id="6aae6-111">Hallo-onderdelen op Hallo brood mededelingenbord zijn:</span><span class="sxs-lookup"><span data-stu-id="6aae6-111">hello components on hello bread board are:</span></span>

- <span data-ttu-id="6aae6-112">Rode LED</span><span class="sxs-lookup"><span data-stu-id="6aae6-112">Red LED</span></span>
- <span data-ttu-id="6aae6-113">220 Ohm weerstand (rood, rood, bruine)</span><span class="sxs-lookup"><span data-stu-id="6aae6-113">220-Ohm resistor (red, red, brown)</span></span>
- <span data-ttu-id="6aae6-114">BME280-temperatuursensor</span><span class="sxs-lookup"><span data-stu-id="6aae6-114">BME280 sensor</span></span>

<span data-ttu-id="6aae6-115">Hallo volgende diagram toont hoe tooconnect uw hardware:</span><span class="sxs-lookup"><span data-stu-id="6aae6-115">hello following diagram shows how tooconnect your hardware:</span></span>

![Hardware-instellingen voor frambozen Pi][img-connection-diagram]

<span data-ttu-id="6aae6-117">Hallo volgende tabel ziet u Hallo verbindingen van Hallo frambozen Pi toohello onderdelen op Hallo breadboard:</span><span class="sxs-lookup"><span data-stu-id="6aae6-117">hello following table summarizes hello connections from hello Raspberry Pi toohello components on hello breadboard:</span></span>

| <span data-ttu-id="6aae6-118">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="6aae6-118">Raspberry Pi</span></span>            | <span data-ttu-id="6aae6-119">Breadboard</span><span class="sxs-lookup"><span data-stu-id="6aae6-119">Breadboard</span></span>             |<span data-ttu-id="6aae6-120">Kleur</span><span class="sxs-lookup"><span data-stu-id="6aae6-120">Color</span></span>         |
| ----------------------- | ---------------------- | ------------- |
| <span data-ttu-id="6aae6-121">GND (Pin 14)</span><span class="sxs-lookup"><span data-stu-id="6aae6-121">GND (Pin 14)</span></span>            | <span data-ttu-id="6aae6-122">LED - ve pincode (18 bis)</span><span class="sxs-lookup"><span data-stu-id="6aae6-122">LED -ve pin (18A)</span></span>      | <span data-ttu-id="6aae6-123">Paars</span><span class="sxs-lookup"><span data-stu-id="6aae6-123">Purple</span></span>          |
| <span data-ttu-id="6aae6-124">GPCLK0 (pincode 7)</span><span class="sxs-lookup"><span data-stu-id="6aae6-124">GPCLK0 (Pin 7)</span></span>          | <span data-ttu-id="6aae6-125">Weerstand (25 bis)</span><span class="sxs-lookup"><span data-stu-id="6aae6-125">Resistor (25A)</span></span>         | <span data-ttu-id="6aae6-126">Orange</span><span class="sxs-lookup"><span data-stu-id="6aae6-126">Orange</span></span>          |
| <span data-ttu-id="6aae6-127">SPI_CE0 (Pin 24)</span><span class="sxs-lookup"><span data-stu-id="6aae6-127">SPI_CE0 (Pin 24)</span></span>        | <span data-ttu-id="6aae6-128">CS (39A)</span><span class="sxs-lookup"><span data-stu-id="6aae6-128">CS (39A)</span></span>               | <span data-ttu-id="6aae6-129">Blauw</span><span class="sxs-lookup"><span data-stu-id="6aae6-129">Blue</span></span>          |
| <span data-ttu-id="6aae6-130">SPI_SCLK (Pin 23)</span><span class="sxs-lookup"><span data-stu-id="6aae6-130">SPI_SCLK (Pin 23)</span></span>       | <span data-ttu-id="6aae6-131">SCK (36A)</span><span class="sxs-lookup"><span data-stu-id="6aae6-131">SCK (36A)</span></span>              | <span data-ttu-id="6aae6-132">Geel</span><span class="sxs-lookup"><span data-stu-id="6aae6-132">Yellow</span></span>        |
| <span data-ttu-id="6aae6-133">SPI_MISO (Pin 21)</span><span class="sxs-lookup"><span data-stu-id="6aae6-133">SPI_MISO (Pin 21)</span></span>       | <span data-ttu-id="6aae6-134">SDO (37 BIS)</span><span class="sxs-lookup"><span data-stu-id="6aae6-134">SDO (37A)</span></span>              | <span data-ttu-id="6aae6-135">Wit</span><span class="sxs-lookup"><span data-stu-id="6aae6-135">White</span></span>         |
| <span data-ttu-id="6aae6-136">SPI_MOSI (Pin 19)</span><span class="sxs-lookup"><span data-stu-id="6aae6-136">SPI_MOSI (Pin 19)</span></span>       | <span data-ttu-id="6aae6-137">SDI (38 BIS)</span><span class="sxs-lookup"><span data-stu-id="6aae6-137">SDI (38A)</span></span>              | <span data-ttu-id="6aae6-138">Groen</span><span class="sxs-lookup"><span data-stu-id="6aae6-138">Green</span></span>         |
| <span data-ttu-id="6aae6-139">GND (pincode 6)</span><span class="sxs-lookup"><span data-stu-id="6aae6-139">GND (Pin 6)</span></span>             | <span data-ttu-id="6aae6-140">GND (35A)</span><span class="sxs-lookup"><span data-stu-id="6aae6-140">GND (35A)</span></span>              | <span data-ttu-id="6aae6-141">Zwart</span><span class="sxs-lookup"><span data-stu-id="6aae6-141">Black</span></span>         |
| <span data-ttu-id="6aae6-142">3.3 V (pincode 1)</span><span class="sxs-lookup"><span data-stu-id="6aae6-142">3.3 V (Pin 1)</span></span>           | <span data-ttu-id="6aae6-143">3Vo (34 bis)</span><span class="sxs-lookup"><span data-stu-id="6aae6-143">3Vo (34A)</span></span>              | <span data-ttu-id="6aae6-144">Rood</span><span class="sxs-lookup"><span data-stu-id="6aae6-144">Red</span></span>           |

<span data-ttu-id="6aae6-145">toocomplete hello hardware-installatie, moet u:</span><span class="sxs-lookup"><span data-stu-id="6aae6-145">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="6aae6-146">Verbinding maken met uw frambozen Pi toohello voeding opgenomen in het Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="6aae6-146">Connect your Raspberry Pi toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="6aae6-147">Verbinding maken met uw frambozen Pi tooyour netwerk met Hallo Ethernet-kabel is opgenomen in de kit.</span><span class="sxs-lookup"><span data-stu-id="6aae6-147">Connect your Raspberry Pi tooyour network using hello Ethernet cable included in your kit.</span></span> <span data-ttu-id="6aae6-148">U kunt ook kunt u instellen [draadloze netwerkverbinding] [ lnk-pi-wireless] voor uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="6aae6-148">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="6aae6-149">U hebt nu Hallo hardware-instellingen van uw Pi frambozen voltooid.</span><span class="sxs-lookup"><span data-stu-id="6aae6-149">You have now completed hello hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="6aae6-150">Aanmelden en Hallo terminal</span><span class="sxs-lookup"><span data-stu-id="6aae6-150">Sign in and access hello terminal</span></span>

<span data-ttu-id="6aae6-151">U hebt twee opties tooaccess een terminal-omgeving op uw Pi frambozen:</span><span class="sxs-lookup"><span data-stu-id="6aae6-151">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="6aae6-152">Als u een toetsenbord hebt en verbonden tooyour frambozen Pi bewaken, kunt u Hallo Raspbian GUI tooaccess een terminalvenster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6aae6-152">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

- <span data-ttu-id="6aae6-153">Hallo opdrachtregel toegang op uw frambozen Pi gebruik van SSH op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6aae6-153">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="6aae6-154">Een terminalvenster in Hallo GUI gebruiken</span><span class="sxs-lookup"><span data-stu-id="6aae6-154">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="6aae6-155">Hallo standaardreferenties voor Raspbian zijn gebruikersnaam **pi** en het wachtwoord **frambozen**.</span><span class="sxs-lookup"><span data-stu-id="6aae6-155">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="6aae6-156">In de taakbalk Hallo in Hallo GUI, kunt u Hallo starten **Terminal** hulpprogramma Hallo-pictogram dat op een monitor lijkt.</span><span class="sxs-lookup"><span data-stu-id="6aae6-156">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="6aae6-157">Meld u aan met SSH</span><span class="sxs-lookup"><span data-stu-id="6aae6-157">Sign in with SSH</span></span>

<span data-ttu-id="6aae6-158">U kunt SSH gebruiken voor toegang tot opdrachtregel tooyour frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="6aae6-158">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="6aae6-159">Hallo artikel [SSH (Secure Shell)] [ lnk-pi-ssh] wordt beschreven hoe tooconfigure SSH op uw Pi frambozen en hoe tooconnect van [Windows] [ lnk-ssh-windows] of [Linux en Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="6aae6-159">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="6aae6-160">Aanmelden met gebruikersnaam **pi** en het wachtwoord **frambozen**.</span><span class="sxs-lookup"><span data-stu-id="6aae6-160">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="6aae6-161">Optioneel: Een map op uw Pi frambozen delen</span><span class="sxs-lookup"><span data-stu-id="6aae6-161">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="6aae6-162">Desgewenst kunt u tooshare een map op uw frambozen Pi met uw bureaublad omgeving.</span><span class="sxs-lookup"><span data-stu-id="6aae6-162">Optionally, you may want tooshare a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="6aae6-163">U toouse uw voorkeur bureaublad teksteditor delen van een map kunt (zoals [Visual Studio Code](https://code.visualstudio.com/) of [Sublime Text](http://www.sublimetext.com/)) tooedit bestanden op uw Pi frambozen in plaats van `nano` of `vi`.</span><span class="sxs-lookup"><span data-stu-id="6aae6-163">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="6aae6-164">tooshare een map met Windows, configureert een Samba-server op Hallo frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="6aae6-164">tooshare a folder with Windows, configure a Samba server on hello Raspberry Pi.</span></span> <span data-ttu-id="6aae6-165">Ook gebruiken Hallo ingebouwde [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server met een SFTP-client op het bureaublad.</span><span class="sxs-lookup"><span data-stu-id="6aae6-165">Alternatively, use hello built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

### <a name="enable-spi"></a><span data-ttu-id="6aae6-166">SPI inschakelen</span><span class="sxs-lookup"><span data-stu-id="6aae6-166">Enable SPI</span></span>

<span data-ttu-id="6aae6-167">Voordat u de voorbeeldtoepassing Hallo uitvoeren kunt, moet u Hallo seriële randapparatuur Interface (SPI)-bus op Hallo frambozen Pi inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6aae6-167">Before you can run hello sample application, you must enable hello Serial Peripheral Interface (SPI) bus on hello Raspberry Pi.</span></span> <span data-ttu-id="6aae6-168">Hallo frambozen Pi communiceert met de Hallo BME280 sensor apparaat via Hallo SPI-bus.</span><span class="sxs-lookup"><span data-stu-id="6aae6-168">hello Raspberry Pi communicates with hello BME280 sensor device over hello SPI bus.</span></span> <span data-ttu-id="6aae6-169">Gebruik Hallo opdracht tooedit Hallo-configuratiebestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="6aae6-169">Use hello following command tooedit hello configuration file:</span></span>

```sh
sudo nano /boot/config.txt
```

<span data-ttu-id="6aae6-170">Hallo regel zoeken:</span><span class="sxs-lookup"><span data-stu-id="6aae6-170">Find hello line:</span></span>

`#dtparam=spi=on`

- <span data-ttu-id="6aae6-171">toouncomment hello regel verwijderen Hallo `#` aan Hallo begin.</span><span class="sxs-lookup"><span data-stu-id="6aae6-171">toouncomment hello line, delete hello `#` at hello start.</span></span>
- <span data-ttu-id="6aae6-172">Sla de wijzigingen (**Ctrl-O**, **Enter**) en sluit de editor af hello (**Ctrl X**).</span><span class="sxs-lookup"><span data-stu-id="6aae6-172">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>
- <span data-ttu-id="6aae6-173">tooenable SPI, opnieuw opstarten Hallo frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="6aae6-173">tooenable SPI, reboot hello Raspberry Pi.</span></span> <span data-ttu-id="6aae6-174">Opnieuw wordt opgestart nadat de verbinding verbreekt Hallo terminal, moet u toosign in opnieuw wanneer Hallo frambozen Pi opnieuw wordt gestart:</span><span class="sxs-lookup"><span data-stu-id="6aae6-174">Rebooting disconnects hello terminal, you need toosign in again when hello Raspberry Pi restarts:</span></span>

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