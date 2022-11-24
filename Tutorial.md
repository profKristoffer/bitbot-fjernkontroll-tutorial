# Bitbot-fjernkontroll med akselerometer

## Introduksjon

Vi skal nå lage en fjernkontroll for å styre vår Bitbot basert på helningsvinkelen til fjernkontrollen. Dette gir god presisjon når vi skal styre bitboten, men det kan være litt komplisert å programmere.
Fjernkontrollen vår skal sende data fra akselerometeret til vår mottaker, den skal bruke en LED på fjernkontrollens skjerm til å gi oss en indikasjon på hvordan vi styrer og vi skal bruke en av knappene på fjernkontrollen til å starte og stoppe Bitboten.

## Steg 1

I ``|basic:ved start|`` velger vi en radiogruppe og lager tre variabler, ``||variables:Gass||``, ``||variables:Sving||`` og ``||variables:Kjør||``. Sett ``||variables:Gass||`` og ``||variables:Sving||`` til 0 og sett ``||variables:Kjør||`` til -1.
Vi kommer til å bruke ``||variables:Kjør||`` til å styre om bitboten skal kjøre eller ikke ved å variere mellom -1 og 1. -1 kommer til å bety at bitboten ikke skal kjøre, mens 1 betyr at bitboten skal kjøre.


```blocks
radio.setGroup(1)
Gass=0;
Sving=0;
Kjør= -1;
```
## Steg 2

I ``||basic:gjenta for alltid||`` skal vi oppdatere variablene våre med målinger fra akselerometeret. Sett ``||variables:Gass||`` og ``||variables:Sving||`` til å være ``||input:helningsvinkelen||``. Vi ønsker at ``||variables:Gass||`` skal settes til helningsvinkelen forover-bakover og ``||variables:Sving||`` til helningsvinkelen høyre-venstre.
Legg også inn blokker for å sende alle tre variablene med ``||radio:radio send verdi||``. 
```blocks
basic.forever(function () {
Gass = input.rotation(Rotation.Pitch)
Sving = input.rotation(Rotation.Roll)

radio.sendValue("Gass", Gass)
radio.sendValue("Sving", Sving)
radio.sendValue("Kjør", Kjør)
})

```

## Steg 3
Vi skal bruke knapp A til å styre om vår Bitbot skal kjøre eller ikke kjøre. Hvis vi setter vår variabel ``||variables:Kjør||`` til å være -1 skal Bitboten stoppe. Hvis vi setter den til 1
Koden vår må da kunne sette variabelen til 1 hvis verdien var -1 og sette den til -1 hvis verdien var 1. Prøv deg frem for å finne en løsning på dette, eller se hintet for å se et forslag.

```blocks
input.onButtonPressed(Button.A, function(){
Kjør = -1*Kjør
})
```




<!---
```blocks

```
``||||``
--->

<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>