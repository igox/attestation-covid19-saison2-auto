# Générateur de certificat de déplacement en "1-click"
## Objet du projet

Ce projet permet de générer une attestation de déplacement en "1-click" pour le confinement saison 2 lance en France le vendredi 30 Octobre 2020.
En effet la version numérique du gouvernement (https://media.interieur.gouv.fr/deplacement-covid-19/) nécessite
- Plus d'un click pour générer une attestation
- Force a re-renter les informations a chaque utilisation sur certains navigateurs (see [autocomplete](https://gist.github.com/niksumeiko/360164708c3b326bd1c8) set to [false](https://github.com/LAB-MI/attestation-deplacement-derogatoire-q4-2020/blob/a2566e82555c56442dbdc6857c21f0e4c8c5dc39/src/js/form.js#L22)),
<!-- Presente des anomalies sur dispositif mobile pour télécharger #attestations > 1 par jour (achats + sports) sur dispositif mobile -->
Ce projet a été élabore en partant de la base de code de la version numérique du gouvernement dont la version est disponible sur Github ici:
https://github.com/LAB-MI/attestation-deplacement-derogatoire-q4-2020

Ce projet est deployé a cet URL sur Google Cloud Platform (cloud run):
[https://attestationcovid.site/](https://attestationcovid.site/)

## Usage

Concu comme un lien a bookmarker sur un dispositif mobile (telephone, tablette, etc), l'ouverture de ce lien declenchera le telechargement d'une nouvelle attestation enrichie des informations fournies dans le lien.

Cette exemple de lien (prealablement bookmarke) [https://attestationcovid.site/?address=15 rue d'Antibes&birthday=20/03/1882&city=Antibes&firstname=Rene&minutesoffset=5&lastname=Coty&placeofbirth=Le Havre&zipcode=06600&reason=sport_animaux](https://attestationcovid.site/?address=15%20rue%20d%27Antibes&birthday=20/03/1882&city=Antibes&firstname=Rene&minutesoffset=5&lastname=Coty&placeofbirth=Le%20Havre&zipcode=06600&reason=sport_animaux) generera une attestation avec les informations suivantes:

- **15 rue d'Antibes** *l'addresse de votre habitation*
- **20/03/1882** *la date de votre aniversaire*
- **Antibes** *la ville d'habitation*
- **Rene** *votre prenom*
- **03/11/2020 a 13H18** *la date de sortie generee a partir de l'heure actuelle en ajoutant un offset (positif pour une date future ou negatif pour une date passee)*
- **Coty** *votre nom*
- **Le Havre** *votre lieu de naissance*
- **06600** *votre code postal*
- **une case cochee** *la raison de votre sortie qui selon les choix gouvernementaux pourront etre: travail, achats, sante, famille, handicap, sport_animaux, convocation, missions, enfants*

Appreciez votre sortie, sortez couvert et respectez les gestes barrières !

En général deux bookmarks suffisent car seule la raison change.

Je recommende d'utiliser sur Android Firefox qui permet de changer facilement l'URL et d'exporter un lien en application.
<!-- chrome a aussi le widget favoris -->   

## Développer

### Installer le projet

```console
git clone https://github.com/igox/attestation-covid19-saison2-auto
cd attestation-covid19-saison2-auto
npm i
npm start
```

## Générer et tester le code de production

### Tester le code de production en local

#### Générer le code de production pour tester que le build fonctionne en entier

```console
npm run build:dev
```

#### Tester le code de production en local

```console
npx serve dist
```

Et visiter http://localhost:5000

Le code à déployer sera le contenu du dossier `dist`

## Deployer 

```shell script
sudo docker build . -t igox/covid
sudo docker run -p 5000:5000 igox/covid
```

## Crédits
Ce projet a été réalisé à partir d'un fork du depôt [Générateur de certificat de déplacement en "1-click"](https://github.com/scoulomb/attestation-covid19-saison2-auto) par @scoulomb.

Les projets open source suivants ont été utilisés pour le développement de ce
service :

- [PDF-LIB](https://pdf-lib.js.org/)
- [qrcode](https://github.com/soldair/node-qrcode)
- [Bootstrap](https://getbootstrap.com/)
- [Font Awesome](https://fontawesome.com/license)


<!-- remove idea file https://stackoverflow.com/questions/10067848/remove-folder-and-its-contents-from-git-githubs-history -->

