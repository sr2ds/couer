# Coeur - static site management

Coeur is being made based on [Typer](https://typer.tiangolo.com/) (Thanks @tiangolo).

## Name explanation

"cœur" is a French word for "core" or "heart".

This tool is called Coeur for two personal reasons: 1. it will be the core of my blog-farm; 2. one of my favorite places is the Sacre ***Cœur*** in Paris.

## What does this tool will solve?

I'm bringing Coeur to the world to solve some specific problems that I'm dealing with when trying to manage big blogs as static sites. By big, I mean more than 100.000 post files.

Imagine the following scenario: You have a set of blogs with a lot of content, they can be within WordPress or any tool of this kind. The more content and traffic your blog has, the more you'll need to worry about your infrastructure.

Some time ago, I migrated my blog projects to SSG, which means only static content generated with the contents, and I can keep all of them hosted for free using GitHub Pages or Netlify.

The problem is that the SSG tools available today are not optimized for this amount of content, and with artificial intelligence, it is very practical to generate quality content on a large scale.

So, Coeur will solve this. It will be a tool that will allow me to build larger blogs and continue to maintain them for free, allowing me to explore other content niches and generate more and more content for my users.

This tool is being built based on several years of experience I have with creating blogs/sites using various tools, including WordPress, VuePress, VitePress, Zola, and probably some others that were less relevant in my tests.

If I were to summarize Coeur in a single sentence, considering the end of the project where we will have all modules ready and not just the SSG, I would say:

The complete tool for building blogs with over a million posts and hosting them for free.

## How to install

Coeur is a common python package, you can install from pypi:

```sh
pip install --user blog-coeur
```

The command to be used is `blog-coeur` and get `help` to start to use:

```sh
blog-coeur --help
```

## Module SSG - Static Site Generator

The first module of `coeur` is the `ssg` to be possible to build a complete static website from a `sqlite` database and also the base feature to import from markdown to database.

### How to use

#### Create your coeur app

To start your project, you can run the `create` command with your new project name, this command will to create the new folder with the basic stuff to work:

```sh
blog-coeur ssg create my-blog
```

#### Development Server

To build the blog we need some local server to simplify or life, you can run this command inside of coeur project to use a simple locally server:

```sh
blog-coeur ssg server --max-posts=1000 --port=8081
```

The param `max-posts` will be useful when you post has some much posts, this way the build will be more fast in development time.

#### Building Static Site

To build your blog, you can run the `build` command inside the blog directory:

```sh
blog-coeur ssg build
```

The blog will be generated inside the directory "public".

#### Markdown Importation

If you are using the `Zola Framework` and want to migrate to Coeur, you can import your markdown files into the Coeur database.

Considering that you are inside the Coeur Blog repository, copy the posts directory here and run the command replacing "./content" for your posts directory.

```sh
blog-coeur ssg markdown-to-db "./content"
```

### SSG Features

 * Import markdown files from Zola Framework
 * Basic template for blog usage, based on zolarwind (thanks for @thomasweitzel)
 * HTML Minify
 * Sitemap Generation with pagination
 * Hot reload
 
 ### TODO List

- [ ] Custom templates (themes)
    - [ ] Documentation about templates
- [ ] Allow to manage the posts from SQLAlchemyAdmin dashboard
- [ ] Support to use post Tags
- [ ] Hot reload v2 - add websocket to auto-refresh the html in the browser

## Module CMP - Content Machine Processor

The CMP module was designed to simplify content creation powered by the OpenAI API.

### How to use

The content will be created as posts inside the blog's SQLite database, which is generated by the ssg module. It's important to start your project using the ssg command.

Assuming you already have the blog created with Coeur, you need to setting up your open-ai key in the `.env` file and then you can use the cmp module as follows:

```
blog-coeur cmp title-to-post "Aguas de Lindóia" --custom-prompt="Create a full article about the city, need to be funny and talking in positive way about the place"

```

The first parameter is required and will be the title of the post.

It is highly recommended to use a custom-prompt to enhance your experience and get better results. This prompt can be in any language.

You can also set the img-url parameter to include an image in the post. This needs to be a valid image URL, such as one hosted on S3.


## Module PDS – Post Distribution Service

This module will help us to automatically publish the blog posts in the social midias.

## Benchmark Overview

My initial goal was to be able to build my project without exploding my RAM memory as happened with all the frameworks I tried and used throughout the growth of my blog, these benchmark numbers below are the real numbers for the same blog that consumes 12GB to be built with Zola.

It is possible that I can optimize the build time to make it faster, however, it will consume a little more RAM memory. For now it's acceptable.

### Importing - from Markdown to DB
Importing 103594 posts from Zola markdowns from command `blog-coeur ssg markdown-to-db ./content`:

```sh
Processed: 103594 | Duration: 00:02:11.162591
Debug: RSS: 934.58 MB | VMS: 957.69 MB | Data: 925.75 MB | USS: 922.11 MB | PSS: 923.16 MB | CPU: 71.00%
```

This is the final debug line, spending around 934.58 MB to do all importation in 02 minutes.

Remembering that you need do it only one time.

### Building

The current build is taking 05 minutes and consuming around 362 MB of RSS, with the `minify=false`:

```sh
Processed: 103594 | Duration: 00:05:19.639324
Debug: RSS: 362.93 MB | VMS: 629.91 MB | Data: 388.62 MB | USS: 350.16 MB | PSS: 351.26 MB | Processed: 103594 | CPU: 99.40%
```


# Do you want to help?

This is an open-source project, and I need help to make it better.

If you are a developer, feel free to contact me to work on items from my personal roadmap, or you can suggest something new. Be free, let's do it together.

If you are a company, contact me to support the growth of my project. I'm open to improve it for specifics new use-cases.