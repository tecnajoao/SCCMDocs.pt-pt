---
title: Inscrever dispositivos no ambiente de trabalho de análise
titleSuffix: Configuration Manager
description: Saiba como inscrever dispositivos no ambiente de trabalho de análise.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 19e46eb99d5b16b955f0ffe70e497d188f9fc807
ms.sourcegitcommit: ad25a7bdd983c5a0e4c95bffdc61c9a1ebcbb765
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/26/2019
ms.locfileid: "55073399"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>Como inscrever dispositivos no ambiente de trabalho de análise 

> [!Note]  
> Estas informações se relaciona com o serviço de pré-visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft faz não oferece quaisquer garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Quando [ligar o Configuration Manager](/sccm/desktop-analytics/connect-configmgr) para análises de ambiente de trabalho, configure as definições para inscrever dispositivos para análise de ambiente de trabalho. Pode alterar estas definições em qualquer altura. Além disso, certifique-se de que os dispositivos estão atualizados. 



## <a name="update-devices"></a>Atualizar os dispositivos

Existem dois tipos de atualizações que tem de aplicar a melhor experiência com a análise de ambiente de trabalho: 
- [Atualizações de compatibilidade](#bkmk_appraiser)  
- [Experiências de utilizador e telemetria de serviço ligado](#bkmk_diagtrack)


### <a name="bkmk_appraiser"></a> Atualizações de compatibilidade

O componente de compatibilidade (Appraiser) executa o diagnóstico no dispositivo Windows para avaliar o estado de compatibilidade com versões mais recentes do Windows 10.

Microsoft incrementa regularmente as atualizações para este componente, mas não altera o número KB associado. Certifique-se de que tenha sempre a versão mais recente da atualização.

Reinicie dispositivos depois de instalar as atualizações de compatibilidade pela primeira vez.

> [!Tip]  
> Utilize o Gestor de configuração para instalar a versão mais recente destas atualizações automaticamente. Para obter mais informações, consulte [implementar atualizações de software](/sccm/sum/deploy-use/deploy-software-updates).  

> [!Note]  
> Existe uma atualização opcional relacionada, [KB 3150513](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=3150513). Esta atualização fornece configuração atualizada e definições para as atualizações mais antigas de compatibilidade. Para obter mais informações, consulte [mais recente atualização de definições de compatibilidade para Windows](https://support.microsoft.com/help/3150513).  

#### <a name="windows-10"></a>Windows 10
Windows 10 inclui o componente de compatibilidade. Para obter a atualização de compatibilidade mais recente, instale a atualização cumulativa mais recente do Windows 10.

#### <a name="windows-81"></a>Windows 8,1
Transferir a atualização: [KB 2976978](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2976978) 

Executa o diagnóstico nos sistemas Windows 8.1 que participam no programa de melhoramento da experiência do cliente do Windows. Este diagnóstico ajudam a determinar se pode ter problemas de compatibilidade ao atualizar para o Windows 10.

Para obter mais informações, consulte [de atualização de compatibilidade para manter o Windows atualizados no Windows 8.1](https://support.microsoft.com/help/2976978).

#### <a name="windows-7-with-service-pack-1"></a>Windows 7 com Service Pack 1
Transferir a atualização: [KB 2952664](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2952664) 

É executado diagnósticos no Windows 7 com sistemas de Service Pack 1 (SP1) que participam no programa de melhoramento da experiência do cliente do Windows. Este diagnóstico ajudam a determinar se pode ter problemas de compatibilidade ao atualizar para o Windows 10.

Para obter mais informações, consulte [de atualização de compatibilidade para manter o Windows atualizados no Windows 7](https://support.microsoft.com/help/2952664).


### <a name="bkmk_diagtrack"></a> Experiências de utilizador e telemetria de serviço ligado

Com a dados de diagnóstico Windows ativados, o serviço ligado a experiência de utilizador e telemetria (DiagTrack) recolhe dados do sistema, o aplicativo e o driver. A Microsoft analisa esses dados e partilhe o mesmo é com por meio da análise de ambiente de trabalho.

A melhor experiência, instale as atualizações seguintes, consoante a versão do SO.

> [!Note]  
> Ao instalar estas atualizações, esperar que os comportamentos seguintes: 
> - Dispositivos que inscrever para o ambiente de trabalho Analytics aparecem no serviço em menos de uma hora  
> - Dispositivos comunicam rapidamente o estado em atualizações de qualidade e funcionalidade para Windows e o Office  
> 
> Sem estas atualizações, esses processos podem demorar mais de 48 horas para um dispositivo comunicar ao ambiente de trabalho de análise.  


#### <a name="windows-10"></a>Windows 10
Instale a atualização cumulativa mais recente do Windows 10.

<!-- 
- Windows 10 1809: Included in RTM build
- Windows 10 1803: [KB4458469](https://support.microsoft.com/help/4458469) (OS Build 17134.319)
- Windows 10 1709: [KB4457136](https://support.microsoft.com/help/4457136) (OS Build 16299.697)
- Windows 10 1703: [KB4457141](https://support.microsoft.com/help/4457141) (OS Build 15063.1358)
- Windows 10 1607: [KB4457127](https://support.microsoft.com/help/4457127) (OS Build 14393.2517)
 -->

#### <a name="windows-81"></a>Windows 8,1
Instalar o rollup mensal de Outubro de 2018, [KB4462926](https://support.microsoft.com/help/4462926)

#### <a name="windows-7"></a>Windows 7
Instalar o rollup mensal de Outubro de 2018, [KB4462923](https://support.microsoft.com/help/4462923)



## <a name="device-enrollment"></a>Inscrição de dispositivos

O serviço de análise de ambiente de trabalho tem sem agentes para instalar. Inscrição de dispositivos necessita de configurar as definições nos dispositivos que pretende monitorizar. Estas definições controlam a que instância de análise de ambiente de trabalho, o dispositivo deve enviar seus dados e outras opções de configuração.

> [!Note]  
> Se já estiver a utilizar o Windows Analytics, utilize essa mesma área de trabalho para a análise de ambiente de trabalho. Terá de reinscrever os dispositivos para análise de ambiente de trabalho que tiver inscrito anteriormente no Windows Analytics. 
> 
> Só pode ter uma área de trabalho de análise de ambiente de trabalho por inquilino do Azure AD. Dispositivos apenas podem enviar dados de diagnóstico para uma área de trabalho.   

O Configuration Manager fornece uma experiência integrada para gerir e implementar estas definições para os clientes. A melhor experiência, utilize o Configuration Manager. 

Quando liga o Configuration Manager para análise de ambiente de trabalho, configura as definições para inscrever dispositivos. Para obter mais informações, consulte [como ligar o Configuration Manager com o ambiente de trabalho Analytics](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).

Para alterar estas definições, utilize o seguinte procedimento:

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **serviços Cloud**e selecione o **dos serviços do Azure** nó. Selecione a ligação ao ambiente de trabalho de análise e escolha **propriedades** na faixa de opções. 

2. Sobre o **dados de diagnóstico** página, fazer alterações, conforme necessário para as seguintes definições:  

    - **ID comercial**: não deverá ser necessário alterar ou editar este valor. Para obter mais informações sobre resolução de problemas com o ID comercial, consulte [configuração do ID comercial](/sccm/desktop-analytics/troubleshooting#commercial-id-configuration).  

    - **Nível de dados de diagnóstico do Windows 10**: Para obter mais informações, consulte [níveis de dados de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

    - **Permite que o nome de dispositivo em dados de diagnóstico**: Para obter mais informações, consulte [nome do dispositivo](#device-name).  

    Quando fizer alterações a esta página, o **funcionalidade disponível** página mostra uma pré-visualização da funcionalidade de análise de ambiente de trabalho com as definições de dados de diagnóstico selecionado.  

3. Sobre o **ligação de análise do Microsoft 365** página, fazer alterações, conforme necessário para as seguintes definições:

    - **Nome a apresentar**: O portal de análise de ambiente de trabalho apresenta esta ligação do Configuration Manager com este nome.  

    - **Coleção de destino**: Esta coleção inclui todos os dispositivos que configura o Configuration Manager com o seu ID comercial e as definições de dados de diagnóstico. É o conjunto completo de dispositivos do Configuration Manager liga-se para o serviço de análise de ambiente de trabalho.  

    - **Os dispositivos da coleção de destino utilizar um proxy de usuário autenticado para comunicações de saída**: Por predefinição, este valor é **não**. Se for necessário no seu ambiente, definido como **Sim**. Para obter mais informações, consulte [autenticação de servidor de Proxy](/sccm/desktop-analytics/enable-data-sharing#proxy-server-authentication).  

    - **Selecione as coleções específicas para sincronizar com a análise de ambiente de trabalho**: Selecione **adicionar** para incluir coleções adicionais. Essas coleções estão disponíveis no portal do Analytics de ambiente de trabalho para o agrupamento com planos de implantação. Certifique-se incluir coleções de exclusão de piloto e piloto.  

        Essas coleções continuam a sincronizar como as alterações de associação. Por exemplo, o seu plano de implementação utiliza uma coleção com uma regra de associação do Windows 7. À medida que esses dispositivos atualizar para o Windows 10 e do Configuration Manager avalia a associação à coleção, esses dispositivos soltem fora de coleta e ao plano de implantação.  


### <a name="windows-settings"></a>Definições do Windows

O Configuration Manager define as seguintes definições do Windows em `Microsoft\Windows\DataCollection`:

| Política   | Valor  |
|----------|--------|
| **CommercialId** | Ordem de um dispositivo a aparecer no ambiente de trabalho de análise, configurá-lo com o ID da comercial. sua organização |
| **AllowTelemetry**  | Definir `1` para **básica**, `2` para **avançado**, ou `3` para **completa** dados de diagnóstico. Análise de área de trabalho requer que os dados de diagnóstico, pelo menos, básicos. A Microsoft recomenda que utilize o nível avançado (limitado) com a análise de ambiente de trabalho. Para obter mais informações, consulte [dados de diagnóstico de configurar o Windows na sua organização](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | *Aplica-se para o Windows 10, versão 1709 ou posterior*: Esta definição aplica-se apenas quando a definição de AllowTelemetry se `2`. Limita os eventos de dados de diagnóstico avançado enviados à Microsoft para apenas os eventos necessários para análise de ambiente de trabalho. Para obter mais informações, consulte [Windows 10, versão 1709 avançada de eventos de dados de diagnóstico e de campos utilizados pelo Windows Analytics](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields).|
| **AllowDeviceNameInTelemetry** | *Aplica-se para o Windows 10, versão 1803 e posterior*: Um separado participar, é necessário para permitir que os dispositivos para continuarão a enviar o nome do dispositivo.<br> <br>Nota: O nome do dispositivo não é enviado à Microsoft por predefinição. Se não tiver de enviar o nome do dispositivo, aparecerá na área de trabalho de análise como "Desconhecido". Esse comportamento pode tornar difícil identificar e avaliar os dispositivos. Para obter mais informações, consulte [nome do dispositivo](#device-name). |
| **CommercialDataOptIn** | *Aplica-se ao Windows 7 e Windows 8.1*: Um valor de `1` é necessária para a análise de ambiente de trabalho. Para obter mais informações, consulte [participação ativa-em dados comerciais no Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |

Ver estas definições no editor de diretiva de grupo no seguinte caminho: **Configuração do computador** > **modelos administrativos** > **componentes do Windows** > **dados coleção e pré-visualização Baseia-se**. 


### <a name="device-name"></a>Nome do dispositivo

A partir do Windows 10, versão 1803, o nome do dispositivo já não é recolhido por predefinição. Recolher o nome do dispositivo com os dados de diagnóstico requer um separado participar. Sem o nome do dispositivo, é mais difícil de identificar quais os dispositivos que requerem atenção durante a avaliação de uma atualização para uma nova versão do Windows ou do Office. 

Se não tiver de enviar o nome do dispositivo, aparecerá na área de trabalho de análise como "Desconhecido".

![Lista de dispositivos Analytics área de trabalho, que mostra os nomes de "desconhecidos"](media/unknown-device-name.png)

Há uma opção nas definições do Configuration Manager para análise de ambiente de trabalho configurar esta opção: **Permite que o nome de dispositivo em dados de diagnóstico**. Esta definição do Configuration Manager controla a definição de política do Windows, AllowDeviceNameInTelemetry.
 

### <a name="conflict-resolution"></a>Resolução de conflitos

Em geral, utilize coleções do Configuration Manager para inscrição e as definições de análise de ambiente de trabalho de destino. Utilize associação direta ou consultas para incluir ou excluir os dispositivos da coleção. Para obter mais informações, consulte [como criar coleções](/sccm/core/clients/manage/collections/create-collections).

O Configuration Manager apenas configura as definições do Windows se ainda não existir um valor. Se precisar de configurar diferentes parâmetros para um único grupo de dispositivos, pode utilizar [política de grupo](#group-policy). Definições de visadas pela política de grupo têm precedência sobre as definições do Gestor de configuração.

Se direcionar os clientes do Configuration Manager com as definições de análise do Windows e análise de ambiente de trabalho, as definições para a análise de ambiente de trabalho têm prioridade. 

Quando configura o nível de dados de diagnóstico, defina o limite superior para o dispositivo. Por predefinição no Windows 10, versão 1803 e posterior, os usuários podem escolher definir um nível mais baixo. Pode controlar este comportamento ao utilizar a definição de política de grupo **interface de utilizador de participar da definição de telemetria de configurar**. Para obter mais informações, consulte [dados de diagnóstico de configurar o Windows na sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).



## <a name="next-steps"></a>Passos seguintes

Avance para o artigo seguinte para criar planos de implantação no ambiente de trabalho de análise.
> [!div class="nextstepaction"]  
> [Criar planos de implantação](/sccm/desktop-analytics/create-deployment-plans)  
