# Documentação do Middleware entre o Blip e o Zoho CRM
## Como configurar

1. Crie uma conta em https://www.zoho.com/pt-br/crm/, não é necessário carregar os dados da amostra.
2. Vá para https://api-console.zoho.com/ e clique em 'GET STARTED'.
3. Clique na opção 'Self Client' e clique em 'CREATE'.
4. Se abrir uma janela perguntando 'Are you sure to enable self-client?', clique em 'OK'. Você será redirecionado para uma tela assim:

![image](https://doc-08-0s-docs.googleusercontent.com/docs/securesc/tt7pv5a6kriekca37j2ehrg01df0g9b3/ek80m7i1giskt7e731poucds5aobmhod/1648067025000/06912951035512271498/13621911303316140662/1huiGZA7Jv9NevcJufoR5e1bxsslJtq2S?e=view&ax=ACxEAsZlsqMjegBJjz2H3vOeSuSZf3KY1C_hsTW6fGPjzn5RRzz_n8V9sS66uGqZue9Er2HnurJiDXHdA7LXJ4moF1uqIDvSfaIRGbPxiECeeY8WTdq1P1eGhhbK4qdsQ-OMgNrBxN_Ua-kHs_gIn38Sbo_ApZi0M9LbnaoEtFF9bmxZuOzhjl_OmQpoSXyBDxCGy65W1XB8ssN7V8gwd8gfADSOJk6KHvROccPjmo69RmCdkfq0qTSbslPJmd2gmycpS9F1RaH5QpnZ_h31J1RgfVCsNiaBIOqaZfJkuE2tf1iLQ-eRmuUz9yOAk_WzHx6Ghy3d79xIr70hIYVRCvSKmyelAQJufzyvQgAqzPoXBCWeOoq-KMTAMqnDlXsshVWk98BdIWyzU4vIr-ef7sim6_fs8M_RE7bN-w80PktQZsQ9l6o0bZxv10H1PQfg4WzzBW7a1fcR8N0v5YDO69F-rmvIodYfLHLw624HNfL104l_MfNyUBc9DDdIPKQZKKuMme3dn4bNFhzCmmlTkl2l_atQgsWo1xv4pMiP7AvTNsOxa4Tk9cPbTPXWEj2bakRKHO5Orn9QVHX2m0ESO-O9hCXL02sZuEnLUq1H_wuoWgK-zjInarloFknA2KxJHtzPCEzQiN9oDsVAk4kcIOsdY4yw894XbNkA7Mj9jwFGX-SXIbi1XucXUwgUFN3HIbnrRz9wtAqYnRId_w&authuser=0&nonce=fbtc63e6m2668&user=13621911303316140662&hash=r6fvabk4edf8mf97u1ik311l2ie1s91j)

5. Clique em 'Generate Code'.

![image](https://drive.google.com/uc?export=view&id=1huiGZA7Jv9NevcJufoR5e1bxsslJtq2S)

Você vai para uma tela assim:

![image](https://drive.google.com/uc?export=view&id=1NBYyeGJsP-dcDh6anMOt3D9FN8NZmueV)

6. No campo 'Scope' você vai definir quais operações o client terá permissão para executar, preencha com o seguinte:
`ZohoCRM.modules.ALL,ZohoCRM.settings.ALL,ZohoCRM.notifications.READ,ZohoCRM.notifications.CREATE,ZohoCRM.notifications.UPDATE,ZohoCRM.notifications.DELETE,ZohoCRM.users.ALL,ZohoCRM.org.ALL,ZohoCRM.bulk.ALL,ZohoCRM.coql.READ,ZohoFiles.files.ALL `
7. Em 'Time Duration' escolha '10 minutes'.
8. Em 'Scope Description' coloque o que quiser que caracterize o client (não aparecerá pra mais ninguém além de você).
9. A tela deve estar assim agora:

![image](https://drive.google.com/uc?export=view&id=1w2cGF6Yz5XPGspKKYwQ0HxwXHwO1cdPc)

Role a janela para baixo até encontrar o botão 'CREATE' e clique nesse botão.
10. Nessa tela, clique em 'CRM'

![image](https://drive.google.com/uc?export=view&id=1peftAqTYaElyxhqLMIyqRhAoGIBSuSBV)

Depois, em 'Production' clique no nome da sua empresa

![image](https://drive.google.com/uc?export=view&id=1NysKPoBLhmwRv-ksN59l4oZ6MT5QkPtl)

Role a janela para baixo até encontrar o botão 'CREATE' e clique nesse botão.
11. Será gerado um código, que expira em 10 minutos (tempo que foi preenchido no passo 7 desse tutorial):

![image](https://drive.google.com/uc?export=view&id=1VawNvd1FsxeMhPe-KQbJYPQ5aW7dwKYR)

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
    
    ![image](https://drive.google.com/uc?export=view&id=1GXnTLOmuZm6eIzqTRjttUJGjTtvrAllA)
    
    * A response esperada é:
    
    ![image](https://drive.google.com/uc?export=view&id=15_6wyx6gAmGobqiQ3XGg9_oS9L3JT__A)

13. Acesse https://products.dawntech.dev/ e se já não estiver logado, faça login.
14. Clique na opção de configurar o Zoho CRM.

![image](https://drive.google.com/uc?export=view&id=1Xg-VBtvTOgaB3h57C1YrA7yaxPFOufWY)

15. Preencha os 3 campos.
     - client_id e client_secret são os mesmos que os utilizados no passo 12 desse tutorial.
     - refresh_token é o `refresh_token` que veio na response do passo 12 desse tutorial.

![image](https://drive.google.com/uc?export=view&id=1nzxTrck4ZJVCENKvR4vD1Ji5i-Z8_bGj)

16. Clique em 'Alterar valores'. Pronto, o seu middleware está middleware está pronto para ser usado.
