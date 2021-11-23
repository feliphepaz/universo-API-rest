# Universo WordPress Rest API 🪐

Para criar a API que seria consumida no site da [Universo Academy]() foi usado o banco de dados do WordPress e o plugin JWT Authentication para utilizar o JSON Web Token. Os seus métodos de cadastro e validação de usuários foi o que facilitou o desenvolvimento do sistema de login da plataforma EAD. Os endpoints aqui criados são o retorno de funções que seriam utilizadas nesse sistema:

Requisição | Endpoint | Method | O que faz
:------ | :------ | :------ | :------
user_post | /user | POST | Cria o usuário no WordPress
user_get | /user | GET | Puxa as informações do usuário
password_lost | /password/lost | POST | Gera o link para redefinir a senha do usuário
password_reset | /password/reset | POST | Cria uma nova senha para o usuário

## 🌀 Como funciona?
1. Ao fazer o cadastro, a API realiza o `user_post` para criar o usuário no banco de dados. 
2. Agora com o usuário já criado, ele pode fazer o login. Aqui se inicia um processo mais complexo, começando pelo POST no JWT Authentication do qual irá gerar um token.
3. Este token será salvo no `localStorage` do usuário e será incluído na opção Authorization ao fazer a requisição de `user_get`, permitindo assim o acesso aos dados do usuário logado.
4. Com o token salvo no navegador, a plataforma consegue fazer o login automático toda vez que aquele usuário acessa o site. Porém como o token expira em 24 horas, é sempre necessário fazer a validação.
5. Para fazer essa autenticação, um POST será feito no JWT usando o endpoint '/token/validate'. Ele irá verificar se o token está expirado ou não. Caso não esteja, ele realiza o `autoLogin()`. Caso o contrário, ele desloga o usuário obrigando-o a gerar um novo token.


