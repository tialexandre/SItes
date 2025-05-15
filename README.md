Localização dos Arquivos Instalados pelo Script de Instalação Dehydrated

Este documento detalha onde cada arquivo de configuração é instalado pelo script de instalação automatizada do cliente ACME Dehydrated, com suporte ao hook da Cloudflare e integração com o Nginx.

Diretórios Criados e Usados

Diretório

Função

/etc/dehydrated/

Diretório principal de configuração do Dehydrated

/etc/dehydrated/hooks/

Armazena os scripts de hook, como o da Cloudflare

/etc/dehydrated/domains.d/

Arquivos individuais de configuração por domínio

/etc/pki/acme/

Destino final dos certificados emitidos (CERTDIR)

/var/www/dehydrated/

Diretório web usado opcionalmente para http-01 (caso utilizado)

/etc/nginx/custom.d/ ou snippets/

Snippets do Nginx, varia conforme a distro (RHEL vs Ubuntu)

/tmp/<tmpdir>

Diretório temporário usado durante a execução, é limpo ao final

Arquivos Instalados

1. Cliente Dehydrated

Origem: GitHub (clonado temporariamente)

Destino: /sbin/dehydrated

Função: binário principal para emitir/renovar certificados

2. Arquivo de configuração principal

Destino: /etc/dehydrated/config

Conteúdo: Parâmetros como CERTDIR, DOMAINS_D, HOOK, entre outros

3. Lista de domínios

Destino: /etc/dehydrated/domains.txt

Conteúdo: Lista de domínios e aliases para certificação

4. Hooks da Cloudflare

Origem: GitHub (socram8888)

Destino: /etc/dehydrated/hooks/cloudflare.sh

Permissão: Executável (chmod +x)

Função: Automatiza desafio DNS-01 via API da Cloudflare

5. Exemplo de domínio (config individual)

Origem: NimbusNetwork GitHub

Destino: /etc/dehydrated/domains.d/exemplo.com.br

Conteúdo: Configuração customizada para o domínio exemplo.com.br, incluindo o hook

6. Script de renovacão automática

Destino: /etc/cron.daily/acme-renew

Permissão: Executável (chmod +x)

Função: Roda o Dehydrated diariamente para renovar certificados próximos do vencimento

7. Snippet para o Nginx (acme.conf)

Destino:

/etc/nginx/snippets/acme.conf (Ubuntu)

/etc/nginx/custom.d/acme.conf (Rocky/EL8/EL9)

Função: Configuração de suporte ao desafio HTTP ACME caso necessário

Outros

Registro ACME:

O comando dehydrated --register --accept-terms registra a conta no Let's Encrypt e cria arquivos de conta em /etc/dehydrated/accounts/

Limpeza temporária:

O diretório temporário criado com mktemp -d é removido após a instalação.

Resumo

Arquivo/Dir

Localização Final

Cliente dehydrated

/sbin/dehydrated

Configuração principal

/etc/dehydrated/config

Lista de domínios

/etc/dehydrated/domains.txt

Hooks

/etc/dehydrated/hooks/cloudflare.sh

Domínios individuais

/etc/dehydrated/domains.d/<dominio>

Certificados

/etc/pki/acme/<dominio>/*.pem

Script de renovacão CRON

/etc/cron.daily/acme-renew

Snippet NGINX

/etc/nginx/snippets/acme.conf ou custom.d/

Se desejar, posso gerar uma tabela pronta para publicar no seu Wiki.js com esse mapeamento.
