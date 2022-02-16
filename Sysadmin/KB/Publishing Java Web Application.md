## Environment Variables

**`$CATALINA_HOME`** This variable points to the directory where Tomcat is installed. Usually it's something like `C:\Apache Tomcat 9.0`

**`$CATALINA_BASE`** This variable points to the directory of a particular instance of Tomcat. If this variable is not set explicitly, then it will be assigned the same value as `$CATALINA_HOME`.

Web applications are deployed to the `$CATALINA_HOME\webapps` directory.

## Create and deploy WAR file

1. Create a **WAR** (**W**eb **Ar**chive) file from Eclipse. **Right-click** the project name > **Export** > **WAR File**
2. Copy the WAR file to `$CATALINA_HOME\webapps\`. Tomcat will automatically unpack the archive and run the app.
3. Modify `$CATALINA_HOME\webapps\$APP_DIR\resources\settings.xml` to fit the environment you are running the app in.

## Troubleshooting

Logging is usually enabled by default and logs can be found in the $CATALINA_BASE\logs directory.

## See also

* [How to create WAR file for Java web application in Eclipse](https://www.codejava.net/ides/eclipse/eclipse-create-deployable-war-file-for-java-web-application)
* [How to Deploy a WAR File to Tomcat](https://www.baeldung.com/tomcat-deploy-war)