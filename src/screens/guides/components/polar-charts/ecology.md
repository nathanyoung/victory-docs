# Polar Charts

Victory supports polar charts for `VictoryArea`, `VictoryBar`, `VictoryLine` and `VictoryScatter`, as well as wrapper components like `VictoryChart`, `VictoryGroup` and `VictoryStack`. This guide provides explanations for polar-specific props as well as examples of polar charts.

```playground
<div>
  <VictoryChart polar
    domain={{ x: [0, 360] }}
    theme={VictoryTheme.material}
  >
    <VictoryPolarAxis tickCount={8}/>
    <VictoryBar
      data={sampleData}
      style={{ data: { fill: "#c43a31", stroke: "black", strokeWidth: 2 }}}
    />
  </VictoryChart>

  <VictoryChart
    theme={VictoryTheme.material}
  >
    <VictoryAxis tickCount={8}/>
    <VictoryBar
      data={sampleData}
      style={{ data: { fill: "#c43a31", stroke: "black", strokeWidth: 2 }}}
    />
  </VictoryChart>
</div>
```
## Creating Polar Charts

In most cases, creating a polar chart is as easy as adding the `polar` prop to the top level component (usually `VictoryChart`).

```playground
<VictoryChart polar
  domain={{ x: [0, 360] }}
  height={400} width={400}
>
  <VictoryBar
    style={{ data: { fill: "#c43a31", width: 50 }}}
    data={sampleData}
  />
</VictoryChart>
```

To configure axes for polar charts, use the [`VictoryPolarAxis`] component. `VictoryPolarAxis` uses a similar set of props to `VictoryAxis`

```playground
<VictoryChart polar
  domain={{ x: [0, 360] }}
  height={400} width={400}
>
  <VictoryPolarAxis dependentAxis
    style={{
      axis: {stroke: "none"},
      tickLabels: { fill: "none"},
       grid: { stroke: "grey", strokeDasharray: "4, 8" }
    }}
  />
  <VictoryPolarAxis
    tickValues={[0, 45, 90, 135, 180, 225, 270, 315]}
  />
  <VictoryBar
    style={{ data: { fill: "#c43a31", width: 50 }}}
    data={sampleData}
  />
</VictoryChart>
```

`VictoryGroup` and `VictoryStack` also work with polar charts:

```playground
<VictoryChart polar
  domain={{ x: [0, 360] }}
  height={400} width={400}
>
  <VictoryPolarAxis dependentAxis
    style={{
      axis: {stroke: "none"},
      tickLabels: { fill: "none"},
       grid: { stroke: "grey", strokeDasharray: "4, 8" }
    }}
  />
  <VictoryPolarAxis
    tickValues={[0, 45, 90, 135, 180, 225, 270, 315]}
  />
  <VictoryStack
    colorScale={["#ad1b11", "#c43a31", "#dc7a6b"]}
    style={{ data: { width: 50} }}
  >
    <VictoryBar data={sampleData}/>
    <VictoryBar data={sampleData}/>
    <VictoryBar data={sampleData}/>
  </VictoryStack>
</VictoryChart>
```

Add interactivity to polar charts with standard events, or container components. The following Polar charts work with `VictorySelectionContainer`, `VictoryVoronoiContainer`, and `VictoryZoomContainer`.

```playground
<VictoryChart polar
  domain={{ x: [0, 360] }}
  height={400} width={400}
  containerComponent={<VictoryZoomContainer/>}
>
  <VictoryPolarAxis dependentAxis
    style={{
      axis: {stroke: "none"},
      tickLabels: { fill: "none"},
       grid: { stroke: "grey", strokeDasharray: "4, 8" }
    }}
  />
  <VictoryPolarAxis
    tickValues={[0, 45, 90, 135, 180, 225, 270, 315]}
  />
  <VictoryStack
    colorScale={["#ad1b11", "#c43a31", "#dc7a6b"]}
    style={{ data: { width: 50} }}
  >
    <VictoryBar data={sampleData}/>
    <VictoryBar data={sampleData}/>
    <VictoryBar data={sampleData}/>
  </VictoryStack>
</VictoryChart>
```


[`VictoryPolarAxis`]: https://formidable.com/open-source/victory/docs/victory-polar-axis
