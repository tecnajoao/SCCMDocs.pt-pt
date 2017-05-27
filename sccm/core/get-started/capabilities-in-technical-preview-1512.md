---
title: "Capacidades na pré-visualização técnica 1512 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1512."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e4d9e414-1346-4ed4-85d0-64d602b68731
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 5cf8d54fbaa98a75ac2a875a23a43b1d3e5be0dd
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1512-for-system-center-configuration-manager"></a>Funcionalidades de pré-visualização técnica 1512 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta as funcionalidades que estão disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1512. Pode instalar esta versão para atualizar e adicionar novas capacidades para o seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão da pré-visualização técnica, consulte o tópico de introdução, [pré-visualização técnica do System Center Configuration Manager](technical-preview.md), para se familiarizar com geral requisitos e limitações à utilização de uma pré-visualização técnica, como atualizar entre as versões e como fornecer comentários sobre as funcionalidades numa pré-visualização técnica.  

 Seguem-se novas funcionalidades que pode experimentar com esta versão.  

##  <a name="bkmk_devicehealth"></a> Device Health Attestation  
 A partir da 1512 de pré-visualização técnica, os administradores podem ver o estado de atestado de estado de funcionamento de dispositivo do Windows 10 na consola do Configuration Manager.  Esta funcionalidade está disponível para o Configuration Manager e do Configuration Manager com o Microsoft Intune. Atestado de estado de funcionamento do dispositivo permite ao administrador garantir que o cliente computadores ter BIOS fidedigna, TPM e as configurações de software de arranque. Para suportar atestado de estado de funcionamento do dispositivo, dispositivos cliente tem de executar Win10 com 2 TPM ativado. Atestado de estado de funcionamento do dispositivo apresenta o número de dispositivos ativados para cada um dos seguintes:  

-   Início antecipado antimalware  

-   BitLocker  

-   Arranque seguro  

-   Integridade do código  

A consola também apresenta as principais definições de atestado de estado de funcionamento de em falta com o número de dispositivos.  

Para pré-visualizar a vista de atestado de estado de funcionamento do dispositivo, na consola do Configuration Manager vá para o **monitorização** área de trabalho de, clique em **segurança** nó e, em seguida, clique em **atestado de estado de funcionamento**.  

##  <a name="bkmk_viewterms"></a>Na consola de monitorização para os termos e condições  
A partir da 1512 pré-visualização técnica, quando integrar o Configuration Manager com o Microsoft Intune, pode utilizar a consola do Configuration Manager para ver quais os utilizadores aceitaram os termos e condições configurados pelo seu departamento de TI e quais os utilizadores não têm.  

**Para ver informações de resumo:**  

-   Na consola do Configuration Manager, aceda a **monitorização** > **descrição geral** > **implementações** e selecione a implementação de termos e condições que pretende visualizar.  

**Para ver informações detalhadas:**  

1.  Na consola do Configuration Manager, aceda a **ativos e compatibilidade** > **descrição geral** > **definições de compatibilidade** > **termos e condições**e, em seguida, selecione os termos e condições que pretende visualizar.  

2.  Na parte inferior da consola, selecione o **implementações** separador, selecione a implementação e, em seguida, clique em **Ver estado.**  

##  <a name="bkmk_EPpolicy"></a>Foram introduzidos melhoramentos nas definições de política do Endpoint Protection  
A pré-visualização técnica do 1512 adicionámos as seguintes novas definições na política de proteção contra software maligno do Endpoint Protection:  

-   Proteção em tempo real: **Bloquear Aplicações Potencialmente Indesejáveis ao transferir e antes da instalação**  

    -   PUA (Potential Unwanted Applications) é uma classificação de ameaça baseada em reputação e identificação orientada por pesquisa. Normalmente, trata-se de bundlers de aplicações indesejadas ou das respetivas aplicações agregadas.  

    -   A definição de política de proteção está ativada (definido para "Sim") por predefinição. Quando ativada, esta definição bloqueia PUA no momento da transferência e da instalação. No entanto, pode excluir ficheiros ou pastas para satisfazer as necessidades específicas do ambiente de específicas.  

-   Analise as definições: **Analisar unidades de rede mapeadas quando executar uma análise completa**  

    -   Esta definição fornece maior granularidade ao administrador permitir análises a pedido dos ficheiros de rede sem o risco de análise sempre mapeado unidades de rede durante uma análise completa agendada.  

    -   A definição **analisar ficheiros de rede** primeiro tem de ser ativada ("yes") para estar disponível para configurar esta definição.  

    -   Por predefinição, esta definição é "Não" significado que uma análise completa não terão acesso unidades de rede mapeadas.  

-   Definições de submissão de exemplos de ficheiros de exemplo automática:  

     O motor de proteção contra software maligno pode solicitar exemplos de ficheiros para serem enviados para a Microsoft para análise adicional. Por predefinição, será sempre apresentado um aviso antes de enviar esses exemplos. Os administradores podem agora gerir as seguintes definições para configurar este comportamento:  

    -   Avançado: **Ativar automaticamente os ficheiros submissão de exemplos ajudar a determinar se certos itens detetados são maliciosos**:  Altere esta definição como "Sim" para ativar a submissão de ficheiro automática. Por predefinição, esta definição é "Não" que significa que a submissão de ficheiro automática está desativada e serão pedidos aos utilizadores antes de enviar exemplos.   (Esta definição primeiro foi introduzida no System Center 2012 R2 Configuration Manager SP1)  

    -   Avançado: **Permitir que os utilizadores modificar as definições de submissão de exemplos de ficheiros de exemplo automática**: Esta definição determina se um utilizador com direitos administrativos locais no dispositivo pode alterar a ficheiro definição da submissão automática na interface de cliente. Por predefinição, esta definição é "Não" que significa que só podem ser alteradas as definições a partir da consola do Configuration Manager e os administradores locais no dispositivo não é possível alterar esta configuração.  

         Por exemplo, o seguinte mostra a definição do Windows Defender no Windows 10 definido pelo administrador como ativada e o utilizador não tem permissão para modificá-lo:  

         ![TechRef &#95; WinDefender](../../core/get-started/media/TechRef_WinDefender.png "TechRef_WinDefender")  

    Além disso, existentes **excluir pastas e ficheiros** política definição na secção "Definições de exclusão" antimalware do endpoint protection é melhorada para permitir exclusões de dispositivo. Por exemplo, agora pode especificar o seguinte como exclusão: **\device\mvfs** (em Sistema de Ficheiros com Múltiplas Versões). A política não valida o caminho de dispositivo; a política do endpoint protection é fornecida para o motor de proteção contra software maligno no cliente que têm de ser capaz de interpretar a cadeia de dispositivo.  

**Pré-requisitos para utilizar políticas do Endpoint Protection:**  

Antes de poder utilizar as políticas do Endpoint Protection tem de instalar e gerir o cliente do Endpoint Protection utilizando as definições de cliente do Endpoint Protection. Isto é feito com o cliente do System Center Endpoint Protection para Windows 7, Windows 8, Windows 8.1 ou geridos Windows Defender para Windows 10. Consulte o artigo [Endpoint Protection no System Center Configuration Manager](../../protect/deploy-use/endpoint-protection.md).  

