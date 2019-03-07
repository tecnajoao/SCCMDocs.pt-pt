---
title: Windows Autopilot para os dispositivos existentes
titleSuffix: Configuration Manager
description: Utilizar uma sequência de tarefas do Configuration Manager para a recriação de imagem e aprovisionar um dispositivo com Windows 7 para o modo de controlada pelo usuário do Windows Autopilot
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 2e96f847-5b5a-4da9-8e8f-6aa488838508
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6878e36e5bf20774f6eef1ee855dda2f95dabfb4
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558012"
---
# <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot para os dispositivos existentes
<!--3607717, fka 1358333-->

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

[Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) fornece uma forma para que as organizações são enviados inalterados atualizados os dispositivos Windows 10 diretamente para o utilizador final e definir o fluxo de aprovisionamento, o utilizador passa por obter um dispositivo de Windows 10 seguro e produtivo. O dispositivo está registado com o serviço do Windows Autopilot, para poder atribuir o perfil de Autopilot do Windows necessário. Este perfil define a experiência de out-of-box (OOBE) para que o dispositivo. 

[Windows Autopilot para dispositivos existentes](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) está disponível com o Windows 10, versão 1809 ou posterior. Esta funcionalidade permite-lhe criar uma nova imagem e aprovisionar um dispositivo Windows 7 para [modo de controlada pelo usuário do Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) utilizando uma sequência de tarefas do Configuration Manager única e nativo. 



## <a name="prerequisites"></a>Pré-requisitos

- Adquira a mídia de instalação para Windows 10 versão 1809 ou posterior. Em seguida, crie uma imagem de SO do Configuration Manager. Para obter mais informações, consulte [imagens do sistema operacional de gerir](/sccm/osd/get-started/manage-operating-system-images).

- No Microsoft Intune, crie perfis para o Windows Autopilot. Para obter mais informações, consulte [Windows inscrever dispositivos no Intune com o Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot).

- Um dispositivo ainda não estiver registado no serviço do Windows Autopilot. Se o dispositivo já está registado, o perfil atribuído tem precedência. O Autopilot para o perfil de dispositivos existente só se aplica se que o perfil online exceder o tempo limite.



## <a name="create-the-configuration-file"></a>Criar o ficheiro de configuração

1. Num dispositivo Windows com ligação à internet, abra uma janela de comando do PowerShell administrativa e execute os seguintes comandos:  

    1. Instalar os módulos necessários e aceitar pedidos para continuar  
        ``` PowerShell  
        Install-Module AzureAD
        Install-Module WindowsAutopilotIntune 
        Import-Module WindowsAutopilotIntune 
        ```

    2. Inicie sessão no Intune com as credenciais de administrador  
        ``` PowerShell  
        Connect-AutopilotIntune 
        ```

    3. Obter todos os perfis do Autopilot do Windows associados do seu inquilino do Intune  
        ``` PowerShell  
        $AutopilotProfile = Get-AutopilotProfile
        ```

    4. Crie um ficheiro de configuração para cada perfil. Os ficheiros são com o nome para o nome a apresentar do perfil e guardados na área de trabalho do utilizador atual.<!--PowerShell example courtesy of GitHub user treestryder from SCCMDocs issue #1196-->  
        ``` PowerShell  
        $AutopilotProfile | ForEach-Object { $_ | ConvertTo-AutoPilotConfigurationJSON | Set-Content -Encoding Ascii "~\Desktop\$($_.displayName).json" }
        ```  

        > [!Note]  
        > O ficheiro de configuração só pode conter um perfil. Cada perfil deve ser dentro de chavetas `{}`.  

2. Guardar um dos perfis para um com o nome de ficheiro codificado ANSI **AutopilotConfigurationFile.json**. Guarde-o para uma localização adequada como um Gestor de configuração da origem do pacote.  

    > [!Tip]  
    > Se utilizar o cmdlet do PowerShell **out-File** para redirecionar a saída JSON para um arquivo, ele usa codificação Unicode por predefinição. Este cmdlet também pode truncar longas linhas. Utilize o **Set-Content** cmdlet com o `-Encoding ASCII` parâmetro para definir a codificação de texto adequado.   
    > 
    > Bloco de notas do Windows utiliza por predefinição de codificação ANSI.  

3. Crie um pacote do Configuration Manager que contém este ficheiro. Ele não requer um programa. Para obter mais informações, consulte [criar um pacote](/sccm/apps/deploy-use/packages-and-programs#create-a-package-and-program).  

    > [!NOTE]  
    > Windows requer que este ficheiro é denominado **AutopilotConfigurationFile.json**. Para utilizar mais do que um perfil de Autopilot, crie pacotes separados do Configuration Manager.  



## <a name="create-the-task-sequence"></a>Criar a sequência de tarefas

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione o **sequências de tarefas** nó. Selecione **criar sequência de tarefas** na faixa de opções.  

2. Sobre o **criar nova sequência de tarefas** , selecione a opção de **implementar o Windows Autopilot para dispositivos existentes**.  

3. Sobre o **informações da sequência de tarefas** página, especifique um nome, opcionalmente, adicione uma descrição e selecione uma imagem de arranque. Para obter mais informações sobre versões de imagem de arranque suportados, consulte [suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).  

4. Sobre o **instalar o Windows** , selecione o Windows 10 **pacote de imagem**. Em seguida, configure as seguintes definições:  

    - **Índice de imagens**: Selecione Enterprise, Education ou profissional, conforme exigido pela sua organização  

    - Ativar a opção para **particionar e formatar o computador de destino antes de instalar o sistema operativo**  

    - **Configurar a sequência de tarefas para utilização com o Bitlocker**: Se ativar esta opção, a sequência de tarefas inclui os passos necessários para ativar o Bitlocker  

    - **Chave de produto**: Se tiver de especificar uma chave de produto para ativação do Windows, introduza-o aqui  

    - Selecione uma das seguintes opções para configurar a conta de administrador local no Windows 10:  
        - **Gerar a palavra-passe de administrador local aleatoriamente e desativar a conta em todas as plataformas de suporte (recomendado)**
        - **Ativar a conta e especificar a palavra-passe de administrador local**

5. Sobre o **configurar rede** , selecione a opção de **Junte-se a um grupo de trabalho**. Esta sequência de tarefas utiliza a ferramenta de preparação do sistema Windows (sysprep). Se o dispositivo estiver associado a um domínio, o sysprep falhe.  

6. Sobre o **instalar o Configuration manager** página, adicione as propriedades de instalação necessários para o seu ambiente.  

    > [!Tip]  
    > A sequência de tarefas só precisa dessas informações se os componentes do cliente do Configuration Manager são necessários durante a sequência de tarefas antes da execução de sysprep. Por exemplo, para instalar atualizações de software ou aplicativos. Se não estiver a realizar estas ações, o cliente não é necessário. Será desinstalado antes da sequência de tarefas executa o sysprep.  

7. O **incluem atualizações** página seleciona por predefinição, a opção **não instalar quaisquer atualizações de software**.  

    > [!Tip]  
    > Utilize a manutenção de imagens offline para manter a imagem atualizada com as mais recentes atualizações de qualidade do Windows 10. Para obter mais informações, consulte [aplicar atualizações de software numa imagem de SO](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates).  

8. Sobre o **instalar aplicações** página, pode selecionar aplicações a instalar durante a sequência de tarefas. No entanto, a Microsoft recomenda que espelhar a abordagem de imagem de assinatura com este cenário. Depois do dispositivo Aprovisiona com Autopilot, aplicam-se de que todas as aplicações e configurações de cogestão Microsoft Intune ou Configuration Manager. Este processo fornece uma experiência consistente entre os usuários a receção de novos dispositivos e como as que utilizam o Windows Autopilot para dispositivos existentes.  

8. Sobre o **preparação do sistema** página, selecione o pacote que inclui o ficheiro de configuração do Autopilot. Por predefinição, a sequência de tarefas reinicia o computador depois de ser executado Sysprep do Windows. Também pode selecionar a opção para **encerrar o computador após a conclusão desta sequência de tarefas**. Esta opção permite-lhe preparar um dispositivo e, em seguida, entregá-la a um utilizador para uma experiência consistente do Autopilot.  

9. Conclua o assistente.  

Se editar a sequência de tarefas, é semelhante à sequência de tarefas padrão para aplicar uma imagem de SO existente. Esta sequência de tarefas inclui os seguintes passos adicionais:  

- **Aplicar a configuração do Windows Autopilot**: Este passo aplica-se o ficheiro de configuração do Autopilot do pacote especificado. Não é um novo tipo de passo, ele tem um **executar linha de comandos** passo para copiar o ficheiro.  

- **Preparar Windows para captura**: Este passo executa o Sysprep do Windows e tem a definição para **encerrar o computador depois de executar esta ação**. Para obter mais informações, consulte [preparar Windows para captura](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareWindowsforCapture).  

O Windows Autopilot para dispositivos existentes tarefas resultados de sequência num dispositivo associado ao Azure Active Directory (Azure AD). 

Utilizar o OneDrive para empresas [mover pasta conhecida](https://docs.microsoft.com/onedrive/redirect-known-folders) para se certificar de que os dados do utilizador é uma cópia de segurança antes da atualização do Windows 10.



## <a name="next-steps"></a>Passos seguintes

Utilize a cogestão para melhorar as funcionalidades de gestão dos seus dispositivos Windows 10. O segundo caminho para a cogestão é através do aprovisionamento moderno com o Windows Autopilot. Para obter mais informações, veja os artigos seguintes:

- [O que é a cogestão?](/sccm/comanage/overview)
- [Caminhos de cogestão](/sccm/comanage/quickstart-paths)
- [Windows Autopilot com cogestão](/sccm/comanage/quickstart-autopilot)

