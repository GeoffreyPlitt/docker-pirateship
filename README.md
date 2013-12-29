docker-pirateship
=================

**A pirate ship built on Docker.**

This project pulls several [Docker](http://www.docker.io/)'fied downloading tools and runs them in a [Vagrant](http://www.vagrantup.com/) VM.

Tools included:
- [CouchPotato](https://couchpota.to/) via https://github.com/GeoffreyPlitt/docker-couchpotato
- [Headphones](https://github.com/rembo10/headphones#readme) via https://github.com/GeoffreyPlitt/docker-headphones
- [NZBmegasearcH](http://pillone.github.io/usntssearch/) via https://github.com/GeoffreyPlitt/docker-megasearch
- [Sabnzbd](http://sabnzbd.org/) via https://github.com/GeoffreyPlitt/docker-sabnzb
- [Sick Beard](http://sickbeard.com/) via https://github.com/GeoffreyPlitt/docker-sickbeard

---

Usage:

    vagrant up

Then go to:
- CouchPotato: [http://localhost:5050](http://localhost:5050)
- Headphones: [http://localhost:8181](http://localhost:8181)
- NZBmegasearcH: [http://localhost:5000](http://localhost:5000)
- Sabnzbd: [http://localhost:8080](http://localhost:8080)
- Sick Beard: [http://localhost:8081](http://localhost:8081)
