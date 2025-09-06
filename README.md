# 📧 Servidor de E-mail Básico no Ubuntu

Este repositório contém os documentos e um roteiro simplificado para montar um servidor de e-mail básico em uma máquina **Ubuntu**. A ideia é criar um ambiente de demonstração para entender os componentes principais de um sistema de e-mail.

## 🚀 Tecnologias Utilizadas

  * **Postfix:** Responsável por enviar e receber e-mails (MTA - Mail Transfer Agent).
  * **Dovecot:** Fornece acesso aos e-mails através dos protocolos IMAP/POP3.
  * **Roundcube (Opcional):** Um cliente de webmail para acessar as contas via navegador.

## ⚙️ Roteiro de Instalação e Configuração

Siga os passos abaixo para configurar o servidor de e-mail na sua máquina Ubuntu.

### 1\. Atualizar o Sistema

É sempre uma boa prática garantir que o sistema esteja atualizado antes de começar.

```bash
sudo apt update && sudo apt upgrade -y
```

### 2\. Instalar o Postfix

O Postfix é o coração do nosso servidor. Durante a instalação, ele fará algumas perguntas de configuração.

```bash
sudo apt install postfix -y
```

**Durante a instalação:**

  * **Tipo de configuração:** Selecione `Internet Site`.
  * **System mail name:** Defina um nome para o seu domínio local. Por exemplo: `meuservidor.local`.

Se precisar revisar as configurações depois, edite o arquivo principal:

```bash
sudo nano /etc/postfix/main.cf
```

### 3\. Instalar o Dovecot

O Dovecot é necessário para que os usuários possam acessar suas caixas de entrada usando clientes de e-mail como Thunderbird ou aplicativos de celular. Ele implementa os protocolos IMAP e POP3.

```bash
sudo apt install dovecot-imapd dovecot-pop3d -y
```

O arquivo de configuração principal geralmente não precisa de alterações, mas você pode encontrá-lo aqui:

```
/etc/dovecot/dovecot.conf
```

### 4\. Criar Usuários de Teste

Para demonstrar o envio e recebimento de e-mails, podemos usar os usuários locais do próprio Ubuntu como contas de e-mail.

```bash
sudo adduser alice
sudo adduser bob
```

Agora, os e-mails enviados para `alice` ou `bob` no servidor local serão entregues em suas respectivas caixas de entrada.

### 5\. Testar o Envio de E-mail Local

Vamos usar a ferramenta `mail` para enviar uma mensagem de teste. Primeiro, instale o `mailutils` se ainda não tiver:

```bash
sudo apt install mailutils -y
```

**Exemplo:**
Faça login como o usuário `alice` e envie uma mensagem para `bob`.

```bash
# Exemplo de como enviar um email de Alice para Bob
echo "Oi Bob, teste do servidor!" | mail -s "Teste" bob
```

Para verificar se a mensagem foi recebida, faça login como o usuário `bob` e digite `mail`:

```bash
# Logado como bob
mail
```

Você verá a mensagem de `alice` na lista.

### 6\. (Opcional) Instalar um Webmail com Roundcube

Para uma demonstração mais visual e interativa, você pode instalar um cliente de webmail. O Roundcube é uma ótima opção.

```bash
sudo apt install roundcube roundcube-core roundcube-mysql -y
```

Após a instalação, você poderá acessar o webmail pelo navegador:
`http://<ip-do-servidor>/roundcube`

Use os usuários que você criou (`alice`, `bob`) para fazer login e testar o envio e recebimento de e-mails diretamente pela interface web.

## 🎬 Demonstração para Apresentação

Para uma apresentação, a demonstração pode seguir esta lógica:

1.  **Explique o Papel de Cada Componente:**
      * **Postfix:** É o carteiro que envia e recebe e-mails.
      * **Dovecot:** É a caixa dos correios, que organiza e entrega os e-mails aos usuários.
2.  **Faça uma Demonstração Prática:**
      * Mostre o processo de envio de uma mensagem de `alice` para `bob`.
      * Em seguida, mostre como `bob` recebe essa mensagem, seja pela linha de comando ou pela interface do Roundcube.
