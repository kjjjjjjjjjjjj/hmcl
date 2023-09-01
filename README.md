# hmcl@@ -71,6 +71,7 @@ public static void main(String[] args) {
        Logging.start(Metadata.HMCL_DIRECTORY.resolve("logs"));	        Logging.start(Metadata.HMCL_DIRECTORY.resolve("logs"));


        checkJavaFX();	        checkJavaFX();
        verifyJavaFX();
        detectFractureiser();	        detectFractureiser();


        Launcher.main(args);	        Launcher.main(args);
@@ -112,6 +113,19 @@ private static void checkJavaFX() {
        }	        }
    }	    }


    /**
     * Check if JavaFX exists but is incomplete
     */
    private static void verifyJavaFX() {
        try {
            Class.forName("javafx.beans.binding.Binding"); // javafx.base
            Class.forName("javafx.stage.Stage");           // javafx.graphics
            Class.forName("javafx.scene.control.Skin");    // javafx.controls
        } catch (Exception e) {
            showErrorAndExit(i18n("fatal.javafx.incomplete"));
        }
    }

    /**	    /**
     * Indicates that a fatal error has occurred, and that the application cannot start.	     * Indicates that a fatal error has occurred, and that the application cannot start.
     */	     */
  2 changes: 2 additions & 0 deletions2  
HMCL/src/main/resources/assets/lang/I18N.properties
@@ -357,6 +357,8 @@ Please use antivirus software to perform a full scan immediately, and then chang
fatal.javafx.incompatible=Missing JavaFX environment.\n\	fatal.javafx.incompatible=Missing JavaFX environment.\n\
HMCL cannot automatically install JavaFX under Java versions below 11.\n\	HMCL cannot automatically install JavaFX under Java versions below 11.\n\
Please update your Java to version 11 or higher.	Please update your Java to version 11 or higher.
fatal.javafx.incomplete=The JavaFX environment is incomplete.\n\
Please try replacing your Java or reinstalling OpenJFX.
fatal.javafx.missing=Missing JavaFX environment.\n\	fatal.javafx.missing=Missing JavaFX environment.\n\
If you are using Java 11 or higher, please downgrade it to Oracle JRE 8 (java.com), or install BellSoft Liberica Full JRE (bell-sw.com/pages/downloads/?package\=jre-full).\n\	If you are using Java 11 or higher, please downgrade it to Oracle JRE 8 (java.com), or install BellSoft Liberica Full JRE (bell-sw.com/pages/downloads/?package\=jre-full).\n\
Or, if you are using OpenJDK distributions, please make sure it has OpenJFX included.	Or, if you are using OpenJDK distributions, please make sure it has OpenJFX included.
  3 changes: 2 additions & 1 deletion3  
HMCL/src/main/resources/assets/lang/I18N_zh.properties
@@ -356,7 +356,8 @@ extension.sh=Bash 指令碼


fatal.fractureiser=Hello Minecraft! Launcher 檢測到你的電腦被 Fractureiser 病毒感染，存在嚴重安全問題。\n請立即使用殺毒軟體進行全盤查殺，隨後修改你在此電腦上登入過的所有帳號的密碼。	fatal.fractureiser=Hello Minecraft! Launcher 檢測到你的電腦被 Fractureiser 病毒感染，存在嚴重安全問題。\n請立即使用殺毒軟體進行全盤查殺，隨後修改你在此電腦上登入過的所有帳號的密碼。
fatal.javafx.incompatible=缺少 JavaFX 運行環境。\nHMCL 無法在低於 Java 11 的 Java 環境上自行補全 JavaFX 運行環境，請更新到 Java 11 或更高版本。	fatal.javafx.incompatible=缺少 JavaFX 運行環境。\nHMCL 無法在低於 Java 11 的 Java 環境上自行補全 JavaFX 運行環境，請更新到 Java 11 或更高版本。
fatal.javafx.missing=找不到 JavaFX，	fatal.javafx.incomplete=JavaFX 運行環境不完整，請嘗試更換你的 Java 或者重新安裝 OpenJFX。
fatal.javafx.missing=缺少 JavaFX 運行環境，請使用包含 OpenJFX 的 Java 運行環境啟動 Hello Minecraft! Launcher。\n你可以訪問 https://docs.hmcl.net/help.html 頁面尋求幫助。
fatal.config_change_owner_root=你正在使用 root 帳戶啟動 Hello Minecraft! Launcher，這可能導致你未來無法使用其他帳戶正常啟動 Hello Minecraft! Launcher。\n是否繼續啟動？	fatal.config_change_owner_root=你正在使用 root 帳戶啟動 Hello Minecraft! Launcher，這可能導致你未來無法使用其他帳戶正常啟動 Hello Minecraft! Launcher。\n是否繼續啟動？
fatal.config_in_temp_dir=你正在臨時資料夾中啟動 Hello Minecraft! Launcher，你的設定和遊戲數據可能會遺失，建議將 HMCL 移動至其他位置再啟動。\n是否繼續啟動？	fatal.config_in_temp_dir=你正在臨時資料夾中啟動 Hello Minecraft! Launcher，你的設定和遊戲數據可能會遺失，建議將 HMCL 移動至其他位置再啟動。\n是否繼續啟動？
fatal.config_loading_failure=Hello Minecraft! Launcher 無法載入設定檔案。\n請確保 Hello Minecraft! Launcher 對 "%s" 目錄及該目錄下的檔案擁有讀寫權限。	fatal.config_loading_failure=Hello Minecraft! Launcher 無法載入設定檔案。\n請確保 Hello Minecraft! Launcher 對 "%s" 目錄及該目錄下的檔案擁有讀寫權限。
  1 change: 1 addition & 0 deletions1  
HMCL/src/main/resources/assets/lang/I18N_zh_CN.properties
@@ -358,6 +358,7 @@ extension.sh=Bash 脚本


fatal.fractureiser=Hello Minecraft! Launcher 检测到你的电脑被 Fractureiser 病毒感染，存在严重安全问题。\n请立即使用杀毒软件进行全盘查杀，随后修改你在此电脑上登陆过的所有账户的密码。\n你可以访问 https://docs.hmcl.net/help.html 页面寻求帮助。	fatal.fractureiser=Hello Minecraft! Launcher 检测到你的电脑被 Fractureiser 病毒感染，存在严重安全问题。\n请立即使用杀毒软件进行全盘查杀，随后修改你在此电脑上登陆过的所有账户的密码。\n你可以访问 https://docs.hmcl.net/help.html 页面寻求帮助。
fatal.javafx.incompatible=缺少 JavaFX 运行环境。\nHello Minecraft! Launcher 无法在低于 Java 11 的 Java 环境上自行补全 JavaFX 运行环境，请更新到 Java 11 或更高版本。\n你可以访问 https://docs.hmcl.net/help.html 页面寻求帮助。	fatal.javafx.incompatible=缺少 JavaFX 运行环境。\nHello Minecraft! Launcher 无法在低于 Java 11 的 Java 环境上自行补全 JavaFX 运行环境，请更新到 Java 11 或更高版本。\n你可以访问 https://docs.hmcl.net/help.html 页面寻求帮助。
fatal.javafx.incomplete=JavaFX 运行环境不完整，请尝试更换你的 Java 或者重新安装 OpenJFX。
fatal.javafx.missing=缺少 JavaFX 运行环境，请使用包含 OpenJFX 的 Java 运行环境启动 Hello Minecraft! Launcher。\n你可以访问 https://docs.hmcl.net/help.html 页面寻求帮助。	fatal.javafx.missing=缺少 JavaFX 运行环境，请使用包含 OpenJFX 的 Java 运行环境启动 Hello Minecraft! Launcher。\n你可以访问 https://docs.hmcl.net/help.html 页面寻求帮助。
fatal.config_change_owner_root=你正在使用 root 账户启动 Hello Minecraft! Launcher, 这可能导致你未来无法正常使用其他账户正常启动 Hello Minecraft! Launcher。\n你可以访问 https://docs.hmcl.net/help.html 页面寻求帮助。\n是否继续启动？	fatal.config_change_owner_root=你正在使用 root 账户启动 Hello Minecraft! Launcher, 这可能导致你未来无法正常使用其他账户正常启动 Hello Minecraft! Launcher。\n你可以访问 https://docs.hmcl.net/help.html 页面寻求帮助。\n是否继续启动？
fatal.config_in_temp_dir=你正在临时文件夹中启动 Hello Minecraft! Launcher, 你的设置和游戏数据可能会丢失，建议将 HMCL 移动至其他位置再启动。\n你可以访问 https://docs.hmcl.net/help.html 页面寻求帮助。\n是否继续启动？	fatal.config_in_temp_dir=你正在临时文件夹中启动 Hello Minecraft! Launcher, 你的设置和游戏数据可能会丢失，建议将 HMCL 移动至其他位置再启动。\n你可以访问 https://docs.hmcl.net/help.html 页面寻求帮助。\n是否继续启动？(android.os.Build.VERSION.SDK_INT >= android.os.Build.VERSION_CODES.N) {
