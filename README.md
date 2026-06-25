## 🚀 Subindo o Docker
1. Insira sua chave do **NGROK** no arquivo `.env` seguindo o modelo do `.env.example`.
2. No terminal, rode o comando `docker compose up -d` para subir os containers.
3. Aguarde o n8n iniciar completamente e acesse-o em: `http://localhost:5678`.

## 🔑 Configurando as Chaves de Teste (Para o Avaliador)

Como esta é uma instalação nova e local, o n8n solicitará que você crie uma conta de usuário administrador no primeiro acesso (`http://localhost:5678`). 

### 📥 Importando o Fluxo
1. Após criar sua conta e acessar o painel do n8n, clique no botão de **três pontinhos (...)** no canto superior direito.
2. Selecione a opção **Import from File** (Importar de um arquivo).
3. Selecione o arquivo `workflow-chatbot-telegram.json` incluído neste projeto.

---

## ⚙️ Configurando as Credenciais

Após importar, você verá que alguns nós exibem um alerta de erro de credenciais. Siga as instruções abaixo para inserir as chaves da API do Telegram e do OpenWeather:

### 1. Inserir a Credencial do Telegram
1. No painel do n8n, dê um duplo clique no primeiro nó chamado **Telegram Trigger**.
2. No campo **Credential for Telegram API**, clique na lista de seleção e escolha **- Create New Credential -** (Criar Nova Credencial).
3. No campo **Access Token**, insira o token do seu bot do Telegram (obtido com o `@BotFather`).
4. Clique em **Save** (no canto superior direito da janela flutuante) e feche-a.

### 2. Inserir a Credencial do OpenWeather
1. Dê um duplo clique no nó chamado **HTTP - GET LAT/LON with Geocoding in in API OpenWeather**.
2. No campo **Credential for Generic Credential Type**, certifique-se de que está selecionado *Query Auth*.
3. Na lista de seleção logo abaixo, clique e escolha **- Create New Credential -**.
4. Configure os parâmetros de autenticação conforme sua chave do OpenWeather:
   * **Name:** `appid`
   * **Value:** *[Cole aqui a sua chave de API do OpenWeather]*
5. Clique em **Save** e feche a janela.

> 🚨 **PASSO CRUCIAL PARA O TESTE FUNCIONAR:** > Após configurar as duas credenciais, você deve obrigatoriamente ativar o fluxo mudando a chave no canto superior direito do n8n de **Inactive** para **Active**. Isso fará com que o n8n registre automaticamente a URL do seu túnel Ngrok no webhook do Telegram.

---

### 🧪 3. Faça sua busca no Telegram
Agora o bot está pronto! Abra o Telegram, procure pelo bot que você configurou e envie uma mensagem simulando os cenários abaixo:

* **Caso de Sucesso:** Envie `Cidade, Estado` (Ex: `São Paulo, SP` ou `Atibaia, SP`). O bot responderá com a temperatura atual em tempo real.
* **Caso de Erro (Formato):** Envie apenas `São Paulo`. O bot indicará que o formato está incorreto.
* **Caso de Erro (Localização):** Envie uma cidade combinada com o estado errado (Ex: `Atibaia, RJ`). O bot informará que a cidade não foi localizada naquele estado.