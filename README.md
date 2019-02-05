# Instruction to translate Elm guide

An instruction to maintain translation project of [Elm guide](https://guide.elm-lang.org) well based on [Japanese translation project](https://github.com/elm-jp/guide/) by [Elm-jp](https://elm-lang.jp).

The Elm guide is the best document for learning Elm, so translating it into your language helps a lot with making Elm mainstream.
Nice contribution!

## Preparing a very beginning of translation project for your language

Let's create your own translation project step by step.

1. Clone original repository of Elm guide.

    This becomes a bases of your translation project.

    ```sh
    $ git clone https://github.com/evancz/guide.elm-lang.org.git $MY_REPOSITORY_NAME
    ```

    Replace `$MY_REPOSITORY_NAME` with repository name of your translation project.

1. Change remote repository to your own.

    Set remote URL to your own.
    This enables to `git push` your translations to your own repository.

    ```sh
    $ cd $MY_REPOSITORY_NAME
    $ git remote set-url origin $MY_REPOSITORY
    ```

    Replace `$MY_REPOSITORY_NAME` with git URL of your translation project.

1. Put extra files to maintain translation project.

    We have prepared extra files to maintain translation project.
    Clone and overwrite original files by them.

    ```sh
    $ git clone https://github.com/elm-jp/instruction-to-translate-elm-guide.git
    $ cp -r instruction-to-translate-elm-guide/template/* .
    $ rm -rf instruction-to-translate-elm-guide
    ```

1. Push your initial commit as a translation project.

    ```sh
    $ git add .
    $ git commit -m 'Initialise as a translation project'
    $ git push origin master
    ```

Conglaturations! After these setups, you have published the very beginning of your own translation project.

## Update diff link

The `book/about_translation.md` has a link to check if the version is up to date.
It would look like as follows:

```
https://github.com/evancz/guide.elm-lang.org/compare/b8b589364746afb7bb58402841672aa85a2455bf...master
```

To update it, first check actual commit hash you based on.

```bash
$ git log
commit b48d447351774c61f7c6506b6ffe22339a380b84 (HEAD -> master)
Author: Your Name
Date:   Tue Feb 5 12:20:31 2019 +0900

    Initialise as as a translation project

commit bbc2192b87b50fdb62f014cf16f24d00682afff9 (origin/master, origin/HEAD)
Merge: 466516e b8b5893
Author: Evan Czaplicki <evancz@users.noreply.github.com>
Date:   Tue Jan 8 13:32:29 2019 +0100

    Merge pull request #182 from Kevin-Kawai/master

    Fixed typo in interop section

commit b8b589364746afb7bb58402841672aa85a2455bf
Author: Kevin-Kawai <kevin.fredricks@gmail.com>
Date:   Sat Dec 29 11:25:25 2018 +0900
...
...
```

In this case, your base commit hash is `bbc2192b87b50fdb62f014cf16f24d00682afff9`.
(Note that the top commit is not by original repository.)

So, resulting URL is as follows:

```
https://github.com/evancz/guide.elm-lang.org/compare/bbc2192b87b50fdb62f014cf16f24d00682afff9...master
```

## Start development server

It's time to serve your initial Elm guide.
At first, you need to install dependencies.

```sh
$ npm i && npm run install
```

OK. Now you can serve development server.

```sh
$ npm start
...
...
Starting server ...
Serving book on http://localhost:4000
```

It informs you that development server is on `http://localhost:4000`.
You'll see original Elm guide contents on the URL.

### Publish "About translation" chapter

All pages to be served are in the directory `book/`.
At the step of copying translation specific files you've done before,
new file named `about_translation.md` was put in `book/`.

But the page does not appear on menu. Why?
To make new page public, you have to update `book/SUMMARY.md`.

Open the file in your favorite editor, and put new line at the top of list.

```md
# Summary

* [翻訳について](about_translation.md)
* [Introduction](README.md)
* [Install](install.md)
...
```

The term "翻訳について" means "About translation" in Japanese, so you should rename it in your own language.

Save the changes, and after a few second the site should be reloaded automatically.
By this operation, new chapter you've added now will appear.

### What is translation table?

You may notice that there is "Translation table" in `book/about_translation.md`.
It is used to unify how to translate terms that frequently appears among pages.

When you noticed that a term appears frequently and its translation is not obvious, it's time to add new line to the table.
To explain actual way to use "Translation table", we'll introduce `pretranslate` command.

### `pretranslate` command

To translate a page, you have a convenent command named "pretranslate".
It just automatically comments out original sentences, but it has another important role.
If a sentence contains terms appears in the translation table, it puts a note about how to translate the term.

This is done by just matching terms in translation table with ignoring cases.
To utilize this simple algorithm to check terms, you should put a term into translation table in a singular form.
E.g., "type alias" matches to "Type aliases", but "type aliases" does not match to "type alias". So you should register "type alias" rather than "type aliases".

Also, for terms conjugating irregularly, it is recommended to put conjugated forms as comments.
The `pretranslate` command do checkes comment lines, but the line does not appears on translated site.

So, it would look like following example.

```
| translateion      | original term   |
|:-----------------:|:---------------:|
| 型の別名          | type alias      |
| ミニファイ        | minify          |
<!-- | ミニファイ        | minifies          | -->
<!-- | ミニファイ        | minified          | -->
```

Not all the terms to unify translation should be shown to readers of your translation site.
For example, the term "chapter" appears frequently and its Japanese translation varies among translators, but readers are not interesting so much in the original term of the translation.
In such situation, you also should comment out them as the case of conjugated forms explained above.

### First translation

Let's actually translate a file.
The `book/about_translation.md` is the best page to translate at first.

First thing you need to do is to `pretranslate` the file.
The `pretranslate` command has been already installed with `npm i`, so use it with `npx`.
(The `npx` would be already installed on your machine if you are using latest version of `node`.)

```sh
$ npx pretranslate book/about_translation.md
book/about_translation.md has been pretranslated
```

OK, it's turn to actually translate the page.
Put your translations bellow each comment-outed sentence.
All the time you save your changes, the development server should update the contents on web browser.
Check if it appears as you expect.

After translating, do not forget to `git push`.

```sh
$ git add .
$ git commit -m 'First translation'
$ git push origin master
```

## Preparing to publish

It's time to publish your site to internet.
The first thing to do is compile into static files.

```bash
$ npm run build
```

It would generate `docs` directory containing resulting static files.
Let's `git push` them.

```bash
$ git add docs
$ git commit -m 'Update docs'
$ git push origin master
```

## Publish

Now you can publish pages.
Japanese team uses GitHub Pages, but Netlify or any hosting services would be also OK.
We do not explain how to do with them, but all you need would be just registering `docs` directory to publish.

## [Optional] Serve the site on your own domain

Though it's optional, Japanese team uses our own domain ("guide.elm-lang.jp") to serve pages.
One of the notable benefit to use own domain is that it enables us to serve pages at root level.
E.g., By default, it is served on "https://elm-jp.github.io/guide/", but with own domains it is on "https:/guide.elm-lang.jp/".
Because original Elm guide is served on root level, using your own domain reduces extra works to modify contents to publish on sub directory.

## [Recommended] Use robots.txt

Initially, your site could be assumed as [duplicate content](https://support.google.com/webmasters/answer/66359?hl=en).
If assumed as duplicate content, your site is downvoted or even treated as a spam site by search engines.
To avoid such problems, I recommend you to use `robots.txt`.
You should have `book/robots.txt` when copying this repository.
If your pages are served on root level of your domain, it works.
If not, you have to put the file on root level in any way.

By default, the `book/robots.txt` disables search engine crawler to access any files.
You can `Allow` accessing to translated pages by modifying this file.
After translating `book/about_translation.md`, uncomment the line in the `book/robots.txt`.

## [Recommended] Announce your community about your translation project

It is great idea to do translations with your local Elm community.
Some of them in the community would have passion to contribute to Elm, so they would be willing to help you.
Working with others enhances translation, and also cheers you no to give up.
High quality Japanese translation project is realised by Elm-jp (Japanese Elm community).
