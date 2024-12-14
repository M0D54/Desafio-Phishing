## Utilizando o Gophish para criação de Phishing

O Gophish é uma ferramenta de código aberto voltada para simular campanhas de phishing, permitindo que profissionais de segurança testem a conscientização de usuários e identifiquem vulnerabilidades organizacionais.

### 1. **Instalação e Configuração**

1. **Baixar e descompactar**:

[Gophish](https://github.com/gophish/gophish/releases)

   ```
   unzip gophish.zip
   ```
   
2. **Editar a configuração de rede**:
   Abrir o arquivo de configuração `config.json` e ajustar o IP em `"listen_url"` para o endereço desejado
   
   Exemplo:
   ```json
   "listen_url": "0.0.0.0:3333"
   ```

3. **Tornar o executável e iniciar o Gophish**:
   ```
   chmod +x gophish
   ./gophish
   ```
   Por padrão, o Gophish será iniciado na porta **3333**.

4. **Credenciais de acesso**:
   - **Usuário**: `admin`
   - **Senha**: `gophish`

### 2. **Criando grupos e usuários**

No painel do Gophish:
1. Acesse a aba **Users & Groups**.
2. Clique em **New Group** para criar um grupo de testes.
3. Adicione usuários manualmente ou importe uma lista de colaboradores de um arquivo CSV.

### 3. **Criando o template de e-mail**

1. Acesse a aba **Templates** e clique em **New Template**.
2. Configure o e-mail:
   - **Título**: Nome do template.
   - **Conteúdo**: Edite diretamente ou importe de outro e-mail.
   - Utilize **placeholders** para personalizar as mensagens, como `{{.FirstName}}` para o nome do usuário.
   
   Exemplo de mensagem:
   ```
   Olá {{.FirstName}},
   Identificamos uma tentativa de login em sua conta. Clique aqui para confirmar.
   ```

3. Teste o e-mail:
   - Envie o e-mail para si mesmo antes de configurar o phishing para validar o comportamento esperado.

### 4. **Criando a Landing Page**

A landing page é uma página falsa pra onde o usuário será redirecionado ao clicar no link do seu e-mail.

#### Opções:
1. **Importar automaticamente**:
   - Forneça a URL da página oficial (ex.: página de login do Facebook).
   - Ative a captura de dados e configure o redirecionamento para a página verdadeira após o envio.

2. **Criar manualmente**:
   - Clone a página verdadeira:
     1. Acesse o site original no navegador.
     2. Clique em "Salvar como" e salve como `index.html`.
   - Configure um servidor local com Python:
     ```
     python3 -m http.server
     ```
   - No Gophish, importe a página clonada do servidor local.

3. **Resolver problemas de funcionalidade**:
   - Inspecione o código fonte da página.
   - Remova ou edite controles de JavaScript que bloqueiam o envio de dados.

### 5. **Configurando o Perfil de E-mail**

1. Na aba **Sending Profiles**, configure o servidor de e-mail para envio.
   - **Servidor SMTP**:
     - Gmail: `smtp.gmail.com:587`
     - Outros provedores: Utilize as configurações correspondentes.
   - **Autenticação**: Forneça o e-mail e senha.
   - **Segurança**:
     - Para Gmail, desative o 2FA e reduza o nível de segurança da conta.

### 6. **Criando a Campanha de Phishing**

1. Acesse a aba **Campaigns** e clique em **New Campaign**.
2. Configure:
   - Grupo de usuários.
   - Template de e-mail.
   - Landing page.
   - Perfil de envio.
3. Inicie a campanha.

### 7. **Monitorando os Resultados**

O Gophish fornece métricas detalhadas em tempo real:
- **Abertura do e-mail**: Data, hora, navegador e sistema operacional.
- **Cliques no link**: Identifica os usuários que acessaram a landing page.
- **Envio de dados**: Captura as credenciais inseridas.
