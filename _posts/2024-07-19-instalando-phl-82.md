# Instalando o PHL 8.2
## Instalando e configurando sistema PHL - Personal Home Library

Autor e download do PHL - http://www.elysio.com.br

BibliotecaPHL é um sistema para gerenciar uma biblioteca, empréstimo, consulta, cadastros e tudo aquilo que uma biblioteca necessita para funcionar. Aqui mostro como instalar o PHL, não tenho conhecimento de como gerenciar o sistema, banco de dados, usuários, livros e outros.

Todos os passos a seguir deve ser feito com usuário ROOT ou ter acesso sudo.

***Não funciona em 64Bits porque arquivos foram compilados em 32bits.***

Ambiente
```
Linux Debian Lenny Arquitetura 32Bits ou 686.
Apache2 e PHL82

Diretório que vamos usar para descompactar o tar.gz do PHL
/usr/local/src/

Diretorio padrao Apache2, Document Root  
/var/www

Diretorio CGI do apache
/usr/lib/cgi/bin

Diretorio do PHL dentro do apache
/var/www/http

Download  http://www.elysio.com.br/site/downloads.html
```

Instalar o apache e ligar/carregar o modulo CGI.
```
apt-get install apache2
a2enmod cgid
```

Pacotes instalados no sistema, pode usar o comando:
```
dpkg -l | grep -i apache
ii  apache2 2.2.11-2ubuntu2.5   Apache HTTP Server metapackage
ii  apache2-mpm-prefork   2.2.11-2ubuntu2.5   Apache HTTP Server - traditional non-threade
ii  apache2-utils 2.2.11-2ubuntu2.5  utility programs for webservers
ii  apache2.2-common    2.2.11-2ubuntu2.5    Apache HTTP Server common files
ii  libapache2-mod-php5    5.2.6.dfsg.1-3ubuntu4.4 server-side, HTML-embedded scripting languag
ii  libapr1    1.2.12-5ubuntu0.1    The Apache Portable Runtime Library
ii  libaprutil1    1.2.12+dfsg-8ubuntu0.3   The Apache Portable Runtime Utility Library
```

## Instalação

vamos para o diretorio src
```
cd /usr/local/src
```

Faça o download do pacote mais novo no site do fabricante com wget
```
wget -c http://www.elysio.com.br/downloads/phl82_090619.tar.gz
```

vamos descompactar o pacote:
```
tar zxfv phl82_090619.tar.gz
```

um diretorio "http" foi criado, é o conteudo do PHL. Vamos copia-lô  para o diretorio www do apache para que fique acessivel pelo navegador.
```
cp /usr/local/src/http /var/www/. -prav
cd /var/www/http
```

Inicie o apache2
```
/etc/init.d/apache2 start
```

Vamos editar o arquivo cgi-bin/phl82.cip para alterar os caminhos dos arquivos do PHL, vamos colocar o caminho completo nas configurações.Para isso vamos usar o comando ***sed***.Os camandos abaixo fazem essas  alterações.

Faça uma copia do arquivo phl82.cip
```
cp -prav cgi-bin/phl82.cip cgi-bin/phl82.cip.original
```

Alterando o original para o caminho do diretorio apache.
```
more cgi-bin/phl82.cip.original | sed s/http/'var\/www\/http'/g > cgi-bin/phl82.cip
```
