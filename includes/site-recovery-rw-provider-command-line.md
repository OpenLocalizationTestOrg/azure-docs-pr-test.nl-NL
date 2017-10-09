UnifiedSetup.exe [/ ServerMode < CS/PS >] [/ InstallDrive <DriveLetter>] [/ MySQLCredsFilePath <MySQL credentials file path>] [/ VaultCredsFilePath <Vault credentials file path>] [/ EnvType < VMWare/NonVMWare >] [/ PSIP < IP-adres toobe gebruikt voor gegevensoverdracht] [/CSIP <IP address of CS toobe registered with>] [/ PassphraseFilePath <Passphrase file path>]

Parameters:

* /ServerMode: Verplicht. Hiermee geeft u op of beide Hallo-servers voor configuratie en het proces moeten worden geïnstalleerd, of alleen Hallo processerver. Invoerwaarden: CS, PS.
* InstallLocation: Verplicht. Hallo-map in welke Hallo-onderdelen zijn geïnstalleerd.
* /MySQLCredsFilePath. Verplicht. Hallo-bestandspad in welke Hallo MySQL serverreferenties worden opgeslagen. Hallo-bestand moet in deze indeling:
* [MySQLCredentials]
* MySQLRootPassword = "<Password>"
* MySQLUserPassword = "<Password>"
* /VaultCredsFilePath. Verplicht. Hallo-locatie van het kluisreferentiebestand Hallo
* /EnvType. Verplicht. Hallo-type van de installatie. Waarden: VMware, NonVMware
* /PSIP en /CSIP. Verplicht. Hallo IP-adres van de processerver Hallo en de configuratieserver.
* /PassphraseFilePath. Verplicht. Hallo-locatie van Hallo wachtwoordzin bestand.
* /BypassProxy. Optioneel. Hiermee geeft u op dat die server van de configuratie Hallo verbindt tooAzure zonder een proxy.
* /ProxySettingsFilePath. Optioneel. Proxy-instellingen (Hallo standaard proxyserver vereist verificatie of een aangepaste proxy). Hallo-bestand moet in deze indeling:
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "<IP-adres>"
* ProxyPort = "<Port>"
* ProxyUserName="<User Name>"
* ProxyPassword="<Password>"
* DataTransferSecurePort. Optioneel. Hallo-poortnummer voor gegevens van replicatie.
* SkipSpaceCheck. Optioneel. Hiermee wordt aangegeven dat de controle op vrije ruimte in de cache moet worden overgeslagen.
* AcceptThirdpartyEULA. Verplicht. Hallo van derden overeenkomst accepteert.
* ShowThirdpartyEULA. Verplicht. Hiermee wordt de gebruiksrechtovereenkomst van derden weergegeven. Indien opgegeven als invoer, worden alle andere parameters genegeerd.
