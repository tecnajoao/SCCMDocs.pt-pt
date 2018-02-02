---
title: "Atualizar dispositivos Windows para uma versão diferente"
titleSuffix: Configuration Manager
description: "Atualize automaticamente os dispositivos que executem o ambiente de trabalho do Windows 10 ou Windows 10 Mobile para uma edição diferente com o Configuration Manager."
ms.custom: na
ms.date: 01/26/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
caps.latest.revision: 
caps.handback.revision: 
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95e3385ad9bca9c87e48d731ffeebfa387fece65
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/01/2018
---
# <a name="upgrade-windows-devices-with-the-edition-upgrade-policy-in-system-center-configuration-manager"></a>Atualizar dispositivos Windows com a política de atualização de edição no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


O **política de atualização de edição** permite-lhe atualizar automaticamente os dispositivos que executam uma das seguintes versões do Windows 10 para uma edição diferente:

- Windows 10 Desktop
- Windows 10 Mobile

São suportados os seguintes caminhos de atualização:

- A partir do Windows 10 Pro para Windows 10 Enterprise
- Na home page do Windows 10 para Windows 10 Education
- Do Windows 10 Mobile para Windows 10 Enterprise móveis

Os dispositivos tem de ser inscritos no Microsoft Intune ou executar o software de cliente do Configuration Manager. Esta política não é atualmente compatível com computadores que são geridos pela MDM no local.

## <a name="before-you-start"></a>Antes de começar  
 Antes de começar a atualizar dispositivos para a versão mais recente, reveja os seguintes pré-requisitos:  

-   Para ambientes de trabalho edições do Windows 10: Uma chave de produto válida para a nova versão do Windows em todos os dispositivos de destino com a política. Esta chave de produto pode ser uma chave de ativação múltipla (MAK) ou um volume genérico (GVLK) de chave de licenciamento. Uma GVLK é também referida como uma chave de configuração de cliente de serviço (KMS) de gestão de chaves. Para obter mais informações, consulte [plano para ativação de volume](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Para obter uma lista de chaves de configuração de cliente KMS, consulte [anexo A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) do guia de ativação do Windows Server. <!--496871-->  

-   Para Windows 10 Mobile: Um ficheiro de licença do XML da Microsoft Volume Licensing Service Center (VLSC). Este ficheiro contém as informações de licenciamento para a nova versão do Windows em todos os dispositivos de destino com a política.

- Para gerir este tipo de política, tem de ser o Configuration Manager **administrador total** função de segurança.

## <a name="configure-the-edition-upgrade-policy"></a>Configurar a política de atualização de edição  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **as definições de compatibilidade** > **atualização de edição do Windows 10**.  

3.  No separador **Início** , no grupo **Criar** , clique em **Criar Política de Atualização de Edição**.  

4.  Clique em **Criar Política**.  

5.  Na página **Geral** do **Assistente para Criar Política de Atualização de Edição**, especifique as seguintes informações:  

    -   **Nome** -introduza um nome para a política de atualização de edição  

    -   **Descrição** (opcional) - opcionalmente, introduza uma descrição para a política que o ajudem a identificá-la na consola do Intune  

    -   **SKU para atualizar dispositivo para** – na lista pendente, selecione a edição de destino do ambiente de trabalho do Windows 10 ou Windows 10 Mobile  

    -   **Informações de licenciamento** - selecione um dos seguintes:  

        -   **Chave de produto** -introduza uma chave de produto válida para a edição de ambiente de trabalho de destino. o Windows 10  

            > [!NOTE]  
            >  Depois de criar uma política que contém uma chave de produto, já não será possível editar a chave de produto. O Configuration Manager obscures a chave por motivos de segurança. Para alterar a chave de produto, tem de introduzir novamente a chave completa.  

        -   **Ficheiro de licenciamento** -clique em **procurar** para selecionar um ficheiro de licenciamento válido no formato XML. O Configuration Manager utiliza este ficheiro de licença para atualizar os dispositivos Windows 10 Mobile.  

6.  Conclua o assistente.  


## <a name="deploy-the-edition-upgrade-policy"></a>Implementar a política de atualização de edição  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **as definições de compatibilidade** > **atualização de edição do Windows 10**.  

3.  Selecione a política de atualização de edição do Windows 10 que pretende implementar e, em seguida, no separador **Início** no grupo **Implementação** , clique em **Implementar**.  

4.  No **implementar o Windows 10 de atualização de edição** diálogo caixa, primeiro selecione a coleção à qual pretende implementar a política. Selecione o agendamento através do qual o cliente avalia a política e, em seguida, clique em **OK**. Para PCs geridos com o cliente do Configuration Manager, tem de implementar a política para uma coleção de dispositivos. Para PCs que estão inscritos no Intune, pode implementar a política a um utilizador ou uma coleção de dispositivos. 



## <a name="next-steps"></a>Passos seguintes

Monitorizar esta implementação a partir de **implementações** nó do **monitorização** área de trabalho. Se observar erros a indicar uma implementação bem-sucedida, por exemplo:
- **Não aplicável a este dispositivo**
- **Falha na conversão do tipo de dados**

Estes erros não significam que falhou a implementação. Certifique-se no PC de destino que a atualização efetuada com êxito.

Depois do cliente avalia a política de destino, será reiniciado dentro de duas horas para aplicar a atualização. Certifique-se de informar os utilizadores nos quais implementou a política ou agendar a política a executar os utilizadores fora do horário de trabalho.

Se aparecer o erro seguinte no **DcmWmiProvider.log** no cliente, verifique se está a utilizar a chave correta para o seu cenário de ativação. Para obter mais informações, consulte o [antes de começar](#before-you-start) secção. Se estiver a utilizar um serviço de gestão de chaves para ativação, certifique-se de que utiliza um [chave de configuração de cliente do KMS](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys).  <!-- 496871 -->   

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`
