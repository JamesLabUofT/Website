# Updating the James Lab website

Any member of the lab should be able to modify the website. What follows is an overview of key aspects of the lab website, and how to modify them. **In almost all cases, you should be making edits on Rstudio, NOT directly on github.com.** On Rstudio, you are able to render the pages you are changing which allows you to check that nothing is broken.

To edit on RStudio, you must:

1.  Clone the repository (if you haven't already)

2.  `git pull` to make sure the most up to date changes are on your local machine

3.  Make changes

4.  !!! Render the quarto pages you've changed to ensure nothing is broken !!!

5.  `git commit` the changes, using a clear commit message (e.g. `Changed Leo Jourdan's picture`, not `edit picture` or `modified my picture`)

6.  `git push`

General documentation for quarto, and quarto websites are a great place to start if you need to make more significant changes: <https://quarto.org/docs/websites/>.

### Navigation bar (top bar) and bottom contact bar

The navigation bar contents is dictated by the `_quarto.yml` file. You can modify which pages are linked by modifying the `navbar` attribute (common edit is to display or hide the Opportunities page)

The bottom contact bar is determined by the `page-footer` attribute in `_quarto.yml`

### Updating the News

The news is displayed in two locations: the front page (`index.qmd`), and the news page (`news.qmd`). On the front page, news images are not displayed and the number of news items is limited. Otherwise, both behave similarly.

All news items are automatically pulled from the `news/news.yml` file, which also includes instructions for how to add new items. Any news item must have a description and date, and optionally a link and an image. **When adding new news to the website, it's important to try rendering the news.qmd file, as it's relatively easy to break the formatting of the news/news.yml file.**

You can change how news are pulled from this yml file and displayed on the front page by modifying `news/newsTemplateFrontPage.ejs`. Similarly, you can modify how news are displayed on the news page by modifying `news/newsTemplate.ejs`.

### Updating People page

The People page (`people.qmd`) automatically populates pictures, names and other attributes from the `people/grad` (for graduate students), `people/pdf` (for postdocs), `people/staff` (for staff members). `people/supervisor` (Patrick) and `people/undergrad` for (undergraduate research assistants).

To add a new lab member, copy the contents of `people/peopleTemplate.qmd` into a file `people/category/firstnamelastname.qmd`, then edit it with that new member's name, bio, etc... You can put their profile picture in `images/people/firstnamelastname` . The correct path to put in the `image` attribute at the top of their `.qmd` file is `../../images/people/firstnamelastname/pictureFileName.extension` Always be sure to render the file before pushing it.

Note that you might have to uncomment a section in `people.qmd` if the added member is the only one in their category (e.g. going from 0 undergraduate research assistant to 1). Similarly, if there are no more people in a certain category, you can comment that section.

To remove a lab member, you can move their relevant file into the `people/alumni` folder. If they have a new role somewhere, you can add `current: "Role title @ Company name"` to the top of their .qmd file. Be sure to give them the `ended: year` attribute as well.

The alumni list pulls from the `.qmd` files in `people/alumni` AND the `alumni.yml` file. `alumni.yml` was used to transition the old lab alumni list from the previous James Lab website, but could be used to include anyone who hadn't had a personal `.qmd` file.

If you want to make different categories of people (e.g. split `graduate students` into `PhD` and `MScF` or add an `MFC` category), you will need to make a new folder for that category, and edit the `people.qmd` listing attribute and content body to pull filed from that folder. You should be able to look to other categories as a reference.

### Modifying other pages

Other pages are relatively straightforward to edit: find their `.qmd` file, make the edit, render to check and you're good to go. Note the "internal James Lab" file at `misc/internal.qmd` which people can't navigate to directly from the main pages but is still hosted on the server.

### Website configuration

The website is hosted as a github page. A github "action" (`Quarto Publish`) automatically renders the `.qmd` files into `.html` files when changes are pushed. A different github action (`pages-build-deployment`) will then push the changed `.html` files to the website. These actions can be modified in the `.github/workflows/publish.yml` file. Look for a tutorial for quarto websites hosted on github pages.

By default, github pages are hosted on `jameslabuoft.github.io/RepositoryName/`. We've modified the settings to publish on `jameslab.ca` instead (how to do this is well documented). Although it is important to have the file `CNAME` at the root of the project, and include it as a "ressource" in `_quarto.yml`.

There is a github bot that automatically posts in the #lab_website slack channel when a new commit is pushed to the repository, and whether the changes were successfully rendered and the website updated. If there are issues when rendering the changes (formatting error, for example). It will show up here. Keep an eye on it!
