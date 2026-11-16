Built with 
select 
    --spec.name "Spec Name", rsnl.networklistname "List Name", nl.*, 
    distinct nle.transportid, nle.platform_name
from routingspec spec
join routingspecnetworklist rsnl on rsnl.routingspecid = spec.id
join networklist nl on nl.name = rsnl.networklistname and nl.transportmediumtype like 'goes%'
join networklistentry nle on nl.id = nle.networklistid
where spec.datasourceid in (select id from datasource where datasource.datasourcetype = 'lrgs')
order by 
    --spec.name asc, rsnl.networklistname asc,
    nle.transportid asc
;

from cwbi-dev