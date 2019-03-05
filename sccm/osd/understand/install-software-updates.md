---
title: Instalar Atualizações de Software
titleSuffix: Configuration Manager
description: Recomendações para utilizar o passo de sequência de tarefas instalar atualizações de Software no Configuration Manager.
ms.date: 03/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 72d1ccd5-3763-4f88-9273-e1a73e8f4286
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 132ef497f25f550eccc068e310c1336050ef3b42
ms.sourcegitcommit: 33a006204f7f5f9b9acd1f3e84c4bc207362d00a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/04/2019
ms.locfileid: "57305845"
---
# <a name="install-software-updates"></a>Instalar Atualizações de Software

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O **instalar atualizações de Software** passo é frequentemente utilizado nas sequências de tarefas do Configuration Manager. Ao instalar ou atualizar o sistema operacional, aciona os componentes de atualizações de software para procurar e implementar atualizações. Este passo pode causar desafios para alguns clientes, por exemplo, os atrasos de tempo limite de tempo, ou omitido atualizações. Utilize as informações neste artigo para ajudar a atenuar os problemas comuns com este passo e para resolução de problemas melhor quando algo corre mal.

Para obter mais informações sobre o passo, consulte [instalar atualizações de Software](/sccm/osd/understand/task-sequence-steps#BKMK_InstallSoftwareUpdates)



## <a name="recommendations"></a>Recomendações

Para ajudar a este processo seja concluída com êxito, utilize as seguintes recomendações:
- [Utilizar o fornecimento offline](#use-offline-servicing)
- [Único índice](#single-index)
- [Reduzir o tamanho da imagem](#bkmk_resetbase)


### <a name="use-offline-servicing"></a>Utilizar o fornecimento offline

Utilize o Gestor de configuração para instalar regularmente as atualizações de software aplicáveis aos seus ficheiros de imagem. Essa prática, em seguida, reduz o número de atualizações que terá de instalar durante a sequência de tarefas. 

Para obter mais informações, consulte [aplicar atualizações de software numa imagem](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates).


### <a name="single-index"></a>Único índice

Muitos arquivos de imagem incluem vários índices, tal como para diferentes edições do Windows. Reduza o arquivo de imagem para um único índice que necessita. Esta prática reduz a quantidade de tempo para aplicar atualizações de software à imagem. Ele também permite a recomendação seguinte reduzir o tamanho da imagem. 


### <a name="bkmk_resetbase"></a> Reduzir o tamanho da imagem

Quando aplica as atualizações de software à imagem, Otimize a saída ao remover quaisquer atualizações substituídas. Utilize a ferramenta de linha de comando DISM, por exemplo: 

```
dism /Mount-Image /ImageFile:C:\Data\install.wim /MountDir:C:\Mountdir
dism /Image:C:\Mountdir /Cleanup-Image /StartComponentCleanup /ResetBase 
dism /Unmount-Image /MountDir:C:\Mountdir /Commit  
```



## <a name="image-engineering-decisions"></a>Decisões de engenharia de imagem

Ao projetar seu processo de geração de imagens, há várias opções que podem afetar a instalação de atualizações de software:

- [Periodicamente recapturar a imagem](#bkmk_goldimage)  
- [Utilizar o fornecimento offline](#bkmk_offline)  
- [Utilizar apenas a imagem predefinida](#bkmk_installwim)


### <a name="bkmk_goldimage"></a> Periodicamente recapturar a imagem

Tem um processo automatizado para capturar uma imagem de SO personalizada com base numa agenda regular. Esta sequência de tarefas captura instala as atualizações de software mais recentes. Estas atualizações podem incluir cumulativas, não cumulativa e outras atualizações críticas, como a manutenção de atualizações de pilha (SSU). A sequência de tarefas de implementação instala todas as atualizações adicionais desde captura.

Para obter mais informações sobre este processo, consulte [criar uma sequência de tarefas para capturar um sistema operacional](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system).


#### <a name="advantages"></a>Vantagens
- Menos atualizações a aplicar-se no momento da implementação por cliente, o que economiza tempo e de largura de banda durante a implementação
- Atualizações de menos de se preocupar sobre a causar o reinício
- Imagem personalizada para a organização
- Variáveis a menos no momento da implementação

#### <a name="disadvantages"></a>Desvantagens 
- Tempo para criar e capturar a imagem, mesmo que principalmente é automatizado
- Mais tempo para distribuir a imagem aos pontos de distribuição, o que pode ser visto como falha para implementações ativas
- Tempo para testar através de ambientes de pré-produção pode ter mais de ciclo de patches de SO, que pode tornar a imagem atualizada irrelevantes 


### <a name="bkmk_offline"></a> Utilizar o fornecimento offline

Gestor de configuração de agenda para aplicar atualizações de software para as imagens. 

Para obter mais informações, consulte [aplicar atualizações de software numa imagem](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates).


#### <a name="advantages"></a>Vantagens
- Menos atualizações a aplicar-se no momento da implementação por cliente, o que economiza tempo e de largura de banda durante a implementação
- Atualizações de menos de se preocupar sobre a causar o reinício
- Pode agendar o processo de manutenção no site

#### <a name="disadvantages"></a>Desvantagens 
- Seleção manual de atualizações 
- Mais tempo para distribuir a imagem aos pontos de distribuição
- Suporta apenas a atualizações com base em CBS. Ele não é possível aplicar atualizações do Office

> [!Tip]  
> Pode automatizar a seleção de atualizações de software com o PowerShell. Utilize o [Get-CMSoftwareUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmsoftwareupdate?view=sccm-ps) cmdlet para obter uma lista de atualizações. Em seguida, utilize o [New-CMOperatingSystemImageUpdateSchedule](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmoperatingsystemimageupdateschedule?view=sccm-ps) agendar do cmdlet para criar a manutenção offline. O exemplo seguinte mostra um método para automatizar esta ação:
> 
> ```PowerShell
> # Get the OS image
> $Win10Image = Get-CMOperatingSystemImage -Name "Windows 10 Enterprise"
> 
> # Get the latest cumulative update for Windows 10 1809
> $OSBuild = "1809"
> $LatestUpdate = Get-CMSoftwareUpdate -Fast | Where {$_.LocalizedDisplayName -Like "*Cumulative Update for Windows 10 Version $OSBuild for x64*" -and $_.LocalizedDisplayName -notlike "*Dynamic*"} | Sort-Object ArticleID -Descending | Select -First 1 
> Write-Host "Latest update for Windows 10 build" $OSBuild "is" $LatestUpdate.LocalizedDisplayName
> 
> # Create a new update schedule to apply the latest update
> New-CMOperatingSystemImageUpdateSchedule -Name $Win10Image.Name -SoftwareUpdate $LatestUpdate -RunNow -ContinueOnError $True 
> ```


### <a name="bkmk_installwim"></a> Utilizar apenas a imagem predefinida

Utilize o ficheiro de imagem do Install. wim do Windows do padrão nas suas sequências de tarefas de implementação.

#### <a name="advantages"></a>Vantagens
- Uma boa fonte conhecida, que reduz o risco de Corrupção de imagem como um possível problema
- Elimina as modificações de imagem como um possível problema

#### <a name="disadvantages"></a>Desvantagens 
- Potencial para elevado volume de atualizações durante a implementação
- Tempo de implantação maior para todos os dispositivos
- Não poderá ter precisado personalizações, requer passos de sequência de tarefas adicionais para personalizar



## <a name="flowchart"></a>Fluxograma

Este diagrama de fluxograma mostra o processo ao incluir o passo instalar atualizações de Software numa sequência de tarefas.

[Ver o diagrama com tamanho máximo](media/ts-step-install-software-updates.svg)

![Diagrama de fluxograma para o passo de sequência de tarefas instalar atualizações de Software](media/ts-step-install-software-updates.svg)  

1. **Processo é iniciado no cliente**: Uma sequência de tarefas em execução num cliente inclui o passo de atualizações de Software instalar.
2. **Compilar e avaliar políticas**: O cliente compila todas as políticas de atualização de software num espaço de nomes WMI RequestedConfigs. (CIAgent.log)
3. *É esta instância na primeira vez que ele é chamado?*  
    1. **Sim**: Aceda a **análise completa**  
    2. **Não**: *É a etapa configurada com a opção para [avaliar atualizações de software nos resultados da análise em cache](/sccm/osd/understand/task-sequence-steps#evaluate-software-updates-from-cached-scan-results)?*
        1. **Sim**: Aceda a **lê a partir de resultados em cache**
        2. **Não**: Aceda a **análise completa**
4. Processo de análise: uma análise completa ou de uma análise dos resultados em cache, com a monitorização do processo em paralelo.
    1. **Análise completa**: O motor de sequência de tarefas chama o agente de atualização de software por meio de atualizar a API de análise para fazer uma *completo* analisar. (WUAHandler.log, ScanAgent.log)  
        1. **Verificação do agente de soma - completa**: Processo de análise normal via Windows Update Agent (WUA), que comunica com o ponto de atualização de software a executar o WSUS. Ele adiciona as atualizações aplicáveis para o arquivo de atualização de local. (WindowsUpdate.log, UpdateStore.log)
    2. **Lê a partir de resultados em cache**: O motor de sequência de tarefas chama o agente de atualização de software por meio de atualizar a API de análise para verificar em relação a metadados em cache. (WUAHandler.log, ScanAgent.log) 
        1. **Pesquisa de agente de soma - armazenados em cache**: Verifica o Windows Update Agent (WUA) em relação a atualizações já armazenado em cache no arquivo de atualização de local. (WindowsUpdate.log, UpdateStore.log)
    3. **Temporizador de verificação de início**: O motor de sequência de tarefas inicia um temporizador e aguarda. (Este processo ocorre em paralelo com a análise completa ou de uma análise do processo de resultados em cache.)
        1. **Monitorização**: O motor de sequência de tarefas monitoriza o agente de soma para obter o estado.
        2. *O que é a resposta do agente de soma?*
            - **Em curso**: O temporizador atingiu o valor na variável de sequência de tarefas [SMSTSSoftwareUpdateScanTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSSoftwareUpdateScanTimeout)? (Predefinição 1 hora)
                - **Sim**: O passo falhar.
                - **Não**: Aceda a **monitorização**
            - **Falha ao**: O passo falhar.
            - **Completa**: Aceda a **Enumerate lista de atualização**
5. **Enumerar a lista de atualização de**: O agente de soma enumera a lista de atualizações retornados pelo exame, determinar que está disponível ou obrigatória.
6. *Existem todas as atualizações na lista de resultados da análise?*
    - **Sim**: Aceda a **instalar atualizações**
    - **Não**: Nada para instalar, a etapa for concluída com êxito. 
7. Processo de implantação: O processo de instalação de atualizações acontece em paralelo com a implementação do processo de monitorização.
    1. **Instalar atualizações**: O motor de sequência de tarefas chama o agente de soma através da API de implementação de atualização para instalar todas as atualizações disponíveis ou apenas obrigatórias. Este comportamento, se baseia-se a configuração do passo, se seleciona **necessário para instalação - atualizações de software obrigatórias apenas** ou **disponível para instalação - todas as atualizações de software**. Também pode especificar esse comportamento, utilizando o [SMSInstallUpdateTarget](/sccm/osd/understand/task-sequence-variables#SMSInstallUpdateTarget) variável.
        1. **Instalação do agente de soma**: Processo de instalação normal com atual em cache a lista de atualizações, com transferência de conteúdo padrão. Instale atualização via Windows Update Agent (WUA). (UpdatesDeployment.log, UpdatesHandler.log, WuaHandler.log, WindowsUpdate.log)
    2. **Iniciar Temporizador de implementação e mostrar o progresso**: O motor de sequência de tarefas inicia um temporizador de instalação, mostra o progresso da secundária em intervalos de 10% na interface do Usuário de progresso de TS e espera.
        1. **Monitorização**: O motor de sequência de tarefas consulta o agente de soma para obter o estado.
        2. *O que é a resposta do agente de soma?*
            - **Em curso**: *O processo de instalação tenha estado inativo durante 8 horas?*
                - **Sim**: O passo falhar.
                - **Não**: Aceda a **monitorização**
            - **Falha ao**: O passo falhar.
            - **Completa**: Aceda a *é a etapa configurada com a opção de **avaliar atualizações de software nos resultados da análise em cache**?*


### <a name="timeouts"></a>Tempos limite

O diagrama inclui dois das variáveis do tempo limite que se aplicam a este passo. Existem outros timers padrão de outros componentes que podem afetar esse processo. 

- Tempo limite de análise de atualização: 1 hora (smsts)  
- Tempo limite do pedido de localização: 1 hora (Locationservices, CAS.log)  
- Tempo limite da transferência de conteúdo: 1 hora (DTS.log)  
- Tempo limite do ponto de distribuição inativa: 1 hora (Locationservices, CAS.log)  
- Tempo limite inativo instalação total: 8 horas (smsts)  



## <a name="troubleshooting"></a>Resolução de Problemas

Utilize os seguintes recursos e as informações adicionais para ajudar a resolver problemas com este passo:

- Lembre-se de que as implementações de atualização de software na mesma coleção, como a implementação de sequência de tarefas de destino.  

- Certifique-se incluir os pontos de atualização de software em grupos de limites. Para obter mais informações, consulte esta [artigo Microsoft Support](https://support.microsoft.com/help/4041012/1702-clients-do-not-get-software-updates-from-configuration-manager).  

- Para ajudar a resolver problemas relacionados com o processo de gestão de atualizações de software, consulte [Software Update Management de resolução de problemas](https://support.microsoft.com/help/10680/software-update-management-troubleshooting-in-configuration-manager).  

- Para ajudar a melhorar o desempenho geral, reduza o tamanho do catálogo de atualização de software. Por exemplo:  

    - Remova classificações desnecessárias, produtos e idiomas. Para obter mais informações, consulte [configurar classificações e produtos para sincronizar](/sccm/sum/get-started/configure-classifications-and-products).  

    - Reindexar a base de dados e reconstruir as estatísticas. Para obter mais informações, consulte a [desempenho do Configuration Manager e o documento técnico de orientação de dimensionamento](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e).  

    - Recuse atualizações desnecessárias, por exemplo:
        - Substituído (a partir da versão 1810, Configuration Manager também faz esta ação para. Para obter mais informações, consulte [comportamento de limpeza WSUS a partir da versão 1810](/sccm/sum/deploy-use/software-updates-maintenance#wsus-cleanup-behavior-starting-in-version-1810).)
        - Itanium
        - Beta
        - Versão seguinte
        - ARM
        - Versões do Windows que não está a implementar

