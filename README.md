🚀 Roteiro básico para montar um servidor de e-mail no Ubuntu
1. Atualizar o sistema
sudo apt update && sudo apt upgrade -y

2. Instalar Postfix
sudo apt install postfix -y


Durante a instalação, ele abre um menu de configuração:

Tipo de configuração: selecione Internet Site

System mail name: coloque o domínio que vai simular, exemplo: meuservidor.local

Depois você pode revisar o arquivo principal:

sudo nano /etc/postfix/main.cf

3. Instalar Dovecot (para IMAP/POP3)
sudo apt install dovecot-imapd dovecot-pop3d -y


Isso permite que os usuários acessem o e-mail com clientes como Thunderbird ou até o celular.

Arquivo principal:

/etc/dovecot/dovecot.conf


Geralmente não precisa mudar nada além do básico.

4. Criar usuários de teste

Como você provavelmente não tem domínio registrado para a demo, dá pra usar usuários locais do Ubuntu como contas de e-mail:

sudo adduser alice
sudo adduser bob


Agora o alice pode mandar e receber e-mails para o bob dentro do servidor.

5. Testar envio de e-mail local

Com o comando mail (instale se precisar):

sudo apt install mailutils -y


Exemplo: logado como alice, enviar para bob:

echo "Oi Bob, teste do servidor!" | mail -s "Teste" bob


Depois logue como bob e rode:

mail


Você verá a mensagem de Alice.

6. (Opcional) Instalar um Webmail (para demo mais bonita)

Exemplo com Roundcube:

sudo apt install roundcube roundcube-core roundcube-mysql -y


Aí você acessa pelo navegador http://ip-da-vm/roundcube e faz login com os usuários criados (alice, bob).

7. Mostrar na apresentação

Explicar que Postfix → envia e recebe e-mails

Dovecot → entrega os e-mails para os usuários (IMAP/POP3)

Fazer uma demo rápida: Alice envia um e-mail, Bob recebe
