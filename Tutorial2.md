# BitBot mottaker med akselerometer

Vi skal nå lage koden for en BitBot slik at den kan bli fjernstyrat av en fjernkontroll basert på akselerometeret. Du finner link til tutorial for både mottaker og fjernkontroll her: https://profkristoffer.github.io/bitbot-fjernkontroll-tutorial/  

Vår mottaker skal bruke motta radiosignalene som blir sendt fra fjernkontrollern, lagre disse i variabler og bruke de til å kjøre en BitBot.

## Steg 1
I ``||Basic: ved start||`` må vi velge radiogruppe ved å bruke ``||radio: radio sett gruppe||``. **Husk** at du må velge samme radiogruppe som fjernkontrollern din!  

Vi må også lage tre ``||variables:variabler||``, ``||variables:Gass||``,``||variables:Sving||`` og ``||variables:kjør||``. Sett  ``||variables:gass||`` og ``||variables:styr||`` lik 0 og sett ``||variables:kjør||`` til -1.

```blocks
    radio.setGroup(1);
    Gass=0;
    Sving=0;
    Kjør=-1:
```

## Steg 2
Nå skal vi begynne å motta verdiene som vår fjernkontroll sender over radioen.  

Finn en ``||radio:når radio mottar name value||``-blokk og dra den inn i arbeidsområdet. Inne i denne blokken legger du en ``||logic:Hvis||``-blokk.  










<!---
```blocks

```
``||||``
--->

<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>