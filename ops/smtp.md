# Amboary ny lohamilina fandefasana mailaka SMTP anao manokana

## SAVARANONANDO

Ny SMTP dia afaka mividy mivantana ny serivisy amin'ny mpivarotra rahona, toy ny:

* [Amazon SES SMTP](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [Ali cloud mailaka push](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

Azonao atao ihany koa ny manangana mpizara mailaka anao manokana - fandefasana tsy misy fetra, vidiny ambany.

Eto ambany, asehontsika tsikelikely ny fomba fananganana mpizara mailaka manokana.

## Safidin'ny mpizara

Ny mpizara SMTP mpampiantrano tena dia mitaky IP ho an'ny daholobe misy seranana 25, 456, ary 587 misokatra.

Ny rahona ho an'ny daholobe fampiasa mahazatra dia nanakana ireo seranana ireo amin'ny alàlan'ny default, ary mety ho azo atao ny manokatra azy ireo amin'ny alàlan'ny famoahana baikon'ny asa, saingy tena manahirana tokoa izany.

Manoro hevitra aho hividy amin'ny mpampiantrano manana ireo seranana misokatra ireo ary manohana ny fametrahana anaran-tsehatra mivadika.

Eto, manoro hevitra an'i [Contabo aho](https://contabo.com) .

Contabo dia mpamatsy fampiantranoana miorina ao Munich, Alemaina, naorina tamin'ny 2003 miaraka amin'ny vidiny tena mifaninana.

Raha misafidy Euro ho vola hividianana ianao dia ho mora kokoa ny vidiny (server misy fahatsiarovana 8GB sy CPU 4 dia mitentina eo amin'ny 529 yuan isan-taona, ary maimaim-poana mandritra ny herintaona ny saram-pametrahana voalohany).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

Rehefa mametraka baiko dia `prefer AMD` , ary ny mpizara manana CPU AMD dia hanana fampisehoana tsara kokoa.

Amin'ity manaraka ity dia horaisiko ho ohatra ny VPS an'i Contabo hanehoana ny fomba fananganana mpizara mailaka anao manokana.

## Ny rafitra rafitra Ubuntu

Ny rafitra miasa eto dia Ubuntu 22.04

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Raha ny mpizara amin'ny ssh dia mampiseho `Welcome to TinyCore 13!` (araka ny aseho amin'ny sary etsy ambany), midika izany fa tsy mbola napetraka ny rafitra. Azafady tapaho ny ssh ary andraso minitra vitsivitsy vao hiditra indray.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

Rehefa miseho `Welcome to Ubuntu 22.04.1 LTS` dia vita ny fanombohana, ary afaka manohy ireto dingana manaraka ireto ianao.

### [Tsy azo atao] Atombohy ny tontolon'ny fampandrosoana

Tsy voatery io dingana io.

Ho fanamorana dia apetrako ao amin'ny [github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) ny fametrahana sy ny rafitry ny rindrambaiko ubuntu.

Alefaso ity baiko manaraka ity mba hametrahana amin'ny tsindry iray.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

Ireo mpampiasa Shinoa, azafady ampiasao ity baiko manaraka ity, ary ny fiteny, ny faritry ny ora, sns. dia hapetraka ho azy.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### Contabo dia mamela ny IPV6

Alefaso ny IPV6 mba hahafahan'ny SMTP mandefa mailaka misy adiresy IPV6 ihany koa.

edit `/etc/sysctl.conf`

Ovao na ampio ireto andalana manaraka ireto

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

Araho [ny torolalana contabo: Manampy ny fifandraisana IPv6 amin'ny mpizara anao](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

Amboary `/etc/netplan/01-netcfg.yaml` , ampio andalana vitsivitsy araka ny asehon'ny sary etsy ambany (Efa manana an'ireo andalana ireo ny rakitra Contabo VPS default, esory fotsiny izy ireo).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

Avy eo dia `netplan apply` mba hampiharana ny fandrindrana novaina.

Rehefa vita ny fanamboarana dia azonao atao ny mampiasa `curl 6.ipw.cn` hijerena ny adiresy ipv6 an'ny tambajotra ivelany.

## Clone ny ops fitehirizam-bokatra

```
git clone https://github.com/wactax/ops.soft.git
```

## Mamorona certificat SSL maimaim-poana ho an'ny anaran'ny sehatrao

Ny fandefasana mailaka dia mila taratasy fanamarinana SSL ho an'ny fanafenana sy sonia.

Mampiasa [acme.sh](https://github.com/acmesh-official/acme.sh) izahay hamokarana mari-pankasitrahana.

acme.sh dia fitaovana fanaovana sonia automatique automatique open source,

Ampidiro ny trano fitehirizam-bokatra ops.soft, run `./ssl.sh` , ary hisy fampirimana `conf` hatsangana ao **amin'ny lahatahiry ambony** .

Tadiavo ny mpamatsy DNS anao avy [amin'ny acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) , manova `conf/conf.sh` .

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

Avy eo, mandehana `./ssl.sh 123.com` mba hamoronana mari-pankasitrahana `123.com` sy `*.123.com` ho an'ny anaranao.

Ny hazakazaka voalohany dia hametraka ho azy [acme.sh](https://github.com/acmesh-official/acme.sh) ary hanampy asa voalahatra ho an'ny fanavaozana mandeha ho azy. Hitanao `crontab -l` , misy tsipika toy izao manaraka izao.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

Ny lalana ho an'ny taratasy fanamarinana novokarina dia toy ny `/mnt/www/.acme.sh/123.com_ecc。`

Ny fanavaozana ny certificat dia hiantso ny script `conf/reload/123.com.sh` , ovay ity script ity, azonao atao ny manampy baiko toy ny `nginx -s reload` hamelombelona ny cache certificat amin'ireo rindranasa mifandraika amin'izany.

## Manamboara mpizara SMTP miaraka amin'ny chasquid

[chasquid](https://github.com/albertito/chasquid) dia mpizara SMTP open source voasoratra amin'ny fiteny Go.

Ho solon'ny programa mpizara mailaka taloha toa ny Postfix sy Sendmail, ny chasquid dia tsotra sy mora ampiasaina, ary mora kokoa amin'ny fampandrosoana faharoa.

Run `./chasquid/init.sh 123.com` dia hapetraka ho azy amin'ny tsindry iray (soloo ny 123.com amin'ny anaran'ny sehatra fandefasanao).

## Amboary ny sonia mailaka DKIM

DKIM dia ampiasaina handefa sonia mailaka mba hisorohana ny taratasy tsy ho raisina ho spam.

Rehefa vita soa aman-tsara ny baiko dia hasaina ianao hametraka ny rakitra DKIM (araka ny aseho eto ambany).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

Ampio rakitra TXT fotsiny amin'ny DNS-nao (araka ny aseho etsy ambany).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Jereo ny satan'ny serivisy & diariny

 `systemctl status chasquid` Jereo ny toeran'ny serivisy.

Ny toetry ny fampandehanana ara-dalàna dia aseho amin'ny sary etsy ambany

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` na `journalctl -xeu chasquid` dia afaka mijery ny log de error.

## Avereno ny tefim-pizarana anaran-tsehatra

Ny anaran'ny sehatra mifamadika dia ny mamela ny adiresy IP ho voavaha amin'ny anaran'ny sehatra mifandraika amin'izany.

Ny fametrahana anarana sehatra mivadika dia afaka manakana ny mailaka tsy ho fantatra ho spam.

Rehefa voaray ny mailaka, ny mpizara mpandray dia hanao famakafakana ny anaran'ny sehatra mivadika amin'ny adiresy IP an'ny mpizara fandefasana mba hanamafisana raha manana anarana domain mivadika marina ilay mpizara mpandefa.

Raha toa ka tsy manana anaran-tsehatra mivadika ny mpizara mpandefa na raha tsy mifanandrify amin'ny adiresy IP an'ny mpizara mandefa ny lohamilina mpandefa, dia mety ho fantatry ny mpizara mpandray ny mailaka ho spam na mandà izany.

Tsidiho ny [https://my.contabo.com/rdns](https://my.contabo.com/rdns) ary amboary araka ny aseho eto ambany

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

Aorian'ny fametrahana ny anaran'ny sehatra mivadika dia tadidio ny manamboatra ny famahana ny famahana ny anaran'ny sehatra ipv4 sy ipv6 amin'ny mpizara.

## Amboary ny anaran'ny mpampiantrano chasquid.conf

Amboary `conf/chasquid/chasquid.conf` amin'ny sandan'ny anaran'ny sehatra mivadika.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

Avy eo dia mandehana `systemctl restart chasquid` hamerenana ny serivisy.

## Backup conf amin'ny git repository

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

Ohatra, mamerina ny lahatahiry conf amin'ny fizotry ny github-ko manokana toy izao manaraka izao

Mamorona trano fanatobiana entana manokana aloha

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

Ampidiro ny lahatahiry conf ary alefaso any amin'ny trano fanatobiana entana

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## Ampio mpandefa

mihazakazaka

```
chasquid-util user-add i@wac.tax
```

Afaka manampy mpandefa

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### Hamarino fa napetraka tsara ny tenimiafina

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

Aorian'ny fampidirana ny mpampiasa dia havaozina `chasquid/domains/wac.tax/users` , tadidio ny mandefa azy any amin'ny trano fanatobiana entana.

## DNS manampy rakitra SPF

SPF (Sender Policy Framework) dia teknolojia fanamarinana mailaka ampiasaina hisorohana ny hosoka amin'ny mailaka.

Manamarina ny mombamomba ny mpandefa mailaka izy io amin'ny alàlan'ny fanamarinana fa ny adiresy IP an'ilay mpandefa dia mifanaraka amin'ny firaketana DNS an'ny anaran'ny sehatra lazainy, manakana ny mpisoloky tsy handefa mailaka hosoka.

Ny fampidirana rakitra SPF dia afaka manakana ny mailaka tsy ho fantatra ho spam araka izay azo atao.

Raha tsy mahazaka karazana SPF ny mpizara anaran-tsehatra anao, ampio fotsiny ny rakitra karazana TXT.

Ohatra, ny SPF an'ny `wac.tax` dia toy izao manaraka izao

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

SPF ho an'ny `_spf.wac.tax`

`v=spf1 a:smtp.wac.tax ~all`

Mariho fa `include:_spf.google.com` , izany dia satria hamboariko `i@wac.tax` ho adiresy fandefasana ao amin'ny boaty mailaka Google any aoriana.

## DNS configuration DMARC

DMARC dia fanafohezana ny (Fanamarihana hafatra mifototra amin'ny domaine, tatitra & fampifanarahana).

Ampiasaina izy io mba hisamborana ny fisondrotan'ny SPF (mety vokatry ny hadisoan'ny fandrindrana, na misy olon-kafa mody ho anao handefasana spam).

Ampio rakitra TXT `_dmarc` ,

Toy izao ny votoatiny

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

Ny dikan'ny paramètre tsirairay dia toy izao manaraka izao

### p (Politika)

Manondro ny fomba fitantanana mailaka tsy mahomby ny fanamarinana SPF (Sender Policy Framework) na DKIM (DomainKeys Identified Mail). Ny p parameter dia azo apetraka amin'ny iray amin'ireo soatoavina telo:

* tsy misy: Tsy misy fepetra raisina, ny valin'ny fanamarinana ihany no averina amin'ny mpandefa amin'ny alàlan'ny rafitra fanaovana tatitra mailaka.
* Quarantine: Ampidiro ao amin'ny lahatahiry spam ny mailaka izay tsy nandalo ny fanamarinana, fa aza mandà mivantana ny mailaka.
* mandà: Mitsipaka mivantana ireo mailaka tsy voamarina.

### fo (Safidy tsy fahombiazana)

Mamaritra ny habetsaky ny fampahalalana naverina tamin'ny alàlan'ny rafitra fanaovana tatitra. Azo apetraka amin'ny iray amin'ireto sanda manaraka ireto izany:

* 0: Mitatitra ny valin'ny fanamarinana ho an'ny hafatra rehetra
* 1: Mitatitra hafatra tsy mahomby amin'ny fanamarinana ihany
* d: Mitatitra fotsiny ny tsy fahombiazan'ny fanamarinana ny anaran'ny sehatra
* s: mitatitra fotsiny ny tsy fahombiazan'ny fanamarinana SPF
* l: Mitatitra ny tsy fahombiazan'ny fanamarinana DKIM ihany

### rua & ruf

* rua (Reporting URI for Aggregate reports): Adiresy mailaka handraisana tatitra mitambatra
* ruf (Reporting URI for forensic reports): adiresy mailaka handraisana tatitra amin'ny antsipiriany

## Ampio rakitra MX handefasana mailaka amin'ny Google Mail

Satria tsy nahita boaty mailaka orinasa maimaim-poana izay manohana ny adiresy iraisan'ny rehetra aho (Catch-All, afaka mahazo mailaka alefa amin'ity anaran-tsehatra ity, tsy misy fameperana amin'ny prefixes), dia nampiasa chasquid aho handefasana ny mailaka rehetra amin'ny mailbox-ko.

**Raha manana boaty mailaka ara-barotra karamainao manokana ianao dia aza ovaina ny MX ary tsidiho ity dingana ity.**

Ahitsio `conf/chasquid/domains/wac.tax/aliases` , apetraho ny boaty mailaka

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` manondro ny mailaka rehetra, `i` dia ny tovan'ny adiresy mailaka an'ny mpampiasa nandefa noforonina etsy ambony. Mba handefasana mailaka dia mila manampy tsipika ny mpampiasa tsirairay.

Avy eo ampio ny rakitra MX (Tondroiko mivantana ny adiresin'ny anaran'ny sehatra mivadika eto, araka ny aseho amin'ny andalana voalohany amin'ny sary etsy ambany).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

Rehefa vita ny fanitsiana dia afaka mampiasa adiresy mailaka hafa ianao handefasana mailaka any amin'ny `i@wac.tax` sy `any123@wac.tax` hahitana raha afaka mahazo mailaka ao amin'ny Gmail ianao.

Raha tsy izany dia jereo ny log chasquid ( `grep chasquid /var/log/syslog` ).

## Mandefasa mailaka amin'ny i@wac.tax amin'ny Google Mail

Taorian'ny nahazoan'ny Google Mail ny mailaka dia nanantena aho fa hamaly amin'ny `i@wac.tax` fa tsy i.wac.tax@gmail.com.

Tsidiho ny [https://mail.google.com/mail/u/1/#settings/accounts](https://mail.google.com/mail/u/1/#settings/accounts) ary tsindrio ny "Add another email address".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

Avy eo, ampidiro ny kaody fanamarinana voarain'ny mailaka nampitaina.

Farany, azo apetraka ho adiresin'ny mpandefa default (miaraka amin'ny safidy mamaly amin'ny adiresy mitovy).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

Amin'izany fomba izany, nahavita ny fametrahana ny mpizara mailaka SMTP izahay ary mampiasa ny Google Mail handefasana sy handraisana mailaka.

## Alefaso mailaka andrana mba hijerena raha mahomby ny fandrindrana

Ampidiro `ops/chasquid`

Run `direnv allow` ny fametrahana ny fiankinan-doha (direnv dia napetraka tamin'ny dingana fanombohana tokana teo aloha ary nisy hook iray nampiana ny akorandriaka)

dia mihazakazaka

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

Ny dikan'ny masontsivana dia toy izao manaraka izao

* mpampiasa: SMTP solonanarana
* pass: tenimiafina SMTP
* ho: mpandray

Afaka mandefa mailaka fitsapana ianao.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

Amporisihina ny hampiasa Gmail handraisana mailaka andrana hanamarinana raha mahomby ny fanitsiana.

### TLS encryption mahazatra

Araka ny asehon'ny sary etsy ambany dia misy ity hidin-trano kely ity, izay midika fa nahomby ny fanamarinana SSL.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

Avy eo tsindrio ny "Show Original Email"

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### DKIM

Araka ny asehon'ny sary etsy ambany, ny pejin'ny mailaka Gmail tany am-boalohany dia mampiseho DKIM, izay midika fa mahomby ny fanitsiana DKIM.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

Jereo ny Received amin'ny lohatenin'ny mailaka tany am-boalohany, ary hitanao fa ny adiresy mpandefa dia IPV6, izay midika fa ny IPV6 dia voarindra tsara ihany koa.
