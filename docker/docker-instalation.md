### Instalação do Docker
Existem basicamente duas vertentes de como instalar o Docker dentro de uma máquina.

+ **Para Sistemas Linux** : o Docker _host_ é a própria instalação do SO Linux, isso porque o Dockeré fortemente baseado no LXC, que é uma tecnologia Linux. Sendo assim, o Docker _client_, o Docker _engine_ e os containers rodam no mesmo ambiente;
+ **Para Sistemas MacOS** : o _kernel_ do MacOS não é compatível com o mesmo existente em distribuições Linux. Por essa razão, é criado uma VM Linux a qual será o Docker _host_, onde o Docker _engine_ e os containers irão ser executados mas o Docker _client_ continuará sendo executado no mesmo ambiente do SO, acessando o Docker _engine_ de forma remota. A criação dessa VM é feita de forma automática pelo Docker, se tornando transparente ao usuário;
+ **Para Sistemas Windows** : o sistema windows possui um detalhe em particular. Para versões antigas do Windows 10 que não possuem o módulo WSL (_Windows Subsystem for Linux_) ou para versões anteriores (8, 7 etc) segue-se da mesma forma como ocorre em sistemas MacOS. Caso seja uma versão do Windows 10 que possua o módulo WSL, segue-se da forma como ocorre em sistemas Linux.

![Docker Install illustration](https://github.com/islanrodrigues/my-personal-annotations/blob/master/images/docker/docker_install.png)