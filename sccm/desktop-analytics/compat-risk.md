---
title: Risco de compatibilidade para aplicações do Windows
titleSuffix: Configuration Manager
description: Saiba mais sobre os riscos de compatibilidade para aplicações do Windows no ambiente de trabalho de análise.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8deaa8eef49b2d4792146cb47ecdf094eaed4eac
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123769"
---
# <a name="compatibility-risk-for-windows-apps-in-desktop-analytics"></a>Risco de compatibilidade de aplicações do Windows no ambiente de trabalho de análise 

> [!Note]  
> Estas informações se relaciona com o serviço de pré-visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft faz não oferece quaisquer garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Avaliações de atualização do Windows Analytics eram genéricas, por exemplo: Atenção necessária ou a correção disponível. Ela não fornece qualquer indicador visual sobre como atribuir aplicações com problemas ou atualizar informações. Análise de área de trabalho substitui esse recurso com **riscos de compatibilidade**. Análise de área de trabalho mostra a avaliação de riscos de aplicações para aplicações apenas na vista de implementação para um cenário de pré-atualização. Ele categoriza as aplicações com base em informações que Microsoft obtém a partir das máquinas incluídas num plano de implementação atual.

Análise de área de trabalho utiliza as seguintes categorias de riscos de compatibilidade:

- **Baixa**: O serviço foi encontrado nenhum sinais colocar esta aplicação em risco para um Windows atualizar. É muito provável que funcione SO de destino como-é.  

- **Médio**: Análise indica que o aplicativo pode ter com deficiências visuais funcionalidade, embora a atualização é provavelmente possível.  

- **Alta**: O aplicativo é quase certo que falhar durante ou após a atualização. Ele poderá ter uma remediação.  

- **Desconhecido**: A aplicação não foi avaliada pelo analisador de estado de funcionamento da aplicação. Existem não existem outras informações tais como *problemas conhecidos do MS* ou *pronto para Windows*.  



## <a name="risk-assessment-engine"></a>Motor de avaliação de risco

Existem várias fontes que o analisador de estado de funcionamento da aplicação utiliza para gerar a classificação de risco.

![Diagrama de áreas de motor de avaliação de riscos de analisador de estado de funcionamento da aplicação](media/aha-risk-assessment-engine.png)


### <a name="ms-known-issues"></a>Problemas conhecidos do MS

O analisador de estado de funcionamento da aplicação examina o banco de dados da compatibilidade de aplicações Microsoft para os problemas conhecidos. Ele usa esse banco de dados para determinar qualquer blocos existentes de compatibilidade para as aplicações disponíveis ao público da Microsoft ou de outros editores. Esta verificação aplica-se apenas para o SO de destino para o plano de implantação que selecionar.


### <a name="ready-for-windows"></a>Pronto para Windows

O arquivo de dados pronto para o Windows verifica a existência de blocos de compatibilidade num dispositivo. Ele também correlaciona os dados de outros clientes relatórios de aplicações semelhante. A Microsoft utiliza dados de outros dispositivos semelhantes em que esta aplicação reportado sem problemas. 


### <a name="app-health-analyzer-signals-for-compatibility-assessment"></a>Analisador de estado de funcionamento da aplicação sinaliza para avaliação de compatibilidade

Utilize o Kit de ferramentas de analisador de estado de funcionamento da aplicação para recolher sinais adicionais para compatibilidade de aplicativos. Para obter mais informações, consulte [analisador de estado de funcionamento da aplicação](/sccm/desktop-analytics/app-health-analyzer). 

Os sinais seguintes estão atualmente disponíveis:

#### <a name="adopted-version-available"></a>Versão adotado disponível
Existe outra versão desta aplicação que está altamente adotada por outros clientes. Este sinal utiliza dados de pronto para Windows. Se existirem quaisquer bloqueadores de atualização com a sua versão atual, considere implementar a versão alternativa em vez disso.

#### <a name="16-bit"></a>16-bit
Remover todos os componentes de 16 bits de aplicativos e substituir por equivalentes de 32 bits ou 64 bits. Para obter mais informações, consulte [o Windows Vista e a história do desenvolvedor do Windows Server 2008: Manual de compatibilidade de aplicativos](https://msdn.microsoft.com/library/aa480152.aspx). 

A outra opção consiste em ativar o da máquina DOS Virtual NT (NTVDM) para o suporte no Windows 10.

#### <a name="requires-admin-privileges"></a>Requer privilégios de administrador
A aplicação requer o usuário tenha acesso administrativo para o dispositivo. Utilize um manifesto de aplicação para estas aplicações que requerem permissões de administrador. Para obter mais informações, consulte [criar e incorporar um manifesto de aplicativo](https://msdn.microsoft.com/library/bb756929.aspx).
<!--Is this a better, more current link? https://docs.microsoft.com/windows/desktop/sbscs/application-manifests-->

Análise de área de trabalho recomenda a aplicação para o teste do piloto. Isso deve funcionar para o piloto, mas encontrará quaisquer regressões. 

#### <a name="java-dependency"></a>Dependência de Java
Muitas aplicações de Java baseiam-se num instalado em separado Java Runtime Environment (JRE). Enquanto as versões mais antigas do JRE podem continuar a trabalhar no Windows 10, o Oracle suporta apenas as versões mais recentes do JRE. Usar um JRE de sem suporte mais antigo pode ter vulnerabilidades de segurança. Verifique se a sua aplicação é executada em versões mais recentes do JRE.

#### <a name="not-dpi-aware"></a>Não-DPI
A aplicação pode ter problemas de exibição com resoluções de tela avançada no Windows 10. Utilize um manifesto de aplicação para evitar quaisquer problemas com essas resoluções. Para obter mais informações, consulte [manifestos de aplicativo](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests).

Análise de área de trabalho recomenda a aplicação para o teste do piloto. Isso deve funcionar para o piloto, mas encontrará quaisquer regressões. 

#### <a name="visual-basic-version-6-vb6"></a>Versão 6 (VB6) do Visual Basic
Análise de área de trabalho recomenda a aplicação para o teste do piloto. Aplicativos de VB6, muitas vezes, são compatíveis. Se a aplicação regresses durante o piloto devido a quaisquer dependências adicionais ou widgets, em seguida, deve atualizar a aplicação para o Visual Basic .NET 

#### <a name="os-version-dependency"></a>Dependência de versão do SO
Considere redeveloping a aplicação para utilizar a API de auxiliares de versão ou a aplicação de destino com o Windows 10 do manifesto.

Análise de área de trabalho recomenda a aplicação para o teste do piloto. Isso deve funcionar para o piloto, mas encontrará quaisquer regressões. 

#### <a name="silverlight-framework"></a>Framework do Silverlight
A Microsoft recomenda que aplicações não baseadas no browser não usar o Silverlight. A data de fim do suporte para o Silverlight 5 é de 2021 de Outubro. 

Navegadores da web mais atuais não suportam o Silverlight.

| Browser | Suporte |
|---------|---------|
| Google Chrome | Fim do suporte: Setembro de 2015 |
| Firefox | Fim do suporte: Março de 2017 |
| Microsoft Edge | Plug-in não disponível |

Análise de área de trabalho recomenda a aplicação para o teste do piloto. Isso deve funcionar para o piloto, mas encontrará quaisquer regressões. 

#### <a name="net-framework-1011"></a>.NET framework 1.0/1.1 
O .NET framework versão 1.0 não é suportada no Windows 10. Versão 1.1 não é compatível no Windows 10. Se a aplicação de um editor de terceiros, contacte o fornecedor para solicitar uma versão que está em conformidade com o Windows 10. Caso contrário, redevelop a aplicação para utilizar uma versão suportada do .NET.

#### <a name="net-framework-2030"></a>.NET framework 2.0/3.0 
.NET 2.0 e 3,5 estruturas são suportadas no Windows 10. Terá de ativar a funcionalidade do Windows. Para obter mais informações, consulte [instalar o .NET Framework 3.5 no Windows 10](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10).

#### <a name="ui-access"></a>Acesso de interface do Usuário
Aplicações com acesso à IU podem ignorar os níveis de controle de interface de utilizador para orientar o privilégio de entrada superior ao windows na área de trabalho. Só utilize esta definição para aplicativos de apoio compatíveis com tecnologia de interface de utilizador.

Se não estiver a utilizar funcionalidades de acessibilidade na sua aplicação, defina o sinalizador de acesso de interface do Usuário no manifesto do aplicativo como false. Para obter mais informações, consulte [criar e incorporar um manifesto de aplicativo](https://msdn.microsoft.com/library/bb756929.aspx).

#### <a name="driver-dependency"></a>Dependência de Driver
A aplicação é dependente de um driver. Análise de área de trabalho recomenda a aplicação para o teste do piloto. Isso deve funcionar para o piloto, mas encontrará quaisquer regressões. Se tiver quaisquer problemas, contacte o publicador para solicitar uma versão que está em conformidade com o Windows 10.



## <a name="app-confidence-simulation-for-a-sample-population"></a>Simulação de confiança de aplicação para uma população de exemplo

Os gráficos seguintes são de um estudo de caso do exemplo. Estes dados realça a utilização do analisador de estado de funcionamento de aplicações com análises de ambiente de trabalho para adotar uma abordagem orientada por dados para a validação de aplicação. Esta abordagem pode ajudar a reduzir o tempo e esforço em testar seus aplicativos durante a atualização do Windows 10.

Estes dados mostram as métricas de confiança para 60 dispositivos com 899 aplicações, incluindo aplicações de linha de negócio.

![Antes e depois gráficos que mostram a confiança de aplicações](media/aha-app-confidence-simulation.png)
