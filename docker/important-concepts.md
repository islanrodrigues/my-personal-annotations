### Conceitos Importantes
O Docker é uma tecnologia de virtualização, porém ele não é uma tecnologia de virtualização tradicional baseado em máquinas virtuais (VMs). Em outras palavras, o Docker é uma _engine_ de administração de containers. O Docker se baseia em uma tecnologia chamada de LXC (Linux Containers). Essa tecnologia é pertencente ao sistema Linux.

![LXC vs Docker illustration](https://github.com/islanrodrigues/my-personal-annotations/blob/master/images/docker/lxc_vs_docker.png)

**Containers** -- é um processo segregado; isolado do sistema _host_, onde a partir deste processo é possível iniciar aplicações também de forma isolada do sistema _host_. Associado a esse container existe também um sistema de arquivos completo e isolado, permitindo executar o seu _software_ dentro de uma ambiente o mais controlado possível. Em outras palavras, são ambientes leves e portáteis no qual aplicações são executadas, onde todos os binários e bibliotecas necessárias são encapsuladas para a execução de uma aplicação. As boas práticas dizem que um container deve ser o mais minimalista possível, o que permite evoluir de forma mais profissional, isso porque você adquire um ambiente mais flexível, onde o container fica totalmente dedicado a uma demanda em específico.


**O que difere Containers de Máquinas Virtuais** -- o conceito de containers se difere do conceito de VMs pelo fato de necessitar de recursos da máquina _host_. O container não é executado de forma totalmente independente da máquina _host_ (como é o caso da VM). Dentre estes recursos compartilhados entre o container e o sistema _host_ está principalement o _kernel_, binários, bibliotecas etc. Desta forma, o container tem uma necessidade de processamento e memória muito menor se comparado a uma máquina virtual.

![VM vs Container illustration](https://github.com/islanrodrigues/my-personal-annotations/blob/master/images/docker/vm_vs_container.png)

**Imagens Docker** -- uma imagem, em Docker, é um modelo de sistema de arquivos somente leitura usado para criar um container. Um container está associado a processo (executando na mémoria) enquanto a imagem está relacionada a um arquivo, onde dentro deste existe um sistema de arquivo no qual o container irá se basear para montar a sua estrutura de processo. As imagens podem ser criadas através de um processo chamado de **build** ou de um comando chamado de **commit**, sendo este último desencorajado e considerado uma má prática. As imagens podem ser armazenadas em repositórios e disponibilizados para outras pessoas. Esses repositórios são hospedados em ambientes chamados de _Registry_, sendo o mais comum deles o _Registry_ próprio do Docker (vide [Dockerhub](https://hub.docker.com/)). As imagens são compostas por uma ou mais camadas (_layers_), onde cada camada representa uma ou mais mudanças no sistema de arquivo. A junção destas é o que forma a imagem Docker. Somente a última camada pode ser alterada quando um container for iniciado. O objetivo dessa divisão em camadas é justamente a questão do reuso, onde se torna possível uma imagem ser composta a partir de camadas de outras imagens.

**Arquitetura básica do Docker** -- o Docker é dividido em pelo menos duas partes. Existe o **Daemon** - também conhecimento como _Docker server_ ou _Docker engine_ - e a parte relacionada ao cliente (_client_); permitindo acessar o **Daemon** via interface de linha de comando (CLI) que se encontra instalada na mesma máquina em que o Docker se encontra, via app (API REST) ou via ferramenta gráfica.

![Docker Architecture illustration](https://github.com/islanrodrigues/my-personal-annotations/blob/master/images/docker/docker_architecture.png)



