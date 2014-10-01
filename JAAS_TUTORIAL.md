
####################################
#  Modifica al file standalone.xml #
####################################
 

   <datasource jta="false" jndi-name="java:/DefaultDS" pool-name="DefaultDS" enabled="true" use-java-context="true" use-ccm="true">
                    <connection-url>jdbc:oracle:thin:@10.35.20.49:1521:sanity</connection-url>
                    <driver>oracle</driver>
                    <pool>
                        <min-pool-size>5</min-pool-size>
                        <max-pool-size>20</max-pool-size>
                        <prefill>true</prefill>
                        <use-strict-min>false</use-strict-min>
                        <flush-strategy>FailingConnectionOnly</flush-strategy>
                    </pool>
                    <security>
                        <user-name>seus</user-name>
                        <password>seus</password>
                    </security>
                    <validation>
                        <valid-connection-checker class-name="org.jboss.jca.adapters.jdbc.extensions.oracle.OracleValidConnectionChecker"/>
                        <stale-connection-checker class-name="org.jboss.jca.adapters.jdbc.extensions.oracle.OracleStaleConnectionChecker"/>
                        <exception-sorter class-name="org.jboss.jca.adapters.jdbc.extensions.oracle.OracleExceptionSorter"/>
                    </validation>
                    <timeout>
                        <blocking-timeout-millis>30000</blocking-timeout-millis>
                        <idle-timeout-minutes>5</idle-timeout-minutes>
                    </timeout>
                </datasource>





[.....]


 <security-domain name="DBAuthTest">
                    <authentication>
                        <login-module code="org.jboss.security.auth.spi.DatabaseServerLoginModule" flag="required">
                            <module-option name="java:/DefaultDS" value="java:/DefaultDS"/>
                            <module-option name="principalsQuery" value="select password from  SEUS.UTENTI where UTENTE=?"/>
                            <module-option name="rolesQuery" value="select RUOLO, 'Roles' from  SEUS.UTENTI where  UTENTE=?"/>
                            <module-option name="hashAlgorithm" value="MD5"/>
                            <module-option name="hashEncoding" value="base64"/>
                        </login-module>
                        <login-module code="org.jboss.security.auth.spi.RoleMappingLoginModule" flag="optional">
                            <module-option name="rolesProperties" value="/home/userone/jboss-as-7.0.1.Final/standalone/configuration/test-roles.properties"/>
                            <module-option name="replaceRole" value="false"/>
                        </login-module>
                    </authentication>
                </security-domain>


#############################
#  Modifica al file web.xml #
############################

La modifica può avvenire sia tramite il pannello "security" messo a disposizione da netbeans sia a livello testuale.

<?xml version="1.0" encoding="UTF-8"?>
<web-app version="3.0" xmlns="http://java.sun.com/xml/ns/javaee" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd">
    <session-config>
        <session-timeout>
            30
        </session-timeout>
    </session-config>
    <welcome-file-list>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>
    <security-constraint>
        <display-name>Constraint-0</display-name>
        <web-resource-collection>
            <web-resource-name>Constraint-0</web-resource-name>
            <description/>
            <url-pattern>/b/*</url-pattern>
            <url-pattern>/v/*</url-pattern>
        </web-resource-collection>
        <auth-constraint>
            <role-name>admin</role-name>
        </auth-constraint>
        <user-data-constraint>
            <transport-guarantee>NONE</transport-guarantee>
        </user-data-constraint>
    </security-constraint>
    <login-config>
        <auth-method>FORM</auth-method>
        <form-login-config>
            <form-login-page>/login.jsp</form-login-page>
            <form-error-page>/error.html</form-error-page>
        </form-login-config>
    </login-config>
    <security-role>
        <role-name>admin</role-name>
    </security-role>
</web-app>


###################################
#  Modifica al file jboss-web.xml #
###################################

 Impostare il security-domain con il nome java:/jass/ "nome dato al db in standalone" 

<?xml version="1.0" encoding="UTF-8"?>
<jboss-web>
  <context-root>/ProvaLog</context-root>
   <security-domain>java:/jaas/DBAuthTest</security-domain>
</jboss-web>
