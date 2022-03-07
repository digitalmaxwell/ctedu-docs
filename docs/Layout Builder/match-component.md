---

---

# Match Component

This function is responsible for matching an entry in Contentful to a Component in our application. The entry data is passed to the Components props, and then the function does some pre-processing before returning the rendered component. Follow along to learn how this function is used throughout our application and how to implement it yourself.

## Breakdown

Below is a simplified version of this component.

... explain recursivness (link to dynamic template component docs in contentful), implementation in columnGrid, rich text, renderLayout. 

```jsx title="/src/components/ContentfulLayoutBuilder/MatchComponent.js"
const MatchComponent = ({contentType, componentData, parentData, nestedComponent, padding, layout, index, backgroundColor}) => {
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
        //We have 20+ components. Add yours to this switch statement
    }
    return cloneElement(Component, {styles: styles})

```