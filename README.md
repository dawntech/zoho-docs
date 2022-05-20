## Como configurar
### Configurações iniciais
1. Crie uma conta em <https://www.zoho.com/pt-br/crm/>, não é necessário carregar os dados da amostra.
2. Vá para <https://api-console.zoho.com/> e clique em 'GET STARTED'.
3. Clique na opção 'Self Client' e clique em 'CREATE'.
4. Se for redirecionado para a página abaixo, clique em 'OK'.

    ![image](./images/tela_confirmation_self_client.png)

    Você será redirecionado para essa página:

    ![image](./images/tela_client_id_secret.png)

5. Clique em 'Generate Code'.

    ![image](./images/tela_go_to_generate_code.png)

    Você vai para uma tela assim:

    ![image](./images/tela_clean_generate_code.png)

6. No campo 'Scope' você vai definir quais operações o client terá permissão para executar, preencha com o seguinte:
`ZohoCRM.modules.ALL,ZohoCRM.settings.ALL,ZohoCRM.notifications.READ,ZohoCRM.notifications.CREATE,ZohoCRM.notifications.UPDATE,ZohoCRM.notifications.DELETE,ZohoCRM.users.ALL,ZohoCRM.org.ALL,ZohoCRM.bulk.ALL,ZohoCRM.coql.READ,ZohoFiles.files.ALL `
7. Em 'Time Duration' escolha '10 minutes'.
8. Em 'Scope Description' coloque o que quiser que caracterize o client (não aparecerá para mais ninguém além de você).
9. A tela deve estar assim agora:

    ![image](./images/tela_generate_code.png)

    Role a janela para baixo até encontrar o botão 'CREATE' e clique nesse botão.

10. Nessa tela, clique em 'CRM'

    ![image](./images/tela_clicar_crm.png)

    Depois, em 'Production', clique no nome da sua empresa.

    ![image](./images//tela_clicar_crm_2.png)

    Role a janela para baixo até encontrar o botão 'CREATE' e clique nesse botão.

11. Será gerado um código, que expira em 10 minutos (tempo que foi preenchido no passo 7 desse tutorial), copie esse código:

    ![image](./images/tela_generated_code.png)

12. Agora abra o Postman, ou software similar e faça uma requisição com as seguintes informações:
    - Método: `POST`
    - URL: `https://accounts.zoho.com/oauth/v2/token`
    - Headers: `Content-Type: application/x-www-form-urlencoded`
    - Body: no formato `x-www-form-urlencoded` com as seguintes keys:
        * code: é o código recém copiado do Zoho.
        * redirect_url: uma url que não é usada nesse middleware, então pode usar um valor qualquer.
        * client_id: valor que pode ser encontrado em 'Client Secret' (ver imagem abaixo).
        * client_secret: valor que também pode ser encontrado em 'Client Secret' (ver imagem abaixo).
        * grant_type: `authorization_code`

        ![image](./images/tela_client_secret_highlighted.png)
        Vai direcionar para a tela exibida no passo 4 desse tutorial.

    * A request ficará nesse formato:
    
    ![image](./images/tela_get_refresh_token_request.png)
    
    * A response esperada é:
    
    ![image](./images/tela_get_refresh_token_response.png)

    Guarde o refresh_token

13. Acesse <https://products.dawntech.dev/> e se já não estiver logado, faça login. Perceba que além do seu e-mail, aparecerá o seu ID, que será utilizado para acessar o middleware.
14. Clique na opção de configurar o Zoho CRM.

    ![image](./images/tela_products_dawntech.png)

15. Preencha os 3 campos.
     - client_id e client_secret: mesmos valores que os utilizados no passo 12 desse tutorial.
     - refresh_token: `refresh_token` que veio na response do passo 12 desse tutorial.

    ![image](./images/tela_settings.png)

16. Clique em 'Alterar valores'.

### Habilitando notificações

Esse passo é necessário para que Zoho e Blip possam conversar.

1. Na sua tela inicial do Blip, entre no seu chatbot Roteador.

    ![image](./images/tela_blip.png)

2. Vá nas configurações.

    ![image](./images/tela_clicar_bot_configs.png)

3. Vá para "Informações de conexão" e guarde os valores do "Cabeçalho de autenticação (Authorization)" e da "Url para enviar comandos".

    ![image](./images/tela_connection_info.png)

4. Vá para <https://zoho.dawntech.dev/enable-notification>

    > Se você for redirecionado para <https://products.dawntech.dev> siga esses passos:
    
    > 4.1 Faça o login se já não estiver feito, e clique em "Acessar produto" ao lado de "Zoho CRM":

    ![image](./images/tela_products_access_zoho.png)

    > 4.2 Clique na aba "Notifications".

    ![image](./images/tela_inicial_zoho_crm.png)

    > 4.3 Clique no botão "Enable Notification".

    ![image](./images/tela_notifications_zoho.png)

5. Preencha os campos colocando em "Bot Commands URL" o valor que foi pego da "Url para enviar comandos" no passo 3 e em "Bot Key" o valor que foi pego do "Cabeçalho de autenticação (Authorization)" também no passo 3 e clique em "Enable notification".

    ![image](./images/tela_enable_notification.png)

6. Se tudo der certo, você será redirecionado para a tela inicial do middleware e verá essa notificação no canto inferior esquerdo da tela:

    ![image](./images/success_notification.png)

7. Para visualizar a notificação recém habilitada, clique na aba "Notifications" como mostra o passo 4.2.

# Documentação de rotas

## Inserção de leads

- Método: `POST`
- URL: `https://api.zoho.dawntech.dev/api/leads`
- Headers: `dawntech-user-id: <user_id>`
- Body:
```
[
    {
        "Last_Name": string | Last name of the lead,
        "First_Name": string | First name of the lead,
        "Email": string | Email of the lead,
        "Company": string | Company where the lead works
    },
    ...
]
```

## Atualização de leads
- Método: `PUT`
- URL: `https://api.zoho.dawntech.dev/api/leads/:<id_do_lead_a_ser_atualizado>`
- Headers: `dawntech-user-id: <user_id>`
- Body:
```
[
    {
        "Last_Name": string | Last name of the lead,
        "First_Name": string | First name of the lead,
        "Email": string | Email of the lead,
        "Company": string | Company where the lead works
    },
    ...
]
```

## Busca de leads
- Método: `GET`
- URL: `https://api.zoho.dawntech.dev/api/leads`
- Headers: `dawntech-user-id: <user_id>`

## Procura de leads
- Método: `GET`
- URL: `https://api.zoho.dawntech.dev/api/leads/search?word=<termo_a_ser_procurado>`
- Headers: `dawntech-user-id: <user_id>`

## Remoção de lead
- Método: `DELETE`
- URL: `https://api.zoho.dawntech.dev/api/leads/:<id_do_lead_a_ser_deletado>`
- Headers: `dawntech-user-id: <user_id>`