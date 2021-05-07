### Sencillo test de prueba tipo blog (articulos y usuarios, en una relación one-to-many) del funcionamiento de la gema devise-auth-token cómo método de autenticación para APIs en ruby on rails 6.1
### Para el desarrollo de éste código seguí la guía brindada por: https://www.youtube.com/channel/UCr9w-w_dwEK1pXp1Rec1K6g
#### Actualmente tengo el repositorio hosteado en Heroku y pueden testearlo si así lo desean: https://devise-auth-testing.herokuapp.com más abajo incluiré los endpoints, pero están todos detallados en la documentación.

* #### Documentación: 
* #### https://devise-token-auth.gitbook.io/devise-token-auth/usage
* ####                https://github.com/lynndylanhurley/devise_token_auth

La gema resulta muy útil y completa, tiene todas las funciones que una API podría necesitar para realizar la autenticacion de sus clientes, por ejemplo creación de cuentas, login, logout, validación de token, token refresh, invalidación de token después de cada request, confirmación de cuenta vía correo electrónico, cambio de contraseña, configuración de nickname de usuario y más. Su implementación es muy sencilla y la guía provista anteriormente detalla cada paso con precisión, la recomiendo 100% !
* https://www.youtube.com/playlist?list=PLqsayW8DhUmsuvK17gwSI_rKbAlmxFIw5

* ### ENDPOINTS:
* #### CREAR CUENTA NUEVA -> POST: https://devise-auth-testing.herokuapp.com/api/auth
Acepta request tipo POST, parametros: email, password y password_confirmation. Al enviar el request se crea una nueva cuenta que deberá ser confirmada vía mail antes de poder ser utilizada.

* #### LOGUEARSE -> POST: https://devise-auth-testing.herokuapp.com/api/auth/sign_in
Acepta request tipo POST, parametros: email, password. Antes de poder utilizar éste endpoint deberemos haber confirmado la cuenta vía mail, de otra manera recibiremos un error. Aquí recibiremos información acerca del usuario creado en el body, y recibiremos tres parametros muy importantes en Headers, uid(mail), client y access-token, los cuales utilizaremos luego para validar nuestra identidad.

* ### VALIDAR TOKEN -> GET: https://devise-auth-testing.herokuapp.com/api/auth/validate_token
* Acepta request tipo GET, recibe cómo parametros: access-token, uid y client, los cuales obtuvimos al loguearnos. Si la información es correcta recibiremos un succress, de otra manera, será no autorizado o información invalida.
* 
* ### CREAR UN NUEVO ARTICULO -> POST: https://devise-auth-testing.herokuapp.com/api/articles
Para crear un nuevo articulo deberemos enviar vía header nuestro access-token, client y uid. Luego en el body debemos enviar los parametros title y body. Con ésto crearemos un nuevo articulo perteneciente a nuestro usuario. Para ver éste articulo realizaremos un GET en la misma dirección.

### Pueden seguir revisando los endpoints posibles en: https://devise-token-auth.gitbook.io/devise-token-auth/usage la documentación está muy clara y precisa.

Por ultimo, adjunto algunas imágenes de la API siendo testeada en HEROKU.

* ### Creando una cuenta:
![creando cuenta post](https://user-images.githubusercontent.com/81385234/117499913-4a14fa80-af52-11eb-853d-73ea3e18dc5b.jpg)

* ### Sign in SIN confirmar la cuenta por correo: 
![sign in sin confirmar cuenta](https://user-images.githubusercontent.com/81385234/117499973-631dab80-af52-11eb-875e-490137c9ad69.jpg)

* ### Email de confirmación: 
![confirmation email](https://user-images.githubusercontent.com/81385234/117500026-72045e00-af52-11eb-9e8f-075aa10b52cf.jpg)

* ### Sign in con la cuenta ya creada (Body y headers)
![sign_in success](https://user-images.githubusercontent.com/81385234/117500141-97916780-af52-11eb-8a6b-525a1dd0d5c5.jpg)

![sign_in success headers](https://user-images.githubusercontent.com/81385234/117500171-a6781a00-af52-11eb-9a35-f3bfc22b9406.jpg)

* ### Validacion de token
![validate_token ](https://user-images.githubusercontent.com/81385234/117500244-b7c12680-af52-11eb-8c9c-36fa085fed52.jpg)

* ### Creando un articulo con nuestro nuevo usuario (con uid, client y access-token en headers, y 'body' y 'title' como parametros de articulo en el body)
![succesful articles post with headers](https://user-images.githubusercontent.com/81385234/117500372-eccd7900-af52-11eb-81f3-c1aa1047a937.jpg)

Como podemos ver, la gema resulta muy poderosa para una API y puede ser utilizada en producción muy fácilmente, brinda una seguridad robusta y una configuración sencilla.






