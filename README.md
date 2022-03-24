# Documentação do Middleware entre o Blip e o Zoho CRM
## Como configurar

1. Crie uma conta em https://www.zoho.com/pt-br/crm/, não é necessário carregar os dados da amostra.
2. Vá para https://api-console.zoho.com/ e clique em 'GET STARTED'.
3. Clique na opção 'Self Client' e clique em 'CREATE'.
4. Se for redirecionado para a seguinte página, clique em 'OK':

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
8. Em 'Scope Description' coloque o que quiser que caracterize o client (não aparecerá pra mais ninguém além de você).
9. A tela deve estar assim agora:

![image](./images/tela_generate_code.png)

Role a janela para baixo até encontrar o botão 'CREATE' e clique nesse botão.

10. Nessa tela, clique em 'CRM'

![image](./images/tela_clicar_crm.png)

Depois, em 'Production', clique no nome da sua empresa

![image](./images//tela_clicar_crm_2.png)

Role a janela para baixo até encontrar o botão 'CREATE' e clique nesse botão.

11. Será gerado um código, que expira em 10 minutos (tempo que foi preenchido no passo 7 desse tutorial), copie esse código:

![image](./images/tela_generated_code.png)

12. Agora abra o Postman, ou algo similar e faça uma requisição com as seguintes informações:
    - Método: `POST`
    - URL: `https://accounts.zoho.com/oauth/v2/token`
    - Headers: `Content-Type: application/x-www-form-urlencoded`
    - Body: no formato `x-www-form-urlencoded` com as seguintes keys:
        * code: é o código recém copiado do Zoho
        * redirect_url: uma url que não é usada nesse middleware, então pode usar um valor qualquer
        * client_id: valor que pode ser encontrado em 'Client Secret', a tela que é aberta no passo 4 desse tutorial
        * client_secret: valor que também pode se encontrado em 'Client Secret'
        * grant_type: `authorization_code`
    * A request ficará nesse formato:
    
    ![image](./images/tela_get_refresh_token_request.png)
    
    * A response esperada é:
    
    ![image](./images/tela_get_refresh_token_response.png)

13. Acesse https://products.dawntech.dev/ e se já não estiver logado, faça login.
14. Clique na opção de configurar o Zoho CRM.

![image](./images/tela_products_dawntech.png)

15. Preencha os 3 campos.
     - client_id e client_secret são os mesmos que os utilizados no passo 12 desse tutorial.
     - refresh_token é o `refresh_token` que veio na response do passo 12 desse tutorial.

![image](./images/tela_settings.png)

16. Clique em 'Alterar valores'. Pronto, o seu middleware está pronto para ser usado.
