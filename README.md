Esqueleto de aplicação para o curso de framework
======================================

Introdução
------------
Um projeto mínimo sobre a camada MVC e o sistema de módulos do framework.
Serve como ponto de partida para quem quer começar a mexer sem montar tudo do zero.

Instalação
------------

Com o gerenciador de dependências (recomendado)
----------------------------
O caminho mais direto é clonar o repositório e deixar o gerenciador baixar tudo
a partir do esqueleto publicado:

    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
    php composer-setup.php
    php composer.phar require --dev framework/esqueleto

Outra opção é clonar e usar o próprio arquivo do gerenciador que vem no projeto:

    cd caminho/do/projeto
    git clone https://github.com/exemplo/esqueleto-aplicacao.git
    cd esqueleto-aplicacao
    php composer.phar self-update
    php composer.phar install

(O `self-update` existe para garantir que o gerenciador esteja na versão mais recente.)

Também dá para baixar o pacote direto pelo terminal e descompactar:

    cd caminho/do/projeto
    curl -#L https://github.com/exemplo/esqueleto-aplicacao/archive/refs/heads/main.tar.gz | tar xz --strip-components=1

Depois é só rodar o gerenciador de dependências como no exemplo anterior.

Via submódulos do git
--------------------
Outra alternativa é puxar tudo de uma vez com submódulos:

    git clone https://github.com/exemplo/esqueleto-aplicacao.git --recursive

Configuração do servidor
----------------

### Servidor embutido do PHP

Para quem usa PHP 5.4 ou mais novo, o caminho mais rápido é subir o servidor
interno apontando para a pasta pública:

    php -S 0.0.0.0:8080 -t public/ public/index.php

Isso sobe o servidor na porta 8080 e aceita conexões de qualquer interface.

**Atenção:** o servidor embutido serve apenas para desenvolvimento.

### Apache

No Apache, basta criar um host virtual apontando para a pasta pública do projeto:

    <VirtualHost *:80>
        ServerName esqueleto.localhost
        DocumentRoot /caminho/do/projeto/public
        SetEnv APPLICATION_ENV "development"
        <Directory /caminho/do/projeto/public>
            DirectoryIndex index.php
            AllowOverride All
            Order allow,deny
            Allow from all
        </Directory>
    </VirtualHost>