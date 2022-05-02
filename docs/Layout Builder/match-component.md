---

---

# Match Component

This function is responsible for matching an entry in Contentful to a Component in our application. The entry data is passed to the Components props, and then the function does some pre-processing before returning the rendered component. Follow along to learn how this function is used throughout our application and how to implement it yourself.


## Implementation

### Setup GraphQL query

MatchComponent uses the Content Type returned from a contentful query to return a matching component. In order to implement Match Component you first need to set up your query. Check out the code example for setting up a page [here](/Layout%20Builder/Pages#code-setup). As you can see, the static query uses the [Page Fragment](/Frameworks/gatsby#page-fragment) which is used to query components. Inside every component query make sure to add the Content Type field so that the component can be rendered using Match Component.

:::tip
Below is an example of the Button query. Add the **sys.contentType.sys.id** field to your query when adding a component to Match Component. 
:::

```jsx title="/src/graphql-fragments/ButtonFragment.js"
import { graphql } from 'gatsby'

export const ButtonFragment = graphql`
    fragment ButtonFragment on ContentfulButton {
        sys {
            contentType {
                sys {
                    id
                }
            }
        }
        text
        buttonStyle {
            className
            size
        }
        internalLink
        externalLink
        sampleTrainingPopUp
        calendlyPopUpLink
    }
`;
```
<!-- ... explain recursivness (link to dynamic template component docs in contentful), implementation in columnGrid, rich text, renderLayout.  -->

### Add your component

Below is a shortened verion of Match Component. Once you have set up the query, add your component to the switch statement using `componentData` 

```jsx title="/src/components/ContentfulLayout/MatchComponent.js"
import React, { cloneElement } from "react"
//import your components here

const MatchComponent = ({ contentType, componentData, parentData, nestedComponent, padding, layout, index, backgroundColor }) => {
    let Component, styles = {}

    if (padding) styles = componentPadding({contentType, componentData, nestedComponent, layout, index})

    switch (contentType) {
        case 'dynamicTemplateComponent':
            if (!parentData[componentData.componentKey] || !parentData[componentData.componentKey].sys) return null;
            Component = MatchComponent({
                contentType: parentData[componentData.componentKey].sys.contentType.sys.id,
                componentData: parentData[componentData.componentKey],
                parentData: parentData,
                nestedComponent: nestedComponent,
                padding: padding,
                layout: layout,
                index: index,
                backgroundColor: backgroundColor
            })
            break;
        case 'button':
            Component = (
                <ContentfulButton
                    buttonStyle={componentData.buttonStyle}
                    internalLink={componentData.internalLink}
                    externalLink={componentData.externalLink}
                    text={componentData.text}
                    sampleTrainingPopUp={componentData.sampleTrainingPopUp}
                    calendlyPopUpLink={componentData.calendlyPopUpLink}
                    wrapperStyle={{marginTop: '40px'}}
                />
            )
            break;
        //We have 20+ components. Add yours to this switch statement
    }
    return cloneElement(Component, {styles: styles})

```

#### Recursiveness

This function is designed to work recursively with Dynamic Template Components. This allows Contentful Entries with templates to render components stored in the entry within a dynamic template. Learn more about Dynamic Template Components [here](/Layout%20Builder/Templates#dynamic-template-components). As you can see, the first case in the switch statement is `dynamicTemplateComponent`, this will pass the parent data back into Match Component so that it can match the right component for that template.

#### Props

`contentType` ..

`componentData` Data from GraphQL query

`parentData` Data for templates that need to access components in the parent entry

`nestedComponent` Boolean that affects spacing when a component in this switch statement calls function

`padding` ..

`layout` ..

`index` ..
 
`backgroundColor` ..

## Component Padding
```jsx title="/src/components/ContentfulLayout/componentPadding.js"

const componentPadding = ({contentType, componentData, nestedComponent, layout, index}) => {
    let styles;
    let paddingObj = {top: '5rem', right: '2.5rem', bottom: '5rem', left: '2.5rem'}
    let marginTop;

    //skip dynamic template component, wait for match
    if (contentType != 'dynamicTemplateComponent') {
        if (nestedComponent) {
            //components with backgrounds get larger margins top and bottom
            //smaller components like video, button etc get 50% reduced margins top and bottom
            if (!componentData.backgroundColor) {
                paddingObj.left = '0'
                paddingObj.right = '0'
                paddingObj.top = '2.5rem'
                //account for last nested component
                if (layout && index == (layout.length - 1)) paddingObj.bottom = '0'
                else paddingObj.bottom = '2.5rem'
            }
        } else {
            //this doesnt run for nested components, because they require space-y-10 for Column Grid and Rich Text field.
            //space-y causes a gap between all components making the statement below irrelevent. This is meant for base pages
            //When there are two components with matching background color next to each other in layout, the first component doesnt have padding bottom
            if (componentData.backgroundColor && layout && layout[index + 1] && layout[index + 1].backgroundColor) {
                if (componentData.backgroundColor.className === layout[index + 1].backgroundColor.className) paddingObj.bottom = '0'
            }
        }

        //When there are two components without a background color next to each other, the first component doesnt have padding bottom
        if (!componentData.backgroundColor && layout && layout[index + 1] && !layout[index + 1].backgroundColor) {
            paddingObj.bottom = '0'
        }
    }
    if(contentType === `questionAnswer`){
        paddingObj.top = '0'
    }
    
    return styles = {padding:`${paddingObj.top} ${paddingObj.right} ${paddingObj.bottom} ${paddingObj.left}`, marginTop: `${marginTop}`}
}

```

<!-- ## Render Layout -->

...

<!-- # Use Cases

There are multiple places in our application where Match Component is used.

### Column Grid

```jsx title="/src/components/ContentfulLayout/LayoutComponents/ColumnGrid.js"
MatchComponent({
    contentType: componentData.sys.contentType.sys.id,
    componentData: componentData,
    parentData: parentData,
    nestedComponent: true,
    padding: false,
    layout: false,
    index: i,
    backgroundColor: backgroundColor
})

```

### Rich Text

### Pages and Templates -->