---
---

# Templates


Templates are reusable entries that contains a customizable layout. This allows for dynamically generated pages or frequently created layouts to be easily updated in one place.


## Setup Contentful Entry
Just like creating a page, first you need to setup an entry in contentful. Select the "Template" Content Type in the search bar and click Add Template.

![Add Template](/img/add-template-2.png)

When creating a new template, add a unique title and build the layout however you like.

**Below is an example of the Location Template:**

![Location Template Example](/img/location-template-3.png)

## Add Template Field to Content Model

Now that you have created your template, you need to add a template reference field wherever you want the template to be used.

Select `Add Field` in your Content Model and you will see this pop up. Select the `Reference` type.

![Add Template to Content Model](/img/add-template-to-content-model-10.png)

Give the Field a name and select `One reference`.

![Add Template to Content Model](/img/add-template-to-content-model-9.png)

Next, click the `Create and configure` button and navigate to the validation tab. Here you can select what content models are allowed to be added to your new reference field. Select "Template" so this field only displays the templates available to you.

![Add Template to Content Model](/img/add-template-to-content-model-8.png)

Once complete, the template field will be accessible in your content model. Here is an example of what our Location Content Model looks like:

![Add Template to Content Model](/img/add-template-to-content-model-11.png)

## Code Setup

Now that you have set up your Template in Contentful, there are a few steps involved to get it working in our application.

New templates are created in the `/src/templates/` folder and then rendered using `gatsby-node.js` with the `createPage` function provided by gatsby.js. You can learn more about the gatsby actions we leverage [here](/Frameworks/gatsby).

### Create pages

Below is an example of templates being implemented for the CTEDU location pages.
First we query all of the location pages with their respective slug and title. Then the code loops through the data and renders the pages dynamically using the `createPage` function. The slug is used to generate the page path and the title is passed to the context of the template.

**For your use case, adapt the query to your paramaters and add any additional pre-processing neccessary.**

```jsx title="gatsby-node.js"

  template = `./src/templates/location3.js`

  const locations = await graphql(`
  {
    allContentfulLocation {
      edges {
        node {
          title
          slug
        }
      }
    }
  }
  `)

  locations.data.allContentfulLocation.edges.forEach(edge => {
    let title = edge.node.title
    let slug = edge.node.slug

    actions.createPage({
      path: slug,
      component: require.resolve(template),
      context: {
        title: title
      }
    })
  })
```

### Create Template

Once you have configured your dynamically rendered your pages in `gatsby-node.js`, you need to set up the template component.

Inside of the query, we can access the context from `createPage` function. We use the title to fetch each locations data, which is then passed to the prop `data` in the `Location` component. `RenderLayoutBlocks` uses this data to parse the layout of the page.

**Use this location template as a model for your own implementation:** 

```jsx title="/src/templates/location3.js"

import React from 'react'
import { graphql } from 'gatsby'
import Layout from "../components/Layout/layout"
import SEO from "../components/seo"
import RenderLayoutBlocks from "../components/ContentfulLayout/renderLayoutBlocks"

const Location = ({location, data}) => {
    return (
        <Layout>
            <SEO location={location} title={data.contentfulLocation.seoTitle} description={data.contentfulLocation.seoDescription}/>
            { data.contentfulLocation.template &&
                <RenderLayoutBlocks
                    layout={data.contentfulLocation.template.layout}
                    parentData={data.contentfulLocation}
                />
            }
        </Layout>
    )
}

export default Location

export const query = graphql`
    query($title: String!) {
        contentfulQuery(title: { eq: $title }) {
            title
            seoTitle
            seoDescription
            description1 {
                raw
            }
            description2 {
                raw
            }
            template {
                ...TemplateFragment
            }
        }
    }
` 

```

## Access entry data within Template

Next we will cover how to use Variables and Dynamic Template Components in your templates.

### Variables

...

### Dynamic Template Components

The Dynamic Template Components content type allows for embedding dynamic components into a your template.

The field "Component Key" looks for the field with the corresponding Content Type.

![Powerful Paragraph Dynamic Template Component Example](/img/powerful-paragraph-dynamic-template-component-example.png)

In this example, the Powerful Paragraph Template is being used for this Blog Post. `Powerful Paragraph Section One` contains a reference to a Rich Text entry.

![Template Example](/img/template-example-4.png)