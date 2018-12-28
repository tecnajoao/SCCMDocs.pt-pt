---
title: Passos de sequência de tarefas para gerir a conversão de BIOS em UEFI
titleSuffix: Configuration Manager
description: Saiba como personalizar uma sequência de tarefas de implementação do sistema operativo para preparar uma partição FAT32 para a transição para UEFI.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bd1181bd14779a6ac659927979185aa174203206
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53420180"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Passos de sequência de tarefas para gerir a conversão de BIOS em UEFI
Windows 10 fornece muitos novos recursos de segurança que exigem dispositivos habilitados para UEFI. Terá de PCs Windows modernos que suportem UEFI, mas estiver a utilizar o BIOS legado. Conversão de um dispositivo para UEFI requer que cada PC, criar novas partições no disco rígido e reconfigurar o firmware. Ao utilizar sequências de tarefas no Configuration Manager, pode preparar um disco rígido BIOS para conversão de UEFI, converter de BIOS para UEFI, como parte do processo de atualização no local e recolher informações de UEFI como parte do inventário de hardware.

## <a name="hardware-inventory-collects-uefi-information"></a>Inventário de hardware recolhe informações de UEFI
Partir da versão 1702, um novo de inventário de hardware classe (**SMS_Firmware**) e a propriedade (**UEFI**) estão disponíveis para ajudar a determinar se um computador é iniciado no modo UEFI. Quando um computador é iniciado no modo UEFI, o **UEFI** estiver definida como **verdadeiro**. Esta opção estiver ativada no inventário de hardware por predefinição. Para obter mais informações sobre o inventário de hardware, consulte [como configurar inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive-for-bios-to-uefi-conversion"></a>Criar uma sequência de tarefas personalizado para preparar o disco rígido de BIOS para conversão de UEFI
A partir do Configuration Manager versão 1610, agora pode personalizar uma sequência de tarefas de implementação do sistema operativo com uma nova variável, TSUEFIDrive, para que o **reiniciar o computador** passo, irá preparar uma partição FAT32 na unidade de disco rígida para a transição para UEFI. O procedimento seguinte fornece um exemplo de como pode criar passos de sequência de tarefas para preparar o disco rígido para o BIOS para conversão de UEFI.

### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Para preparar a partição FAT32 para a conversão para UEFI:
Uma sequência de tarefas existente para instalar um sistema operativo, vai adicionar um novo grupo com os passos para fazer o BIOS para conversão de UEFI.

1. Crie um novo grupo de sequência de tarefas após os passos para capturar definições e ficheiros e antes dos passos para instalar o sistema operativo. Por exemplo, criar um grupo depois do **capturar arquivos e configurações** com o nome de grupo **BIOS para UEFI**.
2. Na **opções** separador do novo grupo, adicione uma nova variável de sequência de tarefas como uma condição em que **smstsbootuefi sempre** é **não igual** para **verdadeiro**. Isto impede que os passos no grupo de em execução quando um computador já está no modo UEFI.

   ![BIOS para o grupo UEFI](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. Em novo grupo, adicione a **reiniciar o computador** passo de sequência de tarefas. Na **especificam as ações a executar após o reinício**, selecione **está selecionada a imagem de arranque atribuída a esta sequência de tarefas** para iniciar o computador no Windows PE.  
4. Sobre o **opções** separador, adicione uma variável de sequência de tarefas como uma condição em que **smstsinwinpe é igual a false**. Isto impede que este passo em execução se o computador já está no Windows PE.

   ![Reinicie o passo de computador](../../core/get-started/media/restart-in-windows-pe.png)
5. Adicione um passo para iniciar a ferramenta de OEM que converterá o firmware de BIOS para UEFI. Normalmente, será uma **executar linha de comandos** passo de sequência de tarefas com uma linha de comando para iniciar a ferramenta de OEM.
6. Adicione o passo de sequência de tarefas formatar e particionar disco que será particionar e formatar o disco rígido. No passo, efetue o seguinte:
   1. Crie a partição FAT32 que será convertida para UEFI antes do sistema operativo é instalado. Escolher **GPT** para **tipo de disco**.
    ![Formatar e particionar passo de disco](../media/format-and-partition-disk.png)
   2. Vá para as propriedades para a partição FAT32. Introduza **TSUEFIDrive** no **variável** campo. Quando a sequência de tarefas Deteta esta variável, irá preparar para a transição de UEFI antes de reiniciar o computador.
    ![Propriedades de partição](../../core/get-started/media/partition-properties.png)
   3. Crie uma partição NTFS que o motor de sequência de tarefas utiliza para salvar seu estado e para armazenar ficheiros de registo.
7. Adicionar a **reiniciar o computador** passo de sequência de tarefas. Na **especificam as ações a executar após o reinício**, selecione **está selecionada a imagem de arranque atribuída a esta sequência de tarefas** para iniciar o computador no Windows PE.  

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Converter de BIOS para UEFI durante uma atualização no local
Windows 10 Creators Update introduz uma ferramenta de conversão simples que automatiza o processo para criar novas partições de disco rígido para o hardware preparado para UEFI e integra-se a ferramenta de conversão para o 7 do Windows para o processo de atualização do Windows 10 no local. Ao combiná-essa ferramenta com a sequência de tarefas de atualização do sistema operativo e a ferramenta de OEM que converte o firmware de BIOS para UEFI, pode converter seus computadores de BIOS para UEFI durante uma atualização no local para a atualização para criativos do Windows 10.

**Requisitos de**:
- Atualização para criativos do Windows 10
- Computadores que suportem UEFI
- Ferramenta de OEM que converte o firmware do computador de BIOS para UEFI

### <a name="to-convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Para converter BIOS para UEFI durante uma atualização no local
1. Crie uma sequência de tarefas de atualização do sistema operativo que executa uma atualização in-loco para o Windows 10 Creators Update.
2. Edite a sequência de tarefas. Na **grupo pós-processamento**, adicione os seguintes passos de sequência de tarefas:
   1. No geral, adicione uma **executar linha de comandos** passo. Irá adicionar a linha de comandos para o MBR2GPT ferramenta que converte um disco de MBR para GPT sem modificar ou eliminar dados a partir do disco. Na linha de comandos, escreva o seguinte:  **MBR2GPT /convert /disk:0 /AllowFullOS**. Também pode optar por executar o MBR2GPT. Ferramenta EXE no Windows PE em vez de em todo o sistema operativo. Pode fazê-lo ao adicionar um passo para reiniciar o computador WinPE antes do passo para executar o MBR2GPT. Ferramenta EXE e remover a opção de /AllowFullOS da linha de comando. Para obter detalhes sobre a ferramenta e as opções disponíveis, consulte [MBR2GPT. EXE](https://technet.microsoft.com/itpro/windows/deploy/mbr-to-gpt).
   2. Adicione um passo para iniciar a ferramenta de OEM que converterá o firmware de BIOS para UEFI. Normalmente, será um passo de sequência de tarefas executar linha de comandos com uma linha de comando para iniciar a ferramenta de OEM.
   3. No geral, adicione a **reiniciar o computador** passo. Para especificar o que executar após o reinício, selecione **o sistema de operativo predefinido atualmente instalado**.
3. Implemente a sequência de tarefas.
