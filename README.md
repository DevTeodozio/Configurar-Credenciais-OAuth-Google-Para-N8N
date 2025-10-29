# Configurando as credenciais do OAuth Google para os nós de serviços do Google:


## Para configurar uma credencial do Google para o N8N hospedado no Render.com, é necessário gerar um ID do cliente OAuth no Google Claud Console e configurar as variáveis de ambiente corretas no Render.com. O processo principal envolve a configuração da tela de consentimento e a criação da credencial no Google Cloud Console, seguida pela inclusão do Client ID, Client Secret a URL de direcionamento no N8N.


1ª ETAPA - CRIAR AS VARIÁVEIS DE AMBIENTE DO N8N NO RENDER:

A URL do OAuth no Google Cloud Console precisa ser uma URL pública e acessível e deve ser HTTPS. 
Logo, precisamos definir as variáveis de ambiente no Render:


1 - Abra o Render;

2 - No projeto criado, selecione n8n (está na lista SERVICE NAME - que você criou seguindo os passos do vídeo aqui);

3 - Na aba lateral, selecione Ambiente (Environment);

4 - Clique no botão + Create environment group (+ Criar grupo de ambiente);

5 - Insira as seguintes chaves:

Chave 1:  N8N_EXTERNAL_BACKEND

Chave 2:  N8N_HOST

Chave 3:  N8N_PORT

Chave 4:  N8N_PROTOCOL;

Chave 5:  VUE_APP_URL_BASE_API

Chave 6:  WEBHOOK_TUNNEL_URL

Chave 7:  WEBHOOK_URL

Valores (na ordem de cada chave):

Valor 1:  https://n8n-canal.onrender.com 

Valor 2:  n8n-zzzz.onrender.com

Valor 3:  443

Valor 4:  https

Valor 5:  https://n8n-zzzz.onrender.com

Valor 6:  n8n-zzzz.onrender.com

Valor 7:  https://n8n-zzzz.onrender.com


(Obs.: Substitua a sequência zzzz pela sua sequência que aparece após "n8n-...." na barra de endereços do seu espaço de trabalho. Selecione e copie somente até render.com, antes da barra /home/workflow se você estiver em um ambiente de trabalho no seu n8n.
Exemplo: https://n8n-z99l.onrender.com);

6 - Salve e reinicie o serviço.
(É provável que, ao abrir o N8N, você tenha que inserir novamente o e-mail, como se estivesse criando uma conta do zero. Continue, como estivesse criando tudo novamente)


(link de referência da 1ª etapa: https://community.n8n.io/t/i-m-self-hosting-the-latest-n8n-docker-image-on-render-com-http-render-com/133124/5)


2ª ETAPA - CONFIGURAR AS CREDENCIAIS NO GOOGLE CLOUD CONSOLE:

1 - Abra o Google Cloud Console (se não tiver uma conta, crie-a);

2 - Clicar em New Project (Novo Projeto) - no botão superior esquerdo Project Picker (Selecione um projeto);

3 - Insira o nome do seu projeto no campo Project name (Nome do projeto). Exemplo: Automacoes n8n;

4 - No campo Location (Localização), pode deixar como "No organization";

5 - Clicar em Create (Criar) e espere o projeto ser criado;

6 - Se você tiver mais de um projeto, clique no botão superior esquerdo do Project Picker (Selecione um projeto) e selecione o projeto criado (se for o primeiro projeto, o botão já aparece com o nome dele. Exemplo: Automacoes N8N). Na lista que aparece, clique no nome do projeto;

7 - Na seção "Acesso Rápido", clique no botão APIs & Services (APIs e Serviços);

8 - Na aba lateral, clique em Credentials (Credenciais);

9 - Clique em "+ Create credentials" (Criar credentiais) e, na lista suspensa, selecione "OAuth Client ID" (ID do cliente OAuth);
----- ----- ----- ----- ----- ----- ----- -----


### Tela de Consentimento:

10 - Na página que aparece, clique no aviso da faixa amarela abaixo, no botão Configure consent screen (Configurar tela de consentimento) e, logo em seguida, clique no botão Get started (Começar);
11 - Insira o nome do aplicativo, no campo App name;
12 - Insira o e-mail de suporte (se já estiver conectado ao Google, aparece seu e-mail);
13 - Clique em Next (Próximo);
14 - Em Audience (Audiência), selecione o público External (Externo);
15 - Em Contact Information (Informações de Contato), insira o mesmo e-mail da etapa anterior;
16 - Clique em Next (Próximo) e, em Finish (Terminar), clique no botão para aceitar os termos da política de dados do usuário. Clique em Continue e, em seguida, clique em Create (Criar);
17 - Criada a Tela de Consentimento, volte para a tela Home (Tela inicial) do seu projeto para, agora sim, criar as credenciais do OAuth.
----- ----- ----- ----- ----- ----- ----- -----


### Criando as credenciais:

18 - Na seção "Acesso Rápido", clique no botão APIs & Services (APIs e Serviços);

19 - Na aba lateral, clique novamente em Credentials (Credenciais);

20 - Clique em "+ Create credentials" (Criar credentiais) e, na lista suspensa, selecione "OAuth Client ID";

21 - No campo Application type (Tipo de aplication), selecione Web application, pois o n8n é uma aplicação web;

22 - Insira um nome para o seu app;

23 - Na seção  Authorized redirect URIs (URIs de redirecionamento autorizados) logo abaixo, na mesma página do Google Cloud Console, insira a URL que foi copiada de um nó do Google (Por exemplo, se você selecionou o nó Google Sheets, no n8n, no campo OAuth Redirect URL desse nó, copie e cole no campo de URLs autorizadas, lá na página do Google Cloud. Basicamente, a URL é a mesma para qualquer nó do Google, seja Sheets, Drive etc.);

24 - Clique em Create e, na janela pop-up "OAuth client created" que aparece, copie o Client ID e cole lá no nó que você inseriu no n8n, cole no campo ID do cliente. Faça o mesmo com o Client secret da janela pop-up, colando no campo Segredo do cliente, lá no nó que você inseriu no n8n (Obs.: salve essas duas chaves em um bloco de notas);
----- ----- ----- ----- ----- ----- ----- -----

### Adicionando o e-mail como Usuário de Teste:
25 - Vá para a barra lateral esquerda do seu projeto no Google Cloud Console e clique em OAuth consent screen (Tela de consentimento OAuth);

26 - Na barra lateral esquerda, novamente, clique em Audience (Público-alvo) e, na página que aparece, na seção Test user (Usuários de teste), clique no botão para adicionar um usuário;

27 - Na barra lateral direita que aparece, adicione o e-mail e clique em Salvar (Recomendo adicionar o mesmo e-mail que você colocou na criação do projeto);

28 - Volte para o N8N, e clique em Sign in with Google (Faça login com o Google), o botão azul que aparece lá no final, no nó que você inseriu. Em seguida, selecione o e-mail de teste;

29 - O Google vai informar que "não verificou este app", mesmo assim clique em Continuar. Em seguida, selecione todos os serviços que você quer dar permissão e clique em continuar;

30 - No nó que você selecionou, vai dar um erro de permissão, pois você ainda não habilitou o serviço de API do nó lá lo Google Cloud Console. Por exemplo, se você selecionou Google Sheets, ao clicar na lista suspensa para escolher a planilha onde você quer registrar os dados, ela não vai aparecer pois você não habilitou. Volte para o Google Cloude Console e habilite, pesquisando na barra de pesquisa do projeto o nome do serviço e clicando no botão Enable (Habilitar) da API. Uma vez habilitadas as APIs que você quer, o processo é mais simples, pois você só precisará  selecionar a credencial e inserir o Client ID e o Client Secret no novo nó que você inseriu no seu fluxo de trabalho. Novamente, clique em Sign in with Google (Faça login com o Google), o botão azul que aparece lá no final, no nó que você inseriu e pronto!
A conexão foi bem-sucedida!

(Link de referência da 2ª etapa: https://www.youtube.com/watch?v=Ck_661qqC3Q&lc=UgxCKWIGYMSobjG-Sy54AaABAg)
----- ----- ----- ----- ----- ----- ----- -----

Comigo deu certo!
Faça os testes e comente se você também conseguiu!
Espero ter ajudado.😉
