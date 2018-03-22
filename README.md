# docs-collaboration-system


This is the live documentation website for Collaboration System . It is created using Docusaurus.

The website is serving from gh-pages branch.
The source code is at master branch.

Requirements -

Nodejs -v8.6.0
NPM

Clone the repository and inside website folder of the repository run

```
npm install
```

There a two folders 'docs' and 'website'

The 'docs folder is where your documentation written in md files will reside'

While creating the documentation keep the file name and id same.

Set the path to your documentation in website/sidebars.json file
Place your documentation file name in one of the available sidebar or you can create your own sidebars in json format.


Check your site using following in the website folder -

```
npm start
```

If your site is running properly, you can finally build the site.

```
npm run build
```

Copy all the files from website/build/docs-collarationsystem/ and move to gh-pages branch.
