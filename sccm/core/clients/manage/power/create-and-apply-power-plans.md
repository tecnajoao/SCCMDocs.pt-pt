---
title: Criar e aplicar esquemas de energia
titleSuffix: Configuration Manager
description: Criar e aplicar esquemas de energia no System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 738eddaa-52e2-467f-b453-821ef2884d47
caps.latest.revision: "6"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: ec32a0b1591fffe77ace91f478e03302f429c957
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-create-and-apply-power-plans-in-system-center-configuration-manager"></a>Como criar e aplicar esquemas de energia no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Gestão de energia no System Center Configuration Manager permite-lhe aplicar esquemas de energia que são fornecidas com o Configuration Manager para coleções de computadores na sua hierarquia ou criar os seus próprios esquemas de energia personalizados. Utilize o procedimento neste tópico para aplicar um esquema de energia incorporado ou personalizado a computadores.  

> [!IMPORTANT]  
>  Só pode aplicar esquemas de energia do Configuration Manager para coleções de dispositivos.  

 Se um computador for membro de várias coleções, em que cada aplica esquemas de energia diferentes, serão executadas as seguintes ações:  

-   Esquema de energia: Se forem aplicados vários valores para definições de energia para um computador, é utilizado o valor menos restritivo.  

-   Hora de reativação: Se forem aplicadas várias horas de reativação a um computador de secretária, será utilizada a hora mais próxima da meia-noite.  

 Utilize o relatório **Computadores com Vários Esquemas de Energia** para apresentar todos os computadores com vários esquemas de energia aplicados aos mesmos. Isto pode ajudar a detetar os computadores que têm conflitos de energia. Para obter mais informações sobre os relatórios de gestão de energia, consulte [como monitorizar e planear a gestão de energia no System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

> [!IMPORTANT]  
>  Definições de energia configuradas utilizando a política de grupo do Windows irão substituir as definições configuradas pela gestão de energia do Configuration Manager.  

 Utilize o procedimento seguinte para criar e aplicar um esquema de energia do Configuration Manager.  

### <a name="to-create-and-apply-a-power-plan"></a>Para criar e aplicar um esquema de energia  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , clique em **Coleções de Dispositivos**.  

3.  Na lista **Coleções de Dispositivos** , clique na coleção para a qual pretende aplicar as definições de gestão de energia e, em seguida, no separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

4.  No **gestão de energia** separador do *< nome da coleção\>***propriedades** caixa de diálogo, selecione **especificar definições de gestão de energia para esta coleção**.  

    > [!NOTE]  
    >  Também pode clicar em **Procurar** e, em seguida, copiar as definições de gestão de energia de uma determinada coleção para a coleção selecionada.  

5.  Nos campos **Início** e **Fim** , especifique a hora de início e de fim das horas de pico (ou horário comercial).  

6.  Ative a **Hora de reativação (computadores de secretária)** para especificar a hora em que um computador de secretária será reativado da suspensão ou da hibernação para instalar atualizações agendadas ou instalar software.  

    > [!IMPORTANT]  
    >  A gestão de energia utiliza a funcionalidade de hora de reativação interna do Windows para reativar os computadores do modo de suspensão ou hibernação. As definições de hora de reativação não se aplicam aos computadores portáteis, de modo a evitar cenários em que poderão ser reativados quando não estão ligados à corrente. A hora de reativação é aleatória e os computadores serão reativados durante um período de uma hora a partir da hora de reativação especificada.  

7.  Se pretender configurar um esquema de energia personalizada para as horas de pico (ou horário comercial), selecione **Pico Personalizado (ConfigMgr)** a partir da lista pendente **Esquema de pico** e clique em **Editar**. Se pretender configurar um esquema de energia para as horas fora de pico (ou horário não comercial), selecione **Fora de Pico Personalizado (ConfigMgr)** a partir do **Esquema fora de pico** na lista pendente e, em seguida, clique em **Editar**.  

    > [!NOTE]  
    >  Pode utilizar o relatório **Atividade do Computador** para o ajudar a decidir as agendas a utilizar para as horas de pico e fora de pico quando aplicar os esquemas de energia a coleções de computadores. Para obter mais informações, consulte [como monitorizar e planear a gestão de energia no System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

     Também pode selecionar a partir de esquemas de energia incorporados, **Equilibrado (ConfigMgr)**, **Elevado Desempenho (ConfigMgr)** e **Poupança de Energia (ConfigMgr)**, e clicar em **Ver** para apresentar as propriedades de cada esquema de energia.  

    > [!NOTE]  
    >  Não é possível modificar os esquemas de energia incorporados.  

8.  No *< nome do plano de energia\>***propriedades** diálogo caixa, configure as seguintes definições:  

    -   **Nome:** Especifique um nome para este esquema de energia ou utilize o valor predefinido fornecido.  

    -   **Descrição:**  Especifique uma descrição para este esquema de energia ou utilize o valor predefinido fornecido.  

    -   **Especifique as propriedades deste esquema de energia:** Configure as propriedades do plano de energia. Para desativar uma propriedade, desmarque a respetiva caixa de verificação. Para obter informações sobre as definições disponíveis, consulte [Available power management plan settings](#BKMK_Plans) neste tópico.  

        > [!IMPORTANT]  
        >  As definições ativadas são aplicadas nos computadores quando o esquema de energia é aplicado. Se desmarcar a caixa de verificação de uma definição de energia, o valor no computador cliente não é alterado quando o esquema de energia é aplicado. Desmarcar uma caixa de verificação não restaura a definição de energia para o valor anterior antes de ter sido aplicado um esquema de energia.  

9. Clique em **OK** para fechar o *< nome do plano de energia\>***propriedades** caixa de diálogo.  

10. Clique em **OK** para fechar o *< nome da coleção\>***definições** caixa de diálogo e para aplicar o esquema de energia.  

##  <a name="BKMK_Plans"></a> Available power management plan settings  
 A tabela seguinte lista as definições de gestão de energia disponíveis no Configuration Manager. Pode configurar diferentes definições para quando o computador está ligado à corrente ou em execução com energia da bateria. Dependendo da versão do Windows que estiver a utilizar, algumas definições poderão não ser configuráveis.  

> [!NOTE]  
>  As definições de energia que não configurar irão manter o respetivo valor atual nos computadores cliente.  

|Nome|Descrição|  
|----------|-----------------|  
|**Desligar o ecrã após (minutos)**|Especifica o período de tempo, em minutos, que o computador tem de estar inativo antes de o ecrã ser desativado. Especifique o valor **0** se não pretender que a gestão de energia desative o ecrã.|  
|**Suspensão após (minutos)**|Especifica o período de tempo, em minutos, que o computador tem de estar inativo antes de ser suspenso. Especifique um valor de **0** se não pretender que a gestão de energia suspenda o computador.|  
|**Pedir uma palavra-passe ao reativar**|A **Sim** ou **não** valor Especifica se uma palavra-passe é necessária para desbloquear o computador quando é reativado da suspensão.|  
|**Ação do botão de energia**|Especifica a ação que é executada quando é premido o botão de energia do computador. Especifica a ação que ocorre quando o utilizador fecha a tampa de um computador portátil. Os valores possíveis **fazer nada**, **no modo de suspensão**, **hibernação**, e **Encerrar**.|  
|**Botão de energia do menu Iniciar**|Especifica a ação que ocorre quando prime o botão de energia do menu **Iniciar** do computador. Especifica a ação que ocorre quando o utilizador fecha a tampa de um computador portátil. Os valores possíveis **no modo de suspensão**, **hibernação**, e **Encerrar**.|  
|**Ação do botão de suspensão**|Especifica a ação que ocorre quando prime o botão **Suspender** do computador. Especifica a ação que ocorre quando o utilizador fecha a tampa de um computador portátil. Os valores possíveis **fazer nada**, **no modo de suspensão**, **hibernação**, e **Encerrar**.|  
|**Ação de fechar a tampa**|Especifica a ação que ocorre quando o utilizador fecha a tampa de um computador portátil. Os valores possíveis **fazer nada**, **no modo de suspensão**, **hibernação**, e **Encerrar**.|  
|**Desligar o disco rígido após (minutos)**|Especifica o período de tempo, em minutos, que o disco rígido do computador tem de estar inativo antes de ser desligado. Especifique um valor de **0** se não pretender que a gestão de energia desative o disco rígido do computador.|  
|**Hibernar após (minutos)**|Especifica o período de tempo, em minutos, que o computador tem de estar inativo antes de ser hibernado. Especifique um valor de **0** se não pretender que a gestão de energia hiberne o computador.|  
|**Ação de pouca bateria**|Especifica a ação que ocorre quando a bateria do computador atinge o nível de notificação de bateria baixa especificado. Especifica a ação que ocorre quando o utilizador fecha a tampa de um computador portátil. Os valores possíveis **fazer nada**, **no modo de suspensão**, **hibernação**, e **Encerrar**.|  
|**Ação de bateria crítica**|Especifica a ação que é tomada quando a bateria do computador atinge o nível de notificação de bateria crítica especificado. Especifica a ação que ocorre quando o utilizador fecha a tampa de um computador portátil. Os valores possíveis incluem **no modo de suspensão**, **hibernação**, e **Encerrar**.|  
|**Permitir suspensão híbrida**|Selecionar o **no** ou **desativar** valor Especifica se o Windows guarda um ficheiro de hibernação quando em suspensão, que podem ser utilizados para restaurar o estado do computador em caso de perda de energia enquanto entrou em suspensão.<br /><br /> A suspensão híbrida foi concebida para computadores de secretária e, por predefinição, não está ativada nos computadores portáteis. Em computadores que executem o Windows 7, ativar o modo de suspensão híbrida desativa a funcionalidade de hibernação.|  
|**Permitir ação de estado de espera durante a suspensão**|Selecionar o **no** ou **desativar** valor permite que o computador esteja no modo de espera, ainda consome alguma energia, mas permite que o computador seja reativado mais rapidamente. Se esta definição estiver definida como **Desativada**, o computador só pode hibernar ou ser desligado.|  
|**Inatividade necessária para suspender (%)**|Especifica a percentagem de tempo inativo no tempo de processador do computador necessária para o computador entrar no modo de suspensão. Para computadores com o Windows 7, este valor é sempre definido como **0**.|  
|**Ativar o temporizador de reativação do Windows para computadores de secretária**|Selecionar o **ativar** ou **desativar** valor pode ativar o temporizador incorporado do Windows ser utilizado pela gestão de energia para reativar um computador de secretária. Quando um computador de secretária é reativado com o temporizador de reativação do Windows, permanecerá ativo durante dez minutos por predefinição, para ter tempo para instalar atualizações ou receber políticas.<br /><br /> Os temporizadores de reativação não são suportados em computadores portáteis para impedir cenários em que poderão ser reativados quando não estão ligados.|  
