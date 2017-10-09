---
title: een gemiddelde aaaCreate stack op een Linux VM in Azure | Microsoft Docs
description: Meer informatie over hoe toocreate een MongoDB, snelle AngularJS en Node.js (gemiddelde) stack is op een Linux VM in Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 82a8e34e60d2bb6e6670ee007faa1113ea78b716
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a>Maak een stack MongoDB, snelle AngularJS en Node.js (gemiddelde) op een Linux VM in Azure

Deze zelfstudie leert u hoe tooimplement een MongoDB, snelle AngularJS en Node.js (gemiddelde) stack is op een Linux VM in Azure. GEMIDDELDE Hallo-stack die u maakt kan toevoegen, verwijderen en het weergeven van rapporten in een database. Procedures voor:

> [!div class="checklist"]
> * Een Linux-VM maken
> * Node.js installeren
> * MongoDB installeren en het Hallo-server instellen
> * Express installeren en routes toohello server instellen
> * Toegang Hallo routes met AngularJS
> * Hallo-toepassing uitvoeren

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).


## <a name="create-a-linux-vm"></a>Een Linux-VM maken

Een resourcegroep maken met de Hallo [az groep maken](https://docs.microsoft.com/cli/azure/group#create) opdracht en maak een Linux-VM met Hallo [az vm maken](https://docs.microsoft.com/cli/azure/vm#create) opdracht. Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.

Hallo volgende voorbeeld wordt een resourcegroep met de naam van hello Azure CLI toocreate *myResourceGroupMEAN* in Hallo *eastus* locatie. Een virtuele machine gemaakt met de naam *myVM* met SSH-sleutels als deze niet al bestaan op de standaardlocatie van de sleutel. toouse een specifieke set sleutels, gebruik Hallo--ssh-sleutel / waarde-optie.

```azurecli-interactive
az group create --name myResourceGroupMEAN --location eastus
az vm create \
    --resource-group myResourceGroupMEAN \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --admin-password 'Azure12345678!' \
    --generate-ssh-keys
az vm open-port --port 3300 --resource-group myResourceGroupMEAN --name myVM
```

Wanneer Hallo VM is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen: 

```azurecli-interactive
{
  "fqdns": "",
  "id": "/subscriptions/{subscription-id}/resourceGroups/myResourceGroupMEAN/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.72.77.9",
  "resourceGroup": "myResourceGroupMEAN"
}
```
Let op Hallo `publicIpAddress`. Dit adres is gebruikte tooaccess Hallo VM.

Gebruik Hallo volgende opdracht toocreate een SSH-sessie met de Hallo VM. Zorg ervoor dat toouse Hallo juiste openbare IP-adres. In ons voorbeeld boven onze IP is adres 13.72.77.9.

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a>Node.js installeren

[Node.js](https://nodejs.org/en/) is een JavaScript-runtime gebouwd op van de Chrome V8 JavaScript-engine. Node.js wordt gebruikt in deze zelfstudie tooset Hallo die Express routes en AngularJS-controllers.

Installeer op Hallo VM, met Hallo bash-shell die u hebt geopend met SSH, Node.js.

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a>MongoDB installeren en het Hallo-server instellen
[MongoDB](http://www.mongodb.com) -gegevens opslaat in flexibele, zoals JSON-documenten. Velden in een database kunnen afwijken van het document toodocument en gegevensstructuur na verloop van tijd kan worden gewijzigd. Voor onze voorbeeldtoepassing toevoegen we adresboek records tooMongoDB die rapportnaam, isbn nummer, auteur en het aantal pagina's bevatten. 

1. Virtuele machine, met Hallo bash-shell die u hebt geopend met SSH, ingesteld op Hallo Hallo MongoDB-sleutel.

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. Hallo Pakketbeheer bijwerken met Hallo-sleutel.
  
    ```bash
    sudo apt-get update
    ```

3. MongoDB installeren.

    ```bash
    sudo apt-get install -y mongodb
    ```

4. Hallo-server niet starten.

    ```bash
    sudo service mongodb start
    ```

5. Ook moet tooinstall Hallo [hoofdtekst parser](https://www.npmjs.com/package/body-parser-json) pakket toohelp ons Hallo JSON toohello-server aanvragen doorgegeven verwerken.

    Hallo npm Pakketbeheer installeren.

    ```bash
    sudo apt-get install npm
    ```

    Hallo hoofdtekst parser pakketten installeren.
    
    ```bash
    sudo npm install body-parser
    ```

6. Maak een map met de naam *Books* en voeg de tooit van een bestand met de naam *server.js* die Hallo-configuratie voor de webserver Hallo bevat.

    ```node.js
    var express = require('express');
    var bodyParser = require('body-parser');
    var app = express();
    app.use(express.static(__dirname + '/public'));
    app.use(bodyParser.json());
    require('./apps/routes')(app);
    app.set('port', 3300);
    app.listen(app.get('port'), function() {
        console.log('Server up: http://localhost:' + app.get('port'));
    });
    ```

## <a name="install-express-and-set-up-routes-toohello-server"></a>Express installeren en routes toohello server instellen

[Express](https://expressjs.com) is een minimaal en flexibel Node.js web application framework met functies voor webtoepassingen en mobiele toepassingen. Express wordt gebruikt in deze zelfstudie toopass adresboek informatie tooand uit onze MongoDB-database. [Mongoose](http://mongoosejs.com) biedt een ongecompliceerde, schema's gebaseerde oplossing toomodel uw toepassingsgegevens. Mongoose wordt gebruikt in deze zelfstudie tooprovide een boek schema voor Hallo-database.

1. Snelle en Mongoose installeren.

    ```bash
    sudo npm install express mongoose
    ```

2. In Hallo *Books* map, maak een map met de naam *apps* en toevoegen van een bestand met de naam *routes.js* Hello express routes die zijn gedefinieerd.

    ```node.js
    var Book = require('./models/book');
    module.exports = function(app) {
      app.get('/book', function(req, res) {
        Book.find({}, function(err, result) {
          if ( err ) throw err;
          res.json(result);
        });
      }); 
      app.post('/book', function(req, res) {
        var book = new Book( {
          name:req.body.name,
          isbn:req.body.isbn,
          author:req.body.author,
          pages:req.body.pages
        });
        book.save(function(err, result) {
          if ( err ) throw err;
          res.json( {
            message:"Successfully added book",
            book:result
          });
        });
      });
      app.delete("/book/:isbn", function(req, res) {
        Book.findOneAndRemove(req.query, function(err, result) {
          if ( err ) throw err;
          res.json( {
            message: "Successfully deleted hello book",
            book: result
          });
        });
      });
      var path = require('path');
      app.get('*', function(req, res) {
        res.sendfile(path.join(__dirname + '/public', 'index.html'));
      });
    };
    ```

3. In Hallo *apps* map, maak een map met de naam *modellen* en toevoegen van een bestand met de naam *book.js* met Hallo adresboek Modelconfiguratie is gedefinieerd.  

    ```node.js
    var mongoose = require('mongoose');
    var dbHost = 'mongodb://localhost:27017/test';
    mongoose.connect(dbHost);
    mongoose.connection;
    mongoose.set('debug', true);
    var bookSchema = mongoose.Schema( {
      name: String,
      isbn: {type: String, index: true},
      author: String,
      pages: Number
    });
    var Book = mongoose.model('Book', bookSchema);
    module.exports = mongoose.model('Book', bookSchema); 
    ```

## <a name="access-hello-routes-with-angularjs"></a>Toegang Hallo routes met AngularJS

[AngularJS](https://angularjs.org) biedt een webframework voor het maken van weergaven in uw webtoepassingen. In deze zelfstudie we het gebruik van de AngularJS tooconnect onze webpagina snelle en acties uitvoeren op onze adresboek-database.

1. Hallo directory ook een back-up wijzigen*Books* (`cd ../..`), en maak vervolgens een map met de naam *openbare* en toevoegen van een bestand met de naam *script.js* met Hallo-controller de configuratie is gedefinieerd.

    ```node.js
    var app = angular.module('myApp', []);
    app.controller('myCtrl', function($scope, $http) {
      $http( {
        method: 'GET',
        url: '/book'
      }).then(function successCallback(response) {
        $scope.books = response.data;
      }, function errorCallback(response) {
        console.log('Error: ' + response);
      });
      $scope.del_book = function(book) {
        $http( {
          method: 'DELETE',
          url: '/book/:isbn',
          params: {'isbn': book.isbn}
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
      $scope.add_book = function() {
        var body = '{ "name": "' + $scope.Name + 
        '", "isbn": "' + $scope.Isbn +
        '", "author": "' + $scope.Author + 
        '", "pages": "' + $scope.Pages + '" }';
        $http({
          method: 'POST',
          url: '/book',
          data: body
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
    });
    ```
    
2. In Hallo *openbare* map, maakt u een bestand met de naam *index.html* met Hallo webpagina gedefinieerd.

    ```html
    <!doctype html>
    <html ng-app="myApp" ng-controller="myCtrl">
      <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
        <script src="script.js"></script>
      </head>
      <body>
        <div>
          <table>
            <tr>
              <td>Name:</td> 
              <td><input type="text" ng-model="Name"></td>
            </tr>
            <tr>
              <td>Isbn:</td>
              <td><input type="text" ng-model="Isbn"></td>
            </tr>
            <tr>
              <td>Author:</td> 
              <td><input type="text" ng-model="Author"></td>
            </tr>
            <tr>
              <td>Pages:</td>
              <td><input type="number" ng-model="Pages"></td>
            </tr>
          </table>
          <button ng-click="add_book()">Add</button>
        </div>
        <hr>
        <div>
          <table>
            <tr>
              <th>Name</th>
              <th>Isbn</th>
              <th>Author</th>
              <th>Pages</th>
            </tr>
            <tr ng-repeat="book in books">
              <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
              <td>{{book.name}}</td>
              <td>{{book.isbn}}</td>
              <td>{{book.author}}</td>
              <td>{{book.pages}}</td>
            </tr>
          </table>
        </div>
      </body>
    </html>
    ```

##  <a name="run-hello-application"></a>Hallo-toepassing uitvoeren

1. Hallo directory ook een back-up wijzigen*Books* (`cd ..`) en het Hallo-server starten met deze opdracht uit te voeren:

    ```bash
    nodejs server.js
    ```

2. Open een browser toohello webadres op dat u hebt vastgelegd voor Hallo VM. Bijvoorbeeld: *http://13.72.77.9:3300*. U ziet er ongeveer zo Hallo na pagina:

    ![Book record](media/tutorial-mean/meanstack-init.png)

3. Gegevens in de tekstvakken Hallo invoeren en op **toevoegen**. Bijvoorbeeld:

    ![Book record toevoegen](media/tutorial-mean/meanstack-add.png)

4. Na het Hallo-pagina te vernieuwen, ziet u dat lijkt op deze pagina:

    ![Lijst adresboekrecords](media/tutorial-mean/meanstack-list.png)

5. U kunt klikken **verwijderen** en Hallo book record verwijderen uit Hallo-database.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie maakt u een webtoepassing waarin wordt bijgehouden adresboek registreert met behulp van een gemiddelde gemaakt stack op een Linux-VM. U hebt geleerd hoe u:

> [!div class="checklist"]
> * Een Linux-VM maken
> * Node.js installeren
> * MongoDB installeren en het Hallo-server instellen
> * Express installeren en routes toohello server instellen
> * Toegang Hallo routes met AngularJS
> * Hallo-toepassing uitvoeren

Hoe gaan van de volgende zelfstudie toolearn toohello toosecure webservers met SSL-certificaten.

> [!div class="nextstepaction"]
> [Webserver met SSL beveiligde](tutorial-secure-web-server.md)
