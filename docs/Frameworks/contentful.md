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
An entry is an instance of a content model stored in Contentful. Each entry can be embedded in multiple places helping to avoid duplicate variations of certain sections/components. This creates consistency across the site and has proven very useful.

Entries can also be embedded within each other using [references](https://www.contentful.com/help/references/) to create robust layouts, templates etc. Checkout the Layout Builder documentation to learn how entries are translated into components.

- [Create a Page](/Layout%20Builder/Pages)
- [Create a template](/Layout%20Builder/Templates)

<!-- - Create a page -->

![Entry Example](/img/content-model-example-6.png)

## Webhook

Webhooks are HTTP callbacks which can be used to send notifications when data in Contentful is changed, allowing external systems to react to changes to do things such as trigger a website rebuild or send a notification to a chat application. [Learn More.](https://www.contentful.com/developers/docs/concepts/webhooks/)

For our project, we are utilizing the git dispatch API to trigger a build for our repository (see the image below). What happens on this API call is configured using git actions. Learn more about our deployment setup [here](/Deployment/Git#actions).

![Webhook1](/img/webhook-1.png)

After setting up the URL and specific triggers, we have set up a custom *filter* to only publish live when the `release` page entry is published. This is a temporary solution and we are working on a more robust preview setup as you're reading this. :monkey:

![Webhook2](/img/webhook-2.png)

You can also customize the payload which will show up in the git actions tab.

![Webhook2](/img/webhook-3.png)
