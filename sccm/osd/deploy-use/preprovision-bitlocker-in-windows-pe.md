---
title: Aprovisionar antecipadamente o BitLocker no Windows PE
titleSuffix: Configuration Manager
description: A tarefa de Preprovision BitLocker no Configuration Manager permite que o BitLocker a partir do ambiente de pré-instalação do Windows antes da implantação de sistema operativo.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c7c94ba0-d709-4129-8077-075a8abaea1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 10c072c89064472398c068a62079d1af120b1a11
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416559"
---
# <a name="preprovision-bitlocker-in-windows-pe-with-system-center-configuration-manager"></a>Aprovisionar antecipadamente o BitLocker no Windows PE com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O **provisão prévia do BitLocker** passo de sequência de tarefas no System Center Configuration Manager permite-lhe ativar o BitLocker a partir do ambiente de pré-instalação do Windows (Windows PE) antes da implementação do sistema operativo. Apenas o espaço de disco utilizado é encriptado e, portanto, os tempos de encriptação são muito mais rápidos. Para isso, é aplicado ao volume formatado um protetor de limpeza gerado aleatoriamente e o volume é encriptado antes da execução do processo de configuração do Windows. A capacidade de pré-aprovisionar o BitLocker foi introduzida com o Windows 8 e o Windows Server 2012. No entanto, pode pré-aprovisionar o BitLocker num disco rígido e instalar o Windows 7, desde que siga os passos específicos. Após a conclusão do Programa de Configuração do Windows 7, é necessário definir um protetor de chave do BitLocker porque o painel de controlo do BitLocker no Windows 7 não suporta o BitLocker com um protetor de limpeza. É necessário adicionar um protetor de chave, utilizando o passo **Ativar BitLocker** ou a ferramenta de linha de comandos manage-bde.exe.  

 Geralmente, é necessário efetuar o seguinte para pré-aprovisionar com êxito o BitLocker num computador que vai instalar o Windows 7:  

- Reiniciar o computador no Windows PE  

  > [!IMPORTANT]  
  >  É necessário utilizar uma imagem de arranque com o Windows PE 4 ou posterior para pré-aprovisionar o BitLocker. Para obter mais informações sobre versões suportadas do Windows PE no Configuration Manager, consulte [dependências externas ao Configuration Manager](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_ExternalDependencies).  

- Particionar e formatar o disco rígido  

- Provisão prévia do BitLocker  

- Instalar o Windows 7 com o sistema operativo e as definições de rede específicos  

- Adicionar um protetor de chave ao BitLocker  

  No Configuration Manager, a forma recomendada de pré-aprovisionar o BitLocker num disco rígido e instalar o Windows 7 é criar uma nova sequência de tarefas e selecionar **instalar um pacote de imagem existente** partir o **criar nova tarefa Sequência** página do **criar Assistente de sequência de tarefas**. O assistente cria os passos de sequência de tarefas listados na tabela a seguir.  

> [!NOTE]  
>  A sequência de tarefas pode ter passos adicionais, dependendo do modo como foram configuradas as definições no assistente. Por exemplo, pode ter o passo **Capturar Definições do Windows** se tiver selecionado **Definições do Microsoft Windows capturadas** na página **Migração de Estado** do assistente.  

|Passo da sequência de tarefas|Detalhes|  
|------------------------|-------------|  
|Desativar BitLocker|Este passo desativa a encriptação BitLocker, se estiver atualmente ativada. Para mais informações, consulte [Disable BitLocker](../understand/task-sequence-steps.md#BKMK_DisableBitLocker).|  
|Reiniciar o computador no Windows PE|Este passo reinicia o computador no Windows PE através da execução da imagem de arranque atribuída à sequência de tarefas. É necessário utilizar uma imagem de arranque com o Windows PE 4 ou posterior para pré-aprovisionar o BitLocker. Para mais informações, consulte [Restart Computer](../understand/task-sequence-steps.md#BKMK_RestartComputer).|  
|Particionar Disco 0 - BIOS<br /><br /> Particionar Disco 0 - UEFI|Estes passos formatam e particionam a unidade especificada no computador de destino, utilizando BIOS ou UEFI. A sequência de tarefas utiliza UEFI quando deteta que o computador de destino está no modo UEFI. Para mais informações, consulte [Format and Partition Disk](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk).|  
|Provisão prévia do BitLocker|Este passo ativa o BitLocker numa unidade no Windows PE. Apenas o espaço de disco utilizado é encriptado. Uma vez que o disco rígido foi particionado e formatado no passo anterior, não existem dados e a encriptação é concluída rapidamente. Para mais informações, consulte [Pre-provision BitLocker](../understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker).|  
|Aplicar Sistema Operativo|Este passo prepara o ficheiro de resposta que é utilizado para instalar o sistema operativo no computador de destino e define a variável da sequência de tarefas OSDTargetSystemDrive para a letra de unidade da partição que contém os ficheiros do sistema operativo. O ficheiro de resposta e a variável são utilizados pelo passo Configurar Windows e ConfigMgr para instalar o sistema operativo. Para mais informações, consulte [Apply Operating System Image](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).|  
|Aplicar Definições do Windows|Este passo adiciona definições do Windows ao ficheiro de resposta. O ficheiro de resposta é utilizado pelo passo Configurar Windows e ConfigMgr para instalar o sistema operativo. Para mais informações, consulte [Apply Windows Settings](../understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings).|  
|Aplicar Definições de Rede|Este passo adiciona definições de Rede ao ficheiro de resposta. O ficheiro de resposta é utilizado pelo passo Configurar Windows e ConfigMgr para instalar o sistema operativo. Para mais informações, consulte [Apply Network Settings Step](../understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings).|  
|Aplicar Controladores de Dispositivo|Este passo corresponde e instala controladores como parte da implementação do sistema operativo. Para mais informações, consulte [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).|  
|Configurar Windows e ConfigMgr|Este passo efetua a transição do Windows PE para o novo sistema operativo. Este passo da sequência de tarefas é uma parte necessária de qualquer implementação do sistema operativo. Ele instala o cliente de Configuration Manager para o novo sistema operativo e prepara a sequência de tarefas continuar a execução no novo sistema operacional. Para mais informações, consulte [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).|  
|Ativar BitLocker|Este passo ativa a encriptação do BitLocker no disco rígido e define protetores de chave. Uma vez que o disco rígido foi pré-aprovisionado com o BitLocker, este passo é concluído rapidamente. O Windows 7 requer a adição de um protetor de chave. Se não utilizar este passo, pode executar a ferramenta da linha de comandos manage-bde.exe para definir um protetor de chave. Para mais informações, consulte [Enable BitLocker](../understand/task-sequence-steps.md#BKMK_EnableBitLocker).|  
