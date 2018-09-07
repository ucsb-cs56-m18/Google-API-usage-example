# Google API Usage Example


## What is API and what is the benefit of using it?

Two good readings:

* https://medium.freecodecamp.org/what-is-an-api-in-english-please-b880a3214a82

* https://www.mulesoft.com/resources/api/what-is-an-api


## Google Calendar API as an Example

* ### setup the environment for our APIs

  * Enable Google Calendar API on Google Cloud Platform

    * go to https://console.cloud.google.com/home/

    * create a new project for your webapp from "select a project"

    * select that project (it may take a few seconds or so to appear after creation) and go into its dashboard

    * go to "Credentials" in "APIs & Services" panel

    * create credential -> OAuth Client ID (according to google's tutorial, choose other for application type and give it a name )

    * download the JSON file of the newly created credential to PATH_TO_YOUR_PROJECT/src//main/resources (see the download arrow on the right?)

    * add this file into .gitignore

    * _[Important]_ make sure it is ignored before you push local git commits onto GitHub.
          
        __DO NOT UPLOAD THIS JSON FILE TO GITHUB__
      because it contains sensitive information and you don't want people to freely use it. There do exist a few methods to remove it from commit history, if someone still carelessly uploaded it and is unwilling to delete and start a new repository. It comes potentially at a huge cost though and we've suffered and want nobody else to experience. Just double check and don't risk!

  * setup in maven (pom.xml)
    * basically, add a few dependencies

     (make them parallel to sparkjava for example)

        ```xml
        <dependency>
          <groupId>com.google.apis</groupId>
            <artifactId>google-api-services-calendar</artifactId>
          <version>v3-rev260-1.23.0</version>
        </dependency>

        <dependency>
          <groupId>com.google.http-client</groupId>
            <artifactId>google-http-client-jackson2</artifactId>
          <version>1.23.0</version>
        </dependency>

        <dependency>
          <groupId>com.google.oauth-client</groupId>
            <artifactId>google-oauth-client-jetty</artifactId>
          <version>1.23.0</version>
        </dependency>
        ```
* ### coding w/ functionality provided by the APIs

  * importing API library is almost the same as importing any other java class/library/etc...

    you just "import" it: (using our mini demo's main code as an example)
  ```java
  import com.google.api.client.auth.oauth2.Credential;
  import com.google.api.client.extensions.java6.auth.oauth2.AuthorizationCodeInstalledApp;
  import com.google.api.client.extensions.jetty.auth.oauth2.LocalServerReceiver;
  import com.google.api.client.googleapis.auth.oauth2.GoogleAuthorizationCodeFlow;
  import com.google.api.client.googleapis.auth.oauth2.GoogleClientSecrets;
  import com.google.api.client.googleapis.javanet.GoogleNetHttpTransport;
  import com.google.api.client.http.javanet.NetHttpTransport;
  import com.google.api.client.json.JsonFactory;
  import com.google.api.client.json.jackson2.JacksonFactory;
  import com.google.api.client.util.DateTime;
  import com.google.api.client.util.store.FileDataStoreFactory;
  import com.google.api.services.calendar.Calendar;
  import com.google.api.services.calendar.CalendarScopes;
  import com.google.api.services.calendar.model.Event;
  import com.google.api.services.calendar.model.Events;
  ```
  it may seems a lot to import and make use of, but remember you are not using all of them at all times -- relax!

  * now it's the fun part... Time to implement your own design!

    * the documentations built by API developers are always good resources

    * in our case: https://developers.google.com/calendar/concepts/events-calendars

    * In general, a few good practices we would like to recommend are:
      * stop panicking and divide your tasks among group members  
      in this way, you will know what to do (or more frankly, what to google first)
      * keep everyone on track: organize your tasks and issues with simple project boards shared by the entire team
        * try "Projects" (next to "Pull Request") in GitHub repo if you think it will help
      * communicate and make mutual understanding & agreements
      * work on the most important features first


* #### As always, happy coding! You are about to make something great and someone WOW! ;)

# Some git repos that might be helpful

| About | Link |
|-------|------|
|command line app w/ Google Oauth and Calendar API, framework: Maven| https://github.com/google/google-api-java-client-samples/tree/master/calendar-cmdline-sample|
|with both server and client ends, all above and Google AppEngine API|https://github.com/google/google-api-java-client-samples/tree/master/calendar-appengine-sample|



# To use

| To do this | Do this |
| -----------|-----------|
| run the program | Type `mvn exec:java`.  Visit the web page it indicates in the message |
| check that edits to the pom.xml file are valid | Type `mvn validate` |
| clean up so you can recompile everything  | Type `mvn clean` |
| edit the source code for the app | edit files in `src/main/java`.<br>Under that the directories for the package are `edu/ucsb/cs56/pconrad`  |
| edit the source code for the app | edit files in `src/test/java`.<br>Under that the directories for the package are `edu/ucsb/cs56/pconrad`  |
| compile    | Type `mvn compile` |
| run junit tests | Type `mvn test` |
| build the website, including javadoc | Type `mvn site-deploy` then look in either `target/site/apidocs/index.html`  |
| copy the website to `/docs` for publishing via github-pages | Type `mvn site-deploy` then look for javadoc in `docs/apidocs/index.html` |
| make a jar file | Type `mvn package` and look in `target/*.jar` |

| run the main in the jar file | Type `java -jar target/sparkjava-demo-01-1.0-jar-with-dependencies.jar ` |
| change which main gets run by the jar | Edit the `<mainClass>` element in `pom.xml` |
