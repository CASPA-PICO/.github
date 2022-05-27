<h1>CASPA-PICO</h1>
<h4>Cette organisation regroupe tous les codes utilisés pour le fonctionnement de la base et du capteur CASPA-PICO ainsi que le PCB et le socle 3D</h4>
<img src="https://raw.githubusercontent.com/CASPA-PICO/.github/main/images/banner.jpg"></img>
<h2>Programmes utilisés</h2>
<ul>
  <li><a href="https://github.com/CASPA-PICO/CASPA-PICO-Capteur_OS"><b>Capteur OS</b></a> : Programme du microcontrôleur du capteur </li>
  <li><a href="https://github.com/CASPA-PICO/CASPA-PICO-Base_OS"><b>Base OS</b></a> : Programme du microcontrôleur de la base</li>
  <li><a href="https://github.com/CASPA-PICO/PLTP"><b>PLTP</b></a> : Bibliothèque de transmission de données en Bluetooth</li>
  <li><a href="https://github.com/CASPA-PICO/CASPA-PICO-Server"><b>Serveur</b></a> : Programme du serveur web (site et API)</li>
  <li><a href="https://github.com/CASPA-PICO/CASPA-PICO-Gateway"><b>Gateway</b></a> : Programme permettant de faire passerelle entre le site et Grafana</li>
</ul>
<h2>Matériel</h2>
<ul>
  <li><a href="https://github.com/CASPA-PICO/CASPA-PICO-PCB"><b>PCB</b></a> : Fichiers KiCad du PCB du socle</li>
  <li><a href="https://github.com/CASPA-PICO/CASPA-PICO-Socle"><b>Socle 3D</b></a> : Fichiers FreeCAD du socle 3D</li>
</ul>
<h2>Autres</h2>
<ul>
  <li><a href="https://github.com/CASPA-PICO/Website"><b>Site web statique</b></a> : Modèle du site web en version statique (utilisé lors du développement front-end)</li>
  <li><a href="https://github.com/CASPA-PICO/BluetoothDataTransmission"><b>Prototype de transmission Bluetooth</b></a> : tests préliminaires de transmission de données en Bluetooth</li>
  <li><a href="https://github.com/CASPA-PICO/MicroSD-reader"><b>Prototype de lecture de la carte micro SD</b></a> : tests préliminaires de lecture/écriture de fichiers/dossiers sur une carte micro SD</li>
  <li><a href="https://github.com/CASPA-PICO/Base-Wifi"><b>Prototype d'implémentation WiFi</b></a> : tests préliminaires d'implémentation du WiFi sur microcontrôleur</li>
</ul>
<h2>Schéma du système complet</h2>
<img src="https://i.ibb.co/4YJ9myH/image.png" alt="image" border="0">
<h2>Guide de déploiement du serveur</h2>
<h3>Prérequis</h3>
<ul>
  <li><b>JDK</b> : version 17</li>
  <li><b>MongoDB</b> : version >= 5.0.8</li>
  <li><b>InfluxDB</b> : version >= 2.2.0</li>
  <li><b>Grafana</b> : version >= 8.5.3</li>
</ul>
<h3>Configuration d'InfluxDB</h3>
<p>
  <ul>
    <li>Exécuter la commande <i>influx setup</i> pour initialiser la base de données avec un utilisateur, un bucket et une organisation (bien spécifier une période de rétention des données infinie).<br/>
    </li>
<li>Puis, créer un token d'authentification pour permettre au serveur CASPA-PICO d'envoyer des données à InfluxDB :<br/>
<i>influx auth create --org CASPA-PICO --all-access --description CASPA-PICO-Server</i><br/>
    </li>
    <li>
Copier le token affiché en résultat de la commande (ex : nWvU8HlvK-yarKBI_R30QN4S5cETJ6LeLBTD1wErLDEs0Jeby2AoZd4iiAPkljJ1Dt08CvWM9KpNc6APqN1Q3g==) puis coller le token dans le fichier de configuration du serveur CASPA-PICO dans <b>influxdb.token</b> (voir <a href="https://github.com/CASPA-PICO/CASPA-PICO-Server#configuration-du-serveur">ici</a>)
    </li>
    </ul>
</p>
<h3>Configuration de Grafana</h3>
<p>
  Modifier les champs du fichier de configuration de Grafana : <i>sudo nano /etc/grafana/grafana.ini</i><br/>
  Enlever les '#' en début de ligne si ils sont présents pour ces champs
  <ul>
    <li><b>domain</b> = caspa.icare.univ-lille.fr</li>
    <li><b>root_url</b> = %(protocol)s://%(domain)s/grafana/</li>
    <li><b>serve_from_sub_path</b> = true</li>
    <li><b>signout_redirect_url</b> = /</li>
  </ul>
</p>
