### Volumes em Docker

Volumes são uma forma de persistência de dados dentro do universo Docker, sendo estes baseados em diretórios do sistema de arquivo da máquina _host_. Em outras palavras, volume é um mecanismo preferencial para persistir dados que são gerados e/ou manuseados pelos containers. 

**Algumas vantagens do uso de volumes**
+ Facéis de fazer _backup_ ou migração;
+ Fácil gerenciamento via CLI;
+ Podem ser facilmente compartilhados entre containers.

**Montagem do volume** -- há três tipos de montagem de volumes:
+ **_Bind_** : utiliza-se uma pasta presente no _host_ que será montada em um alvo específico dentro do container;
+ **_Volume_** : também conhecido como _Named Volume_, utiliza-se a infraestrutura de volume do Docker, que pode tanto utilizar plugins locais quanto plugins que possibilitam fazer integração com outros serviços externos;
+ **_TmpFS_** : permite reservar um espaço em memória para montagem, sendo útil para dados que possuem um alto nível de mutabilidade mas que não precisam persistir em caso de remoção do container.   

