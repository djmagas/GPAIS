# GPAIS

## INFO.txt
Pakeisti rakto formatą į pem:

cat id_rsa | awk 'BEGIN{print "-----BEGIN RSA PRIVATE KEY-----"}; {print}; END{print "-----END RSA PRIVATE KEY-----"}' > id_rsa.pem

komanda kurios pagalba galima susigeneruot slaptažodį:

echo -n "$SubjektoKodas|"`date +%s%3N` | openssl pkeyutl -sign -inkey id_rsa.pem | base64 -w 0

Testavau su openssl versija 1.1.0g


vietoj $SubjektoKodas reiktų įrašyt subjekto kodą arba scripte prieš tai padeklaruot.
privataus rakto failas turi vadintis id_rsa (arba galit pasikeist)


Postman programą galima atsisiųsti iš čia:
https://www.getpostman.com/apps

Pabandykite patikrinti ar sėkmingai naudojate servisus su ping/pong:

https://tst.gpais.eu/o/vvs/zrn/journal/ping - testinėje aplinkoje
https://www.gpais.eu/o/vvs/zrn/journal/ping - produkcinėje aplinkoje

atsakymas būtų "pong".

Importo nuorodos:
https://www.gpais.eu/o/vvs/srv/products/import
https://www.gpais.eu/o/vvs/zrn/journal/import


## RAKTAI.txt
Bash pavyzdžiai, ištestavau sėkmingai ant www.gpais.eu:

echo -n "99999999|`date +%s%3N`" | openssl pkeyutl -sign -inkey /path/to/id_rsa.pem | base64 -w 0

arba

echo -n "99999999|`date +%s%3N`" | openssl rsautl -sign -inkey /path/to/id_rsa.pem  | base64 -w 0


Atkreipti dėmesį, kad nurodomas pem formato raktas. Galima pasinaudoti šia komanda:

cat id_rsa | awk 'BEGIN{print "-----BEGIN RSA PRIVATE KEY-----"}; {print}; END{print "-----END RSA PRIVATE KEY-----"}' > id_rsa.pem


Bei siūlau iš sistemos pakartotinai parsisiųsti raktų porą, kadangi kaskart parsisiuntus, senieji nebetinka.


Padding'as standartinis. Stiprumas pagal raktą.

## REGISTRACIJOS-ID.txt
Užregistravus GII sąvade ID turi būti suteikiamas automatiškai.
Reikia atsiųsti vartotojo atstovaujamų subjektų srautų registracijos sąrašą. Tai galėsite padaryt VVS sąsajos pagalbos skyriuje:

https://screencast.com/t/Svh19dUFtKez

Tai bus csv failas. Jame "Registracijos ID" stulpelyje rasite identifikatoriaus reikšmę.
