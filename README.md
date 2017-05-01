VM fængsel til nemid kode
=========================

Hvis du ikke stoler på den software der kommer fra NETS (og det burde
du ikke gøre hvis du tager sikkerhed og privatliv seriøst), så er der
her en Virtuel maskine med firefox og den nødvendige software for at
bruge NemID.

Start den virtuelle maskine
===========================

```
vagrant up
```

Start firefox
=============

```
vagrant ssh -- -X LANG=da_DK.UTF-8 firefox -no-remote
```

Kendte fejl
===========

Webside indholdet bliver vist på engelsk
----------------------------------------

Når man besøger visse sider bliver webside indholdet vit på engelsk.
Dette skyldes at `Accept-Language` HTTP request header ikke bliver sat korrekt. Det er en [kendt fejl](https://bugs.launchpad.net/ubuntu/+source/firefox/+bug/1527663) i Firefox.

Man kan løse dette ved at

    1. Besøge `about:preferences#content`
    2. Vælg Sprog, byt om på rækkefølge og click OK
    3. Vælg Sprog, sæt rækkefølge tilbage igen og click OK


