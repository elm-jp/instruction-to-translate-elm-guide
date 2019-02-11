# __Japanese__ translation of guide.elm-lang.org

[Original version](https://github.com/evancz/guide.elm-lang.org/)

__Japanese__ translation project of Elm guide.

## Contributing translation

The way to contribute this project is not only translating by yourself.
Here are some options.

### Read the content as beginner

Elm guide should be understood by beginners.
So, if you are new-be to Elm, it is super helpful to tell us "This translated sentence is not so natural, and I could not understand what it actually means".
Please report as an issue freely.

### Review translations

The greatest part of Elm is that it has a nice compiler.
One bad news about translation is that we do not have such a compiler claims our wrong translations.
We need some _compilers_ who reviews our translations.

We are creating pull requests when creating new translation of pages, so feel free to comment on them.

### Translate pages

#### Preparing environment

If it is the second time you translate, this step can be omitted.

The first thing you have to do is cloning this repository and installing dependencies.

```bash
$ cd $CLONED_DIRECTORY
$ npm i
$ npm run install
```

Make sure to install node.js before.

#### Find a section to translate

You must create an issue "Translate XXXXXX" before translating a page.
It helps others to avoid accidentally start translating the same page.
So, you have to check issues to assure that no one is working on the page you want to translate.

#### Prepare to translate

After deciding which file to translate, it's time to use `pretranslate` command.

```bash
$ npx pretranslate ./book/YOUR_FILE_TO_TRANSLATE
```

Please replace `YOUR_FILE_TO_TRANSLATE` into path to the markdown file you want to translate.
It results in target file is commented out per paragraphs.
You may also see some notes about how to unify translation of a term among other translators.
The note is generated based on the translation table in the `./book/about_translation.md`.
So, it is recommended to put a term into the translation table when you faced a term which should be shared translations among others.

#### Translate

Put your translations under commented out paragraphs.
Make sure to obey the policy written in the section "About translation".

#### Check if it can be rendered correctly.

The command bellow starts a development server.

```bash
$ npm start
...
...
Starting server ...
Serving book on http://localhost:4000
```

Check your translation is rendered as expected by opening the URL.

#### Create PR

After translating a page, create a PR.

## Deploying production server

It is recommended to set up CI to execute following commands when master branch changes.

```bash
$ git checkout master
$ npm run build
$ git add docs && git commit -m 'Update docs' && git push origin master
```

Also, be aware to allow search engine bots to access new page by updating `robots.txt`.

## Merge changes on original content

Elm guide itself is actively updating, so sometimes we have to merge their changes into this repository.

We do update translations by our hands with the aid of `git`.

Here is the way to do that with git.

1. Beforehand, register Evan's original repository as another remote.

```
$ git remote add evan github:evancz/guide.elm-lang.org.git
$ git remote -v
evan	github:evancz/guide.elm-lang.org.git (fetch)
evan	github:evancz/guide.elm-lang.org.git (push)
origin	github:elm-jp/guide.git (fetch)
origin	github:elm-jp/guide.git (push)
```

2. Update `evan/origin` and merge.

```
$ git checkout master
$ git fetch evan
$ git checkout -b merge-evan
$ git merge evan/master
```

Here you would have to resolve conflictions.

After merging, make sure to update diff URL on `about_translation.md`.
