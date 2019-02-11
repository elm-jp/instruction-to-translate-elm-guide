# About translation

This site is __Japanese__ translation of the [Elm guide](https://guide.elm-lang.org/) translated by the member of the local Elm community __Elm-jp__.

The Elm guide is an learning contents of Elm written by Evan, the author of Elm language, so it is the best content to learn Elm.
(And also, it would tells you almost all of the essence to use Elm even in your business!)
Because the Elm guide is for beginners, we are trying to make our translation natural __Japanese__.
Also, we focus on that it can help readers to understand how Evan want to tell us well rather than original Elm guide.
To realise such translation, this is not strict translation.
So if you want to know how Evan exactly says, we recommend you to read original version directly.
But note that we are confident our translation is the best one based on the effort of reviews by __Elm-jp__ members.

## Based original version

<!-- !!!!NOTES FOR TRANSLATERS!!!!
    Update diff link when merging original changes.
-->
We are trying to keep up changes on original content though, this site could be outdated because it is maintained by volunteers.
Check if it is up to date by [diff to latest version](https://github.com/evancz/guide.elm-lang.org/compare/bbc2192b87b50fdb62f014cf16f24d00682afff9...master).
If it says "There isn’t anything to compare.", you know that this translation is up to date.

## How to contribute translation?

It is welcome to help us.
The way to contribute is not only translating, but just reporting "This __Japanese__ sentence is not natural" or "I don't understand what this means" as [an issue on GitHub](https://github.com/elm-jp/guide/issues).
Because Elm guide is for beginners, you should have confidence "If I do not understand, many people also do not! It's not because I am fool, but because who translated this is fool.".

Please see [README.md on GitHub](https://github.com/elm-jp/guide/#readme) for actual way to contributing translation.

## Translation table

Here is a translation table that describes how we translated technical terms into __Japanese__.
It would help you with learning Elm.

<!-- !!!!NOTES FOR TRANSLATORS!!!!

If a sentence contains terms appears in the translation table, the `pretranslate` command puts a note about how to translate the term.

This is done by just matching terms in translation table with ignoring cases.
To utilize this simple algorithm to check terms, you should put a term into translation table in a singular form.
E.g., "type alias" matches to "Type aliases", but "type aliases" does not match to "type alias". So you should register "type alias" rather than "type aliases".

Also, for terms conjugating irregularly, it is recommended to put conjugated forms as comments.
The `pretranslate` command do checkes comment lines, but the line does not appears on translated site.

In the example bellow, we commented out the translation of "chapter" and "section".
It is because their translation varies among translators, but readers do not much interested in the term itself.
-->

<!-- | <Translated> | <Original> | DO NOT REMOVE OR CHANGE THIS LINE -->
| Translated        | Original        |
|:-----------------:|:---------------:|
| 型の別名          | type alias      |
| ミニファイ        | minify          |
<!-- | ミニファイ        | minifies          | -->
<!-- | ミニファイ        | minified          | -->
<!-- | 章 | chapter | -->
<!-- | 節 | section | -->
