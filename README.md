 <h1>
<p align=center>
P3-Tarefa DIG
</p>
</h1>
<h3>
<p align=center>
Juan Gabriel González Romero
</p>
</h3>

---
## 1-Realiza unha consulta "dig danielcastelao.org" e identifica cada parte da resposta (IN, CNAME, A, QUERY SECTION, ANSWER SECTION, AUTHORITY SECTION, etc)
### Terminal:
```
dig danielcastelao.org

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> danielcastelao.org
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 32604
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;danielcastelao.org.		IN	A

;; ANSWER SECTION:
danielcastelao.org.	77	IN	A	178.211.133.37

;; Query time: 22 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Tue Oct 08 20:08:27 CEST 2024
;; MSG SIZE  rcvd: 63

```
### Header:
``` 
; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> danielcastelao.org
;; global options: +cmd
```
### Answer:
```
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 32604
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1
```
### OPT:
```
;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
```

### QUESTION SECTION:
```
;; QUESTION SECTION:
;danielcastelao.org.		IN	A
```


### ANSWER SECTION:
```
;; ANSWER SECTION:
danielcastelao.org.	77	IN	A	178.211.133.37
```


### Información de la consulta:
```
;; Query time: 22 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Tue Oct 08 20:08:27 CEST 2024
;; MSG SIZE  rcvd: 63
```


---
## 2-Realiza consultas dos seguintes nomes e identifica as diferencias: moodle.danielcastelao.org , www.danielcastelao.org 

A diferencia principal vese no apartado de `AUTHORITY SECTION` e `ANSWER SECTION`
### Terminal moodle.danielcastelao.org
```
dig moodle.danielcastelao.org

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> moodle.danielcastelao.org
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 27061
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;moodle.danielcastelao.org.	IN	A

;; AUTHORITY SECTION:
danielcastelao.org.	300	IN	SOA	ns1.hover.com. dnsmaster.hover.com. 1720467415 1800 900 604800 300

;; Query time: 296 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Tue Oct 08 20:41:46 CEST 2024
;; MSG SIZE  rcvd: 113


```

### Terminal www.danielcastelao.org
```
dig www.danielcastelao.org

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> www.danielcastelao.org
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 42314
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;www.danielcastelao.org.		IN	A

;; ANSWER SECTION:
www.danielcastelao.org.	900	IN	A	178.211.133.37

;; Query time: 167 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Tue Oct 08 20:40:39 CEST 2024
;; MSG SIZE  rcvd: 67


```

---
## 3-Averigua o nome e IP dos servidores de DNS autoritativos de www.danielcastelao.org, por qué soen ser 2 servidores autoritativos?
Soen ser dous servidores pola redundancia, balanceo de carga e resiliencia ante ataques.

Para averiguar o nome da IP usaremos dous comandos relacionados entres sí, o primeiro será para saber cal é o nome:
```
dig ns danielcastelao.org

danielcastelao.org. 900 IN NS ns2.hover.com.
danielcastelao.org. 900 IN NS ns1.hover.com.
```
Con estes nomes utilizaremos o comando `dig A <nome_do_servidor>` para saber a ip:
```
ANSWER SECTION: ns2.hover.com. 6961 IN A 64.98.148.13
ANSWER SECTION: ns1.hover.com. 7065 IN A 216.40.47.26
```



---
## 4-Realiza as consultas de nomes inversas: 130.206.164.68 e de outras dúas IPs que se che ocorran.
Para facer a consulta de nomes inversa utilizaremos o comando `dig -x <IP>`
```
68.164.206.130.in-addr.arpa. 7200 IN PTR pluto.tlm.unavarra.es.
68.164.206.130.in-addr.arpa. 7200 IN PTR s164m68.unavarra.es.
```
E as outras IPs poden ser:
```
dig -x 8.8.8.8
8.8.8.8.in-addr.arpa. 86400 IN PTR dns.google.

dig -x 1.1.1.1
1.1.1.1.in-addr.arpa. 3600 IN PTR one.one.one.one.
```
---
## 5-A qué servidor DNS estás consultando? Cómo o podes cambiar sen tocar os ficheiros de configuración do sistema?
Está consultando a:
```
SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
```
Podes cambiar o servidor DNS facendo o comando:
```
dig @<IP_do_servidor> danielcastelao.org
```
---
## 6-Obtén o rexistro SOA (Start of Authority) do dominio  moodle.danielcastelao.org preguntándolle ó servidor DNS de google e logo preoguntándollo directamente ó servidor primario do dominio danielcastelao.org. 
Para obter o rexistro SOA do primeiro paso faremos o comando:
```
dig @8.8.8.8 SOA moodle.danielcastelao.org
```
E para o segundo paso faremos o comando:
```
dig @ns1.hover.com SOA moodle.danielcastelao.org
```

---
## 7-Consulta a IP de www.elpais.com. Cánto tempo queda almaceado o rexistro de recurso no DNS local?, se preguntas ó DNS local por este recurso, qué observas no TTL do rexistro?
Para consultar a IP faremos:
```
dig www.elpais.com

;; QUESTION SECTION:
;www.elpais.com. IN A

;; ANSWER SECTION:
www.elpais.com. 3600 IN A 23.202.46.103
```
Se lle preguntamos o DNS local daranos un TTL de 3600, o que quere dicir que almacenará a resposta durantee unha hora.
```
```
---
## 8-Busca o TTL de distintos nomes de dominio de servicios que escollas, a qué se poden deber as diferencias?
Busquei o TTL de Google,Facebook e GitHub. Os cales son 300, 60, 3600 segundos respectivamente. Isto pode pasar xa que Facebook e Google son servizos dinámicos e GIthub é un servizo estático.
---
## 9-Determina o TTL máximo (original) dun nome de dominio.
O TTL máximo orixinal dun dominio é o valor definido polo propietario do dominio no servidor DNS autoritativo.
---
## 10-Averigua cántas máquinas con distintas IPs están detrás do dominio web www.google.es, sempre son as mesmas e na mesma orde? por qué?
Google usa múltiples servidores en diferentes localizacións xeográficas e redes para distribuír as solicitudes de usuarios. As IPs varían en función do servidor máis próximo ou dispoñible no momento da consulta.
---
## 11-Pregunta o mesmo a un server raiz (J.ROOTSERVERS.NET por exemplo) e comproba na resposta se o server acepta o modo recursivo

Utilizamos o comando:
```
dig @j.root-servers.net www.google.es

;; flags: qr rd; QUERY: 1, ANSWER: 0, AUTHORITY: 13, ADDITIONAL: 26
```
A bandeira rd (recursion desired) está presente na consulta polo tanto acepta modo recursivo.
---
## 12-Se queremos ver tóda-las queries que fai o servidor de DNS, qué opción temos que usar? averigua a IP de www.timesonline.co.uk, especifica os pasos dados
Para ver todalas queries que fai o servidor faremos o comando:
```
dig +trace www.timesonline.co.uk

<<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> +trace www.timesonline.co.uk
;; global options: +cmd
.			13397	IN	NS	l.root-servers.net.
.			13397	IN	NS	b.root-servers.net.
.			13397	IN	NS	e.root-servers.net.
.			13397	IN	NS	h.root-servers.net.
.			13397	IN	NS	d.root-servers.net.
.			13397	IN	NS	i.root-servers.net.
.			13397	IN	NS	f.root-servers.net.
.			13397	IN	NS	c.root-servers.net.
.			13397	IN	NS	g.root-servers.net.
.			13397	IN	NS	k.root-servers.net.
.			13397	IN	NS	m.root-servers.net.
.			13397	IN	NS	j.root-servers.net.
.			13397	IN	NS	a.root-servers.net.
;; Received 239 bytes from 127.0.0.53#53(127.0.0.53) in 5 ms

;; Received 50 bytes from 192.58.128.30#53(j.root-servers.net) in 2 ms


```

---
## 13-Usando a información dispoñible a traveso do DNS especifica a máquina (nome e IP) ou máquinas que actúan como servers de correo do dominio danielcastelao.org
Para isto utilizamos o comando:
```
dig +trace www.timesonline.co.uk

danielcastelao.org. 900 IN MX 10 mx.hover.com.cust.hostedemail.com.
```

---
## 14-Podes obter os rexistros AAAA de www.facebook.com? a qué corresponden?
Para este último paso faremos:
```
dig AAAA www.facebook.com

www.facebook.com. 60 IN AAAA 2a03:2880:f12f:83:face:b00c::25de

```

---
