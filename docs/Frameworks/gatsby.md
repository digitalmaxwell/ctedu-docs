# Gastby JS

This React project is built on [Gatsby](https://www.gatsbyjs.com/) which is a powerful static site generator.

## Basic Commands

Get up and running with the following commands. Follow [this documentation](https://www.gatsbyjs.com/docs/reference/gatsby-cli/) to familarize yourself with the Gatsby CLI.

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
```

## Config API

The file `gatsby-config.js` defines metadata, plugins, and other general configuration. [Learn more](https://www.gatsbyjs.com/docs/reference/config-files/gatsby-config/).


## Node APIs

Code in the file `gatsby-node.js` is run once in the process of building your site. You can use its APIs to create pages dynamically, add data into GraphQL, or respond to events during the build lifecycle. [Learn more](https://www.gatsbyjs.com/docs/reference/config-files/gatsby-node/).

**This is where we generate our blog posts, knowledge base posts, location pages, bios, graduate stories etc.**

Read the template guide for an example using the `createPage` function to [Dynamically Create Pages](/Layout%20Builder/Templates#dynamically-create-pages).

## Browser APIs
The file `gatsby-browser.js` lets you respond to Gatsby-specific events within the browser, and wrap your page components in additional global components. [Learn more](https://www.gatsbyjs.com/docs/reference/config-files/gatsby-browser/).

Currently, we use gatsby-browser to define global css, font awesome, and redux (see the wrapWithProvider component below).

```jsx title="./gatsby-browser.js"
import './src/styles/global.css';

import { library } from '@fortawesome/fontawesome-svg-core'
import { faCalendar, faClock } from '@fortawesome/free-regular-svg-icons'
import { faPlay } from '@fortawesome/free-solid-svg-icons'
import wrapWithProvider from "./src/state/wrap-with-provider"

library.add(faCalendar, faClock, faPlay)

export const wrapRootElement = wrapWithProvider
```

## GraphQL

GraphQL is a query language for requesting information from an API, and a protocol for servers that support it. GraphQL is one of the ways that you can import data into your Gatsby components. [Learn more about Gatsby and GraphQL](https://www.gatsbyjs.com/docs/glossary/graphql/)

### Fragments

Fragments allow you to reuse parts of GraphQL queries. It also allows you to split up complex queries into smaller, easier to understand components. [Learn More.](https://www.gatsbyjs.com/docs/reference/graphql-data-layer/using-graphql-fragments/) In our project, Fragments are crucial to maintaining the queries tied to data stored in Contentful.

Inside of the folder `/src/graphql-fragments/` there are several important files to pay attention to.

`LayoutFragment.js` is a special fragment we designed for the Layout Builder. In this file we have organized all of the queries for Content Models in Contentful that correspond with a component we have built in React. As you can see below, the fragment will only work on the Content Type of _Node_. This represents a reference field in Contentful. Using the spread option, ... _on_ _ContentfulType_ allows you to optionally query data if that content type is present in the reference field. 

There are a few places where this fragment is used: **Pages, Templates, Rich Text and the Column Grid component.**
This fragment gives us a central file where all of the queries can be easily updated.

:::info
One limitation to keep in mind with fragments, is that **you cannot spread a fragment of the same type within itself**. For example, in the code below we don't include the Page, Template, Rich Text and Column Grid fragments, because that would break the rule. Check the code for `PageFragment.js` to see how we resolve this for our setup.
:::

```jsx title="/src/graphql-fragments/LayoutFragment.js"
export const LayoutFragment = graphql`
    fragment LayoutFragment on Node {
        ... on ContentfulButton {
            ...ContentfulButtonFragment
        }
        ... on ContentfulDynamicTemplateComponent {
            ...DynamicTemplateComponentFragment
        }
        ... on ContentfulImage {
            ...ImageFragment
        }
        ... on ContentfulVideo {
            ...VideoFragment
        }
        ... we have 20+ components
    }
`
```

`PageFragment.js` is used to query the SEO Title/description and Layout for each page. As you can see below, the Column Grid and Rich Text fragments are added along side the Layout Fragment to avoid spreading a fragment of the same type within itself. The other fragments generating dynamic layouts follow the same pattern.

```jsx title="/src/graphql-fragments/PageFragment.js"

export const PageFragment = graphql`
    fragment PageFragment on ContentfulPage {
        seoTitle
        seoDescription
        layout {
            ... on Node {
                ... on ContentfulColumnGrid {
                    ...ColumnGridFragment
                }
                ... on ContentfulRichText {
                    ...RichTextFragment
                }
                ...LayoutFragment
            }
        }
    }
`
```