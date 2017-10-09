|Parameternaam| Type | Beschrijving| Mogelijke waarden|
|-|-|-|-|
| /ServerMode|Verplicht|Hiermee geeft u op of beide Hallo-servers voor configuratie en het proces moeten worden geïnstalleerd, of alleen Hallo processerver|CS<br>PS|
|/InstallLocation|Verplicht|Hallo-map in welke Hallo-onderdelen zijn geïnstalleerd| Een map op de computer Hallo|
|/MySQLCredsFilePath|Verplicht|Hallo-bestandspad in welke Hallo MySQL serverreferenties worden opgeslagen|Hallo-bestand moet de hieronder opgegeven Hallo-indeling|
|/VaultCredsFilePath|Verplicht|Hallo-pad van het kluisreferentiebestand Hallo|Geldig bestandspad|
|/EnvType|Verplicht|Type envrionment dat u wilt dat tooprotect |VMware<br>NonVMware|
|/PSIP|Verplicht|IP-adres van Hallo NIC toobe gebruikt voor gegevensoverdracht van replicatie| Een geldig IP-adres|
|/CSIP|Verplicht|Hallo IP-adres van welke Hallo configuratieserver luistert op Hallo-NIC| Een geldig IP-adres|
|/PassphraseFilePath|Verplicht|Hallo volledig pad toolocation van Hallo wachtwoordzin bestand|Geldig bestandspad|
|/BypassProxy|Optioneel|Hiermee geeft u op dat die server van de configuratie Hallo verbindt tooAzure zonder een proxy|toodo deze waarde niet ophalen uit Venu|
|/ProxySettingsFilePath|Optioneel|Proxy-instellingen (Hallo standaard proxyserver vereist verificatie of een aangepaste proxy)|Hallo-bestand moet Hallo-indeling die hieronder zijn opgegeven|
|DataTransferSecurePort|Optioneel|Het poortnummer voor Hallo PSIP toobe gebruikt voor van replicatiegegevens| Geldig poortnummer (standaardwaarde is 9433)|
|/SkipSpaceCheck|Optioneel|Hiermee wordt aangegeven dat de controle op vrije ruimte in de cacheschijf moet worden overgeslagen| |
|/AcceptThirdpartyEULA|Verplicht|Een vlag impliceert acceptatie van de gebruiksrechtovereenkomst van derden| |
|/ShowThirdpartyEULA|Optioneel|Hiermee wordt de gebruiksrechtovereenkomst van derden weergegeven. Indien opgegeven als invoer, worden alle andere parameters genegeerd| |
