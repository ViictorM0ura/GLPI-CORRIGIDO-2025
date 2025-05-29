🛠️ Manual de Instalação do GLPI no Windows
📝 Resumo Inicial
Esta versão do GLPI foi corrigida e otimizada, com todas as funcionalidades funcionando 100%. O módulo de chamados, uma das partes mais críticas do sistema, foi especialmente melhorado para garantir que não haja mais erros na criação, visualização e gestão de chamados. A versão foi testada com sucesso em 2025, oferecendo uma experiência estável e eficiente para o gerenciamento de chamados e ativos.

🔧 Pré-requisitos
Antes de instalar o GLPI, você precisará do seguinte:

Windows 10 ou superior

XAMPP (ou similar) para instalar Apache, MySQL/MariaDB e PHP

GLPI versão mais recente (baixe do site oficial se não quiser usar essa versão com o sistema de chamados mexido)
```
https://glpi-project.org/
```

🚀 Passo a Passo para Instalar o GLPI no Windows
1️⃣ Instalar o XAMPP
O XAMPP é uma plataforma que fornece Apache (servidor web), MySQL/MariaDB (banco de dados) e PHP (linguagem de script), necessários para rodar o GLPI.

Baixar o XAMPP:
Acesse o site oficial do XAMPP e baixe a versão mais recente.

Instalar o XAMPP:
Execute o instalador e siga as instruções para instalar o XAMPP no seu sistema Windows.

2️⃣ Configurar Apache e MySQL no XAMPP
Abrir o XAMPP:
Após a instalação, abra o painel de controle do XAMPP.

Iniciar Apache e MySQL:
No painel, clique em Start para Apache e MySQL. Ambos devem estar com o status "Running".

3️⃣ Baixar e Instalar o GLPI
Baixar o GLPI:
Acesse o site oficial do GLPI e baixe a versão mais recente do GLPI.

Extrair o GLPI:
Extraia o arquivo ZIP do GLPI para a pasta htdocs do XAMPP, que geralmente está localizada em:
```
C:\xampp\htdocs\
```
O caminho completo será algo como:
```
C:\xampp\htdocs\glpi
```
Alterar Permissões (se necessário):
Configure as permissões para garantir que o servidor Apache possa acessar o GLPI.

4️⃣ Configurar o Banco de Dados para o GLPI
Acessar o phpMyAdmin:
No painel do XAMPP, clique em Admin ao lado de MySQL para abrir o phpMyAdmin no navegador.

Criar o Banco de Dados:
No phpMyAdmin, vá até Databases e crie um novo banco de dados chamado glpidb.

Criar um Usuário para o GLPI:
No phpMyAdmin, clique em User Accounts e crie um novo usuário com as seguintes configurações:
Nome de usuário: glpiuser
Senha: (Defina uma senha segura)
Banco de dados: glpidb
Conceda todas as permissões para esse usuário.

5️⃣ Configurar o Servidor Web (Apache ou Nginx)
Apache:
Criar Configuração do Apache:
Crie um arquivo de configuração para o GLPI em /etc/apache2/sites-available/glpi.conf (no seu caso, a configuração pode ser feita no painel do XAMPP).

Adicionar Configurações:
Adicione a configuração básica para o GLPI no arquivo glpi.conf:
```
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot C:/xampp/htdocs/glpi
    ServerName glpi.local
    <Directory C:/xampp/htdocs/glpi>
        AllowOverride All
        Require all granted
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
Habilitar a Configuração:
Ative a configuração e reinicie o Apache:
```
sudo a2ensite glpi.conf
sudo systemctl restart apache2
```

6️⃣ Configuração do GLPI via Navegador
Acessar o GLPI:
Abra o navegador e acesse o GLPI digitando o seguinte endereço:
```
http://localhost/glpi
```

Passar pelo Assistente de Instalação:
O assistente de instalação do GLPI será carregado. Siga as instruções:
Selecione o idioma (por padrão, será Português)
Aceite os termos de licença.
Verifique os pré-requisitos.
Conecte-se ao banco de dados com as credenciais criadas:
Banco de dados: glpidb
Usuário: glpiuser
Senha: (senha que você definiu)

Finalizar a Instalação:
O assistente concluirá a instalação e você será redirecionado para a tela de login do GLPI.

7️⃣ Configuração Inicial do GLPI
Login Padrão:
Após a instalação, faça o login com o usuário:
Usuário: glpi
Senha: glpi

Alterar a Senha do Administrador:
O GLPI solicitará que você altere a senha do administrador no primeiro login.

Configuração de Entidades e Perfis:
Configure as entidades (unidades organizacionais) e perfís de usuários conforme necessário.

8️⃣ Ativando o Módulo de Chamados
Acessar o Menu de Assistência:
No painel principal, clique em Assistência para acessar o módulo de chamados.

Configurar Categorias e Prioridades:
Configure as categorias de chamados, como "Suporte Técnico", "Solicitação de Equipamentos", etc.
Defina as prioridades dos chamados, como "Baixa", "Média" e "Alta".

Configurar Regras de Atribuição de Chamados:
Acesse Administração > Regras de Atribuição para definir como os chamados serão atribuídos automaticamente a técnicos ou equipes.

9️⃣ Configuração de E-mails para Chamados
Configuração de SMTP:
Acesse Configurar > Gateways de E-mail e adicione uma nova conta de e-mail para recebimento de chamados.

Regras de Atribuição para Chamados via E-mail:
Configure as regras para processar os e-mails recebidos e criar chamados automaticamente.
