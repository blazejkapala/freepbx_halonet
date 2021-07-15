# Sprawdzone ustwaienia centrali freepbx z polskim dostawcą VoIP - halonet

## Założenia
Poniższe ustawienia działają dla rozwiązania, że postronie halonet jest:
- jedno konto telefoniczne,
- pod które podpięte jest kilka numerów telefonicznych.

FreePBX:
- rozpoznaje numer na jaki wykonywane jest połączenie i przekierowuje je do właściwego celu,
- w zależności od ustawionych warunków, połączenie jest realizowane przez różne numery telefoniczne, które są podpięte do jednego konta telefonicznego w halonet

Edycja dotyczyła poprawnych ustawień dla sip przychodzącego i wychodzącego

### Trunk -> sip settings -> outbund -> PEER Details:
```
host=sip.halonet.pl
trustrpid=yes
sendrpid=yes
defaultuser=KONTO_TELEFONICZNE_HALONET_NIE_GŁÓWNE
secret=HASLO_DO_KONTA_TELEFONICZNEGO
fromuser=KONTO_TELEFONICZNE_HALONET_NIE_GŁÓWNE
type=friend
qualify=yes
disallow=all
allow=alaw&ulaw
;allow=g729
directmedia=no
insecure=invite
```

### Trunk -> sip settings -> inbund -> USER Details:
```
host=sip.halonet.pl
context=from-pstn-toheader
defaultuser=KONTO_TELEFONICZNE_HALONET_NIE_GŁÓWNE
secret=HASLO_DO_KONTA_TELEFONICZNEGO
fromuser=KONTO_TELEFONICZNE_HALONET_NIE_GŁÓWNE
type=friend
disallow=all
allow=alaw&ulaw
;allow=g729
directmedia=no
qualify=yes
insecure=invite
```

### Trunk -> sip settings -> inbund -> USER Details:
```
KONTO_TELEFONICZNE_HALONET:HASLO_DO_KONTA_TELEFONICZNEGO@sip.halonet.pl/KONTO_TELEFONICZNE_HALONET
```



### Connectivity -> Inboud Routes 
```
Warunki dla poszczególnych numerów telefonów które są przypisane do konta telefonicznego w halonet. 
Numer DID należy podawać wraz z 48.
```

### Connectivity -> outband routes -> Route CID 
```
Ustawiamy numer jaki mamy podpięty do konta w halonet z którego będzie korzystać to wyjście, numer należy wpisać wraz z 48.
Dodatkowo zaznaczamy Override Extension na "Yes"
```

