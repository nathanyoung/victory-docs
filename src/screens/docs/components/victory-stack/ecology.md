# VictoryStack

`VictoryStack` is a wrapper component that renders a given set of children in a stacked layout. Like other wrapper components, `VictoryStack` also reconciles the domain and layout for all its children, and coordinates animations and shared events.

`VictoryStack` works with:
[VictoryArea], [VictoryBar], [VictoryCandlestick], [VictoryErrorBar], [VictoryGroup],[VictoryLine], and [VictoryScatter]

```playground
<VictoryStack>
  <VictoryArea
    data={[{x: "a", y: 2}, {x: "b", y: 3}, {x: "c", y: 5}]}
  />
  <VictoryArea
    data={[{x: "a", y: 1}, {x: "b", y: 4}, {x: "c", y: 5}]}
  />
  <VictoryArea
    data={[{x: "a", y: 3}, {x: "b", y: 2}, {x: "c", y: 6}]}
  />
</VictoryStack>
```

## Props

### animate

`VictoryStack` uses the standard `animate` prop. [Read about it here](https://formidable.com/open-source/victory/docs/common-props#animate)

See the [Animations Guide] for more detail on animations and transitions

**note: `VictoryStack` controls the `animate` prop of its children when set**

```jsx
animate={{
  duration: 2000,
  onLoad: { duration: 1000 }
)}
```

### categories

`VictoryStack` uses the standard `categories` prop. [Read about it here](https://formidable.com/open-source/victory/docs/common-props#categories)

**note: When this prop is set, `VictoryGroup` controls the `categories` prop of its children.**

```jsx
categories={["dogs", "cats", "mice"]}
```

### children

`VictoryStack` works with any combination of the following children: [VictoryArea], [VictoryBar], [VictoryCandlestick], [VictoryErrorBar], [VictoryGroup], [VictoryLine], [VictoryScatter], [VictoryStack], and [VictoryVoronoi]. Children supplied to `VictoryGroup` will be cloned and rendered with new props so that all children share common props such as `domain` and `scale`.


### colorScale

The `colorScale` prop is an optional prop that defines a color scale to be applied to the children of `VictoryStack`. This prop should be given as an array of CSS colors, or as a string corresponding to one of the built in color scales: "grayscale", "qualitative", "heatmap", "warm", "cool", "red", "green", "blue". `VictoryGroup` will assign colors to its children by index, unless they are explicitly specified in styles. Colors will repeat when there are more children than colors in the provided `colorScale`.

*default (provided by default theme):* See [grayscale theme] for more detail

```playground
<VictoryStack
  colorScale={["tomato", "orange", "gold"]}
>
  <VictoryBar
    data={[{x: "a", y: 2}, {x: "b", y: 3}, {x: "c", y: 5}]}
  />
  <VictoryBar
    data={[{x: "a", y: 1}, {x: "b", y: 4}, {x: "c", y: 5}]}
  />
  <VictoryBar
    data={[{x: "a", y: 3}, {x: "b", y: 2}, {x: "c", y: 6}]}
  />
</VictoryStack>
```


### containerComponent

`VictoryStack` uses the standard `containerComponent` prop. [Read about it in detail here](https://formidable.com/open-source/victory/docs/common-props#containercomponent)

```jsx
containerComponent={<VictoryVoronoiContainer dimension="x"/>}
```
### domain

`VictoryStack` uses the standard `domain` prop. [Read about it in detail here](https://formidable.com/open-source/victory/docs/common-props#domain)

**note: `VictoryStack` controls the `domain` prop of its children.**

```jsx
domain={{x: [0, 100], y: [0, 1]}}
```

### domainPadding

`VictoryStack` uses the standard `domainPadding` prop. [Read about it in detail here](https://formidable.com/open-source/victory/docs/common-props#domainpadding)

**note: `VictoryStack` controls the `domainPadding` prop of its children.**

```jsx
domainPadding={{x: [10, -10], y: 5}}
```

### eventKey

`VictoryStack` uses the standard `eventKey` prop to specify how event targets are addressed. **This prop is not commonly used.** [Read about the `eventKey` prop in more detail here](https://formidable.com/open-source/victory/docs/common-props#eventkey)

```jsx
eventKey="x"
```

### events

`VictoryStack` uses the standard `events` prop. [Read about it in more detail here](https://formidable.com/open-source/victory/docs/common-props#events)

See the [Events Guide] for more information on defining events.

**Note: `VictoryStack` coordinates events between children using the `VictorySharedEvents` and the `sharedEvents` prop**

```playground
<VictoryStack
  events={[{
    childName: "all",
    target: "data",
    eventHandlers: {
      onClick: () => {
        return [
          {
            childName: "area-2",
            target: "data",
            mutation: (props) => ({ style: Object.assign({}, props.style, { fill: "gold" }) })
          }, {
            childName: "area-3",
            target: "data",
            mutation: (props) => ({ style: Object.assign({}, props.style, { fill: "orange" }) })
          }, {
            childName: "area-4",
            target: "data",
            mutation: (props) => ({ style: Object.assign({}, props.style, { fill: "red" }) })
          }
        ];
      }
    }
  }]}
>
  <VictoryArea name="area-1" data={sampleData}/>
  <VictoryArea name="area-2" data={sampleData}/>
  <VictoryArea name="area-3" data={sampleData}/>
  <VictoryArea name="area-4" data={sampleData}/>
</VictoryStack>
```
### groupComponent

`VictoryStack` uses the standard `groupComponent` prop. [Read about it in detail here](https://formidable.com/open-source/victory/docs/common-props#groupcomponent)

*default:* `<g/>`

```jsx
groupComponent={<g transform="translate(10, 10)" />}
```
### height

`VictoryStack` uses the standard `height` prop. [Read about it here](https://formidable.com/open-source/victory/docs/common-props#height)

*default (provided by default theme):* `height={300}`

```jsx
height={400}
```

### horizontal

The `horizontal` prop determines whether the bars of any `VictoryBar` children supplied to `VictoryStack` will be laid out vertically or horizontally. The bars will be vertical if this prop is false or unspecified, or horizontal if the prop is set to true.

### labels

The `labels` prop defines labels that will appear above each stack of data. This prop should be given as an array of values or as a function of data. If given as an array, the number of elements in the array should be equal to the length of the data array. Group labels will appear above the center series of the group, and will override the `labels` prop of child components. Omit this prop, and set `labels` props on children for individual labels.

```jsx
labels={["spring", "summer", "fall", "winter"]}`, `labels={(datum) => datum.title}
```

### labelComponent

The `labelComponent` prop takes a component instance which will be used to render labels for each stack. The new element created from the passed `labelComponent` will be supplied with the following props: `x`, `y`, `index`, `datum`, `verticalAnchor`, `textAnchor`, `angle`, `style`, `text`, and `events`. Any of these props may be overridden by passing in props to the supplied component, or modified or ignored within the custom component itself. If `labelComponent` is omitted, a new [VictoryLabel] will be created with the props described above.

*default:* `<VictoryLabel/>`

```jsx
labelComponent={<VictoryLabel dy={20}/>}
```

### name

The `name` prop is used to reference a component instance when defining shared events.

```jsx
name="series-1"
```

### origin

**The `origin` prop is only used by polar charts, and is usually controlled by `VictoryChart`. It will not typically be necessary to set an `origin` prop manually**

[Read about the `origin` prop in detail](https://formidable.com/open-source/victory/docs/common-props#origin)


### padding

`VictoryStack` uses the standard `padding` prop. [Read about it here](https://formidable.com/open-source/victory/docs/common-props#padding)

*default (provided by default theme):* `padding={50}`

```jsx
padding={{ top: 20, bottom: 60 }}
```

### polar

`VictoryStack` uses the standard `polar` prop. [Read about it here](https://formidable.com/open-source/victory/docs/common-props#polar)

### range

**The `range` prop is usually controlled by `VictoryChart`. It will not typically be necessary to set a `range` prop manually**

[Read about the `range` prop in detail](https://formidable.com/open-source/victory/docs/common-props#range)

### scale

`VictoryStack` uses the standard `scale` prop. [Read about it here](https://formidable.com/open-source/victory/docs/common-props#scale)

*default:* `scale="linear"`

```jsx
scale={{x: "linear", y: "log"}}
```

### sharedEvents

**The `sharedEvents` prop is used internally to coordinate events between components. It should not be set manually.**

### sortKey

`VictoryStack` uses the standard `sortKey` prop. [Read about it here](https://formidable.com/open-source/victory/docs/common-props#sortkey)

See the [Data Accessors Guide] for more detail on formatting and processing data.

```jsx
sortKey="x"
```

### standalone

`VictoryStack` uses the standard `standalone` prop. [Read about it here](https://formidable.com/open-source/victory/docs/common-props#standalone)

**note:** When `VictoryGroup` is nested within a component like `VictoryChart`, this prop will be set to `false`

*default:* `standalone={true}`


### style

`VictoryStack` uses the standard `style` prop. [Read about it here](https://formidable.com/open-source/victory/docs/common-props#style)

Styles on children of `VictoryGroup` will override styles set on the `VictoryGroup` component.

*default (provided by default theme):* See [grayscale theme] for more detail

```playground
<VictoryStack
  style={{
    parent: { border: "1px solid #ccc" },
    data: { stroke: "black", strokeWidth: 3 }
  }}
>
  <VictoryBar
    style={{ data: { fill: "#c43a31" } }}
    data={[{x: "a", y: 2}, {x: "b", y: 3}, {x: "c", y: 5}]}
  />
  <VictoryBar
    data={[{x: "a", y: 1}, {x: "b", y: 4}, {x: "c", y: 5}]}
  />
  <VictoryBar
    data={[{x: "a", y: 3}, {x: "b", y: 2}, {x: "c", y: 6}]}
  />
</VictoryStack>
```

### theme

`VictoryStack` uses the standard `theme` prop. [Read about it here](https://formidable.com/open-source/victory/docs/common-props#theme)

See the [Themes Guide] for information about creating custom themes.

*default:* `theme={VictoryTheme.grayscale}`

```jsx
theme={VictoryTheme.material}
```

### width

`VictoryStack` uses the standard `width` prop. [Read about it here](https://formidable.com/open-source/victory/docs/common-props#width)

*default (provided by default theme):* `width={450}`

```jsx
width={400}
```

### xOffset

The `xOffset` prop is used for grouping stacks of bars. This prop will be set by the `VictoryGroup` component wrapper, or can be set manually.



[Animations Guide]: https://formidable.com/open-source/victory/guides/animations
[Data Accessors Guide]: https://formidable.com/open-source/victory/guides/data-accessors
[Custom Components Guide]: https://formidable.com/open-source/victory/guides/custom-components
[Events Guide]: https://formidable.com/open-source/victory/guides/events
[Themes Guide]: https://formidable.com/open-source/victory/guides/themes
[grayscale theme]: https://github.com/FormidableLabs/victory-core/blob/master/src/victory-theme/grayscale.js
[VictoryArea]: https://formidable.com/open-source/victory/docs/victory-area
[VictoryAxis]: https://formidable.com/open-source/victory/docs/victory-axis
[VictoryBar]: https://formidable.com/open-source/victory/docs/victory-bar
[VictoryCandlestick]: https://formidable.com/open-source/victory/docs/victory-candlestick
[VictoryErrorBar]: https://formidable.com/open-source/victory/docs/victory-error-bar
[VictoryGroup]: https://formidable.com/open-source/victory/docs/victory-group
[VictoryLine]: https://formidable.com/open-source/victory/docs/victory-line
[VictoryScatter]: https://formidable.com/open-source/victory/docs/victory-scatter
[VictoryStack]: https://formidable.com/open-source/victory/docs/victory-stack
[VictoryVoronoi]: https://formidable.com/open-source/victory/docs/victory-voronoi
[VictoryLabel]: https://formidable.com/open-source/victory/docs/victory-label
