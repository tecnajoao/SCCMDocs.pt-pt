---
title: Configurar o cliente do Endpoint Protection | Documentos do Microsoft
description: "Saiba como configurar as definições de cliente personalizadas para o Endpoint Protection que podem ser implementados em coleções de computadores na sua hierarquia."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 017bd5b899b364fc832c721d63cc7dbad0a11671
ms.openlocfilehash: 1488aaa465fb9810bc1b641d41dad95189d37418
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---

# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Configurar definições de cliente personalizadas para o Endpoint Protection

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este procedimento configura as definições de cliente personalizadas para o Endpoint Protection que pode ser implementado para coleções de computadores na sua hierarquia.

> [!IMPORTANT]
>  Configure as predefinições de cliente do Endpoint Protection apenas se tiver a certeza de que pretende aplicá-las a todos os computadores na sua hierarquia.

## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>Para ativar o Endpoint Protection e configurar definições personalizadas de cliente

1.  Na consola do Configuration Manager, clique em **Administração**.

2.  Na área de trabalho **Administração** , clique em **Definições do Cliente**.

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Definições Personalizadas do Dispositivo Cliente**.

4.  Na caixa de diálogo **Criar Definições Personalizadas do Dispositivo Cliente** , forneça um nome e uma descrição para o grupo de definições e, em seguida, selecione **Endpoint Protection**.

5.  Configure as definições de cliente do Endpoint Protection que necessita. Para obter uma lista completa das definições de cliente do Endpoint Protection que pode configurar, consulte a secção de Endpoint Protection em [sobre definições de cliente no System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

   > [!IMPORTANT]
   >  Tem de instalar a função de sistema de sites do Endpoint Protection antes de poder configurar as definições de cliente do Endpoint Protection.

6.  Clique em **OK** para fechar a caixa de diálogo **Criar Definições Personalizadas do Dispositivo Cliente** . As novas definições de cliente são apresentadas no nó **Definições do Cliente** da área de trabalho **Administração** .

7.  Para que as definições personalizadas de cliente possam ser utilizadas, tem de implementá-las numa coleção. Selecione as definições personalizadas de cliente que pretende implementar e, em seguida, no separador **Home Page** , no grupo **Definições do Cliente** , clique em **Implementar**.

8.  Na caixa de diálogo **Selecionar Coleção** , escolha a coleção na qual pretende implementar as definições de cliente e, em seguida, clique em **OK**. A nova implementação é apresentada no separador **Implementações** do painel de detalhes.

Os computadores cliente serão configurados com estas definições na próxima vez que transferirem a política de cliente. Para iniciar a obtenção de política para um único cliente, consulte a política de iniciar a obtenção de uma secção de cliente do Configuration Manager no [como gerir clientes no System Center Configuration Manager](../../core/clients/manage/manage-clients.md).

## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image-in-configuration-manager"></a>Como aprovisionar o cliente do Endpoint Protection numa imagem de disco no Configuration Manager
Pode instalar o cliente do Endpoint Protection num computador que pretende utilizar como origem de imagem de disco para a implementação do sistema operativo do Configuration Manager. Este computador é normalmente designado computador de referência. Depois de criar a imagem do sistema operativo, pode utilizar, em seguida, implementação do sistema operativo do Configuration Manager para implementar a imagem que contém pacotes de software, incluindo Endpoint Protection, para os computadores cliente.

Utilize os procedimentos deste tópico para o ajudar a instalar e configurar o cliente do Endpoint Protection num computador de referência

### <a name="prerequisites-for-installing-the-endpoint-protection-client-on-the-reference-computer"></a>Pré-requisitos para Instalar o Cliente do Endpoint Protection no Computador de Referência
A lista seguinte contém os pré-requisitos necessários para instalar o software de cliente do Endpoint Protection num computador de referência.

-   Tem de ter acesso ao pacote de instalação do cliente do Endpoint Protection, **scepinstall.exe**. Este pacote encontra-se no **cliente** pasta da pasta de instalação do Microsoft System Center Configuration Manager no servidor do site.

-   Para certificar-se de que o Endpoint Protection cliente é implementado com a configuração que é necessária na sua organização, crie uma política antimalware e exporte essa política. Em seguida, pode especificar a política antimalware a utilizar quando instalar manualmente o cliente do Endpoint Protection. Para obter mais informações, consulte o artigo [como criar e implementar políticas de proteção contra software maligno do Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).

   > [!NOTE]
   >  Não é possível exportar a **Política Antimalware do Cliente Predefinida** .

-   Se pretender instalar o cliente do Endpoint Protection com as definições mais recentes, tem de transferi-las do [Microsoft Malware Protection Center](http://go.microsoft.com/fwlink/?LinkID=200965).

### <a name="how-to-install-the-endpoint-protection-client-software-on-the-reference-computer"></a>Como Instalar o Software de Cliente do Endpoint Protection no Computador de Referência
É possível instalar o cliente do Endpoint Protection localmente no computador de referência a partir de uma linha de comandos. Para tal, é necessário obter primeiro o ficheiro de instalação **scepinstall.exe**. Também é possível instalar o cliente com uma política antimalware pré-configurada ou com uma política antimalware que tenha sido exportada anteriormente.

## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a>Para instalar o cliente do Endpoint Protection a partir de uma linha de comandos

1.  Copiar **scepinstall.exe** a partir de **cliente** pasta no suporte de instalação do System Center Configuration Manager para o computador no qual pretende instalar o software de cliente do Endpoint Protection.

2.  Abra uma linha de comandos com privilégios de administrador, navegue para a página onde se encontra o ficheiro **scepinstall.exe** e execute o comando seguinte, acrescentando as propriedades adicionais de linha de comandos que forem necessárias:

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
   >  Depois de concluída a instalação de cliente do Endpoint Protection, o cliente efetua automaticamente uma verificação de atualização de definição. Se esta verificação da atualização tiver êxito, não é necessário instalar manualmente o pacote de atualização de definição mais recente.

## <a name="to-install-the-client-software-with-an-antimalware-policy-from-the-command-prompt"></a>Para instalar o software de cliente com uma política antimalware a partir da linha de comandos

1.  Copiar **scepinstall.exe** e a política antimalware exportada ou pré-configurada para o computador no qual pretende instalar o software de cliente do Endpoint Protection.

2.  Abra uma linha de comandos com privilégios de administrador, navegue para a pasta onde se encontram o ficheiro **scepinstall.exe** e a política antimalware e execute o comando seguinte:

   ```
   scepinstall.exe /policy <full path>\<policy file>
   ```

3.  Siga as instruções no ecrã para concluir a instalação do cliente.

4.  Se tiver transferido o pacote de definição mais recente, copie o pacote para o computador cliente e, em seguida, faça duplo clique no pacote de definição para o instalar.

   > [!NOTE]
   >  Depois de concluída a instalação de cliente do Endpoint Protection, o cliente efetua automaticamente uma verificação de atualização de definição. Se esta verificação da atualização tiver êxito, não é necessário instalar manualmente o pacote de atualização de definição mais recente.

## <a name="verify-that-the-endpoint-protection-client-is-installed-correctly"></a>Verificar se o Cliente do Endpoint Protection está Instalado Corretamente
Depois de instalar o cliente do Endpoint Protection no computador de referência, certifique-se de que o cliente está a funcionar corretamente.

### <a name="to-verify-that-the-endpoint-protection-client-is-installed-correctly"></a>Para verificar se o cliente do Endpoint Protection está instalado corretamente

1.  No computador de referência, abra **System Center Endpoint Protection** do Windows são a notificação.

2.  No **base** separador do **System Center Endpoint Protection** diálogo caixa, certifique-se de que **proteção em tempo real** está definido como **no**.

3.  Verifique se é apresentada a indicação **Atualizado** para **Definições de vírus e spyware**.

4.  Para ajudar a garantir que o computador de referência está pronto para criação de imagens, em **Opções de análise**, selecione **Completa**e clique em **Analisar agora**.

### <a name="how-to-prepare-the-endpoint-protection-client-for-imaging"></a>Como Preparar o Cliente do Endpoint Protection para Criação de Imagens
Depois de verificar que o cliente do Endpoint Protection está instalado corretamente no computador de referência, pode preparar o computador para criação de imagens. Execute os seguintes passos para preparar o cliente do Endpoint Protection para criação de imagens.


Para obter mais informações sobre a implementação do sistema operativo no Configuration Manager, consulte o artigo [gerir imagens do sistema operativo com o System Center Configuration Manager](/sccm/osd/get-started/manage-operating-system-images).

### <a name="to-prepare-the-endpoint-protection-client-for-imaging"></a>Para preparar o cliente do Endpoint Protection para criação de imagens

1.  No computador de referência, inicie sessão como utilizador com privilégios administrativos.

2.  Transfira e instale **PsTools** a partir do [Site do Windows SysInternals](http://go.microsoft.com/fwlink/?LinkId=215263) na TechNet.

3.  Abra uma linha de comandos elevada, navegue para a pasta onde instalou PsTools e, em seguida, escreva o seguinte comando

   ```
   Psexec.exe -s -i regedit.exe
   ```

   > [!IMPORTANT]
   >  Tenha cuidado enquanto estiver a executar o Editor de registo desta forma; a opção – s no PsExec.exe executa o Editor de registo com privilégios LocalSystem.

4.  No Editor de Registo, navegue para cada uma das seguintes chaves de registo e elimine-as.

   > [!IMPORTANT]
   >  Tem de eliminar as chaves de registo como último passo antes de criar a imagem do computador de referência. As chaves de registo são recriadas quando o cliente do Endpoint Protection é iniciado. Se reiniciar o computador de referência, tem de eliminar as chaves de registo novamente.

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID**

Depois de concluir os passos anteriores, pode preparar o computador de referência para criação de imagens. Para obter mais informações sobre a implementação do sistema operativo no Configuration Manager, consulte o artigo [gerir imagens do sistema operativo com o System Center Configuration Manager](/sccm/osd/get-started/manage-operating-system-images).

Quando uma imagem que contenha o software de cliente do Endpoint Protection é implementada, o cliente do Endpoint Protection irá reportar automaticamente informações para o site do Configuration Manager para que o computador está atribuído e política aplicável ao computador cliente é transferida e aplicada.
