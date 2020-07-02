
# react-grid-heatmap

![Screenshot](https://raw.githubusercontent.com/arunghosh/react-grid-heatmap/master/example/screenshot.png)

> A react component for heatmap visualisation in grid layout

[![NPM](https://img.shields.io/npm/v/react-grid-heatmap.svg)](https://www.npmjs.com/package/react-grid-heatmap) [![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

## Install

```bash
npm install --save react-grid-heatmap
```

## Usage

**Mandatory fields**

| Name | Type         | Sample                        |
| ---- | ------------ | ----------------------------- |
| data | `number[][]` | `[[1,2,3], [4,5,6], [7,8,9]]` |



```tsx
import React from 'react'
import { HeatMapGrid } from 'react-grid-heatmap'

const xLabels = new Array(24).fill(0).map((_, i) => `${i}`)
const yLabels = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri']
const data = new Array(yLabels.length)
  .fill(0)
  .map(() =>
    new Array(xLabels.length).fill(0).map(() => Math.floor(Math.random() * 50 + 50))
  )

const App = () => {
  return (
    <HeatMapGrid
      data={data}
      xLabels={xLabels}
      yLabels={yLabels}
    />
  )
}

export default App
```

**Optional Parameters**

| Name         | Type     | Description/Example                                     | Default Value |
| ------------ | -------- | ------------------------------------------------------- | ------------- |
| xLabels      | string[] | `['1am', '2am', '3am']`                                 | `null`        |
| yLabels      | string[] | `['Sun', 'Mon']`                                        | `null`        |
| cellHeight   | string   | Height of each cell of the heatmap                      | `"2rem"`      |
| onClick      | function | Adds an handler to cell click<br>`(x, y) => void`       | `null`        |
| square       | boolean  | If set to `true` will render cells as square            | `false`       |
| xLabelsPos   | string   | Location of y labels. It can be `top` or `bottom`       | `"top"`       |
| yLabelsPos   | string   | Location of y labels. It can be `left` or `right`       | `"left"`      |
| cellRender   | function | Render custom content in cell.<br>`(x, y, value) => ()` | `null`        |
| cellStyle    | function | To set custom cell style<br>`(x, y, ratio) => {}`     | `null`        |
| xLabelsStyle | function | To set custom cell style<br>`(index) => {}`     | `null`        |
| yLabelsStyle | function | To set custom cell style<br>`(index) => {}`     | `null`        |


A sample code with all parameters
```js
import React from 'react'
import { HeatMapGrid } from 'react-grid-heatmap'

const xLabels = new Array(24).fill(0).map((_, i) => `${i}`)
const yLabels = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri']
const data = new Array(yLabels.length)
  .fill(0)
  .map(() =>
    new Array(xLabels.length)
      .fill(0)
      .map(() => Math.floor(Math.random() * 50 + 50))
  )

const App = () => {
  return (
    <div
      style={{
        width: '100%'
      }}
    >
      <HeatMapGrid
        data={data}
        xLabels={xLabels}
        yLabels={yLabels}
        // Reder cell with tooltip
        cellRender={(x, y, value) => (
          <div title={`Pos(${x}, ${y}) = ${value}`}>{value}</div>
        )}
        xLabelsStyle={(index) => ({
          color: index % 2 ? 'transparent' : '#777',
          fontSize: '.8rem'
        })}
        yLabelsStyle={() => ({
          fontSize: '.7rem',
          textTransform: 'uppercase',
          color: '#777'
        })}
        cellStyle={(_x, _y, ratio) => ({
          background: `rgb(12, 160, 44, ${ratio})`,
          fontSize: '.8rem',
          color: `rgb(0, 0, 0, ${ratio / 2 + 0.4})`
        })}
        cellHeight='2rem'
        xLabelsPos='bottom'
        onClick={(x, y) => alert(`Clicked (${x}, ${y})`)}
        yLabelsPos='right'
        square
      />
    </div>
  )
}

export default App

```

## License

MIT © [arunghosh](https://github.com/arunghosh)