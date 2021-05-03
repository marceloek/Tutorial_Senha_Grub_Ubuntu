# Tutorial - Como proteger o Grub com senha no Ubuntu.

Proteger o Grub é interessante para restringir o seu acesso prevenindo a edição nos parâmetros de boot e do kernel, além de dificultar o acesso ao modo de recuperação, em caso de usuários mal-intencionados. 

## Inserindo senha ao Grub

#### Passo 1. Abra um terminal (Ctrl + Alt + T).

#### Passo 2. Execute o comando abaixo para criar a senha que será usada no grub. 
``sudo grub-mkpasswd-pbkdf2``

Obs: Será necessário digitar tanto a senha do root como repetir a senha a ser criada. 

#### Passo 3. Como o comando irá retornar o hash da senha digitada, salve-o em algum arquivo de texto.

#### Passo 4. Faça o backup do arquivo de configuração do Grub:
``sudo cp /etc/grub.d/40_custom /etc/grub.d/40_custom.old``

#### Passo 5. Edite o arquivo do grub destinado a customizações:
``sudo nano /etc/grub.d/40_custom``

#### Passo 6. Adicione no final do arquivo as seguintes linhas:
``set superusers="root"``

``password_pbkdf2 root grub.pbkdf2.sha512.xyz``

Sendo que em `set superusers="root"` são os usuários do sistema e em `grub.pbkdf2.sha512.xyz` o hash da sua senha que você deverá substituir.

#### Passo 7. Com as modificações finalizadas é necessário atualizar o Grub:
``sudo update-grub``

#### Passo 8. Reinicie o sistema.

Ao reiniciar o sistema e entrar no Grub qualquer ação será pedido digitar o usuário e a senha correspondente.

## Como remover a senha voltando a configuração original

#### Passo 1. Abra um terminal (Ctrl + Alt + T).

#### Passo 2. Restaure o arquivo de configuração do Grub;

``sudo cp /etc/grub.d/40_custom.old /etc/grub.d/40_custom``

#### Passo 3. Atualize o Grub;

``sudo update-grub``
