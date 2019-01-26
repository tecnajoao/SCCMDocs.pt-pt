---
title: Ativar a partilha de dados
titleSuffix: Configuration Manager
description: Um guia de referência para a partilha de dados de diagnóstico com a análise de ambiente de trabalho.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b009575f235b5aa5b2ecc2574eb672b4b17979e7
ms.sourcegitcommit: ad25a7bdd983c5a0e4c95bffdc61c9a1ebcbb765
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/26/2019
ms.locfileid: "55073394"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Ativar a partilha para a área de trabalho de análise de dados 

> [!Note]  
> Estas informações se relaciona com o serviço de pré-visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft faz não oferece quaisquer garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Para inscrever dispositivos para análise de ambiente de trabalho, eles precisam de enviar dados de diagnóstico para a Microsoft. Se o seu ambiente de utilizar um servidor proxy, utilize estas informações para ajudar a configurar o proxy. 


## <a name="diagnostic-data-levels"></a>Níveis de dados de diagnóstico

![Diagrama de níveis de dados de diagnóstico para análise de ambiente de trabalho](media/diagnostic-data-levels.png)

Quando integrar o Configuration Manager com a análise de ambiente de trabalho, também utilizá-lo para gerir o nível de dados de diagnóstico em dispositivos. A melhor experiência, utilize o Configuration Manager. 

A funcionalidade básica do ambiente de trabalho de análise funciona na **básica** nível de dados de diagnóstico. Não obter dados de utilização ou de estado de funcionamento para os seus dispositivos atualizados sem ativar a **avançado (limitado)** nível. A Microsoft recomenda que habilitar a **avançado (limitado)** nível de dados de diagnóstico. Para obter mais informações, consulte [Windows 10 melhorada eventos de dados de diagnóstico e de campos utilizados pelo Windows Analytics](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)). 

Para obter mais informações, consulte [privacidade de análise de ambiente de trabalho](/sccm/desktop-analytics/privacy).

Os seguintes artigos são também bons recursos para melhor compreender os níveis de dados de diagnóstico do Windows: 

- [Windows 10 e o GDPR para tomadores de decisão de TI](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configurar dados de diagnóstico do Windows na sua organização](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  


> [!Note]  
> No nível avançado (limitado), quando cada cliente faz a verificação completa inicial, envia cerca de 2 MB de dados para a cloud da Microsoft. O delta diário varia entre 250 400 KB por dia. 
> 
> A análise de delta diária ocorre no: 3:00 (hora local do dispositivo). Alguns eventos são enviados a primeira vez disponível ao longo do dia. Estes tempos não são configuráveis.
> 
> Para obter mais informações, consulte [dados de diagnóstico de configurar o Windows na sua organização](https://aka.ms/enterprisetelemetry).  



## <a name="endpoints"></a>Pontos Finais

Para ativar a partilha de dados, configure o servidor de proxy à lista de permissões os seguintes pontos finais:

| Ponto Final  | Função  |
|-----------|-----------|
| `https://v10c.events.data.microsoft.com` | Experiência do usuário conectado e o ponto final de componente de diagnóstico. Utilizado pelos dispositivos com o Windows 10, versão 1703 ou posterior, com cumulativa de 2018-09 atualizar ou posterior instalado. |
| `https://v10.events.data.microsoft.com` | Experiência do usuário conectado e o ponto final de componente de diagnóstico. Utilizado pelos dispositivos com Windows 10, versão 1803 ou posterior, _sem_ a atualização cumulativa de 2018-09 instalada. |
| `https://v10.vortex-win.data.microsoft.com` | Experiência do usuário conectado e o ponto final de componente de diagnóstico. Utilizado pelos dispositivos com Windows 10, versão 1709 ou anterior. |
| `https://vortex-win.data.microsoft.com` | Experiência do usuário conectado e o ponto final de componente de diagnóstico. Utilizado pelos dispositivos que executam o Windows 7 e Windows 8.1 |
| `https://settings-win.data.microsoft.com` | Permite que a atualização de compatibilidade enviar dados à Microsoft. |
| `http://adl.windows.com` | Permite que a atualização de compatibilidade receber os dados de compatibilidade mais recentes da Microsoft. |
| `https://watson.telemetry.microsoft.com` | Erro do Windows (WER) de relatórios. Necessárias para monitorizar o estado de funcionamento de implantação no Windows 10, versão 1803 ou anterior. |
| `https://umwatsonc.events.data.microsoft.com` | Erro do Windows (WER) de relatórios. É necessário para relatórios de estado de funcionamento do dispositivo no Windows 10, versão 1809 ou posterior. |
| `https://ceuswatcab01.blob.core.windows.net`<br> `https://ceuswatcab02.blob.core.windows.net`<br> `https://eaus2watcab01.blob.core.windows.net`<br> `https://eaus2watcab02.blob.core.windows.net`<br> `https://weus2watcab01.blob.core.windows.net`<br> `https://weus2watcab02.blob.core.windows.net` | Erro do Windows (WER) de relatórios. Necessárias para monitorizar o estado de funcionamento de implantação no Windows 10, versão 1809 ou posterior. |
| `https://www.msftncsi.com` | Erro do Windows (WER) de relatórios. É necessário para o estado de funcionamento do dispositivo verificar a conectividade. |
| `https://www.msftconnecttest.com` | Erro do Windows (WER) de relatórios. É necessário para o estado de funcionamento do dispositivo verificar a conectividade. | 
| `https://kmwatsonc.events.data.microsoft.com` | Análise online de pane. É necessário para relatórios de estado de funcionamento do dispositivo no Windows 10, versão 1809 ou posterior. |
| `https://oca.telemetry.microsoft.com`  | Online Crash Analysis (OCA). Necessárias para monitorizar o estado de funcionamento de implantação no Windows 10, versão 1803 ou anterior. |
| `https://login.live.com` | Pedido para fornecer uma identidade de dispositivo mais confiável para a análise de ambiente de trabalho. <br> <br>Para desativar o acesso de conta Microsoft do utilizador final, utilize definições de política em vez de bloquear este ponto final. Para obter mais informações, consulte [conta da Microsoft na empresa](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication). |
| `https://nexusrules.officeapps.live.com` | Utilizado para pedir os eventos de dinâmica de dados de diagnóstico de clientes do Office. Estes dados são útil para fins de desagregação e diagnóstico no portal do Analytics de ambiente de trabalho |
| `https://nexus.officeapps.live.com` | Utilizada pelos clientes do Office para enviar eventos de dados de diagnóstico a partir do Office 14, 15 do Office e versões do Office 16 anteriores ao 16.0.8702. É utilizado para recolher a utilização e fiabilidade sinaliza eventos para análise de ambiente de trabalho. |
| `https://office.pipe.aria.microsoft.com` | Utilizada pelos clientes do Office para enviar eventos de dados de diagnóstico a partir de aplicações do Office universal/modernos e versões de Win32 Office 16 posterior 16.0.8702. É utilizado para recolher a utilização e fiabilidade sinaliza eventos para análise de ambiente de trabalho. |


### <a name="ssl-inspection"></a>Inspeção do SSL

Para a privacidade e integridade dos dados, Windows verifica a existência de um certificado SSL da Microsoft ao se comunicar com os pontos de extremidade de dados de diagnóstico. Interceptação de SSL e a inspeção não são possíveis. Para utilizar a análise de ambiente de trabalho, exclua os pontos finais acima da inspeção do SSL.



## <a name="proxy-server-authentication"></a>Autenticação do servidor proxy

Certifique-se de que um proxy não bloqueia os dados de diagnóstico devido à autenticação. Se a sua organização utilizar autenticação do servidor proxy para tráfego de saída, utilize um ou mais das seguintes abordagens:

- **Ignorar** (recomendado): Configure os servidores de proxy para não exigir autenticação de proxy para o tráfego para os pontos finais de dados de diagnóstico. Esta opção é a solução mais abrangente. Funciona para todas as versões do Windows 10.  

- **Autenticação de proxy de usuário**: Configure dispositivos para utilizar com sessão iniciada no contexto do usuário para autenticação de proxy. Este método requer que os dispositivos a executar o Windows 10, versão 1703 ou posterior. Certifique-se de que os utilizadores têm permissão de proxy para alcançar os pontos de extremidade de dados de diagnóstico. Esta opção requer que os dispositivos têm de utilizadores de consola com permissões de proxy, pelo que não é possível utilizar este método com dispositivos sem periféricos.  

- **Autenticação de proxy do dispositivo**: 
    - Configure um servidor proxy de nível de sistema nos dispositivos.  
    - Configure estes dispositivos para utilizar a autenticação de proxy de saída com base no dispositivo.  
    - Configure servidores de proxy para permitir que as contas de computador acessar os pontos de extremidade de dados de diagnóstico.  



