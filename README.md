# Level Editor Tutorial for Rhythm Doctor

Visit the tutorial website [here](https://rd-editor-docs.github.io/intro). This is the GitHub repository for the tutorial.

This website is built using [Docusaurus 2](https://docusaurus.io/), a modern static website generator. If you want to add information or make some edits, keep reading to see how to make a pull request.


## Local Development

### Requirements

- A GitHub account.
- Basic Git knowledge (e.g. cloning, making commits, pushing/pulling).
	- There are many tutorials on using Git, or you can use something with a user interface like GitHub Desktop.
- Basic terminal knowledge (e.g. running executables, changing directories).
  - There are also many tutorials on using a terminal like (Git) Bash. Windows Powershell can also work in a pinch.
- [Node.js](https://nodejs.org/en/download/) v16 or higher. You can check your Node version with `node -v`.

### Running locally

- First, create a fork of the repository.
	- This can be done by clicking "Fork" on the [main page of the repository](https://github.com/rd-editor-docs/rd-editor-docs.github.io)).
	- This creates a copy of the repository where you are the owner and can thus make changes freely.
- Clone the forked repository to your own computer.
- Navigate to the cloned repository in a terminal and run `npm install` to install required dependencies. This will take a while.

### Making changes

- Run `npm start` to start the website locally (takes ~50s). A browser window will open automatically once ready.
	- Changes to Markdown files should be reflected live without having to restart the server.
		- If this doesn't seem to work, try refreshing the page, or running `npm start -- --poll` instead.
	- However, changes such as new files/folders or configuration changes will require a server restart.
	- Note that this kind of deployment only supports **one locale**. Trying to change locale will result in "no page found" errors.
		- To view a different locale (e.g. French), start with `npm start -- --locale fr`.
- Run `npm run build` to build all the static content (takes ~1-2m) into the `build` directory.
	- Run `npm run serve` to view the site locally. This supports **all locales**.
	- As the static content has already been created, the site will no longer reflect any changes made to Markdown files.
- Push your changes to the `main` branch to trigger an automatic GitHub workflow.
	- This will try to build your changes and deploy the new website (takes ~3 minutes).

### Making a pull request

- Create a pull request to merge your changes into the main repository.
	- This should be done after pushing your commits to your fork and verifying that the built website looks correct.
	- You can use `git merge` or the "Contribute" --> "Make a pull request" buttons on the main page of the forked repository.
- In the pull request description, try to leave a clear summary of the changes.
- Your pull request will be reviewed as soon as possible, and comments may be left on suggested edits before it can be merged.


## Working with Docusaurus

### Documentation pages

All the documentation files are in the `docs` folder.
- A single page `Title` is created from a file `title.md(x)`.
	- Use the `.mdx` extension if you want to leverage JavaScript or React components on the page.
- Nested pages are created from folders that contain Markdown files inside.
	- Typically, there is also a `_category_.json` file that serves as the "base" page for the folder.
		- You can copy a previous file to use as an example.
- Files are added to the sidebar by default.
	- To reorder files in the sidebar (default is alphabetical), prefix the file names with `01-`, `02-`, etc. These are automatically stripped by Docusaurus so they don't show up on the site.
	- You can also use *front matter* at the beginning of Markdown files like so to reorder files:
	```
	---
		sidebar_position: 1
	---
	```

### Media
  
Images should be placed inside the `static/img` folder.
- These can be accessed in Markdown using relative paths (e.g. `![](/img/rows/irregular_oneshots.png`).
- They can also be accessed in JSX components using `src={useBaseUrl('/img/rows/final_oneshot.gif')}`.
  - You will need to have `import useBaseUrl from '@docusaurus/useBaseUrl';` at the top of the page.

If you want styling on images (e.g. to center it on the page or change the size), you have to use JSX and change your file extension to `.mdx`.
```
<img className="no-space" src="https://i.imgur.com/nnolNXe.png" alt="Condition pop-up" width="60%"/>
```
Note that JSX is **NOT** HTML. There are some differences, like using `className` instead of `class`.

CSS is applied globally through the `src/css/custom.css` file, so you can add styles there if you want repeated styling.
	- There are some classes there already that might be helpful for what you need, like `no-space`.

Videos can be embedded by importing ReactPlayer:
- Insert `import ReactPlayer from 'react-player';` at the top of the page.
- Use `<ReactPlayer playing controls url={require('./set_play_style_demo.mp4').default} />` to embed the video.

### Custom pages

If you want to create your own wacky page, it goes in `src/pages`. The homepage is one of those files.
- This type of page lets you leverage React and JavaScript along with custom CSS files.

### Translations

Translations go in `i18n/<locale>/docusaurus-plugin-content-docs/current/<rest of file path>`.
- All files here should have the same structure as `docs/` and have the same names.

If you're adding a new locale (i.e. no pages previously existed for that locale), make sure you add it to the list of locales in `docusaurus.config.js` in the config `i18n` object.
