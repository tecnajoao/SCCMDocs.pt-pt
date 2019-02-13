---
title: Configurar o Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como configurar as definições de cliente personalizadas para o Endpoint Protection.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6669ad415b3c39c805989fd056b68ce7d3bcb24b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126621"
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Configurar definições de cliente personalizadas para o Endpoint Protection

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este procedimento configura as definições personalizadas de cliente do Endpoint Protection, que pode implementar em coleções de dispositivos na sua hierarquia.

> [!IMPORTANT]  
>  Só deve configure as predefinições de cliente do Endpoint Protection se tiver a certeza de que pretende aplicá-las a todos os computadores na sua hierarquia. 



## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>Para ativar o Endpoint Protection e configurar definições personalizadas de cliente

1. Na consola do Configuration Manager, clique em **Administração**.  

2. Na área de trabalho **Administração** , clique em **Definições do Cliente**.  

3. No separador **Home Page** , no grupo **Criar** , clique em **Criar Definições Personalizadas do Dispositivo Cliente**.  

4. Na caixa de diálogo **Criar Definições Personalizadas do Dispositivo Cliente** , forneça um nome e uma descrição para o grupo de definições e, em seguida, selecione **Endpoint Protection**.  

5. Configure as definições de cliente do Endpoint Protection que necessita. Para obter uma lista completa das definições de cliente do Endpoint Protection que pode configurar, consulte a secção Endpoint Protection [sobre as definições de cliente](/sccm/core/clients/deploy/about-client-settings#endpoint-protection).  

   > [!IMPORTANT]  
   >  Instale a função de sistema de sites do Endpoint Protection antes de configurar as definições de cliente do Endpoint Protection.  

6. Clique em **OK** para fechar a caixa de diálogo **Criar Definições Personalizadas do Dispositivo Cliente** . As novas definições de cliente são apresentadas no nó **Definições do Cliente** da área de trabalho **Administração** .  

7. Em seguida, implemente as definições de cliente personalizadas numa coleção. Selecione as definições de cliente personalizadas que pretende implementar. Na **home page** separador a **definições de cliente** , clique em **implementar**.  

8. Na caixa de diálogo **Selecionar Coleção** , escolha a coleção na qual pretende implementar as definições de cliente e, em seguida, clique em **OK**. A nova implementação é apresentada no separador **Implementações** do painel de detalhes.  

Os clientes são configurados com estas definições, quando a próxima vez que transferirem a política de cliente. Para obter mais informações, consulte [iniciar a obtenção de política para um cliente do Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  



## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image"></a>Como aprovisionar o cliente do Endpoint Protection numa imagem de disco

Instale o cliente do Endpoint Protection num computador que pretende utilizar como uma origem de imagem de disco para a implementação de SO do Configuration Manager. Este computador é normalmente designado computador de referência. Depois de criar a imagem do SO, em seguida, utilize a implementação do SO do Configuration Manager para implementar a imagem.

> [!Important]  
> Windows 10 e Windows Server 2016 têm o Windows Defender instalado por predefinição. Não é preciso este procedimento por essas versões do Windows.  

Utilize os procedimentos seguintes para o ajudar a instalar e configurar o cliente do Endpoint Protection no computador de referência.


### <a name="prerequisites"></a>Pré-requisitos

A lista seguinte contém os pré-requisitos necessários para instalar o software de cliente do Endpoint Protection num computador de referência.

- Tem de ter acesso para o pacote de instalação de cliente do Endpoint Protection, **scepinstall.exe**. Encontrar este pacote na **cliente** pasta da pasta de instalação do Configuration Manager no servidor do site.  

- Para implementar o cliente do Endpoint Protection com a configuração necessária da sua organização, criar e exportar uma política antimalware. Em seguida, especifique esta política, quando instala manualmente o cliente do Endpoint Protection. Para obter mais informações, consulte [como criar e implementar políticas antimalware](/sccm/protect/deploy-use/endpoint-antimalware-policies).  

  > [!NOTE]  
  >  Não é possível exportar a **política Antimalware do cliente predefinida**.  

- Se pretender instalar o cliente do Endpoint Protection com as definições mais recentes, baixá-los em [inteligência de segurança do Windows Defender](https://www.microsoft.com/wdsi).  

> [!NOTE]  
> A partir do Configuration Manager 1802, não precisa de instalar o agente de proteção de ponto final (SCEPInstall) em dispositivos Windows 10. Se já estiver instalado em dispositivos Windows 10, o Configuration Manager não removê-lo. Os administradores podem remover o agente do Endpoint Protection em dispositivos Windows 10 que estejam a executar, pelo menos, a versão 1802 do cliente. SCEPInstall.exe ainda podem estar presentes no C:\Windows\ccmsetup em algumas máquinas, mas novas instalações de cliente não devem baixá-lo. <!--503654-->


### <a name="how-to-install-the-endpoint-protection-client-on-the-reference-computer"></a>Como instalar o cliente do Endpoint Protection no computador de referência

Instale o cliente do Endpoint Protection localmente no computador de referência de um prompt de comando. Primeiro, obtenha o ficheiro de instalação **scepinstall.exe**. Para obter mais informações, consulte [instalar o cliente do Endpoint Protection a partir de um prompt de comando](#bkmk_manual-install).

Se necessário, também incluem uma política antimalware pré-configurada ou com uma política antimalware que exportou anteriormente. 



## <a name="bkmk_manual-install"></a> Para instalar o cliente do Endpoint Protection a partir de um prompt de comando

1. Cópia **scepinstall.exe** partir do **cliente** pasta da pasta de instalação do Configuration Manager para o computador no qual pretende instalar o software de cliente do Endpoint Protection.  

2. Abra uma linha de comandos como administrador. Altere o diretório para a pasta com o instalador. Em seguida, execute `scepinstall.exe`, acrescentando as propriedades da linha de comandos adicionais, que necessita:


   |  Propriedade   |                                  Descrição                                   |
   |-------------|--------------------------------------------------------------------------------|
   |    `/s`     |                           Execute o instalador silenciosamente                           |
   |    `/q`     |                        Extraia os ficheiros de instalação silenciosa                        |
   |    `/i`     |                           Execute o instalador normalmente                           |
   |  `/policy`  | Especifique um ficheiro de política antimalware para configurar o cliente durante a instalação |
   | `/sqmoptin` |     Inscreva-se no programa de melhoramento da experiência do cliente da Microsoft (CEIP)     |


3. Siga na tela instruções para concluir a instalação do cliente.  

4. Se tiver transferido o pacote de definição de atualização mais recente, copie o pacote para o computador cliente e, em seguida, faça duplo clique no pacote de definição para o instalar.  

   > [!NOTE]  
   >  Depois de concluída a instalação de cliente do Endpoint Protection, o cliente efetua automaticamente uma verificação de atualização de definição. Se esta verificação de atualização for concluída com êxito, não tem de instalar manualmente o pacote de atualização de definição mais recente.  

#### <a name="example-install-the-client-with-an-antimalware-policy"></a>Exemplo: instalar o cliente com uma política antimalware

`scepinstall.exe /policy <full path>\<policy file>`



## <a name="verify-the-endpoint-protection-client-installation"></a>Verificar a instalação de cliente do Endpoint Protection

Depois de instalar o cliente do Endpoint Protection no seu computador de referência, certifique-se de que o cliente está a funcionar corretamente.

1.  No computador de referência, abra **System Center Endpoint Protection** partir da área de notificação do Windows.  

2.  No **home page** separador da **System Center Endpoint Protection** caixa de diálogo caixa, verifique se **proteção em tempo real** está definido como **no**.  

3.  Certifique-se de que **atualizados** é apresentado para **definições de vírus e spyware**.  

4.  Para se certificar de que o computador de referência está pronto para criação de imagens, em **opções de análise**, selecione **completo**e, em seguida, clique em **analisar agora**.  



## <a name="prepare-the-endpoint-protection-client-for-imaging"></a>Preparar o cliente do Endpoint Protection para criação de imagens

Execute os seguintes passos para preparar o cliente do Endpoint Protection para criação de imagens:

1. No computador de referência, inicie sessão como administrador.  

2. Transfira e instale **PsExec** partir [Windows SysInternals](https://docs.microsoft.com/sysinternals/downloads/psexec).  

3. Executar uma linha de comandos como administrador, altere o diretório para a pasta onde instalou PsTools e, em seguida, escreva o seguinte comando:  

   `psexec.exe -s -i regedit.exe`  

   > [!IMPORTANT]  
   >  Tenha cuidado ao executar o Editor de registo dessa maneira. PsExec.exe executa-o no contexto LocalSystem.  

4. No Editor de registo, elimine as seguintes chaves do registo:  

   > [!IMPORTANT]  
   >  Elimine essas chaves de Registro como o último passo antes do computador de referência de geração de imagens. O cliente do Endpoint Protection recria essas chaves durante o arranque. Se reiniciar o computador de referência, elimine as chaves de registo novamente.  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID`   

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID`

Agora, está pronto para preparar o computador de referência para criação de imagens.

Quando implementa uma imagem de SO que contém o cliente do Endpoint Protection,-lo automaticamente relatórios de informações para o site do Configuration Manager atribuído do dispositivo. O cliente transfere e aplica-se qualquer política de antimalware de destino.  



## <a name="see-also"></a>Consulte também

Para obter mais informações sobre a implementação do sistema operacional no Configuration Manager, consulte [imagens do sistema operacional de gerir](/sccm/osd/get-started/manage-operating-system-images).

