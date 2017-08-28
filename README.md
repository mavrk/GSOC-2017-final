## About the project

Source-code for OAuth module: [https://github.com/mavrk/openmrs-module-oauth2-prototype/tree/oauth2-pure-rest](https://github.com/mavrk/openmrs-module-oauth2-prototype/tree/oauth2-pure-rest)<br>
Source-code for SMART app: [https://github.com/mavrk/SMART-on-fhir-client](https://github.com/mavrk/SMART-on-fhir-client)
 
**Weekly blogs** : [http://planet.openmrs.org/](http://planet.openmrs.org/) [www.sanatt.me](https://www.sanatt.me)<br>
**Download the module** <a href="/GSOC-2017-final/oauth2-0.8.omod" download>.omod</a><br>
**Download the smart-app**  <a href="/GSOC-2017-final/smart-app.zip" download>.zip</a>

**This is only a project report, complete project documentation can be found [here](https://wiki.openmrs.org/display/projects/OAuth2+Module)**

**Project Title** : FHIR OAuth Smart Apps Integration and OAuth module enhancements

**Primary Mentor** : Mayank Sharma

**Project Stats** : 28 major commits, 1200+ lines of code (900+ additions and 300+ deletions)


The project invloved the following main tasks :
- [x] Migration to OpenMRS 2.x
- [x] Create a new REST Controller
- [x] SMART on FHIR application

### Detailed task description and sub-goals ###

- ### Migration to OpenMRS 2.x <br>
  - **Migrate dependencies and configurations to be compatible with OpenMRS 2.x**
    The module previously ran on OpenMRS 1.11 and worked with Spring Security 3. My initial task was to migrate the module to OpenMRS       2.x and use Spring 4 and Spring Security 4. This part took a lot longer that what me and Mayank thought. Spring Security is a           complex framework and it's compatibility issues with Spring versions are many. I had to remove all the deprecated code with new code     and also fix some broken part of the code. 
    A lot had changed from OpenMRS 1.11 to 2.X So I had to redo the whole OAuth Client data model and re-write some portions of the         client.
    
  - **Fix Grant Types**
    This was one of the most challenging portions of the summer. The code was in-place, the procedure was right. Problem? Can't get         tokens :frowning: In my opinion, Spring Security, Spring Security OAuth are excellent frameworks but quite complex too. Spring uses     Jackson to manage all output JSON requests. The tokens which were created and stored in the database, were not returned to the REST     call response. Reason? Jackson. Jackson, Spring security oauth, Spring security and spring mvc taken altogether to do one thing         created such a mess of finding the right version of everything. If I changed a version, thing X would break. Changing it back, would     break Y. This cycle continued for some time, until I managed to find the right versions of everything.
    
  - **Fix UI**
    The previous module used UI extensively. Our initial plan was to scrap out the UI and introduce a controller to manage everything       what UI did. However, the mid-term presentation came by and I had nothing other than token generation to show to the community.         Then, we decided to keep the UI, make the presentation and later provide enough flexibility to the end-user to choose between REST       based controller, UI or both :smile: So I fixed everything wrong in the UI and completed it for the demo during mid-term.
    
    You can see my mid-term demo here : 
    <iframe width="560" height="315" src="https://www.youtube.com/embed/8xicdkiaRas" frameborder="0" allowfullscreen></iframe>
  
- ### Client REST Controller <br>
    After the mid-terms the point of focus was the REST Controller. Using this controller, one could create, manage, view oauth clients     without the UI. Which means that any OWA, Android app, iOS app, etc would be able to manage, create oauth clients and it won't           require opening OpenMRS on a browser and handing everything. Just like almost everything in this summer, the controller didn't go as     planned :stuck_out_tongue: Problem? I wanted to return a client object as JSON response, however Jackson (which handles JSON outputs     in Spring) gave the error "property leading to cycles". Upon research I realized that Jackson depends on getter and setter methods       of a class. My client inherited properties such as getCreator() , getVoidedBy() from the BaseOpenMrsData. getCreator() returns a         User, the User also has a getCreator(), so that formed an infinite loop whenever getCreator() was called by Jackson. So what I did       next was that I broke this loop by creating a new JacksonMappableClient. And now everyone was happy :smile:
    
    You can see a demo for the Client REST Controller here : 
    <iframe width="560" height="315" src="https://www.youtube.com/embed/y2eSck9JUn0" frameborder="0" allowfullscreen></iframe>

- ### SMART on FHIR Application <br>
    This was one of the main goals for the summer. Even if we managed to create the OAuth module, their was not a lot of application to     it. SMART on FHIR is a perfect use-case for our module. So making a sample SMART on FHIR would give OpenMRS community a perfect use-     case for our module. The application came by easily. Their were a few blockers but nothing which would consume 'days' of debugging.     I also made a custom CORS filter for the module to enable Cross-Origin requests if SMART application is hosted on a different s         server.
    
    A demo of SMART on FHIR :
    <iframe width="560" height="315" src="https://www.youtube.com/embed/WYz5ykLTOos" frameborder="0" allowfullscreen></iframe>
    
    
 **Proper project documentation** : [here](https://wiki.openmrs.org/display/projects/OAuth2+Module)
 
 **OpenMRS final presentation** : [Talk thread](https://talk.openmrs.org/t/gsoc-2017-oauth-module-and-fhir-smart-apps-integration-final-presentation/13067)
 
 
 
 
 
