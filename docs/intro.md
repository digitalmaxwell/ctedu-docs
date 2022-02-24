---
sidebar_position: 1
slug: /
---

# Coach Training EDU

Documentation for the coach training edu website built using: **React, Gatsby, Tailwind and Contentful**

## Gatsby

This React project is built on [Gatsby](https://www.gatsbyjs.com/) which is a powerful static site generator.

`gatsby-node.js` is used to generate blog posts, knowledge base posts, location pages

<!-- #### Basic Commands:
Start development server
```
gatsby develop
```
Generate build
```
gatsby build
```
Clean 
```
gatsby clean
``` -->

## Contentful
[Contentful](https://www.contentful.com/) is a headless CMS that easily integrates with Gatsby.

We use Contentful as an interface for the CTEDU team to customize coachtrainingedu.com. In the CMS you can create pages, blog posts, fonts, colors etc..
Unlike a typical CMS like Wordpress, this interface corresponds with custom React components.

This is all possible using [the gatsby source contentful plugin](https://www.gatsbyjs.com/plugins/gatsby-source-contentful/) which allows you to query the Contentful API using Gatsby and GraphQL.

### Content Models
Contentful gives you the flexibility to define explicit fields, types, validation and apperance of how the entry will look in the editor. 
<!-- Here is an example of a the page content model.  -->

![Content Model Example](/img/content-model-example.png)

### Entries
Each entry can be searched in Contentful and embedded in multiple places helping to avoid duplicate variations of certain sections/components etc. This has proven to be very useful.

Entries can also be embedded within each other using [references](https://www.contentful.com/help/references/) to create robust layouts, templates etc. Checkout the Layout Builder to learn how entries are translated into components.

- [Create a Page](/Layout%20Builder/Pages#create-a-page/)
- [Create a template](/)

<!-- - Create a page -->

![Content Model Example](/img/content-model-example-6.png)


## Tailwind CSS
[Tailwind](https://tailwindcss.com/) is a CSS framework that can be composed to build any design, directly in your markup. This is a VERY useful tool helping to provide consistent classes the team can use to develop components.

### Cheat sheet ![](/img/tailwindcomponents-favicon.ico)

[This website](https://tailwindcomponents.com/cheatsheet/) simplifies the tailwind docs so you can easily find the classes you need

### Configuration

Fonts, colors, variants, and tailwind plugins are defined in `tailwind.config.js`

Wnat to learn more? [Visit the official tailwind documentation on configuration](https://tailwindcss.com/docs/configuration#creating-your-configuration-file)

### Custom Styles

You can use tailwind classes in a css file to assemble your own classes and customize default html.

Our branding classes are defined in `styles/global.css`. [Here is further documentation on adding Custom Styles](https://tailwindcss.com/docs/adding-custom-styles#using-css-and-layer)