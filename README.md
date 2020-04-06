# Pharmacies Portugal

**UPDATE**: _It has been almost two years since I left Portugal, and I haven't touched this idea since. It doesn't really make sense for me to pursue this project any further. I leave this repository online just in case someone might find this little information useful, but it is also possible that there are beter online resources available now than back in 2018 when I started looking into this._

This is an attempt at programmatically gathering information of pharmacy opening times and locations around Portugal, and providing an API that would allow client applications to utilize this data.

## Why?

Because most pharmacies are closed on Sundays, and the few online services that provide pharmacy information and pretty bad at this task. There's also no publicly available pharmacy API or easily parsable data available (to my best knowledge).

## Where does the data come from?

Portuguese national healthcare service [SNS](https://www.sns.gov.pt) is split in seven different regions. Each region decides which pharmacies provide extended service on every day of a year. They publish this information once a year on their own websites. The publication comes in a form of multiple PDF files, with one of the regions providing only a link to a zip archive containing the PDFs. The format of PDFs changes from region to region.

List of regions and URLs that link to pharmacy extended service documents:
- Acores: http://www.azores.gov.pt/Portal/pt/entidades/srs-drs/textoImagem/FVMNSRM.htm
- Alentejo: http://www.arsalentejo.min-saude.pt/utentes/Farmacias/Paginas/PesquisaFarmacias.aspx?providerType=21&district=7&council=0
- Algarve: http://www.arsalgarve.min-saude.pt/farmaciasfarmacias-de-servico-para-2017content/farmacias-de-servico-para-2018/#content
- Centro: http://www.arscentro.min-saude.pt/Noticias/Paginas/TurnodasFarmácias2018.aspx
- Lisboa e Vale do Tejo (based on Google search, not confirmed, currently returns 503): http://www.arslvt.min-saude.pt/frontoffice/pages/949
- Madeira: http://iasaude.sras.gov-madeira.pt/Lista.cfm?Tipo=999#
- Norte: http://www.arsnorte.min-saude.pt/farmacias/

It is also possible to fetch some information about all Portuguese pharmacies from SNS in a JSON format. The data contains mostly names and addresses of all pharmacies. Here's an example cURL request:

```
curl -v -X "POST" "https://www.sns.gov.pt/wp-admin/admin-ajax.php" \
     -H 'Content-Type: application/x-www-form-urlencoded; charset=utf-8' \
     --data-urlencode "action=healthProviders" \
     --data-urlencode "nonce=a511872caf" \
     --data-urlencode "method=search" \
     --data-urlencode "providerSubType=21" \
     --data-urlencode "regionId=0" \
     --data-urlencode "districtId=0" \
     --data-urlencode "providerName="
```

## Other websites that provide similar service

A couple of website seem to provide accurate data about pharmacy opening times:
http://www.farmaciasdeservico.net
https://www.revistasauda.pt/localizar/pages/default.aspx


