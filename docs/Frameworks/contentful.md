---
sidebar_position: 2
---

# Contentful
[Contentful](https://www.contentful.com/) is a headless CMS that easily integrates with Gatsby.

We use Contentful as an interface for the CTEDU team to customize coachtrainingedu.com. In the CMS you can create pages, blog posts, fonts, colors etc..
Unlike a typical CMS like Wordpress, this interface corresponds with custom React components.

This is all possible using [the gatsby source contentful plugin](https://www.gatsbyjs.com/plugins/gatsby-source-contentful/) which allows you to query the Contentful API using Gatsby and GraphQL.

## Content Models
Contentful gives you the flexibility to define explicit fields, types, validation and apperance of how the entry will look in the editor. 
<!-- Here is an example of a the page content model.  -->

![Content Model Example](/img/content-model-example.png)

## Entries
Each entry can be embedded in multiple places helping to avoid duplicate variations of certain sections/components. This creates consistency across the site and has proven very useful.

Entries can also be embedded within each other using [references](https://www.contentful.com/help/references/) to create robust layouts, templates etc. Checkout the Layout Builder documentation to learn how entries are translated into components.

- [Create a Page](/Layout%20Builder/Pages)
- [Create a template](/Layout%20Builder/Templates)

<!-- - Create a page -->

![Content Model Example](/img/content-model-example-6.png)