---
---

# Templates

## Create a new template

Templates are meant to be a reusable entry that contains a customizable layout. This allows for dynamically generated pages or frequently created layouts to be easily updated in one place.

Just like creating a page, first you need to setup an entry in contentful. Select the "Template" Content Type in the search bar and click Add Template.

![Add Template](/img/add-template-2.png)

Below is an example of the Powerful Paragraph Template made for Blog Posts. When creating a new template, add a unique Title and build the layout however you like.

![Dynamic Template Example](/img/dynamic-template-example.png)

[add code example here]

<!-- ```jsx title="/src/templates/newTemplate.js"

import React from 'react'
import { graphql } from 'gatsby'
import Layout from "../components/Layout/layout"
import SEO from "../components/seo"
import RenderLayoutBlocks from "../components/ContentfulLayout/renderLayoutBlocks"

const newTemplate = ({location, data}) => {
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

export default newTemplate

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

``` -->

## Dynamic Template Components

Next we will cover accessing entry data within the template.
The Dynamic Template Components content type allows for embedding dynamic components into a your template.

The field "Component Key" looks for the field with the corresponding Content Type.

![Powerful Paragraph Dynamic Template Component Example](/img/powerful-paragraph-dynamic-template-component-example.png)

In this example, the Powerful Paragraph Template is being used for this Blog Post. `Powerful Paragraph Section One` contains a reference to a Rich Text entry.

![Template Example](/img/template-example-4.png)

## Variables
