# Projeto DevOps - Instalação e Publicação do n8n

Este projeto foi desenvolvido como parte de uma prova prática, onde o objetivo era configurar um ambiente completo para rodar o **n8n** em um servidor, utilizando Docker, Nginx e HTTPS com Certbot.

Mesmo sendo uma tarefa desafiadora para mim, principalmente por ainda estar no começo da minha caminhada na programação e em DevOps, consegui finalizar tudo o que foi solicitado.

## Objetivo do Projeto

O desafio era preparar um servidor do zero, configurar o ambiente necessário e deixar o n8n acessível através de um domínio com certificado HTTPS ativo.

O resultado final foi a publicação do n8n no endereço definido para o projeto, com acesso seguro via navegador.

## Tecnologias Utilizadas

- Debian
- Docker
- Docker Compose
- Nginx
- n8n
- Certbot
- Let's Encrypt
- Git e SSH

## Por que usei Debian?

Escolhi o Debian por ser um sistema operacional simples, leve e bastante usado em ambientes de servidor. Além disso, era uma opção adequada para o tipo de configuração exigida na prova.

## Processo de Desenvolvimento

Durante a execução do projeto, precisei configurar várias partes do ambiente manualmente.

As principais etapas foram:

1. Configuração inicial da máquina Debian.
2. Correção de permissões de usuário e acesso root.
3. Ajuste dos repositórios do Debian no arquivo `sources.list`.
4. Correção de problemas de DNS.
5. Instalação de pacotes necessários como `sudo`, `nano` e `curl`.
6. Instalação do Docker e Docker Compose.
7. Criação do diretório do projeto.
8. Criação do arquivo `docker-compose.yml`.
9. Subida do container do n8n.
10. Configuração do Nginx como proxy reverso.
11. Remoção do site padrão do Nginx para evitar conflito.
12. Configuração do domínio.
13. Emissão do certificado HTTPS com Certbot.
14. Criação da conta owner no n8n.
15. Organização e envio do projeto para o GitHub.

## Principais Dificuldades

No início, tive bastante dificuldade com coisas básicas do ambiente Linux.

Uma das primeiras dificuldades foi perceber que eu não estava logado como usuário correto. Ao tentar executar comandos como `sudo` e `nano`, eles não funcionavam. Depois de usar o comando `whoami`, percebi que o problema estava relacionado ao usuário e às permissões.

Também tive problemas porque a instalação do Debian estava muito mínima. Algumas ferramentas importantes não estavam instaladas, então precisei ajustar os repositórios manualmente no `sources.list` para conseguir atualizar o sistema e instalar os pacotes necessários.

Outro problema foi a conexão com DNS. A máquina tinha internet, mas não conseguia resolver os endereços corretamente. Para corrigir isso, precisei configurar manualmente os nameservers:

bash
nameserver 8.8.8.8
nameserver 1.1.1.1

Depois disso, consegui fazer os testes de conexão e continuar a instalação.

Instalação do Docker

Após resolver os problemas de permissão, DNS e atualização do sistema, consegui instalar o Docker.

Também tive dificuldade com o Docker Compose, principalmente por causa do diretório correto onde o projeto deveria ficar. Depois de entender melhor a estrutura, criei uma pasta específica para o n8n, ajustei as permissões e consegui executar o docker compose.

Configuração do n8n

Com o Docker funcionando, criei o arquivo docker-compose.yml para subir o n8n.

Na primeira tentativa, cometi um erro de digitação no arquivo, mas depois de corrigir o problema consegui iniciar o container corretamente, com imagem, volume, rede e porta configurados.

Configuração do Nginx

A instalação do Nginx foi mais tranquila, mas ainda tive alguns erros na criação dos arquivos de configuração.

Removi o site padrão do Nginx para evitar conflito e configurei o proxy reverso apontando para o n8n. Depois disso, validei a sintaxe da configuração e reiniciei o serviço.

Certificado HTTPS

Uma das partes mais importantes do projeto era deixar o domínio com HTTPS.

Achei que essa etapa seria uma das mais difíceis, mas acabou sendo mais simples do que eu imaginava. Utilizei o Certbot com Nginx para gerar o certificado SSL:

sudo apt install -y certbot python3-certbot-nginx
sudo certbot --nginx -d devopstest.fuzzytech.com.br
sudo certbot renew --dry-run

Após isso, o domínio passou a funcionar com cadeado de segurança no navegador.

Finalização no GitHub

Na etapa final, tive dificuldade para subir o projeto para o GitHub porque o console não permitia copiar e colar facilmente o token de acesso.

Tentei algumas alternativas, mas acabei optando por usar chave SSH, que foi uma solução melhor para autenticar e enviar o projeto para o repositório.

Resultado Final

No final, consegui entregar o ambiente funcionando com:

n8n rodando em container Docker;
Nginx configurado como proxy reverso;
domínio apontando corretamente;
HTTPS ativo com Certbot;
conta owner criada no n8n;
projeto versionado no GitHub.
O que aprendi

Esse projeto foi bem importante para mim porque me obrigou a sair da zona de conforto.

Tive dificuldades com comandos, permissões, DNS, instalação de pacotes, Docker, Nginx e Git. Mesmo assim, fui pesquisando, testando e corrigindo cada erro até conseguir finalizar.

Com mais tempo e experiência, eu organizaria melhor as etapas desde o início, criaria os diretórios em uma ordem mais clara e evitaria alguns erros básicos de comando. Mas, apesar das dificuldades, consegui concluir tudo o que foi pedido na prova.

Esse projeto me mostrou que, mesmo começando e ainda tendo muito para aprender, é possível resolver problemas reais com paciência, pesquisa e prática.até desistir e ir para a chave SSH que eu poderia copiar para o browser ao menos.
