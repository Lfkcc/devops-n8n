Resumo Básico
SO Debian pela sua simplicidade e já ser de uso natural e comum para este tipo de situação
A stack usada para conseguir aplicar tudo que foi pedido, criar o usuário e enviar o link com link cadeado foi Docker, Nginx, n8n e Certbot

Com mais tempo eu poderia evitar melhor os erros básicos de comando que sofri, as travas de toda hora sair do que possuía domínio sobre. Teria já adicionado e organizado melhor as pastas que baixei as bibliotecas e trouxe os comandos para utilizar, feito em uma ordem melhor que não me fizesse voltar atrás para confirmar de novo o que foi feito, onde foi colado e a possibilidade de usar ele.


Etapa onde ao tentar executar os códigos encontrei problemas pois eles não iam, não consegui usar o comendo sudo, e nem o nano, e quando fui usar o usando whoami
Percebi que não era o root, esqueci de logar como usuário depois que instalei toda a máquina.

Após isso ainda não conseguia atualizar e nem progredir na programação porque o que foi instalado do Debian era mínimo demais
Assim eu procurei como conseguir utilizar estes comandos que precisa, e descobri que precisaria adicionar eles a sources.list diretamente, assim eu escrevi 
deb http://deb.debian.org/debian trixie main contrib non-free non-free-firmware
deb http://deb.debian.org/debian trixie-updates main contrib non-free non-free-firmware
deb http://security.debian.org/debian-security trixie-security main contrib non-free non-free-firmware

Salvei e depois pedi o update que estava querendo
E o debian ainda não estava se conectando ao DNS
Procurei para ver se não havia erro de internet, mas ela estava se conectando à máquina, então procurei saber o que poderia ser a causa
Assim, vi que precisaria colocar o nameserver 8.8.8.8 e nameserver 1.1.1.1 dentro forçado e fazer a ligação direta dele em Debian.
Depois de forçar essa ligação consegui pingar e fazer a conexão

Através da resolução destes problemas, eu já consegui fazer com a VM tenha conexão a internet direta, e também garanti que os IPs e conexão sejam as obrigatórias para seu funcionamento, isto sendo resolvido graça a resolução de um problema que não estava esperando.

Agora comecei a fazer o básico novamente após corrigir estes erros de permissão e conexão

Voltando a fazer o básico novamente após corrigir estes erros de permissão e conexão

Tive problema com curl que não foi instalado, e preciso dele para fazer a instalação do Docker
Após dar o update consigo Docker funcionando perfeitamente.
Após instalar o docker eu tive problemas novamente para me dar acesso ao grupo docker, mesmo sendo usuário e estando em root eu não consegui utilizar os comandos. Executei atualizações nos comandos e sistemas, mas não funcionou. Puxando para ver onde o docker compose estava vi que não possuía diretório criado, logo eu não estava na pasta onde ele deveria, dessa forma eu criei um diretório para n8n ligando ao meu usuário e consegui rodar o compose, dando permissão de grupo para mim. 

Agora vem a parte de criar o arquivo docker.compose.yml. Eu já havia feito a pasta anteriormente para poder executar os comandos que não estavam sendo feitos por não ligar neste mesmo diretório, então so precisei colar o comando que traz a imagem do n8n e liga ela ao link. De primeira não foi pois errei um sinal no comando mas depois de corrigir e retornar para subir o n8n foi tranquilamente. iniciando sua imagem, conexão, volume e o espaço.

Para fazer a instalação do Nginx foi tranquila, mas deu algum erro na hora de criar sua pasta para diretório, que no fim não descobri qual foi mas apenas ocorreu tranquilamente. Provalmente erro de digitação que se corrigiu depois que eu recriei a pasta novamente. 
Removi o site padrão que vem com o Nginx para nn dar conflito e depois de checar deu completo e funcionando corretamente a syntax

Finalmente como uma das etapas mais importantes e de encerramento emitir o certificado de HTTPS

E, esta que pensei que seria complexa foi simplesmente a reprodução dos comandos genéricos de servidor para requisitar a confirmação
sudo apt install -y certbot python3-certbot-nginx
sudo certbot --nginx -d devopstest.fuzzytech.com.br
sudo certbot renew --dry-run

A maior parte dos problemas até agora foi organizar as 'ferramentas' que usaria para fazer os comandos no Console, criar o root, ativar minhas permissões, bibliotecas e afins. A reprodução de código no Console depois disto fica simples e prática.

A criação da conta owner no n8n funcionou tranquilamente, não houve nenhum problema de conexão já pensando como eu resolvi os problemas que tiveram no início.


Na finalização para subir em git acabei tendo o problema que o console não é possível de copiar nada, nem no histórico ou enquanto escrevo, e para fazer o uso do token e sua larga quantidade de caracteres eu procurei alternativas de possibilitar o ctrl+C ou ctrl+v, desde abrindo meu computador como usuário para usar o CMD do windows, como outras variáveis até desistir e ir para a chave SSH que eu poderia copiar para o browser ao menos.
