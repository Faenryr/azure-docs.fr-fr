---
title: "Didacticiel :Intégration d’Azure Active Directory à TalentLMS | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et TalentLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.translationtype: HT
ms.sourcegitcommit: 818f7756189ed4ceefdac9114a0b89ef9ee8fb7a
ms.openlocfilehash: f28d6fbfad9dae578a20db7218b7e3b174ed859c
ms.contentlocale: fr-fr
ms.lasthandoff: 07/14/2017

---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a>Didacticiel : Intégration d’Azure Active Directory à TalentLMS

Dans ce didacticiel, vous allez apprendre à intégrer TalentLMS à Azure Active Directory (Azure AD).

L’intégration de TalentLMS à Azure AD vous fait bénéficier des avantages suivants :

- Dans Azure AD, vous pouvez contrôler qui a accès à TalentLMS.
- Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à TalentLMS (via l’authentification unique) avec leur compte Azure AD.
- Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

Pour configurer l’intégration d’Azure AD à TalentLMS, vous avez besoin des éléments suivants :

- Un abonnement Azure AD
- Un abonnement TalentLMS pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :

1. Ajout de TalentLMS à partir de la galerie
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-talentlms-from-the-gallery"></a>Ajout de TalentLMS à partir de la galerie
Pour configurer l’intégration de TalentLMS à Azure AD, vous devez ajouter TalentLMS à partir de la galerie à votre liste d’applications SaaS gérées.

**Pour ajouter TalentLMS à partir de la galerie, procédez comme suit :**

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Active Directory][1]

2. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![Applications][2]
    
3. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche, entrez **TalentLMS**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. Dans le volet de résultats, sélectionnez **TalentLMS**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD auprès de TalentLMS avec un utilisateur de test appelé « Britta Simon ».

Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur TalentLMS équivalent dans Azure AD. En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur TalentLMS associé doit être établie.

Dans TalentLMS, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Nom d’utilisateur** pour établir la relation.

Pour configurer et tester l’authentification unique Azure AD auprès de TalentLMS, vous devez suivre les indications des sections suivantes :

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
3. **[Création d’un utilisateur de test TalentLMS](#creating-a-talentlms-test-user)** pour avoir dans TalentLMS un équivalent de Britta Simon lié à la représentation Azure AD de l’utilisateur.
4. **[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application TalentLMS.

**Pour configurer l’authentification unique Azure AD auprès de TalentLMS, procédez comme suit :**

1. Dans le Portail Azure, dans la page d’intégration de l’application **TalentLMS**, cliquez sur **Authentification unique**.

    ![Configurer l’authentification unique][4]

2. Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. Dans la section **Domaine et URL TalentLMS**, procédez comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    a. Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<tenant-name>.TalentLMSapp.com`

    b. Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `http://<tenant-name>.talentlms.com`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels. Pour obtenir ces valeurs, contactez l’[équipe de support client de TalentLMS](https://www.talentlms.com/contact). 
 
4. Dans la section **Certificat de signature SAML**, copiez la valeur **THUMBPRINT** du certificat.

    ![Configurer l’authentification unique](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. Dans la section **Configuration de TalentLMS**, cliquez sur **Configurer TalentLMS** pour ouvrir la fenêtre **Configurer l’authentification**. Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise TalentLMS en tant qu’administrateur.

8. Dans la section **Account & Settings (Compte et paramètres)**, cliquez sur l’onglet **Users (Utilisateurs)**.
   
    ![Compte et paramètres](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Compte et paramètres")

9. Cliquez sur **Single Sign-On (SSO)**.

10. Dans la section Single Sign-On, procédez comme suit :
   
    ![Authentification unique](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Authentification unique")   

    a. Dans la liste **SSO integration type (Type d’intégration SSO)**, sélectionnez **SAML 2.0**.

    b. Dans la zone de texte **Fournisseur d’identité**, collez la valeur de l’**ID d’entité SAML** copié à partir du portail Azure.
 
    c. Collez la valeur de l’**empreinte** à partir du portail Azure dans la zone de texte **Empreinte du certificat**.    

    d.  Dans la zone de texte **URL de connexion à distance**, collez la valeur de **URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.
 
    e. Dans la zone de texte **URL de déconnexion à distance**, collez la valeur de **URL de déconnexion** que vous avez copiée sur le portail Azure.

    f. Renseignez les informations suivantes : 

    * Dans la zone de texte **TargetedID**, tapez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`
     
    * Dans la zone de texte **Prénom**, tapez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`
    
    * Dans la zone de texte **Nom**, tapez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`
    
    * Dans la zone de texte **Email**, tapez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`
    
11. Cliquez sur **Enregistrer**.
 
> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.  Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas. Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.

![Créer un utilisateur Azure AD][100]

**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**

1. Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. Dans la boîte de dialogue **Utilisateur**, procédez comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    a. Dans la zone de texte **Nom**, entrez **BrittaSimon**.

    b. Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.

    c. Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-talentlms-test-user"></a>Création d’un utilisateur de test TalentLMS

Pour se connecter à TalentLMS, les utilisateurs d’Azure AD doivent être approvisionnés dans TalentLMS. Dans le cas de TalentLMS, l’approvisionnement est une tâche manuelle.

**Pour approvisionner un compte d’utilisateur, procédez comme suit :**

1. Connectez-vous à votre locataire **TalentLMS** .

2. Cliquez sur **Users (Utilisateurs)**, puis sur **Add User (Ajouter un utilisateur)**.

3. Dans la boîte de dialogue **Add user** , procédez comme suit :
   
    ![Ajouter un utilisateur](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Ajouter un utilisateur")  

    a. Dans la zone de texte **Prénom**, entrez le prénom de l’utilisateur, par exemple **Britta**.

    b. Dans la zone de texte **Nom**, tapez le nom de l’utilisateur, par exemple **Simon**.
 
    c. Dans la zone de texte **Email**, entrez l’adresse e-mail de l’utilisateur, par exemple **brittasimon@contoso.com**.

    d. Cliquez sur **Add User**.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre outil ou API de création de compte d’utilisateur, fourni par TalentLMS, pour approvisionner des comptes d’utilisateur AAD.
 

### <a name="assigning-the-azure-ad-test-user"></a>Affectation de l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à TalentLMS.

![Affecter des utilisateurs][200] 

**Pour affecter Britta Simon à TalentLMS, procédez comme suit :**

1. Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications, sélectionnez **TalentLMS**.

    ![Configurer l’authentification unique](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.

Lorsque vous cliquez sur la vignette TalentLMS dans le volet d’accès, vous devez être automatiquement connecté à votre application TalentLMS.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png


