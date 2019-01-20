# Introduction to translate Elm guide

An instruction to maintain translation project of [Elm guide](https://guide.elm-lang.org) well based on [Japanese translation project by Elm-jp](https://github.com/elm-jp/guide/).

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

    ```sh
    $ cd $MY_REPOSITORY_NAME
    $ git remote set-url origin $MY_REPOSITORY
    ```

    Replace `$MY_REPOSITORY_NAME` with git URL of your translation project.

1. Put extra files to maintain translation project.

    We have prepared extra files to maintain translation project.
    Clone and overwrite by them.

    ```sh
    $ git clone https://github.com/elm-jp/instruction-to-translate-elm-guide.git
    $ cp -r instruction-to-translate-elm-guide/template/* .
    $ rm -rf instruction-to-translate-elm-guide
    ```

1. Push your initial commit as a translation project.

    Now it's time to publish.

    ```sh
    $ git add .
    $ git commit -m 'Initialise as a translation project'
    $ git push origin master
    ```

Conglaturations! After these setups, now you have published the very beginning of your own translation project.

## Update diff link

The `book/about_translation.md` has a link to check if the version is up to date.
It would look like as follows:

```
https://github.com/evancz/guide.elm-lang.org/compare/b8b589364746afb7bb58402841672aa85a2455bf...master
```

Update it with actual your base commit.

```bash
$ git log
commit bbc2192b87b50fdb62f014cf16f24d00682afff9 (HEAD -> master, origin/master, origin/HEAD)
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

In this case, replace to the following URL.

```
https://github.com/evancz/guide.elm-lang.org/compare/bbc2192b87b50fdb62f014cf16f24d00682afff9...master
```

## Start development server

It's time to serve your initial Elm guide.
At first, you need to install dependencies.

```sh
$ npm i && npm run install
```

Now you can serve development server.

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

All pages to be served are in the directory `book`.
At the step of copying translation specific files you've done before,
`about_translation.md` was created in `book`.

But the page does not appear on menu. Why?
To add new page, you have to update `book/SUMMARY.md`.

Open the file in your favorite editor.
Put new line at the top of contents.

```md
# Summary

* [翻訳について](about_translation.md)
* [Introduction](README.md)
* [Install](install.md)
...
```

"翻訳について" means "About translation" in Japanese, so you should rename it in
your own language.

Save the changes, and after a few second the page should be reloaded
automatically.
In this operation, new chapter you've added now will appear.

### What is translation table?

As you can see `about_translation.md`, there is "Translation table".
It is used to unify how to translate terms frequently appears among all pages.

When you noticed that a term appears frequently and its translation is not
obvious, then add new pair of (translation of a term, original term) to the table.

### `pretranslate` command

To translate a page, you have a convenent command named "pretranslate".
It automatically comments out original sentences, and also do an important
feature.
If a sentence contains terms appears in the translation table,
it puts a note about how to translate the term.

This is done by just matching terms in translation table with ignoring cases.
It means to make this feature work well, you should put a term into
translation table in a singular form.

e.g., "type alias" matches to "Type aliases", but "type aliases" does not match
to "type alias"

Also, for terms conjugating irregularly, it is recommended to put conjugated
forms as comments.

So, it would look like following example.

```
| translateion      | original term   |
|:-----------------:|:---------------:|
| 型の別名          | type alias      |
| ミニファイ        | minify          |
<!-- | ミニファイ        | minifies          | -->
<!-- | ミニファイ        | minified          | -->
```

Not all the terms to unify translation should be shown to readers.
For example, the term "chapter" appears frequently and its Japanese translation varies among translators, but readers do not interesting in the original term of the translation.
In such situation, you also should put them as comments.

### First translation

Let's actually translate a file.
The `book/about_translation.md` is the best page to translate at first.

First thing you need is to `pretranslate` the file.
The `pretranslate` command has been already installed with `npm i`, so use it
with `npx`.

```sh
$ npx pretranslate book/about_translation.md
book/about_translation.md has been pretranslated
```

OK, it's turn to actually translate the page.
After translating, `git push` to master branch.

```sh
$ git add .
$ git commit -m 'First translation'
$ git push origin master
```

## Preparing to publish

It's time to publish.
The first thing to do is compile to static files.

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

## [Optional] Serve on your own domain

Though it's optional, Japanese team uses our own domain ("guide.elm-lang.jp") to serve pages.
One of the notable benefit to use own domains is that it enables us to serve pages at root level.
E.g., By default, it is served on "https://elm-jp.github.io/guide/", but with own domains it is on "https:/guide.elm-lang.jp/".
Because original Elm guide is served on root level, so using your own domains is the easiest way to mimic.

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
High quality Japanese translation project is supported by Elm-jp.
