---
---

# Pages

## Create a new page

![Add Page](/img/add-page.png)

Using the default project structure of gatsby to our advantage, we create our pages in `./src/pages/`
This 

You can use the code below as a model to create a new page:

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
            <SEO location={location} title={data.contentfulPage.seoTitle} description={data.contentfulPage.description}/>
            <RenderLayoutBlocks layout={data.contentfulPage.layout}/>
        </Layout>
    )
}

export default newPage
```

useStaticQuery fetches the data from graphql using the page fragment. This will return the seoTitle, seoDescription, and the layout references.

`RenderLayoutBlocks.js` uses [MatchComponent](/Layout%20Builder/match-component) to render the layout.