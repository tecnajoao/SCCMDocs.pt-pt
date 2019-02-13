---
title: Atualizar dispositivos Windows para uma versão diferente
titleSuffix: Configuration Manager
description: Atualize automaticamente dispositivos que executem o ambiente de trabalho do Windows 10 ou Windows 10 Mobile para uma edição diferente com o Configuration Manager.
ms.date: 01/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3cda70e7a5f1b2cf7dec079a7e933af48f0bf8ad
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128403"
---
# <a name="upgrade-windows-devices-with-the-edition-upgrade-policy-in-system-center-configuration-manager"></a>Atualizar dispositivos Windows com a política de atualização de edição no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


O **política de atualização de edição** permite-lhe atualizar automaticamente dispositivos que executam uma das seguintes versões do Windows 10 para uma edição diferente:

- Windows 10 Desktop
- Windows 10 Mobile

Os seguintes caminhos de atualização são suportados:

- Do Windows 10 Pro para Windows 10 Enterprise
- Do Windows 10 Home para Windows 10 Education
- Do Windows 10 Mobile para do Windows 10 Mobile Enterprise

Os dispositivos tem de ser inscritos no Microsoft Intune ou executar o software de cliente do Configuration Manager. Esta política não é atualmente compatível com PCs que sejam geridos por MDM no local.

## <a name="before-you-start"></a>Antes de começar  
 Antes de começar a atualizar dispositivos para a versão mais recente, consulte os seguintes pré-requisitos:  

-   Para edições para desktop do Windows 10: Uma chave de produto válida para a nova versão do Windows em todos os dispositivos que segmentar com a política. Esta chave de produto pode ser uma chave de ativação múltipla (MAK) ou um volume genérico (GVLK) de chave de licenciamento. Uma GVLK é também referida como uma chave de configuração de cliente do gerenciamento de chaves (KMS serviço). Para obter mais informações, consulte [plano para ativação de volume](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Para obter uma lista de chaves de configuração de cliente KMS, consulte [apêndice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) do guia de ativação do Windows Server. <!--496871-->  

-   Para Windows 10 Mobile: Um ficheiro de licença de XML da Microsoft Volume Licensing Service Center (VLSC). Este ficheiro contém as informações de licenciamento para a nova versão do Windows em todos os dispositivos visados pela política.

- Para gerir este tipo de política, tem de ser no Configuration Manager **administrador total** função de segurança.

## <a name="configure-the-edition-upgrade-policy"></a>Configurar a política de atualização de edição  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **atualização de edição do Windows 10**.  

3.  No separador **Início** , no grupo **Criar** , clique em **Criar Política de Atualização de Edição**.  

4.  Clique em **Criar Política**.  

5.  Na página **Geral** do **Assistente para Criar Política de Atualização de Edição**, especifique as seguintes informações:  

    -   **Nome** -introduza um nome para a política de atualização de edição  

    -   **Descrição** (opcional) - opcionalmente, introduza uma descrição para a política que o ajuda a identificá-lo na consola do Intune  

    -   **SKU para atualizar dispositivo para** – na lista pendente, selecione a edição de destino do ambiente de trabalho do Windows 10 ou Windows 10 Mobile  

    -   **Informações de licenciamento** - selecione um dos seguintes:  

        -   **Chave de produto** -introduza uma chave de produto válida para a edição de área de trabalho de destino com o Windows 10  

            > [!NOTE]  
            >  Depois de criar uma política que contém uma chave de produto, já não será possível editar a chave de produto. O Configuration Manager obscurecem a chave por motivos de segurança. Para alterar a chave de produto, tem de introduzir novamente a chave completa.  

        -   **Ficheiro de licença** -clique em **procurar** para selecionar um ficheiro de licenciamento válido no formato XML. O Configuration Manager utiliza este ficheiro de licença para atualizar dispositivos Windows 10 Mobile.  

6.  Conclua o assistente.  


## <a name="deploy-the-edition-upgrade-policy"></a>Implementar a política de atualização de edição  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **atualização de edição do Windows 10**.  

3.  Selecione a política de atualização de edição do Windows 10 que pretende implementar e, em seguida, no separador **Início** no grupo **Implementação** , clique em **Implementar**.  

4.  Na **implementar a atualização da edição do 10 de Windows** diálogo caixa, primeiro selecione a coleção à qual pretende implementar a política. Selecione o agendamento através do qual o cliente avalia a política e, em seguida, clique em **OK**. Para PCs geridos com o cliente do Configuration Manager, tem de implementar a política para uma coleção de dispositivos. Para PCs que estão inscritos com o Intune, pode implementar a política a um utilizador ou a coleção de dispositivos. 



## <a name="next-steps"></a>Passos seguintes

Monitorizar esta implementação a partir da **implementações** nó da **monitorização** área de trabalho. Se vir erros que indicam um implementação concluído com êxito, por exemplo:
- **Não aplicável para este dispositivo**
- **Falha na conversão de tipo de dados**

Estes erros não significam que a implementação falhou. Verifique, no PC de destino, o que a atualização efetuada com êxito.

Assim que o cliente avalia a política de destino, ele será reiniciado dentro de duas horas para aplicar a atualização. Certifique-se de informar os utilizadores nos quais implementou a política ou agendar a política para executar os usuários fora do horário de trabalho.

Se o seguinte erro for apresentado na **Dcmwmiprovider** no cliente, verifique que está a utilizar a chave adequada para o seu cenário de ativação. Para obter mais informações, consulte a [antes de começar](#before-you-start) secção. Se estiver a utilizar um serviço de gestão de chaves para ativação, certifique-se utilizar um [chave de configuração de cliente KMS](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys).  <!-- 496871 -->   

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`
