---
title: "Resolução de problemas de cliente Windows Defender ou o Endpoint Protection | Microsoft Docs"
description: Saiba como resolver problemas relacionados com o Windows Defender e Endpoint Protection.
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
caps.latest.revision: "7"
caps.handback.revision: "0"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 1b096e71f5131214fb4e235e84d0b7f63e566831
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="troubleshooting-windows-defender-or-endpoint-protection-client"></a>Resolução de problemas de cliente do Windows Defender ou Endpoint Protection

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Se tiver problemas com o Windows Defender ou o Endpoint Protection, contacte o administrador de segurança para obter suporte. Também pode tentar resolver os problemas seguintes:  

-   [Atualizar o Windows Defender ou o Endpoint Protection](#update-windows-defender-or-endpoint-protection)  
-   [A iniciar o serviço Windows Defender ou o Endpoint Protection](#starting-windows-defender-or-endpoint-protection-service)  
-   [Problemas de ligação de Internet](#internet-connection-issues)  
-   [Não é possível remediar a ameaça detetada](#detected-threat-cant-be-remediated)  
-   [Instalar o cliente do Endpoint Protection](#install-the-endpoint-protection-client)  

##  <a name="update-windows-defender-or-endpoint-protection"></a>Atualizar o Windows Defender ou o Endpoint Protection  
 O Windows Defender ou o Endpoint Protection funciona automaticamente com o Microsoft Update para garantir que as definições de vírus e spyware se mantêm atualizadas.  

 **Sintomas**  

 Este artigo aborda problemas comuns das atualizações automáticas, incluindo as seguintes situações:  

-   Vê mensagens de erro a indicar que as atualizações falharam.  

-   Ao verificar a existência de atualizações, recebe uma mensagem de erro indicando que as atualizações das definições de vírus e de spyware não podem ser verificadas, descarregadas ou instaladas.  

-   Apesar de estar ligado à Internet, as atualizações falham.  

-   As atualizações não estão a ser instaladas automaticamente conforme agendado.  

 **Causa**  

 As causas mais comuns dos problemas de atualização são problemas de conectividade Internet. No entanto, se souber que está ligado à Internet, porque consegue navegar noutros sites, o problema poderá ser causado por conflitos com as definições do Windows Internet Explorer.  

> [!IMPORTANT]  
>  Tem de sair do Internet Explorer para concluir estes passos. Portanto, imprima-os, anote-os ou copie-os para outro ficheiro e, em seguida, adicione este tópico aos Favoritos para acesso futuro.  

### <a name="step-1-reset-your-internet-explorer-settings"></a>Passo 1: Repor as definições do Internet Explorer  

1.  Saia de todos os programas abertos, incluindo o Internet Explorer.  

    > [!NOTE]  
    >  Repor estas definições no Internet Explorer elimina os ficheiros temporários, os cookies, o histórico de navegação e as palavras-passe online. Porém, os favoritos não são eliminados.  

2.  Clique em **Iniciar** , procure por **inetcpl.cpl**e, em seguida, prima **Enter**.  

3.  Na caixa de diálogo **Opções da Internet** , clique no separador **Avançadas** .  

4.  Em **Repor definições do Internet Explorer**, clique em **Repor**e, em seguida, clique em **Repor** novamente.  

5.  Aguarde que o Internet Explorer termine a reposição das definições e, em seguida, clique em **OK**.  

6.  Abra o Internet Explorer.  

7.  Abra o Microsoft Security Essentials, clique no separador **Atualizar** e, em seguida, clique em **Atualizar**.  

8.  Se o problema persistir, siga para o passo seguinte.  

### <a name="step-2-set-internet-explorer-as-the-default-browser"></a>Passo 2: Definir o Internet Explorer como browser predefinido  

1.  Saia de todos os programas abertos, incluindo o Internet Explorer.  

2.  Clique em **Iniciar** , procure por **inetcpl.cpl**e, em seguida, prima **Enter**.  

3.  Na caixa de diálogo **Opções da Internet** , clique no separador **Programas** .  

4.  Em **Browser predefinido**, clique em **Predefinir**.  

5.  Clique em **OK**.  

6.  Abra o Windows Defender ou Endpoint Protection. Clique no separador **Atualizar** e, em seguida, clique em **Atualizar**.  

7.  Se o problema persistir, siga para o passo seguinte.  

### <a name="step-3-ensure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>Passo 3: Certifique-se de que a data e hora estão definidas corretamente no seu computador  

1.  Abra o Windows Defender ou Endpoint Protection.  

2.  Se a mensagem de erro que recebeu tiver o código 0x80072f8f, o problema será provavelmente causado por uma data ou hora incorretamente definida no seu computador.  

3.  Para repor a definição de data ou hora do seu computador, siga os passos [Corrigir atalhos incorretos do ambiente de trabalho e tarefas comuns de manutenção do sistema](http://go.microsoft.com/fwlink/?LinkId=155579) (http://go.microsoft.com/fwlink/?LinkId=155579).  

### <a name="step-4-rename-the-software-distribution-folder-on-your-computer"></a>Passo 4: Mudar o nome da pasta de distribuição de Software no seu computador  

1. Parar o serviço de Atualizações Automáticas  

    1.  Clique em **Iniciar** , procure por **services.msc**e, em seguida, clique em **OK**.  

    2.  Clique com o botão direito do rato em **Serviço de Atualizações Automáticas**e, em seguida, clique em **Parar**.  

    3.  Minimize o snap-in Serviços.  

2.  Mude o nome do diretório **SoftwareDistribution** da seguinte forma:  

    1.  Clique em **Iniciar** , procure por  **cmd**e, em seguida, clique em **OK**.  

    2.  Escreva **cd %windir%**e prima **Enter**.  

    3.  Escreva **ren SoftwareDistribution SDTemp**e prima **Enter**.  

    4.  Escreva **exit**e prima **Enter**.  

3.  Inicie o serviço de Atualizações Automáticas da seguinte forma:  

    1.  Maximize o snap-in Serviços.  

    2.  Clique com o botão direito do rato em **Serviço de Atualizações Automáticas**e, em seguida, clique em **Iniciar**.  

    3.  Feche a janela do snap-in Serviços.  

### <a name="step-5-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>Passo 5: Repor o motor de atualização de antivírus da Microsoft no seu computador  

1.  Clique em **Iniciar** , procure por  **cmd**, clique em **OK**, clique com o botão direito do rato em **Linha de comandos**e, em seguida, selecione **Executar como administrador**.  

2.  Na janela da **Linha de Comandos** , escreva os comandos seguintes e prima **Enter** após cada comando:  

     **CD\\**  

     **Defender de files\windows de programa do CD**  

     **Mpcmdrun - RemoveDefinitions-todos os**  

     **Sair**  

3.  Reinicie o computador.  

4.  Abra o Windows Defender ou  
          Endpoint Protection, clique em de **atualização** separador e, em seguida, clique em **atualização**.  

5.  Se o problema persistir, siga para o passo seguinte.  

### <a name="step-6-manually-install-the-virus-and-spyware-definition-updates"></a>Passo 6: Instalar manualmente as atualizações de definições de vírus e spyware  

-   Se estiver a executar um sistema operativo do Windows de 32 bits, transfira manualmente as atualizações mais recentes em [http://go.microsoft.com/fwlink/?LinkID=87342](http://go.microsoft.com/fwlink/?LinkID=87342) (http://go.microsoft.com/fwlink/?LinkID=87342).  

-   Se estiver a executar um sistema operativo do Windows de 64 bits, transfira manualmente as atualizações mais recentes em [http://go.microsoft.com/fwlink/?LinkID=87341](http://go.microsoft.com/fwlink/?LinkID=87341) (http://go.microsoft.com/fwlink/?LinkID=87341).  

-   Clique em **Executar**. As atualizações mais recentes são instaladas manualmente no seu computador.  


### <a name="step-7-contact-support"></a>Passo 7: Contacte o suporte  

-   Caso os passos não tenham resolvido o problema, contacte o suporte. Para obter mais informações, consulte [Suporte ao Cliente](http://go.microsoft.com/fwlink/?LinkID=196174) (http://go.microsoft.com/fwlink/?LinkID=196174).  

##  <a name="starting-windows-defender-or-endpoint-protection-service"></a>A iniciar o serviço Windows Defender ou o Endpoint Protection  
 **Sintoma**  

 Receberá uma mensagem notificando-que **Windows Defender ou o Endpoint Protection não está a monitorizar o computador porque o serviço do programa parou. Deve reiniciá-lo agora.** 

 **Solução**  

### <a name="step-1-restart-your-computer"></a>Passo 1: Reinicie o computador.  

-   Feche todas as aplicações e reinicie o seu computador.  

### <a name="step-2-make-sure-the-windows-defender-or-endpoint-protection-service-is-set-to-automatic-and-is-started"></a>Passo 2: Certifique-se "Windows Defender" ou "Serviço de Endpoint Protection" está definido como automático e é iniciado  

1.  Clique em **Iniciar** , procure por **services.msc**e, em seguida, prima **Enter**.  

2.  Procure o **Serviço Microsoft Antimalware**. Clique com o botão direito do rato no mesmo e selecione **Propriedades** ou faça duplo clique para abrir o serviço.  

3.  Certifique-se de que o "**Tipo de Arranque**" está definido como"**Automático**".  

4.  Clique no botão **Iniciar** para iniciar o serviço. Se o botão **Iniciar** não estiver disponível, clique no botão **Parar** e, em seguida, clique no botão **Iniciar** para reiniciar o serviço.  

5.  Certifique-se de que anota quaisquer erros que possam aparecer durante este processo, submete um incidente online e inclui as informações de erro.  

### <a name="step-3-remove-any-existing-internet-security-programs"></a>Passo 3: Remover quaisquer programas de segurança da Internet existentes  

1.  Clique em **Iniciar** , procure por **appwiz.cpl**e, em seguida, prima **Enter**.  

2.  Na lista de programas instalados, desinstale quaisquer programas de segurança da Internet de terceiros.*  

3.  Reinicie o computador e, em seguida, tente instalar o Windows Defender ou  
          Novamente a proteção de ponto final.  

> [!NOTE]  
>  Algumas aplicações de segurança da Internet não são desinstaladas completamente. Poderá ter de transferir e executar um utilitário de limpeza para a aplicação de segurança anterior de modo a removê-la completamente.  

> [!CAUTION]  
>  Quando remove programas de segurança da Internet, o seu computador fica desprotegido. Se tiver problemas a instalar   
>       Proteção de ponto final após a remoção de programas de segurança da Internet existentes, contacte o Windows Defender ou  
>       Suporte de proteção de ponto final, submetendo um incidente online (para obter mais informações, consulte [como submeter um incidente Online](http://www.microsoft.com/en-ph/security_essentials/Support/8c9074b6-1558-4d14-bc39-d294ced11096.aspx)).  

### <a name="step-4-uninstallreinstall-endpoint-protection"></a>Passo 4: Desinstalar/reinstalar o Endpoint Protection  

1.  Clique em **Iniciar** , procure por **appwiz.cpl**e, em seguida, prima **Enter**.  

2.  Na lista de programas instalados, clique em **Endpoint Protection**e desinstale-o.  

3.  Se lhe for solicitado, reinicie o computador e, em seguida, tente instalar o Endpoint Protection novamente.  

##  <a name="internet-connection-issues"></a>Problemas de ligação de Internet  
 Para garantir que o computador recebe as atualizações mais recentes do Windows Update, tem de estar ligado à Internet.  

### <a name="step-1-verify-that-your-computer-is-connected-to-the-internet"></a>Passo 1: Certifique-se de que o computador está ligado à Internet  

1.  Clique em **Iniciar**, procure por **ncpa.cpl**e, em seguida, prima **Enter**.  

2.  Clique com o botão direito do rato no nome da ligação e clique em **Estado**.  

3.  Se o computador estiver ligado, o estado da ligação aparecerá como **Ligado**, **Ativado**ou **Autenticação** com êxito no Windows XP. No Windows Vista e no Windows 7, o estado do **IPv4** irá aparecer como **Internet**.  

4.  Se o computador não parecer estar ligado, clique com o botão direito do rato no nome da ligação e, em seguida, clique em **Ligar**, **Ativar**, **Autenticar**ou **Reparar**.  

### <a name="step-3-restart-your-computer"></a>Passo 3: Reinicie o computador  

-   Feche quaisquer programas abertos e reinicie o seu computador.  

### <a name="step-4-if-you-still-cant-connect-to-the-internet-check-your-connections"></a>Passo 4: Se ainda não é possível ligar à Internet, verifique as suas ligações  

1.  Se utilizar uma ligação de acesso telefónico, certifique-se de o cabo da ligação telefónica está devidamente inserido na tomada de parede e no modem.  

2.  Se utilizar um modem de cabo, certifique-se de que a ligação de cabo ao modem e a ligação do modem ao computador estão corretas.  

3.  Se utilizar um modem de cabo ou um router DSL, certifique-se de que as ligações ao router e ao computador estão corretas. Experimente desligar e desativar o router e o modem. Aguarde alguns minutos, ligue o modem em primeiro lugar, espere um minuto e, em seguida, ligue o router e reinicie o computador.  

##  <a name="detected-threat-cant-be-remediated"></a>Não é possível remediar a ameaça detetada  
 Quando o Windows Defender ou  
      Endpoint Protection Deteta uma potencial ameaça que esteja oculta dentro de um ficheiro comprimido com uma extensão de nome de ficheiro. zip ou numa partilha de rede, este tenta lidar com a ameaça por em quarentena ou removendo a ameaça.  

### <a name="remove-or-scan-the-file"></a>Remover ou analisar o ficheiro  

-   Se a ameaça detetada estava num ficheiro .zip, navegue até ao ficheiro .zip e, em seguida, remova o ficheiro ou analise-o, clicando com o botão direito do rato no ficheiro ou selecionando **Analisar com o Windows Defender** ou **Analisar com o Endpoint Protection**. Se o Windows Defender ou o Endpoint Protection detetar ameaças adicionais no ficheiro, este notifica-o sobre estas ameaças e permite-lhe escolher uma ação adequada.  

-   Se a ameaça detetada estava numa partilha de rede, navegue até à partilha de rede e analise-a, clicando com o botão direito do rato no ficheiro e selecionando **Analisar com o Windows Defender** ou **Analisar com o Endpoint Protection**. Se o Windows Defender ou o Endpoint Protection detetar ameaças adicionais na partilha de rede, este notifica-o sobre estas ameaças e permite-lhe escolher uma ação adequada.  

-   Se não tiver a certeza da origem do ficheiro, uma das melhores soluções consiste em executar uma análise completa no seu computador. Uma análise completa pode demorar algum tempo a concluir, mas permite que o Windows Defender ou o Endpoint Protection procure a origem da infeção e limpe a mesma.  

##  <a name="install-the-endpoint-protection-client"></a>Instalar o cliente do Endpoint Protection  

> [!NOTE]  
>  O Windows Defender é instalado com o sistema operativo em PCs Windows 10.  

 **Sintomas**  

 Falhas de instalação por um motivo desconhecido ou recebe uma mensagem de erro com código de erro, tal como 0x80070643, 0X8007064A, 0x8004FF2E, 0x8004FF01, 0x8004FF07, 0x80070002, 0x8007064C, 0x8004FF00, 0x80070001, 0x80070656, 0x8004FF40, 0xC0000156, 0x8004FF41 0x8004FF0B, 0x8004FF11, 0x80240022, 0x8004FF04, 0x80070660, 0x800106B5, 0x80070715, 0x80070005, 0x8004EE00, 0x8007003, 0x800B0100, 0x8007064E ou 0x8007007E.  

 Se o seu computador está a executar o Windows XP Service Pack 2 (SP2), poderá ver uma ou mais das seguintes mensagens de erro:  

-   O Assistente de Instalação tem um pacote de rollup de gestor de filtro em falta necessário para concluir a instalação.  

-   Erro de Configuração KB914882, o programa de Configuração não consegue atualizar os ficheiros do Windows XP porque o idioma instalado no seu sistema é diferente do idioma de atualização.  

 **Causa**  

 O Endpoint Protection não pode ser instalado num computador que tenha outros programas de segurança em execução. Por vezes, mesmo que remova outros programas de segurança, estes não são totalmente desinstalados. Tem de executar uma versão genuína do sistema operativo Windows para instalar o Endpoint Protection.  

 **Solução**  

> [!IMPORTANT]  
>  Terá de reiniciar o computador ao resolver este problema. Marque esta página (marque-a como um Favorito) para que seja mais fácil encontrar este tópico novamente ou imprima-o para fácil referência.  

### <a name="step-1-remove-any-existing-security-programs"></a>Passo 1: Remover quaisquer programas de segurança existentes  
**Apenas a proteção de ponto final**

1.  Desinstale completamente quaisquer programas de segurança da Internet existentes.  

2.  Reinicie o computador.  

3.  Instale o Endpoint Protection novamente. Se isto não resolver o problema, siga para o passo seguinte.  

### <a name="step-2-ensure-that-the-windows-installer-service-is-running"></a>Passo 2: Certifique-se de que o serviço Windows Installer está em execução  

1.  Clique em **Iniciar** , procure por **services.msc**e, em seguida, prima **Enter**.  

2.  Clique com o botão direito do rato em **Windows Installer**e, em seguida, clique em **Iniciar**. Se a opção **Iniciar** não estiver disponível e as opções **Parar** e **Reiniciar** estiverem disponíveis, isto indica que o serviço já foi iniciado.  

3.  Na página **Serviços** , no menu **Ficheiro** , clique em **Sair**.  

4.  Clique em **iniciar** e procure **linha de comandos**. Clique com o botão direito do rato em **Linha de Comandos**e, em seguida, clique em **Executar como administrador**.  

5.  Escreva **MSIEXEC /REGSERVER**e, em seguida, prima **Enter**.  

    > [!NOTE]  
    >  Não existe nenhuma indicação de que este comando teve êxito ou falhou.  

6.  Instale o Endpoint Protection novamente. Se isto não resolver o problema, siga para o passo seguinte.  

### <a name="step-3-start-windows-in-selective-startup-mode"></a>Passo 3: Iniciar o Windows em modo de arranque Seletivo  

1.  Clique em **Iniciar** , procure por **msconfig**e, em seguida, prima **Enter**.  

2.  No separador **Geral** , clique em **Arranque Seletivo**e, em seguida, desmarque a caixa de verificação **Carregar Itens de Arranque** .  

3.  No separador **Serviços** , selecione a caixa de verificação **Ocultar Todos os Serviços Microsoft** e, em seguida, desmarque todas as caixas de verificação dos serviços que permanecem na lista.  

4.  Clique em **OK**e, em seguida, clique em **Reiniciar** para reiniciar o computador.  

5.  Tente instalar o Endpoint Protection novamente.  



### <a name="see-also"></a>Consulte também  
 [Perguntas mais frequentes de cliente do Endpoint Protection](../../protect/deploy-use/endpoint-protection-client-faq.md)   

 [Ajuda do cliente do Endpoint Protection](../../protect/deploy-use/endpoint-protection-client-help.md)
