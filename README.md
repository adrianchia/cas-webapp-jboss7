cas-webapp-jboss7
=================

CAS Server Web Application that is compatibie with JBoss 7. This project is derived from original cas-server-webapp from https://github.com/jasig/cas

HTTPS Setup
-------------
By default the application server only have 1 connector, i.e. HTTP connector. To setup HTTPS, do the following:

1. In command prompt/terminal, enter
 
        keytool -genkey -alias tomcat -keypass changeit -keyalg RSA

   * remember to change the alias and keypass to your preference.
   * one caveat for the following question: ``What is your first and last name?`` is that it should be the server name.
   
2. Once you ge the keystore file (usually in your user_home directory), copy over to your standalone/configuration folder.

3. Open up standalone.xml file and find the following

       <connector name="http" protocol="HTTP/1.1" scheme="http" socket-binding="http"/>
   
   add the following underneath
   
       <connector name="https" scheme="https" protocol="HTTP/1.1" socket-binding="https" enable-lookups="false" secure="true">
			<ssl name="test-ssl" password="changeit" protocol="TLSv1" key-alias="tomcat" certificate-key-file="../standalone/configuration/.keystore" />
       </connector>
  
  where password is your keystore password and key-alias is your alias specified in step #1.
  
4. Deploy the custom cas.war to your JBoss deployment folder and try it out!

Reference
---------
https://wiki.jasig.org/display/CASUM/Demo
https://docs.jboss.org/author/display/AS71/SSL+setup+guide 