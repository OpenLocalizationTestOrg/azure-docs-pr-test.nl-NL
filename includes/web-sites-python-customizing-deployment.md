Azure bepaalt dat uw toepassing Python gebruikt **als beide volgende voorwaarden waar zijn**:

* bestand Requirements.txt in de hoofdmap Hallo
* elk bestand .py in de hoofdmap hello of een runtime.txt die python specificeert

Wanneer die Hallo geval is, wordt een specifieke implementatie pythonscript, waarmee Hallo standaard synchronisatie van bestanden, evenals extra Python-bewerkingen zoals gebruikt:

* Automatisch beheer van virtuele omgeving
* Installatie van pakketten die zijn vermeld in requirements.txt met behulp van pip
* Maken van de juiste web.config Hallo op basis van Hallo geselecteerde Python-versie.
* Verzamelen van statische bestanden voor Django-toepassingen

U kunt bepaalde aspecten van Hallo standaard implementatiestappen beheren zonder toocustomize Hallo script.

Als u wilt dat tooskip alle stappen voor Python-specifieke implementatie, kunt u dit lege bestand maken:

    \.skipPythonDeployment

Voor meer controle over de implementatie kunt u Hallo standaard implementatiescript overschrijven door het maken van de volgende bestanden Hallo:

    \.deployment
    \deploy.cmd

U kunt Hallo [Azure-opdrachtregelinterface] [ Azure command-line interface] toocreate Hallo-bestanden.  Gebruik deze opdracht uit vanuit de projectmap:

    azure site deploymentscript --python

Als deze bestanden niet bestaan, maakt Azure een tijdelijk implementatiescript en voert dit script uit.  Het is identiek toohello één u maken met de bovenstaande Hallo-opdracht.

[Azure command-line interface]: http://azure.microsoft.com/downloads/
