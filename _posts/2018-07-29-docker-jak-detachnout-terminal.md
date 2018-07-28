---
title: Jak "odpojit" terminál od běžícího Docker kontejneru, ale nezastavit ho?
date:  2018-07-29 00:20 +0200
tags: [docker, terminál]
---
Pokud začínáte s [_Dockerem_][1], pravděpodobně spouštíte kontejnery pomocí příkazu jako tento:
`docker run -i -t NazevObrazu /bin/bash`. Po stisknutí ENTERu se okamžitě spustí nový kontejner
na základě obrazu `NazevObrazu` a dostanete se do `bash`e uvnitř něj. Můžete samozřejmě napsat
`exit` a z kontejneru se dostanete ven, ale tím ho zároveň zastavíte (uvedete do stavu `exitted`).
Jak se tedy dostat z kontejneru ven, aniž bychom ho tím zároveň zastavili?

Pro názornost budu v příkazech používat obraz [`debian:experimental`][2], který lze stáhnout
příkazem `docker pull debian:experimental`.

Správnou odpovědí je stisknout `CTRL`+`p` a hned poté `CTRL`+`q`. Tím se váš terminál přepne
z `bash`e uvnitř kontejneru do původního `bash` v hostitelském počítači, ale kontejner pořád
poběží. Vizte tuto ukázku:

```bash
mmares@nb:~/diapozitivy$ sudo docker run -i -t debian:experimental
root@48c9f7e155c5:/# zde dejte CTRL+p, CTRL+q
mmares@nb:~/diapozitivy$ sudo docker ps
CONTAINER ID        IMAGE                 COMMAND             CREATED             STATUS              PORTS               NAMES
48c9f7e155c5        debian:experimental   "bash"              21 seconds ago      Up 19 seconds                           angry_jepsen
mmares@:~/diapozitivy$
```

Další možností je spouštět kontejnery příkazem `docker run -i -t -d NazevObrazu /bin/bash`,
kde `-d` znamená "detached" - kontejner se rovnou spustí na pozadí a nemusíte tak provádět
výše uvedenou klávesovou kombinaci.

```bash
mmares@mirek-nb:~/diapozitivy$ sudo docker run -i -t -d debian:experimental
085abeb9658a9aecd63412d1eaae0ea53f29c12bff2da407c746a4b412019822
mmares@mirek-nb:~/diapozitivy$
```

Ke kontejneru se pak můžete připojit pomocí příkazu `docker attach ContainerID`.

```bash
mmares@mirek-nb:~/diapozitivy$ sudo docker attach 085abeb9658a9aecd63412d1eaae0ea53f29c12bff2da407c746a4b412019822
root@085abeb9658a:/#
```

Diskusi na téma tohoto článku a související informace ohledně spouštění kontejnerů v Dockeru
můžete najít v diskusi na [Stack Overflow][3]
jménem [Correct way to detach from a container without stopping it][4].

[1]: https://www.docker.com/
[2]: https://hub.docker.com/_/debian/
[3]: https://stackoverflow.com/
[4]: https://stackoverflow.com/questions/25267372/correct-way-to-detach-from-a-container-without-stopping-it
