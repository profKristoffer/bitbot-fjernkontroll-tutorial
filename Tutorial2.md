## BitBot mottaker med akselerometer

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

Vi trenger tre ulike hvis-setninger for å sjekke hvilke av våre tre variabler vi har mottatt. I hver av hvis-setningene må vi bruke en sammenligningsblokk for å sjekke om ``||radio:name||`` er lik ett av navnene til våre variabler.  

Dra ``||radio:name||`` fra ``||radio:når radio mottar name value||``-blokk og sette den inn i de ulike sammenligningsblokkene og sjekk om det er lik navnet til en av variablene våre.

```blocks
    radio.onReceivedValue(function (name, value){ 
        if(name=="Gass"){
        }
        else if(name=="Sving"){
        }
        else if(name=="Kjør"){
        }
        
    }
```
## Steg 3
Inne i de ulike hvis blokkene skal vi oppdatere variablene våre. Før vi oppdaterer variablene ``||variables:Gass||`` og ``||variables:Sving||`` må vi gjøre noen omregninger med hjelp av ``||Math:regn om||``-blokka. 

Fra fjernkontrollern er ``||variables:Gass||`` -45 når den helles 45 grader fremover og +45 når den helles 45 grader bakover. Dette skal vi regne om slik at den blir 100 når den helles 45 grader frem og -100 når den tippes bakover.  

Lag denne blokka og sett den i den første hvis-setningen  

 ``[Gass = Math.map(-1*value, -45, 45, -100, 100)]``  

På lignende måte varierer ``||variables:Sving||`` fra 45 til -45 og må regnes om til å gå -100 til +100.

Lag denne blokka og sett den i den andre hvis-setningen

 ``[Sving = Math.map(value, -45, 45, -100, 100)]``  

I den siste hvis-setningen trenger vi bare å sette ``||variables:kjør||`` til ``||variables:value||``

```blocks
        radio.onReceivedValue(function (name, value){ 
        if(name=="Gass"){
            Gass = Math.map(-1*value, -45, 45, -100, 100)
        }
        else if(name=="Sving"){
        Sving = Math.map(value, -45, 45, -100, 100)
        }
        else if(name=="Kjør"){
        Kjør=value
        }
        
    }
```









<!---
```blocks

```
``||||``
--->

<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>