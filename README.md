## About the project

**Project Title** : FHIR OAuth Smart Apps Integration and OAuth module enhancements
**Primary Mentor** : Mayank Sharma

The project invloved the following main tasks :
- [ x ] Migration to OpenMRS 2.x
- [ x ] Create a new REST Controller
- [ x ] SMART on FHIR application

### Detailed task description and sub-goals

- #### Migration to OpenMRS 2.x
  - **Migrate dependencies and configurations to be compatible with OpenMRS 2.x**
    The module previously ran on OpenMRS 1.11 and worked with Spring Security 3. My initial task was to migrate the module to OpenMRS       2.x and use Spring 4 and Spring Security 4. This part took a lot longer that what me and Mayank thought. Spring Security is a           complex framework and it's compatibility issues with Spring versions are many. I had to remove all the deprecated code with new code     and also fix some broken part of the code. 
    A lot had changed from OpenMRS 1.11 to 2.X So I had to redo the whole OAuth Client data model and re-write some portions of the         client.
    
  - **Fix Grant Types**
    This was one of the most challenging portions of the summer. The code was in-place, the procedure was right. Problem? Can't get         tokens :frowning: In my opinion, Spring Security, Spring Security OAuth are excellent frameworks but quite complex too. Spring uses     Jackson to manage all output JSON requests. The tokens which were created and stored in the database, were not returned to the REST     call response. Reason? Jackson. Jackson, Spring security oauth, Spring security and spring mvc taken altogether to do one thing         created such a mess of finding the right version of everything. If I changed a version, thing X would break. Changing it back, would     break Y. This cycle continued for some time, until I managed to find the right versions of everything.
    
  - **Fix UI**
    The previous module used UI extensively. Our initial plan was to scrap out the UI and introduce a controller to manage everything       what UI did. However, the mid-term presentation came by and I had nothing other than token generation to show to the community.         Then, we decided to keep the UI, make the presentation and later provide enough flexibility to the end-user to choose between REST       based controller, UI or both :slight_smile: So I fixed everything wrong in the UI and completed it for the demo during mid-term.
    
    You can see my mid-term demo here : 
    <iframe width="560" height="315" src="https://www.youtube.com/embed/8xicdkiaRas" frameborder="0" allowfullscreen></iframe>
  
```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/mavrk/GSOC-2017-final/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
