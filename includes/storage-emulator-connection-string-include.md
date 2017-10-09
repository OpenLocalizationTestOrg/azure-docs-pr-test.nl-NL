de opslagemulator Hallo ondersteunt één vaste account en een bekende verificatiesleutel voor verificatie met gedeelde sleutel. Dit account en de sleutel zijn Hallo alleen gedeelde sleutel referenties zijn toegestaan voor gebruik met Hallo-opslagemulator. Ze zijn:

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> Hallo verificatiesleutel wordt ondersteund door de opslagemulator Hallo is alleen bedoeld voor testen Hallo-functionaliteit van de clientcode voor verificatie. Deze dienen geen elk doeleinde beveiliging. U kunt uw storage-account voor productie en de sleutel niet gebruiken met Hallo-opslagemulator. U moet Hallo ontwikkeling account niet gebruiken met productiegegevens.
> 
> Hallo-opslagemulator ondersteunt alleen verbinding via HTTP. HTTPS is echter Hallo aanbevolen standaardprotocol voor toegang tot resources in een productie-Azure storage-account.
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a>Verbinding maken met toohello emulator account via een snelkoppeling
Hallo gemakkelijkste manier tooconnect toohello opslagemulator van uw toepassing is tooconfigure een verbindingsreeks in het configuratiebestand van de toepassing die verwijst naar de snelkoppeling Hallo `UseDevelopmentStorage=true`. Hier volgt een voorbeeld van een verbinding tekenreeks toohello opslagemulator in een *app.config* bestand: 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a>Verbinding maken met toohello emulator account met behulp van de bekende accountnaam Hallo en sleutel
toocreate een verbindingsreeks dat verwijzingen Hallo emulator accountnaam en sleutels, u Hallo eindpunten opgeven moet voor elk van de Hallo u services wilt toouse van Hallo-emulator in Hallo-verbindingsreeks. Dit is noodzakelijk om Hallo verbindingsreeks verwijst naar Hallo emulator eindpunten, anders dan de voor een productie-opslagaccount zijn. Bijvoorbeeld, ziet Hallo-waarde van de verbindingsreeks er als volgt:

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

Deze waarde is identiek toohello snelkoppeling bovenstaande `UseDevelopmentStorage=true`.

#### <a name="specify-an-http-proxy"></a>Geef een HTTP-proxy
U kunt ook een HTTP-proxy toouse opgeven wanneer u bij het testen van uw service tegen Hallo-opslagemulator. Dit kan handig zijn voor de naleving van HTTP-aanvragen en antwoorden terwijl u fouten bewerkingen op Hallo storage-services opspoort zijn. een proxy toospecify toevoegen Hallo `DevelopmentStorageProxyUri` optie toohello verbindingsreeks en stel de waarde toohello proxy URI. Hier is bijvoorbeeld een verbindingsreeks die de opslagemulator toohello verwijst en een HTTP-proxy configureert:

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

