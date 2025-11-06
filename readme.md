# Fundamentos Técnicos e Estratégicos / Docker & Docker Compose

- Necessário para as aulas 
    - Instalação do Docker desktop 
        - Windows[https://docs.docker.com/desktop/setup/install/windows-install/]  e [https://docs.docker.com/desktop/]
            Verifique se o seu sistema está com a virtualização ativada: [https://docs.docker.com/desktop/troubleshoot/topics/#virtualization]
            Caso você não tenha o WSL instalado ainda, não se preocupe, o instalador do próprio Docker também irá instalar ele.
            “Virtualization enabled in the BIOS” - Esse processo é diferente para cada marca de placa mãe, recomendamos a pesquisar pela sua fabricante.
            Faça o download do instalador na página: [https://docs.docker.com/desktop/install/windows-install/]. Tome cuidado para baixar a versão correta: x86_64 ou ARM
            Duplo clique em Docker Desktop Installer.exe para executar o instalador.
            Quando solicitado, certifique-se de que a opção "Use o WSL 2 em vez do Hyper-V" na página de Configuração está selecionada ou não, dependendo da sua escolha. (recomendamos usar WSL)
            Se o seu sistema suportar apenas uma das duas opções, você não poderá selecionar qual usar.
            Siga as instruções no assistente de instalação para autorizar o instalador e prosseguir com a instalação.
            Quando a instalação for bem-sucedida, selecione Fechar para completar o processo de instalação.
            Deve aparecer a solicitação para Aceitar os Termos para continuar. O Docker Desktop iniciará após você aceitar os termos.
            Observe que o Docker Desktop não será executado se você não concordar com os termos.
    docker
