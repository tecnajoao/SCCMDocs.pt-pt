---
title: "Passos para gerir o BIOS para conversão de UEFI | Configuration Manager"
description: "Saiba como personalizar uma sequência de tarefas de implementação do sistema operativo para preparar uma partição FAT32 para transição para UEFI."
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 528ce515c86c4e778532290026a90a46476c4576
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Passos de sequência de tarefas para gerir o BIOS para conversão de UEFI
Windows 10 fornece várias novas funcionalidades de segurança que necessitam de dispositivos com capacidade de UEFI. Poderá ter moderna PCs Windows que suportem UEFI, mas estiver a utilizar o BIOS legado. A conversão de um dispositivo para UEFI requer a ir para cada computador, reparticionar o disco rígido e reconfigurar o firmware. Utilizando sequências de tarefas no Configuration Manager, pode preparar um disco rígido para o BIOS a conversão de UEFI, a conversão de BIOS em UEFI como parte do processo de atualização no local e recolher informações de UEFI como parte do inventário de hardware.

## <a name="hardware-inventory-collects-uefi-information"></a>Inventário de hardware recolhe informações de UEFI
A partir da versão 1702, um novo inventário de hardware classe (**SMS_Firmware**) e a propriedade (**UEFI**) estão disponíveis para o ajudar a determinar se um computador é iniciado no modo UEFI. Quando um computador for iniciado no modo UEFI, o **UEFI** propriedade está definida como **verdadeiro**. Esta opção estiver ativada no inventário de hardware por predefinição. Para obter mais informações sobre o inventário de hardware, consulte [como configurar inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive-for-bios-to-uefi-conversion"></a>Criar uma sequência de tarefas personalizada para preparar a unidade de disco rígido para o BIOS a conversão de UEFI
A partir do Configuration Manager versão 1610, pode agora personalizar uma sequência de tarefas de implementação do sistema operativo com uma nova variável, TSUEFIDrive, para que o **reiniciar o computador** passo irá preparar uma partição FAT32 no disco rígido para transição para UEFI. O procedimento seguinte fornece um exemplo de como pode criar os passos de sequência de tarefas para preparar a unidade de disco rígido para o BIOS para conversão de UEFI.

### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Para preparar a partição FAT32 para a conversão para UEFI:
Uma sequência de tarefas existente para instalar um sistema operativo, irá adicionar um novo grupo com os passos para fazer o BIOS para conversão de UEFI.

1. Crie um novo grupo de sequência de tarefas depois dos passos para capturar ficheiros e definições e antes dos passos para instalar o sistema operativo. Por exemplo, crie um grupo depois do **capturar ficheiros e definições** com o nome de grupo **BIOS para UEFI**.
2. No **opções** separador do novo grupo, adicione uma nova variável de sequência de tarefas como uma condição em que **smstsbootuefi sempre** é **não igual a** para **verdadeiro**. Isto impede que os passos no grupo de executar quando um computador já está no modo UEFI.

  ![BIOS para o grupo de UEFI](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. No novo grupo, adicione o **reiniciar o computador** passo de sequência de tarefas. No **especificam o que executar após o reinício**, selecione **a imagem de arranque atribuída a esta sequência de tarefas está selecionada** para iniciar o computador no Windows PE.  
4. No **opções** separador, adicione uma variável de sequência de tarefas como uma condição em que **smstsinwinpe é igual a FALSO**. Isto impede que este passo em execução se o computador já está no Windows PE.

  ![Reinicie o passo de computador](../../core/get-started/media/restart-in-windows-pe.png)
5. Adicione um passo para iniciar a ferramenta de OEM converterá o firmware da BIOS em UEFI. Normalmente, este será um **executar linha de comandos** passo de sequência de tarefas com uma linha de comandos para iniciar a ferramenta OEM.
6. Adicione o passo de sequência de tarefas formatar e particionar disco que será particionar e formatar o disco rígido. No passo, efetue o seguinte:
  1. Crie a partição de FAT32 será convertida em UEFI antes do sistema operativo está instalado. Escolha **GPT** para **tipo de disco**.
    ![Formatar e particionar passo de disco](../media/format-and-partition-disk.png)
  2. Vá para as propriedades para a partição FAT32. Introduza **TSUEFIDrive** no **variável** campo. Quando a sequência de tarefas Deteta esta variável, irá preparar para a transição de UEFI antes de reiniciar o computador.
    ![Propriedades da partição](../../core/get-started/media/partition-properties.png)
  3. Crie uma partição NTFS que o motor de sequência de tarefas utiliza para guardar o estado e armazenar ficheiros de registo.
7. Adicionar o **reiniciar o computador** passo de sequência de tarefas. No **especificam o que executar após o reinício**, selecione **a imagem de arranque atribuída a esta sequência de tarefas está selecionada** para iniciar o computador no Windows PE.  

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>A conversão de BIOS em UEFI durante uma atualização no local
Atualização do Windows 10 criadores introduz uma ferramenta de conversão simples que automatiza o processo para reparticionar o disco rígido para hardware ativado para UEFI e integra-se a ferramenta de conversão para o Windows 7 para o processo de atualização do Windows 10 no local. Ao combinar esta ferramenta com a sequência de tarefas de atualização do sistema operativo e a ferramenta do OEM que converte o firmware de BIOS para UEFI, pode converter os seus computadores de BIOS para UEFI durante uma atualização no local para o Windows 10 criadores Update.

**Requisitos**:
- Atualizar do Windows 10 criadores
- Computadores que suportam o UEFI
- Ferramenta de OEM que converte o firmware do computador de BIOS para UEFI

### <a name="to-convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Para converter do BIOS para UEFI durante uma atualização no local
1. Crie uma sequência de tarefas de atualização do sistema operativo que executa uma atualização no local para o Windows 10 criadores Update.
2. Edite a sequência de tarefas. No **grupo pós-processamento**, adicione os seguintes passos de sequência de tarefas:
   1. De geral, adicione um **executar linha de comandos** passo. Irá adicionar a linha de comandos para o MBR2GPT ferramenta que coverts GPT de um disco de MBR sem modificar ou eliminar dados do disco. Na linha de comandos, escreva o seguinte:  **MBR2GPT /convert /disk:0 /AllowFullOS**. Também pode optar por executar o MBR2GPT. Ferramenta EXE no Windows PE em vez de no sistema operativo completo. Pode fazê-lo ao adicionar um passo para reiniciar o computador para WinPE antes do passo para executar o MBR2GPT. Ferramenta EXE e remover a opção de /AllowFullOS na linha de comandos. Para obter detalhes sobre a ferramenta e as opções disponíveis, consulte [MBR2GPT. EXE](https://technet.microsoft.com/itpro/windows/deploy/mbr-to-gpt).
   2. Adicione um passo para iniciar a ferramenta de OEM converterá o firmware da BIOS em UEFI. Normalmente, este será um passo de sequência de tarefas executar linha de comandos com uma linha de comandos para iniciar a ferramenta OEM.
   3. De geral, adicione o **reiniciar o computador** passo. Para especificar o que executar após o reinício, selecione **o sistema operativo predefinido atualmente instalado**.
3. Implemente a sequência de tarefas.
