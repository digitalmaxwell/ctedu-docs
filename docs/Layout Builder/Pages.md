---
---

# Pages

## Create a new page

To create a new page, first you need to setup an entry in contentful. Select the "Page" Content Type in the search bar and click Add Page.

![Add Page](/img/add-page.png)

![New Page Entry](/img/new-page-entry.png)

Using the default project structure of gatsby to our advantage, pages are created in `./src/pages/`

You can use the code below as a model to create a new page.

Change the component name and replace `your-slug-here` with the newly created slug from Contentful.

```jsx title="/src/pages/newPage.js"
import React from "react"
import { graphql, useStaticQuery } from 'gatsby'
import Layout from "../components/Layout/layout"
import SEO from "../components/seo"
import RenderLayoutBlocks from "../components/ContentfulLayout/renderLayoutBlocks"

const newPage = ({location}) => {

    const data = useStaticQuery(graphql`
        query {
            contentfulPage(slug: {eq: "your-slug-here"}) {
                ...ContentfulPageFragment
            }
        }
    `)
    return (
        <Layout>
            <SEO location={location} title={data.contentfulPage.seoTitle} description={data.contentfulPage.seoDescription}/>
            <RenderLayoutBlocks layout={data.contentfulPage.layout}/>
        </Layout>
    )
}

export default newPage
```

useStaticQuery fetches the data from graphql using the page fragment. This will return the seoTitle, seoDescription, and the layout references.

`RenderLayoutBlocks.js` uses [MatchComponent](/Layout%20Builder/match-component) to render the layout.