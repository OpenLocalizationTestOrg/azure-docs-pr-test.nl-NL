Azure bepaalt Hallo-versie van Python toouse voor de virtuele omgeving Hello prioriteit te volgen:

1. versie die is opgegeven in runtime.txt in de hoofdmap Hallo
2. versie die is opgegeven door de Python-instelling in configuratie Hallo web-app (Hallo **instellingen** > **toepassingsinstellingen** blade voor uw web-app in hello Azure Portal)
3. Python-2.7 is Hallo standaardwaarde als geen van bovenstaande Hallo zijn opgegeven

Geldige waarden voor de inhoud van Hallo 

    \runtime.txt

zijn:

* python-2.7
* python-3.4

Als Hallo microversie (derde cijfer) is opgegeven, wordt dit genegeerd.

