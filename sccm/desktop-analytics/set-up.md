---
title: Configurar a análise de ambiente de trabalho
titleSuffix: Configuration Manager
description: Um guia de procedimentos para configurar e inclusão à análise de ambiente de trabalho.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b014499e6be5dcd8fd600cc2c1e5cf22a3eb3a46
ms.sourcegitcommit: ad25a7bdd983c5a0e4c95bffdc61c9a1ebcbb765
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/26/2019
ms.locfileid: "55073628"
---
# <a name="how-to-set-up-desktop-analytics"></a>Como configurar a análise de ambiente de trabalho 

> [!Note]  
> Estas informações se relaciona com o serviço de pré-visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft faz não oferece quaisquer garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Utilize este procedimento para iniciar sessão no ambiente de trabalho de análise e configurá-lo na sua subscrição. Este procedimento é um processo de uso individual para configurar a análise de ambiente de trabalho para a sua organização.  



## <a name="initial-onboarding"></a>Integração inicial

1. Abra o [do portal da análise de ambiente de trabalho](https://aka.ms/m365aprod) na gestão de dispositivos do Microsoft 365 como um utilizador com **administrador de empresa** permissões. Selecione **iniciar**.  

2. Sobre o **aceitar o contrato de serviço** página, verifique o contrato de serviço e selecione **Accept**.  

3. Sobre o **confirmar a sua subscrição** , reveja a lista de necessárias licenças qualificadas. Mudar a definição para **Sim** junto a **tem uma das subscrições suportadas ou superiores**e, em seguida, selecione **seguinte**.  

4. Sobre o **conceder aos utilizadores acesso** página, análise de ambiente de trabalho previamente configura dois grupos de segurança no Azure Active Directory:  

    - **Os proprietários de área de trabalho**: Criar e gerir áreas de trabalho. Estas contas precisam de acesso de proprietário à subscrição do Azure.  

    - **Os contribuintes da área de trabalho**: Criar e gerir planos de implantação nesta área de trabalho. Não precisam de acesso do Azure adicional.  
  
   Para adicionar um utilizador a qualquer grupo, escreva o nome ou endereço de email no **introduza o nome ou endereço de e-mail** secção do grupo adequado. Quando terminar, selecione **seguinte**. 

5. Na página para **configurar a sua área de trabalho**:  

    - Para utilizar uma área de trabalho existente para a análise de ambiente de trabalho, selecione-a e continuar com a próxima etapa.  

        > [!Note]  
        > Se já estiver a utilizar o Windows Analytics, selecione essa mesma área de trabalho. Terá de reinscrever os dispositivos para análise de ambiente de trabalho que tiver inscrito anteriormente no Windows Analytics. 
        > 
        > Só pode ter uma área de trabalho de análise de ambiente de trabalho por inquilino do Azure AD. Dispositivos apenas podem enviar dados de diagnóstico para uma área de trabalho.   

    - Para criar uma área de trabalho para análise de ambiente de trabalho, selecione **adicionar área de trabalho**.  

        1. Introduza um **nome da área de trabalho**.<!--do we have any guidance for this name?-->  

        2. Selecione a lista pendente para **selecione o nome de subscrição do Azure para esta área de trabalho**e escolha a subscrição do Azure para esta área de trabalho.  

        3. Selecione o **região** na lista e, em seguida, selecione **Add**.  

6. Selecione uma área de trabalho nova ou existente e, em seguida, selecione **definido como área de trabalho de análise de ambiente de trabalho**.  Em seguida, selecione **continuar** no **confirmar e conceder acesso** caixa de diálogo.  

7. No separador do browser nova, escolha uma conta a utilizar para iniciar sessão. Selecione a opção para **consentir em nome da sua organização** e selecione **Accept**.  

    > [!Note]  
    > Este consentimento é atribuir a aplicação de MALogAnalyticsReader a função de leitor do Log Analytics para a área de trabalho. Esta função de aplicação é necessária ao ambiente de trabalho de análise. Para obter mais informações, consulte [função de aplicação MALogAnalyticsReader](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader).  

8. Na página para **configurar a sua área de trabalho**, selecione **próxima**.  

9. Sobre o **últimos passos** página, selecione **aceda à área de trabalho de análise**. 

O portal do Azure mostra a área de trabalho de análise **home page** página.



## <a name="create-app-for-configuration-manager"></a>Criar aplicação para o Configuration Manager

Crie uma aplicação no Azure AD para o Configuration Manager.

1. Na [portal do Azure](http://portal.azure.com), aceda à **Azure Active Directory**e selecione **registos das aplicações**. Em seguida, selecione **novo registo de aplicação**.  

2. Na **criar** painel, configure as seguintes definições:  

    - **Nome**: um nome exclusivo que identifica a aplicação, por exemplo: `Desktop-Analytics-Connection`  

    - **Tipo de aplicação**: **Aplicação Web / API**  

    - **Início de sessão no URL**: este valor não é utilizado pelo Configuration Manager, mas necessários pelo Azure AD. Introduza um URL exclusivo e válido, por exemplo: `https://configmgrapp`  
  
   Selecione **Criar**.  

3. Selecione a aplicação e tome nota da **ID da aplicação**. Este valor é um GUID que é utilizado para configurar a ligação do Configuration Manager.  

4. Selecione **configurações** na aplicação e, em seguida, selecione **chaves**. Na **palavras-passe** , digite um **descrição da chave**, especifique uma vencimento **duração**e, em seguida, selecione **guardar**. Copiar o **valor** da chave, que é utilizada para configurar a ligação do Configuration Manager. 

    > [!Important]  
    > Esta é a oportunidade única para copiar o valor da chave. Se não copiá-lo agora, terá de criar outra chave.  
    > 
    > Guarde o valor da chave numa localização segura.  

5. Na aplicação **configurações** painel, selecione **permissões obrigatórias**.  

    1. Sobre o **permissões obrigatórias** painel, selecione **Add**.  

    2. Na **adicionar acesso à API** painel, **selecionar uma API**.  

    3. Procure o **Microsserviço do Configuration Manager** API. Selecione-o e, em seguida, escolha **selecione**.  

    4. Sobre o **ativar o acesso ao** painel, selecione ambas as permissões de aplicação: **Escrever dados de coleta do CM** e **ler os dados de coleção do CM**. Em seguida, escolha **selecione**.  

    5. Sobre o **adicionar acesso à API** painel, selecione **feito**.  

6. Sobre o **permissões obrigatórias** página, selecione **conceder permissões**. Selecione **Sim**.  

7. Copie o ID de inquilino do Azure AD. Este valor é um GUID que é utilizado para configurar a ligação do Configuration Manager. Selecione **do Azure Active Directory** no menu principal e, em seguida, selecione **propriedades**. Copiar o **ID de diretório** valor.  



## <a name="next-steps"></a>Passos seguintes

Avance para o artigo seguinte para ligar o Configuration Manager com a análise de ambiente de trabalho.
> [!div class="nextstepaction"]  
> [Ligar o Configuration Manager](/sccm/desktop-analytics/connect-configmgr)  
