# What I hate about Jekyll

Jekyll has the right spirit: Write as few noise as possible. But it's also heavily fucked up. So you need hours of RTFM and tons of plugins for basic non-surprising behavior. More sensible defaults would be nice. Especially for non-programmers.


## Including Markdown

Everything can be Markdown, why not includes? Jekyll should be smart enough, and convert Markdown if you include a Markdown file instead of HTML. If you fix [this plugin](http://wolfslittlestore.be/2013/10/rendering-Markdown-in-jekyll/) such that it works, you have an additional tag and more API to memorize. One can also override the include tag altogether and make it smart. But the point is, this should be available out of the box.


## YAML front matter

If it's not a post, it needs a YAML header. [That's how we do it here](https://github.com/jekyll/jekyll/issues/290#issuecomment-16363044). WTF? Just do what this guy [said years ago](https://github.com/jekyll/jekyll/issues/290#issuecomment-1264028) and set  up conversion in the config by path or extension.


## Categories

To create posts in a category [you need](https://github.com/jekyll/jekyll/issues/1819#issuecomment-89003858) `category/_posts` instead of `_posts/category`. How does that make sense *from a user's perspective*?


## Liquid whitespace

Not completely Jekyll's fault, but none the less: Liquid tags spam the output with wagonloads of whitespace. They have been talking about this stuff for [three years](https://github.com/Shopify/liquid/issues/216)! With utterly idiotic arguments like:

- [nah](https://github.com/Shopify/liquid/issues/216#issuecomment-54557362), you never know if someone *wanted* the whitespace
- let's try [workaround #93715612](https://github.com/Shopify/liquid/issues/216#issuecomment-205047328) and add tons of useless code everywhere it bothers you

There are a bunch of pull requests stacked up on this topic. What are those people doing all the time? Just merge that shit. At least they have managed to kill empty blocks and Jekyll already uses a [current version](https://github.com/Shopify/liquid/issues/216#issuecomment-33629864). But a non-empty tag block still produces newlines around its content unasked. And no, you *absolutely don't want this*. It's code, it's not supposed to leave any artifacts other than what you tell it to.

## Local links

It's a mess if you want to use relative links and currently impossible without boilerplate (noise). It's also been discussed for [years on end](https://github.com/jekyll/jekyll/issues/332). Did I say [verbose workarounds](http://ricostacruz.com/til/relative-paths-in-jekyll.html) are bullshit? Jekyll should handle that for me. I specify a link

- relative to my source directory
- using categories, collections or page names as variables

and the program should create the correct relative link to the desired object, wherever it has been placed in the output.


## Handling `posts`, `pages` and `collections`

All of them basically do the same thing (hell, it's just Markdown files thrown together). But specific properties, like sorting by date, are hardwired in Jekyll.

`posts` is a collection. Alright, makes sense - the folder structure follows the naming convention. But you just can't rename or delete it. It's built in. Sure, you can delete the folder, but the collection is still there. If you want to iterate over collections, it will *always* be there. Should you not need it, you will have to filter it out with a conditional statement (noise!).

If you try to output posts as a collection, you might be surprized that they are not processed if they don't have a YAML front matter. Because normally, posts are *always* converted.

Why distinguish between collections and categories anyway? Right now you have to set up additional values for collections in the config. If you unified the concept, you could revert back to the homogeneous defaults syntax and just tell the categories and types their Official Titles™, layouts, output properties and what not.


## Layouts and includes

A last thing is the out-of-the-box presentation. When you start a new project, there is all kinds of stuff popping up that a non-programmer neither needs nor understands. Multiple layouts, includes, style sheets with a bunch of declarations, nested HTML tags riddled with classes, fancy logos and a *social network list*. This is the cancer that is killing the Internet!

If the goal is to present a minimal interface that grows with the user's ability, then don't overwhelm with all your useless features. We will find them on our own with time and need. The documentation is already very good and Google + Stackoverflow will do the rest.


## Suggestions

Convert everything that is hooked up to some converter in the config. If a file has a date in front, it's a post, otherwise a page. Files in `foo/bar` have category `foo/bar`. Treat categories as hierarchical sets. Tags are non-hierarchical. Sort by basename per default, use a Jekyll tag to sort by given attribute. Everything else can be handled by the existing setup.

Then present it with Hello World. Just `index.md` showing one "Hello World" post, an *empty* style sheet, and a default layout that only includes a html header. Even the config should be empty except for an empty title and description, so the newcomer can have a look and plug custom values for the first time.

## Conclusion

It seems that what I percieve as very annoying flaws has historical background in development. Once it was just scratching one's own itch, then stuff has been tacked on as an afterthought. Each user adds a new interpretation of what should be or how to work around something. I think the project is mature enough to care about user experience now.
