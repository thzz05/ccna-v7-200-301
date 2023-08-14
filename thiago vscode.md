Início
    Cabo console conecta no switch switch cisco catalyst 2960 24 portas e no pc
    Abre o terminal e digita Enable pra entrar no modo de EXEC PRIVILEGIADO que é uma espécie de root, Disable pra desativar a voltar o modo de antes
 
Setar horário
   clock set 14:17:00 13 august 2023
 
Configurar TUDO
configure terminal                      -> entra na "pasta" configurações
hostname sw-l2-2960-1                   -> nomeia o hostname
    service password-encryption             -> coloca senhas
    service timestamps log datetime msec    -> coloca logs  
        no ip domain-lookup                     -> remove a verificação de comandos por dominio que trava a maquina
        banner motd #AVISO: acesso autorizado somente para funcionarios    -> coloca uma mensagem
        enable secret 123@senac                 -> coloca a senha quando tenta dar enable 
        end                                     -> volta ao inicio como se fosse o inicio do root fora da "pasta" config
        copy running-config startup-config      -> faz a configuração ser salva e abrir toda vez que for iniciado o switch
        exit                                    -> sai de tudo
        username senac secret 123@senac         -> cria usuario e senha local
 
        line console 0                          -> sobe mais um nivel na configuração 
            login local                     -> habilita a autenticação local
            password 123@senac              -> 
            logging synchronous             -> manter o sincronismo dos logs pra nao ficar aparecendo na tela
            exec-timeout 5 30               -> desconecta automaticamente em 5 minutos e 30 segundos
            end........
 
                line vry 0 4 
                    login local
                    password 123@senac
                    logging synchronous
                    exec-timeout 5 30 
                    transport input all
                    end
                    write
 
 
===========================================================================