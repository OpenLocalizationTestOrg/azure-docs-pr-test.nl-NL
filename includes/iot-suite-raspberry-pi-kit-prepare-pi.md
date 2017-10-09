## <a name="prepare-your-raspberry-pi"></a>Uw Raspberry Pi voorbereiden

### <a name="install-raspbian"></a>Raspbian installeren

Als dit Hallo eerste keer dat u uw Pi frambozen gebruikt, moet u tooinstall hello Raspbian besturingssysteem via NOOBS op Hallo SD-kaart is opgenomen in het Hallo-pakket. Hallo [frambozen Pi Software handleiding] [ lnk-install-raspbian] beschrijft hoe een besturingssysteem op uw Pi frambozen tooinstall. Deze zelfstudie wordt ervan uitgegaan dat u hebt Hallo Raspbian-besturingssysteem geïnstalleerd op uw frambozen Pi.

> [!NOTE]
> Hallo SD-kaart is opgenomen in Hallo [Microsoft Azure IoT Starter Kit voor frambozen Pi 3] [ lnk-starter-kits] al NOOBS geïnstalleerd. U kunt opstarten Hallo frambozen Pi van deze kaart en tooinstall hello Raspbian OS kiezen.

### <a name="set-up-hello-hardware"></a>Hallo hardware instellen

Deze zelfstudie wordt gebruikgemaakt van Hallo BME280 sensor opgenomen in Hallo [Microsoft Azure IoT Starter Kit voor frambozen Pi 3] [ lnk-starter-kits] toogenerate telemetrische gegevens. Een tooindicate LED wordt gebruikt wanneer Hallo frambozen Pi een methodeaanroep vanuit Hallo oplossing dashboard verwerkt.

Hallo-onderdelen op Hallo brood mededelingenbord zijn:

- Rode LED
- 220 Ohm weerstand (rood, rood, bruine)
- BME280-temperatuursensor

Hallo volgende diagram toont hoe tooconnect uw hardware:

![Hardware-instellingen voor frambozen Pi][img-connection-diagram]

Hallo volgende tabel ziet u Hallo verbindingen van Hallo frambozen Pi toohello onderdelen op Hallo breadboard:

| Raspberry Pi            | Breadboard             |Kleur         |
| ----------------------- | ---------------------- | ------------- |
| GND (Pin 14)            | LED - ve pincode (18 bis)      | Paars          |
| GPCLK0 (pincode 7)          | Weerstand (25 bis)         | Orange          |
| SPI_CE0 (Pin 24)        | CS (39A)               | Blauw          |
| SPI_SCLK (Pin 23)       | SCK (36A)              | Geel        |
| SPI_MISO (Pin 21)       | SDO (37 BIS)              | Wit         |
| SPI_MOSI (Pin 19)       | SDI (38 BIS)              | Groen         |
| GND (pincode 6)             | GND (35A)              | Zwart         |
| 3.3 V (pincode 1)           | 3Vo (34 bis)              | Rood           |

toocomplete hello hardware-installatie, moet u:

- Verbinding maken met uw frambozen Pi toohello voeding opgenomen in het Hallo-pakket.
- Verbinding maken met uw frambozen Pi tooyour netwerk met Hallo Ethernet-kabel is opgenomen in de kit. U kunt ook kunt u instellen [draadloze netwerkverbinding] [ lnk-pi-wireless] voor uw frambozen Pi.

U hebt nu Hallo hardware-instellingen van uw Pi frambozen voltooid.

### <a name="sign-in-and-access-hello-terminal"></a>Aanmelden en Hallo terminal

U hebt twee opties tooaccess een terminal-omgeving op uw Pi frambozen:

- Als u een toetsenbord hebt en verbonden tooyour frambozen Pi bewaken, kunt u Hallo Raspbian GUI tooaccess een terminalvenster gebruiken.

- Hallo opdrachtregel toegang op uw frambozen Pi gebruik van SSH op uw computer.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Een terminalvenster in Hallo GUI gebruiken

Hallo standaardreferenties voor Raspbian zijn gebruikersnaam **pi** en het wachtwoord **frambozen**. In de taakbalk Hallo in Hallo GUI, kunt u Hallo starten **Terminal** hulpprogramma Hallo-pictogram dat op een monitor lijkt.

#### <a name="sign-in-with-ssh"></a>Meld u aan met SSH

U kunt SSH gebruiken voor toegang tot opdrachtregel tooyour frambozen Pi. Hallo artikel [SSH (Secure Shell)] [ lnk-pi-ssh] wordt beschreven hoe tooconfigure SSH op uw Pi frambozen en hoe tooconnect van [Windows] [ lnk-ssh-windows] of [Linux en Mac OS][lnk-ssh-linux].

Aanmelden met gebruikersnaam **pi** en het wachtwoord **frambozen**.

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a>Optioneel: Een map op uw Pi frambozen delen

Desgewenst kunt u tooshare een map op uw frambozen Pi met uw bureaublad omgeving. U toouse uw voorkeur bureaublad teksteditor delen van een map kunt (zoals [Visual Studio Code](https://code.visualstudio.com/) of [Sublime Text](http://www.sublimetext.com/)) tooedit bestanden op uw Pi frambozen in plaats van `nano` of `vi`.

tooshare een map met Windows, configureert een Samba-server op Hallo frambozen Pi. Ook gebruiken Hallo ingebouwde [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server met een SFTP-client op het bureaublad.

### <a name="enable-spi"></a>SPI inschakelen

Voordat u de voorbeeldtoepassing Hallo uitvoeren kunt, moet u Hallo seriële randapparatuur Interface (SPI)-bus op Hallo frambozen Pi inschakelen. Hallo frambozen Pi communiceert met de Hallo BME280 sensor apparaat via Hallo SPI-bus. Gebruik Hallo opdracht tooedit Hallo-configuratiebestand te volgen:

```sh
sudo nano /boot/config.txt
```

Hallo regel zoeken:

`#dtparam=spi=on`

- toouncomment hello regel verwijderen Hallo `#` aan Hallo begin.
- Sla de wijzigingen (**Ctrl-O**, **Enter**) en sluit de editor af hello (**Ctrl X**).
- tooenable SPI, opnieuw opstarten Hallo frambozen Pi. Opnieuw wordt opgestart nadat de verbinding verbreekt Hallo terminal, moet u toosign in opnieuw wanneer Hallo frambozen Pi opnieuw wordt gestart:

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