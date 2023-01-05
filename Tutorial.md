# Bitbot-fjernkontroll med akselerometer

## Introduksjon

Vi skal nå lage en fjernkontroll for å styre vår Bitbot basert på helningsvinkelen til fjernkontrollen. Dette gir god presisjon når vi skal styre bitboten, men det kan være litt komplisert å programmere.
Fjernkontrollen vår skal sende data fra akselerometeret til vår mottaker, den skal bruke en LED på fjernkontrollens skjerm til å gi oss en indikasjon på hvordan vi styrer og vi skal bruke en av knappene på fjernkontrollen til å starte og stoppe Bitboten.  

Du finner link til tutorial for både mottaker og fjernkontroll her: https://profkristoffer.github.io/bitbot-fjernkontroll-tutorial/ 

## Steg 1

I ``||basic:ved start||`` velger vi en radiogruppe og lager tre variabler, ``||variables:Gass||``, ``||variables:Sving||`` og ``||variables:Kjør||``. Sett ``||variables:Gass||`` og ``||variables:Sving||`` til 0 og sett ``||variables:Kjør||`` til -1.
Vi kommer til å bruke ``||variables:Kjør||`` til å styre om bitboten skal kjøre eller ikke ved å variere mellom -1 og 1. -1 kommer til å bety at bitboten ikke skal kjøre, mens 1 betyr at bitboten skal kjøre.


```blocks
radio.setGroup(1)
Gass=0;
Sving=0;
Kjør= -1;
```
## Steg 2

I ``||basic:gjenta for alltid||`` skal vi oppdatere variablene våre med målinger fra akselerometeret. Sett ``||variables:Gass||`` og ``||variables:Sving||`` til å være ``||input:helningsvinkelen||``. Vi ønsker at ``||variables:Gass||`` skal settes til helningsvinkelen forover-bakover og ``||variables:Sving||`` til helningsvinkelen høyre-venstre.  
Legg også inn blokker for å sende **alle tre** variablene med ``||radio:radio send verdi||``.  

**Merk!** Variabelen ``||input:helningsvinkelen||`` går fra -180 grader til 180 grader og viser retningen en micro:bit holdes. Målingene på ``||input:helningsvinkelen||`` forover-bakover vil være negative når vi heller en micro:bit fremover og positive når vi heller den bakover. Dette er det motsatte av hva vi egentlig ønsker! Dette skal vi rette på i koden til mottakeren.
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
Vi skal bruke knapp A til å styre om vår Bitbot skal kjøre eller ikke kjøre. Hvis vi setter vår variabel ``||variables:Kjør||`` til å være -1 skal Bitboten stoppe. Hvis vi setter den til 1 skal Bitboten kjøre.  
Koden vår må da kunne sette variabelen til 1 hvis verdien var -1 og sette den til -1 hvis verdien var 1. Prøv deg frem for å finne en løsning på dette, eller se hintet for å se et forslag.

```blocks
input.onButtonPressed(Button.A, function(){
Kjør = -1*Kjør
})
```

## En lysende indikator @showhint
Vi ønsker også å lage en LED-indikator som viser hvordan vi styrer. Dette kan vi gjøre ved å bruke ``||led: tenn x = 0, y = 0||``-blokken.  
Med denne blokken kan vi angi hvilken av de 25 LED som skal tennes på skjermen, hvor vi bruker ``||LED:x||`` til å si hvor lyset skal være fra venstre til høyre og ``||LED:y||`` til å si hvor lyset skal være fra topp til bunn. ``||LED:x||`` og ``||LED:y||`` kan ha 0 til 4 som verdi.

Her ser vi et eksempel på hvordan vi først kan få den midterste LEDen til å lyse også den øverst til venstre.

```blocks
led.plot(2,2)
led.plot(0,0)
```

## Regn om @showhint
Siden ``||led: tenn x = 0, y = 0||`` kun kan ta imot tall mellom 0 og 4 må vi regne om våre verdier fra akselerometeret. Blant ``||Math: Matematikk||``-blokkene har vi en ``||math: regn om||``-blokk som kan gjøre akkurat dette! For å bruke den må vi først si hvilken variabel vi skal regne om. Deretter hva som er variabelens minste og største verdi og hva som skal være den minste og høyeste verdien som vi ønsker å få tilbake.   

Her ser vi et eksempel på hvordan denne blokken kan brukes. Variebelen ``||variables: prosent||``, som er et tall mellom 0 og 100, og regnes her om til et tall mellom 0 og 4.
 
```blocks
let prosent = randint(0,100)
basic.showNumber(Math.map(prosent, 0,100, 0,4))
```

## Steg 4
La oss sette det sammen! Bruk ``||LED: tenn||``- og ``||math: regn om||``-blokkene til å få vår indikator til å lyse. Bruk variabelen ``||variables:Sving||`` til ``||LED:x||`` verdi og ``||variables:Gass||`` til ``||LED:y||`` verdi. Legg inn at disse variablene kan variere mellom -45 og 45. De skal regnes om til verdier mellom 0 og 4.  

Vi må også legge inn en ``||basic:tøm skjerm||``-blokk for å viske bort vår gamle indikator. Legg ``||basic:tøm skjerm||`` rett **over** ``||LED: tenn||``-blokka. Hvis du gjør det omvendt vil vi ikke se lyset siden LEDen blir skrudd av før vi oppfatter det.
```blocks
basic.forever(function () {
Gass = -1* input.rotation(Rotation.Pitch)
Sving = input.rotation(Rotation.Roll)
radio.sendValue("Gass", Gass)
radio.sendValue("Sving", Sving)
radio.sendValue("Kjør", Kjør)

// @highlight
basic.clearScreen()

// @highlight
led.plot(Math.map(Sving, -45, 45, 0, 4), Math.map(Gass, -45, 45, 0, 4))

})


```

<!---
```blocks

```
``||||``
--->

<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>