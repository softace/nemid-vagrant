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
