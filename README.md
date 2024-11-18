# **Máquina Virtual Debian 10 - Guia de Utilização**
Este README contém instruções e descrições dos comandos mais utilizados na configuração e gerenciamento de uma máquina virtual Debian 10.

### **Índice**
Verificação de Assinatura
Configuração Simples
Gerenciamento de Usuários
Configuração do Hostname
Partições
Permissões de Superusuário (sudo)
Configuração de Firewall (UFW)
Acesso SSH
Agendamento de Tarefas (Cron)
Bônus
Verificação de Assinatura
Use o comando abaixo para verificar a integridade de um arquivo usando a assinatura SHA-1:

´´´bash
certUtil -hashfile debian10.vdi sha1
```

### **Configuração Simples**
1. Checar ambiente gráfico instalado:

´´´bash
sudo dpkg -l
```
/xorg e /wayland: Protocolo gráfico mais comum para sistemas Linux.

2. Verificar o status do AppArmor e serviços importantes:
´´´bash
sudo aa-status              # Status do AppArmor  
sudo service ssh status     # Status do serviço SSH  
sudo ufw status             # Status do firewall UFW  
cat /etc/os-release         # Ver sistema operacional e versão  
uname -v                    # Versão do kernel do sistema  
```


### **Gerenciamento de Usuários**
1. Ver usuários e grupos:
´´´bash
getent group sudo           # Lista usuários no grupo 'sudo'  
getent group user42         # Lista usuários no grupo 'user42'  
cat /etc/passwd             # Exibe todos os usuários do sistema  
```

2. Criar novo usuário e gerenciar políticas de senha:
´´´bash
sudo adduser username          # Cria um novo usuário  
sudo chage -l username         # Ver informações de expiração de senha  
sudo chage -n 2 username       # Define um mínimo de 2 dias entre alterações de senha  
sudo chage -M 30 username      # Define expiração de senha em 30 dias  
sudo adduser username sudo     # Adiciona ao grupo 'sudo'  
sudo groupadd groupname        # Cria um novo grupo
sudo usermod -aG groupname username # Adiciona usuário ao grupo
```

## **Configuração do Hostname**
Ver e alterar o hostname:
´´´bash
hostname                       # Exibe o nome do host atual  
sudo hostnamectl set-hostname novo-hostname # Altera o hostname  
sudo nano /etc/hostname        # Edita o arquivo de hostname diretamente  
sudo nano /etc/hosts           # Atualiza o nome do host no arquivo hosts  
sudo reboot                    # Reinicia a máquina para aplicar mudanças
```
### **Partições**
Para visualizar as partições do sistema:

´´´bash
lsblk
```

## **Permissões de Superusuário (sudo)**
1 .Configurar regras para sudoers:
´´´bash
sudo visudo
```

2. Acessar logs de sudo:
´´´bash
cd /var/log/sudo/00/00 && ls  
cat log       # Exibe entradas de log  
cat ttyout    # Exibe saídas de log
```

## **Configuração de Firewall (UFW)**
1. Gerenciar o firewall UFW:
´´´bash
sudo ufw status               # Verificar status do firewall  
sudo ufw allow 8080           # Permitir acesso na porta 8080  
sudo ufw delete allow 8080    # Remover permissão para a porta 8080
 ```
## **Acesso SSH**
1. Obter endereço IP da máquina:
´´´bash
ip a
```

2. Conectar via SSH:
´´´bash
ssh username@ip_address -p 4242
```

## **Agendamento de Tarefas (Cron)**
1. Gerenciar Cron:
´´´bash
sudo crontab -l                  # Listar tarefas agendadas  
sudo crontab -u root -e          # Editar tarefas do usuário root  
sudo service cron stop/start     # Parar ou iniciar o serviço Cron  
sudo service cron enable/disable # Habilitar ou desabilitar o Cron  
sudo service cron restart        # Reiniciar o serviço Cron
```

## **Bônus**
1. Realizar testes de conectividade:

´´´bash
dig [site] 
ping [site]
```

2. Redirecionar porta local com SSH:
´´´bash
ssh -N -L 8080:127.0.0.1:8080 username@ip_address -p 4242
```

Acesse no navegador:
´´´bash
http://127.0.0.1
```
