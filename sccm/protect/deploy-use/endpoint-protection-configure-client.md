---
title: Configurar o cliente do Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como configurar as definições de cliente personalizadas para o Endpoint Protection, que podem ser implementadas em coleções de computadores na sua hierarquia.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 10572c367dcdc70bf9c708d3a6bb514c0afa2b24
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Configurar definições personalizadas de cliente do Endpoint Protection

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este procedimento configura as definições personalizadas de cliente do Endpoint Protection, que podem ser implementadas em coleções de computadores na sua hierarquia.

> [!IMPORTANT]
>  Apenas de configurar as predefinições de cliente do Endpoint Protection se tiver a certeza de que pretende aplicá-las a todos os computadores na sua hierarquia. 

## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>Para ativar o Endpoint Protection e configurar definições personalizadas de cliente

1.  Na consola do Configuration Manager, clique em **Administração**.

2.  Na área de trabalho **Administração** , clique em **Definições do Cliente**.

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Definições Personalizadas do Dispositivo Cliente**.

4.  Na caixa de diálogo **Criar Definições Personalizadas do Dispositivo Cliente** , forneça um nome e uma descrição para o grupo de definições e, em seguida, selecione **Endpoint Protection**.

5.  Configure as definições de cliente do Endpoint Protection que precisa. Para obter uma lista completa das definições de cliente do Endpoint Protection que pode configurar, consulte a secção de Endpoint Protection em [sobre definições de cliente no System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

   > [!IMPORTANT]
   >  Tem de instalar a função de sistema de sites do Endpoint Protection antes de poder configurar as definições de cliente do Endpoint Protection.

6.  Clique em **OK** para fechar a caixa de diálogo **Criar Definições Personalizadas do Dispositivo Cliente** . As novas definições de cliente são apresentadas no nó **Definições do Cliente** da área de trabalho **Administração** .

7.  Para que as definições personalizadas de cliente possam ser utilizadas, tem de implementá-las numa coleção. Selecione as definições personalizadas de cliente que pretende implementar e, em seguida, no separador **Home Page** , no grupo **Definições do Cliente** , clique em **Implementar**.

8.  Na caixa de diálogo **Selecionar Coleção** , escolha a coleção na qual pretende implementar as definições de cliente e, em seguida, clique em **OK**. A nova implementação é apresentada no separador **Implementações** do painel de detalhes.

Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a obtenção da política para um único cliente, consulte a obtenção de política Iniciar com uma secção de cliente do Configuration Manager no [como gerir clientes no System Center Configuration Manager](../../core/clients/manage/manage-clients.md).

## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image-in-configuration-manager"></a>Como aprovisionar o cliente do Endpoint Protection numa imagem de disco no Configuration Manager
Pode instalar o cliente do Endpoint Protection num computador que pretende utilizar como origem da imagem de disco para a implementação do sistema operativo do Configuration Manager. Este computador é normalmente designado computador de referência. Depois de criar a imagem do sistema operativo, em seguida, pode utilizar a implementação de sistema operativo do Configuration Manager para implementar a imagem que contém pacotes de software, incluindo o Endpoint Protection, para os computadores cliente.

Utilize os procedimentos neste artigo para o ajudar a instalar e configurar o cliente do Endpoint Protection num computador de referência

### <a name="prerequisites-for-installing-the-endpoint-protection-client-on-the-reference-computer"></a>Pré-requisitos para Instalar o Cliente do Endpoint Protection no Computador de Referência
A lista seguinte contém os pré-requisitos necessários para instalar o software de cliente do Endpoint Protection num computador de referência.

-   Tem de ter acesso ao pacote de instalação do cliente de Endpoint Protection, **scepinstall.exe**. Este pacote pode ser encontrado no **cliente** pasta da pasta de instalação do Microsoft System Center Configuration Manager no servidor do site. Windows 10 e Windows Server 2016 tem o Windows Defender instalado. 

-   Para se certificar de que o Endpoint Protection cliente é implementado com a configuração que é necessária na sua organização, crie uma política antimalware e exporte essa política. Em seguida, pode especificar a política antimalware a utilizar quando instalar manualmente o cliente do Endpoint Protection. Para obter mais informações, consulte [como criar e implementar políticas antimalware do Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).

   > [!NOTE]
   >  O **política Antimalware do cliente predefinida** não pode ser exportado.

-   Se pretender instalar o cliente do Endpoint Protection com as definições mais recentes, tem de transferi-las do [Microsoft Malware Protection Center](http://go.microsoft.com/fwlink/?LinkID=200965).

>[!NOTE]
> A partir do Configuration Manager 1802, dispositivos Windows 10 não é necessário ter o agente do Endpoint Protection (SCEPInstall) instalado. Se já estiver instalado em dispositivos Windows 10, o Configuration Manager não removê-lo. Os administradores podem remover o agente do Endpoint Protection em dispositivos Windows 10 que estejam a executar, pelo menos, a versão do cliente 1802. SCEPInstall.exe ainda pode estar presente nos C:\Windows\ccmsetup algumas máquinas, mas não deve ser transferido em novas instalações de cliente. <!--503654-->
### <a name="how-to-install-the-endpoint-protection-client-software-on-the-reference-computer"></a>Como Instalar o Software de Cliente do Endpoint Protection no Computador de Referência
Pode instalar o cliente do Endpoint Protection localmente no computador de referência de uma linha de comandos. Para tal, é necessário obter primeiro o ficheiro de instalação **scepinstall.exe**. Também pode instalar o cliente com uma política antimalware pré-configurada ou com uma política antimalware que exportou anteriormente.

## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a>Para instalar o cliente do Endpoint Protection a partir de uma linha de comandos

1.  Cópia **scepinstall.exe** do **cliente** pasta no suporte de instalação do System Center Configuration Manager para o computador no qual pretende instalar o software de cliente do Endpoint Protection.

2.  Abra uma linha de comandos com privilégios de administrador, navegue para a pasta onde **scepinstall.exe** está localizado e, em seguida, execute o comando seguinte, acrescentando as propriedades da linha de comandos adicionais que necessita:

   ```
   scepinstall.exe
   ```

    Pode especificar uma das seguintes propriedades de linha de comandos:

   |Propriedade|Descrição|
   |--------------|-----------------|
   |/s|Especifica que irá ser efetuada uma instalação silenciosa.|
   |/q|Especifica que irá ser efetuada uma extração silenciosa dos ficheiros de configuração.|
   |/i|Especifica que deve ser efetuada uma instalação normal.|
   |/noreplace|Especifica que o software antimalware de outro fabricante não foi desinstalado durante a configuração.|
   |/policy|Especifica um ficheiro de política antimalware a utilizar para configurar o cliente durante a instalação.|
   |/sqmoptin|Especifica que esta instalação de software de cliente foi incluída no Programa de Melhoramento da Experiência do Cliente da Microsoft.|

3.  Siga as instruções no ecrã para concluir a instalação do cliente.

4.  Se tiver transferido o pacote de definição de atualização mais recente, copie o pacote para o computador cliente e, em seguida, faça duplo clique no pacote de definição para o instalar.

   > [!NOTE]
   >  Uma vez concluída a instalação de cliente do Endpoint Protection, o cliente efetua automaticamente uma verificação de atualização de definição. Se esta verificação de atualização tiver êxito, não tem de instalar manualmente o pacote de atualização de definição mais recente.

## <a name="to-install-the-client-software-with-an-antimalware-policy-from-the-command-prompt"></a>Para instalar o software de cliente com uma política antimalware a partir da linha de comandos

1.  Cópia **scepinstall.exe** e a política antimalware exportada ou pré-configurada para o computador no qual pretende instalar o software de cliente do Endpoint Protection.

2.  Abra uma linha de comandos com privilégios de administrador, navegue para a pasta onde se encontram o ficheiro **scepinstall.exe** e a política antimalware e execute o comando seguinte:

   ```
   scepinstall.exe /policy <full path>\<policy file>
   ```

3.  Siga as instruções no ecrã para concluir a instalação do cliente.

4.  Se tiver transferido o pacote de definição mais recente, copie o pacote para o computador cliente e, em seguida, faça duplo clique no pacote de definição para o instalar.

   > [!NOTE]
   >  Uma vez concluída a instalação de cliente do Endpoint Protection, o cliente efetua automaticamente uma verificação de atualização de definição. Se esta verificação de atualização tiver êxito, não tem de instalar manualmente o pacote de atualização de definição mais recente.

## <a name="verify-that-the-endpoint-protection-client-is-installed-correctly"></a>Verificar se o Cliente do Endpoint Protection está Instalado Corretamente
Depois de instalar o cliente do Endpoint Protection no computador de referência, certifique-se de que o cliente está a funcionar corretamente.

### <a name="to-verify-that-the-endpoint-protection-client-is-installed-correctly"></a>Para verificar se o cliente do Endpoint Protection está instalado corretamente

1.  No computador de referência, abra **System Center Endpoint Protection** da área de notificação do Windows.

2.  No **home page** separador do **System Center Endpoint Protection** diálogo caixa, certifique-se de que **proteção em tempo real** está definido como **no**.

3.  Certifique-se de que **atualizados** é apresentada para **definições de vírus e spyware**.

4.  Para ajudar a garantir que o computador de referência está pronto para criação de imagens, em **Opções de análise**, selecione **Completa**e clique em **Analisar agora**.

### <a name="how-to-prepare-the-endpoint-protection-client-for-imaging"></a>Como Preparar o Cliente do Endpoint Protection para Criação de Imagens
Depois de verificar que o cliente do Endpoint Protection está corretamente instalado no computador de referência, pode preparar o computador para criação de imagens. Execute os seguintes passos para preparar o cliente do Endpoint Protection para criação de imagens.


Para obter mais informações sobre a implementação do sistema operativo no Configuration Manager, consulte [gerir imagens do sistema operativo com o System Center Configuration Manager](/sccm/osd/get-started/manage-operating-system-images).

### <a name="to-prepare-the-endpoint-protection-client-for-imaging"></a>Para preparar o cliente do Endpoint Protection para criação de imagens

1.  No computador de referência, inicie sessão como utilizador com privilégios administrativos.

2.  Transfira e instale **PsTools** a partir do [Site do Windows SysInternals](http://go.microsoft.com/fwlink/?LinkId=215263) na TechNet.

3.  Abra uma linha de comandos elevada, navegue para a pasta onde instalou PsTools e, em seguida, escreva o seguinte comando

   ```
   Psexec.exe -s -i regedit.exe
   ```

   > [!IMPORTANT]
   >  Tenha cuidado enquanto estiver a executar o Editor de registo desta forma; a opção -s no PsExec.exe executa o Editor de registo com privilégios LocalSystem.

4.  No Editor de Registo, navegue para cada uma das seguintes chaves de registo e elimine-as.

   > [!IMPORTANT]
   >  Tem de eliminar as chaves de registo como último passo antes de criar a imagem do computador de referência. As chaves de registo são recriadas quando o cliente do Endpoint Protection é iniciado. Se reiniciar o computador de referência, tem de eliminar as chaves de registo novamente.

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID**

Depois de concluir os passos anteriores, pode preparar o computador de referência para criação de imagens. Para obter mais informações sobre a implementação do sistema operativo no Configuration Manager, consulte [gerir imagens do sistema operativo com o System Center Configuration Manager](/sccm/osd/get-started/manage-operating-system-images).

Quando uma imagem que contém o software de cliente do Endpoint Protection é implementada, o cliente do Endpoint Protection irá reportar automaticamente informações ao site do Configuration Manager para que o computador está atribuído e política aplicável ao computador cliente será transferida e aplicada.
