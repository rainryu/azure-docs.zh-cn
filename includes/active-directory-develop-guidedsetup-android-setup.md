---
title: include 文件
description: include 文件
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mtillman
editor: ''
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: include
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/19/2018
ms.author: andret
ms.custom: include file
ms.openlocfilehash: 0ed42e4ace17db1e681152589cc46d82c26dddff
ms.sourcegitcommit: e2adef58c03b0a780173df2d988907b5cb809c82
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2018
---
## <a name="set-up-your-project"></a>设置项目

想要改为下载此示例的 Android Studio 项目？ [下载一个项目](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip)，并且在执行该项目之前跳到[配置步骤](#register-your-application)来配置代码示例。

### <a name="create-a-new-project"></a>创建新项目 
1.  打开 Android Studio，然后选择“文件” > “新建” > “新建项目”。
2.  为应用程序命名，然后选择“下一步”。
3.  选择“API 21 或更新版本 (Android 5.0)”，然后选择“下一步”。
4.  将“空活动”保留原样，选择“下一步”，然后选择“完成”。


### <a name="add-msal-to-your-project"></a>将 MSAL 添加到项目
1.  在 Android Studio 中，选择“Gradle 脚本” > “build.gradle (模块: 应用)”。
2.  在“依存关系”下，粘贴以下代码：

    ```ruby  
    compile ('com.microsoft.identity.client:msal:0.1.+') {
        exclude group: 'com.android.support', module: 'appcompat-v7'
    }
    compile 'com.android.volley:volley:1.0.0'
    ```

<!--start-collapse-->
### <a name="about-this-package"></a>关于此包

以上代码中的包安装 Microsoft 身份验证库。 MSAL 负责获取、缓存和刷新用于访问受 Azure Active Directory v2 终结点保护的 API 的用户令牌。
<!--end-collapse-->

## <a name="create-the-application-ui"></a>创建应用程序 UI

1. 转到“资源” > “布局”，然后打开 **activity_main.xml**。 
2. 将活动布局从 `android.support.constraint.ConstraintLayout` 或其他布局更改为 `LinearLayout`。
3. 将 `android:orientation="vertical"` 属性添加到 `LinearLayout` 节点。
4. 将以下代码粘贴到 `LinearLayout` 节点，替换当前内容：

    ```xml
    <TextView
        android:text="Welcome, "
        android:textColor="#3f3f3f"
        android:textSize="50px"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginLeft="10dp"
        android:layout_marginTop="15dp"
        android:id="@+id/welcome"
        android:visibility="invisible"/>

    <Button
        android:id="@+id/callGraph"
        android:text="Call Microsoft Graph"
        android:textColor="#FFFFFF"
        android:background="#00a1f1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="200dp"
        android:textAllCaps="false" />

    <TextView
        android:text="Getting Graph Data..."
        android:textColor="#3f3f3f"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginLeft="5dp"
        android:id="@+id/graphData"
        android:visibility="invisible"/>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="0dip"
        android:layout_weight="1"
        android:gravity="center|bottom"
        android:orientation="vertical" >

        <Button
            android:text="Sign Out"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginBottom="15dp"
            android:textColor="#FFFFFF"
            android:background="#00a1f1"
            android:textAllCaps="false"
            android:id="@+id/clearCache"
            android:visibility="invisible" />
    </LinearLayout>
    ```
