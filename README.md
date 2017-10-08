VM fængsel til nemid kode
=========================

Hvis du bruger NemID nøglefil kræver det installation af
binær 3. parts kode.

Hvis du er forsigtig (og det burde du være hvis du tager sikkerhed og
privatliv seriøst) og derfor ikke har lyst til at installere den
software der kommer fra NETS , så er der her en Virtuel maskine med
firefox og den nødvendige software for at bruge NemID nøglefil.

Start den virtuelle maskine
---------------------------

```
vagrant up
```

Start firefox
-------------

```
vagrant ssh -- -X LANG=da_DK.UTF-8 firefox -no-remote
```
