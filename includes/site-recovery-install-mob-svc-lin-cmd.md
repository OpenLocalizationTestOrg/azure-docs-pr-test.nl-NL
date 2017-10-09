1. Hallo installatieprogramma tooa lokale map (bijvoorbeeld map) op Hallo server die u tooprotect wilt kopiëren. Voer in een terminal Hallo volgende opdrachten:
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. tooinstall Mobility-Service Hallo volgende opdracht uitvoeren:

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. Zodra de installatie is voltooid, moet Hallo Mobility-Service tooget geregistreerde toohello configuratieserver. Hallo na de opdracht tooregister Hallo Mobility-Service met de configuratieserver worden uitgevoerd.

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a>Mobility-Service installatieprogramma vanaf de opdrachtregel

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|Parameter|Type|Beschrijving|Mogelijke waarden|
|-|-|-|-|
|-r |Verplicht|Geeft aan of de Mobility-Service (MS) moet worden geïnstalleerd of MasterTarget(MT) moet worden geïnstalleerd.|MS </br> MT|
|-d |Optioneel|Locatie waar de Mobility-Service moet worden geïnstalleerd|/usr/local/ASR|
|-v|Verplicht|Hiermee geeft u op welke Hallo Mobility-Service ophalen geïnstalleerd Hallo-platform </br> </br>- **VMware** : deze waarde wordt gebruikt als u mobility-service op een virtuele machine uitgevoerd installeert op *VMware vSphere ESXi-Hosts*, *Hyper-V-Hosts* en *Phsyical Servers* </br> - **Azure** : deze waarde wordt gebruikt als u agent op een virtuele machine van Azure IaaS installeert| VMware </br> Azure|
|-q|Optioneel|Hiermee geeft u toorun installatieprogramma in stille modus| N.v.t.|


#### <a name="mobility-service-configuration-command-line"></a>Configuratie van Mobility-Service vanaf de opdrachtregel

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|Parameter|Type|Beschrijving|Mogelijke waarden|
|-|-|-|-|
|-i |Verplicht|IP-adres van de configuratieserver Hallo|Een geldig IP-adres|
|-P |Verplicht|Volledig pad Hallo bestand waarin Hallo verbinding wachtwoordzin is opgeslagen|Een geldige map|
