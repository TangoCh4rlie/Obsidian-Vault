2025-03-31
[[perso]] [[Tous ces projets de merde PTN]][[MP3 Schema]]

---

ce qu'il me faudrait :
- [x] pi 0
- [x] ecran LCD
- [ ] boutons
- [x] resistances
- [x] breadboard
- [x] mp3 jack
- [x] headphone jack board
## TODO
- [x] Connecter l'écran
- [ ] Connecter les boutons
- [ ] Alimenter le raspberry avec la batterie
- [ ] Créer la partie server-less pour stocker les musiques sur un R2

### important
32 bit

## concept 
un ecran qui affiche les musiques qu'il y a dans un dossier
pouvoir selesctionner une musique avec des boutons,

bouttons de directions pour choisir les musiques ou naviguer entre les repertoires
un bouton play ou selectionner les dossier

un jack pour pouvoir brancher un casque

pour les fichier mp3, serverless cloudflare et dès que je met un mp3 sur le R2 il est ajouté dans une liste, facile pour la synchro


[jack](https://forums.raspberrypi.com/viewtopic.php?t=127585)
[raspberry pins](https://www.etechnophiles.com/raspberry-pi-zero-gpio-pinout-specifications-programming-language/)
https://github.com/adafruit/Adafruit_CircuitPython_CharLCD?tab=readme-ov-file
https://umatechnology.org/how-to-play-mp3-and-other-audio-files-on-a-raspberry-pi/

https://www.instructables.com/Passive-Low-Pass-Filter-for-Audio-Circuits-Free-Fo/

pour la batterie
https://www.circuitbasics.com/how-to-power-your-raspberry-pi-with-a-lithium-battery/
amazon
https://www.amazon.fr/EEMB-103395-Rechargeable-Navigation-Enregistreur/dp/B08215B4KK/262-1195336-3091451?pd_rd_w=pOGaq&content-id=amzn1.sym.f4202548-28b9-4238-addd-1e87d5d2f948%3Aamzn1.symc.15cbde64-36a4-47c6-b315-5d1a0d7227bc&pf_rd_p=f4202548-28b9-4238-addd-1e87d5d2f948&pf_rd_r=Z24YV2GJQRX0CY47SST2&pd_rd_wg=tKxel&pd_rd_r=86068bf0-2568-4fa5-a0fd-b133578adc5b&pd_rd_i=B08215B4KK&th=1


### DOC

https://cdn.velleman.eu/downloads/29/infosheets/vma2031602datasheet.pdf
https://www.youtube.com/watch?v=cVdSc8VYVBM

### ServerLess 
https://aws.amazon.com/blogs/media/processing-user-generated-content-using-aws-lambda-and-ffmpeg/
https://docs.aws.amazon.com/lambda/latest/dg/chapter-layers.html


## LOG
jour 1, j'arrive enfin a afficher du texte sur mon écran grace a ce [fichier](https://cdn.velleman.eu/downloads/29/infosheets/vma203_scheme.pdf) 
je me rend compte que le shield que j'ai en plus de l'écran avec les bouton est un peu chiant et que ca va etre compliqué + techniquement pas trop possible. les 5 boutons sont sur une seule sortie analogique et le rasbperry pi 0 n'est pas compatible avec certaines lib pour lire de l'analogique

ligne super importante
dtoverlay=audremap,pins_18_19



