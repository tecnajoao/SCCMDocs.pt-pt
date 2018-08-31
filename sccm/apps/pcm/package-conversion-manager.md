---
title: Gestor de conversão de pacotes
titleSuffix: Configuration Manager
description: Saiba mais sobre o Package Conversion Manager para converter pacotes em aplicações no Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f053fa73-c553-4522-a6b9-f885f23fe57c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7057084ba976408f189a0d4fbb96f176bc0c6656
ms.sourcegitcommit: 759098de944b8f7d5eedfc2bae2cb9a6ba15276f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/30/2018
ms.locfileid: "43297783"
---
# <a name="package-conversion-manager"></a>Gestor de conversão de pacotes

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!--1357861-->

A partir da versão 1806, o Gestor de conversão de pacotes ajuda-o a converter pacotes de legado do Configuration Manager em aplicativos. As aplicações têm vantagens adicionais, tais como as dependências, regras de requisitos, métodos de deteção e afinidade dispositivo / utilizador.

> [!Note]  
> Nesta versão do Configuration Manager, o Gestor de conversão de pacotes é uma funcionalidade de pré-lançamento. Para ativá-la, consulte [funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  

Uma aplicação do Configuration Manager contém arquivos e programas que implementar em dispositivos cliente. No entanto, ao contrário dos pacotes de legado e programas, um aplicativo fornece funcionalidades adicionais de centrada no utilizador. Por exemplo, uma aplicação pode conter tipos de implementação para uma instalação local de um pacote de software, um pacote de aplicação virtual ou uma versão da aplicação para dispositivos móveis.

Para obter mais informações, consulte os artigos seguintes: 
- [Introdução à gestão de aplicações](/sccm/apps/understand/introduction-to-application-management)  
- [Pacotes e programas](/sccm/apps/deploy-use/packages-and-programs)  

> [!Important]  
> Se instalou anteriormente uma versão mais antiga do Gestor de conversão de pacotes, primeiro desinstalá-lo antes de atualizar o seu site. Essa versão integrada não requer a instalação, mas poderá entrar em conflito com as versões existentes.  

Esta versão integrado do Gestor de conversão de pacotes funciona em pacotes no site de ramo atual do Configuration Manager. Não é uma ferramenta autônoma. Se tiver pacotes e programas numa versão mais antiga do Configuration Manager, primeiro migre os pacotes em seu site do ramo atual. Para obter mais informações, consulte [migrar dados entre hierarquias](/sccm/core/migration/migrate-data-between-hierarchies).



## <a name="planning"></a>Planejamento

Antes de começar a converter pacotes em aplicações, primeiro é desenvolva um plano. O processo seguinte é um plano de exemplo:

- [Definir um plano de conversão de pacotes detalhado](#bkmk_define)  

- [Selecionar e preparar pacotes para conversão](#bkmk_prepare)  

- [Selecione os pacotes de teste](#bkmk_test)  

- [Analisar, investigar e converter pacotes](#bkmk_analyze)  

- [Testar e implementar as aplicações](#bkmk_deploy)  


### <a name="bkmk_define"></a> Definir um plano de conversão de pacotes detalhado

Esta secção descreve dois planos de conversão de pacote de exemplo:  

- [Um ambiente de teste de elevada disponibilidade de recursos](#bkmk_define-high): Tem um ambiente de teste com os recursos, permissões e arquitetura para replicar completamente o seu ambiente de produção.  

- [Um ambiente de teste com recursos limitados](#bkmk_define-limited): Não tem um ambiente de teste que replica totalmente o seu ambiente de produção.  

Ajuste estes planos conforme necessário para outros problemas específicos ao seu ambiente.

#### <a name="bkmk_define-high"></a> Exemplo de plano para um ambiente de teste de elevada disponibilidade de recursos

O ambiente de teste tiver os recursos, permissões e arquitetura semelhante ao ambiente de produção. Utilizar o ambiente de teste para analisar eficientemente e converter todos os seus pacotes e, em seguida, testar todas as suas aplicações do Configuration Manager. Depois de concluir esse trabalho, tem de transferi-la para o ambiente de produção. 

Seu plano de conversão de pacotes pode ser semelhante aos passos seguintes:  

1.  Selecione os pacotes que pretende converter.  

2.  Migre os pacotes para conversão para o seu ambiente de teste.  

3.  Prepare os pacotes para conversão.  

4.  Selecione os pacotes de teste.  

5.  Analise, investigue e converta os pacotes de teste.  

6.  Teste as aplicações convertidas.  

7.  Analise e converta os restantes pacotes (não-test).  

8.  Exporte as aplicações de ambiente de teste. Importá-los no seu ambiente de produção.  

#### <a name="bkmk_define-limited"></a> Exemplo de plano para um ambiente de teste com recursos limitados

Ambiente de teste não tem os recursos, permissões e arquitetura semelhante ao ambiente de produção. Não é possível analisar, testar e converter todos os seus pacotes. Neste cenário, apenas analisar, investigar, converter e testar seus pacotes de teste. Em seguida, migre os pacotes restantes para o ambiente de produção para analisar e converter. 

Seu plano de conversão de pacotes pode ser semelhante aos passos seguintes:

1.  Selecione os pacotes que pretende converter.  

2.  Selecione os pacotes de teste.  

3.  Migre os pacotes de teste em seu ambiente de teste.  

4.  Prepare os pacotes de teste para conversão.  

5.  Analise, investigue e converta os pacotes de teste.  

6.  Teste as aplicações convertidas.  

7.  Exporte as aplicações de teste do ambiente de teste. Em seguida, importá-los no seu ambiente de produção.  

8.  Migrar os pacotes restantes no ambiente de produção e prepará-los para conversão.  

9.  Analise, investigue e converta os restantes pacotes no ambiente de produção.  

10. Disponibilize as restantes aplicações no ambiente de produção.  


### <a name="bkmk_prepare"></a> Selecionar e preparar pacotes para conversão

#### <a name="bkmk_prepare-select"></a> Selecione os pacotes que pretende converter

Nem todos os pacotes são adequados para serem convertidos em aplicações. Antes de começar a converter pacotes, identifique os pacotes que não ser convertidos. 

Os melhores tipos de pacotes para converter em aplicativos são aqueles que contêm software destinada ao utilizador, por exemplo:  

 - Ficheiros do Windows Installer (. msi e. msu)  

 - Programas do Microsoft Application Virtualization (App-V)  

 - Ficheiros executáveis do Windows (.exe)  

Os tipos de pacotes que são mantidos preferencialmente como pacotes e não convertidos em aplicações incluem:

 - Ferramentas de manutenção do sistema. Por exemplo, scripts ou utilitários de cópia de segurança.  

 - Pacotes de software que estão fora de suporte.

> [!Tip]  
> Depois de identificar os pacotes que não são adequados para serem convertidos em aplicações, movê-los para uma pasta separada na consola do Configuration Manager. Para criar uma pasta de pacote na consola do Configuration Manager:  
> - Com o botão direito a **pacotes** nó.  
> - Selecione **pastas**e, em seguida, selecione **criar pasta**.  
> - Introduza o nome da pasta, por exemplo `Not Converted`.  
> - Clique em **OK**.  

#### <a name="prepare-the-packages-for-conversion"></a>Prepare os pacotes para conversão

Para cada pacote que pretende converter, certifique-se de que estão em conformidade com as seguintes condições:  

 - A localização de ficheiros de origem é um caminho UNC completo, por exemplo `\\Server\Share\File`.  

 - Os arquivos do Windows Installer usar apenas um código de produto exclusiva.  


### <a name="bkmk_test"></a> Selecione os pacotes de teste

Se possível, o seu grupo de pacotes de teste deve incluir pacotes que cumpram os critérios seguintes:  

 - Pelo menos um pacote de teste com um Estado de preparação **automática**.  

 - Pelo menos um pacote de teste com um Estado de preparação **Manual**.  

O ideal é que seus pacotes de teste devem ser pacotes núcleo, por exemplo:  

 - Pacotes que conheça bem.  

 - Pacotes que são mais importantes para a sua organização.  

 - Pacotes que consiga testar facilmente.  

Identifique os pacotes que são adequados para teste. Em seguida, mova-os para uma pasta separada na consola do Configuration Manager.


### <a name="bkmk_analyze"></a> Analisar, investigar e converter pacotes

#### <a name="analyze-packages"></a>Analisar pacotes

Para analisar um pacote individual ou um pequeno grupo, utilize o Gestor de conversão de pacotes integrado na consola do Configuration Manager. Para obter mais informações, consulte [como analisar e converter pacotes](/sccm/apps/pcm/how-to-analyze-and-convert).  

> [!NOTE]  
> Consulte a **Status de conversão do pacote** nó a **monitorização** área de trabalho. Apresenta informações de resumo sobre os processos de análise e conversão.  

#### <a name="investigate-analysis-results"></a>Investigar os resultados da análise

Depois de analisar os pacotes de teste, investigue os pacotes com um Estado de preparação **Manual** ou **erro**. Determine as razões para terem esse Estado. Algumas razões comuns para um Estado de preparação **Manual** ou **erro** incluem:

 - O pacote não contém as informações necessárias para criar um método de deteção de um tipo de implementação de aplicação.  

 - O pacote não contém as informações necessárias para converter coleções para condições e requisitos globais.  

 - O pacote contém mais de um programa.  

 - O pacote é dependente de outro pacote que ainda não convertido para uma aplicação.  

Para obter mais informações, utilize os seguintes recursos:  

- Reveja as mensagens de erro e correções [referência técnica para mensagens de erro do Gestor de conversão de pacotes](/sccm/apps/pcm/error-messages)  

- Reveja o ficheiro de registo **PCMTrace.log**  

- [Resolver problemas relacionados com o Gestor de conversão de pacotes](/sccm/apps/pcm/troubleshoot-pcm)  

#### <a name="convert-the-packages"></a>Converta os pacotes

Para obter mais informações sobre como converter pacotes, consulte [como analisar e converter pacotes](/sccm/apps/pcm/how-to-analyze-and-convert).

> [!NOTE]  
> Consulte a **Status de conversão do pacote** nó a **monitorização** área de trabalho. Apresenta informações de resumo sobre os processos de análise e conversão.  


### <a name="bkmk_deploy"></a> Testar e implementar as aplicações

Teste as aplicações no seu ambiente de teste ou em seu ambiente de produção, de acordo com o plano de conversão de pacotes detalhado.



## <a name="recommendations"></a>Recomendações

- Utilize o **Status de conversão do pacote** nó a **monitorização** área de trabalho. Apresenta informações de resumo sobre os processos de análise e conversão.  

- Investigue os programas nos seus pacotes conhecidos como wrappers. Utilize o Gestor de conversão de pacotes Plug-in para converter suas funções a funcionalidade equivalente do Configuration Manager.  

- Certifique-se de que testa exaustivamente cada aplicação convertida antes de o implementar num ambiente de produção.  



## <a name="next-steps"></a>Passos seguintes

[Como analisar e converter pacotes](/sccm/apps/pcm/how-to-analyze-and-convert)