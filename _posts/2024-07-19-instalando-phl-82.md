# Instalando o PHL 8.2
## Instalando e configurando sistema PHL - Personal Home Library

Autor e download do PHL - http://www.elysio.com.br

BibliotecaPHL é um sistema para gerenciar uma biblioteca, empréstimo, consulta, cadastros e tudo aquilo que uma biblioteca necessita para funcionar. Aqui mostro como instalar o PHL, não tenho conhecimento de como gerenciar o sistema, banco de dados, usuários, livros e outros.

Todos os passos a seguir deve ser feito com usuário ROOT ou ter acesso sudo.

***Não funciona em 64Bits porque arquivos foram compilados em 32bits.
As informações inseridas em arquiterura 64 ficam todas bagunçadas,
sem nenhum sentido de leitura.***

Ambiente
```
Linux Debian Lenny Arquitetura 32Bits ou 686.
Apache2 e PHL82

Diretório que vamos usar para descompactar o tar.gz do PHL
/usr/local/src/

Diretorio padrao Apache2, Document Root  
/var/www

Diretorio CGI do apache2
/usr/lib/cgi/bin

Diretorio do PHL dentro do apache2
/var/www/http

Download http://www.elysio.com.br/site/downloads.html
```

Instalar o apache2 e ligar/carregar o modulo CGI.
```
apt-get update
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

O conteudo original do arquivo
```
phl_*=/http/bases/phl_*
actab=/http/bases/actab
uctab=/http/bases/uctab
menu*=/http/www/phl82/html/menu*
cabe*=/http/www/phl82/html/cabe*
mens*=/http/www/phl82/html/mens*
rest*=/http/www/phl82/html/rest*
inde*=/http/www/phl82/html/inde*
logo*=/http/www/phl82/html/logo*
atra*=/http/www/phl82/php/mail_lote/atra*
aler*=/http/www/phl82/php/mail_lote/aler*
disp*=/http/www/phl82/php/mail_lote/disp*
usua*=/http/www/phl82/php/mail_lote/usua*
phl.css=/http/www/phl82/css/phl.css
tab_*=/http/cgi-bin/phl82/tabs/tab_*
```

como deve ficar
```
00*=/var/www/http/bases/00*
phl_*=/var/www/http/bases/phl_* actab=/var/www/http/bases/actab
uctab=/var/www/http/bases/uctab
menu*=/var/www/http/www/phl82/html/menu*
cabe*=/var/www/http/www/phl82/html/cabe*
mens*=/var/www/http/www/phl82/html/mens*
rest*=/var/www/http/www/phl82/html/rest*
inde*=/var/www/http/www/phl82/html/inde*
logo*=/var/www/http/www/phl82/html/logo*
atra*=/var/www/http/www/phl82/php/mail_lote/atra*
aler*=/var/www/http/www/phl82/php/mail_lote/aler*
disp*=/var/www/http/www/phl82/php/mail_lote/disp*
usua*=/var/www/http/www/phl82/php/mail_lote/usua*
phl.css=/var/www/http/www/phl82/css/phl.css
tab_*=/var/www/http/cgi-bin/phl82/tabs/tab_*
```

Verifique se o arquivo foi alterado corretamente:
```
more cgi-bin/phl82.cip
```

Feito isso, vamos criar um link do PHL para o diretorio CGI do apache:
```
ln -s /var/www/http/cgi-bin/* /usr/lib/cgi-bin/.
```

Vamos criar outro link, do PHL82 para a raiz do diretorio apache, assim deixamos o sistema PHL acessivel pelo navegador.
```
ln -s /var/www/http/www/phl82 /var/www/.
```

Permissão para o Apache2
```
chown www-data.www-data /var/www/http -R
```

Agora já podemos acessar o PHL pelo navegador, http://ip_servidor/phl82/, se você quer acessar apenas o endereço do servidor e ir direto ao PHL82, faça o link do phl82/index.html para o document root do apache /var/www criando um simbolic link.
```
ln -s http/www/phl82/index.html /var/www/. -f
```

Agora é só acessar o http://ip_servidor com o navegador que irá abrir diretamente o PHL82.

## Erro e solução
### PHL 82 - index.html - valido
Nota sobre copyright contida no arquivo "index.html" foi violada!

Solução
```
phl82.cip - caminho para diretorio está incorreto, verificar todos ou conteúdo do index.html foi alterado errado.
```

### Erro com Ubuntu 64Bits
Arquivo wxis.exe foi compilado em 32bits.
```
tail -f /var/log/apache2/error.log 
[Tue Oct 16 13:36:58 2012] [error] (2)No such file or directory: exec of '/var/www/phl82/cgi-bin/wxis.exe' failed
[Tue Oct 16 13:36:58 2012] [error] [client 192.168.250.250] Premature end of script headers: wxis.exe, referer: http://172.0.0.1/phl82/
```

### Erro WXIS|fatal error
```
WXIS|fatal error|unavoidable|recread/xropn/w| 
usuario apache não tem permissão para ler arquivos
```

Solução, dar permissão de dono aos arquivos para o usuario que executa o apache.
```
cd /var/www/http
chmod 755 bases -R
chown www-data:www-data bases -R
```
