# react-component-export-image

## Introduction

- Export component as jpeg, png or pdf
- Each export expect a {React.RefObject} node, optional fileName, and optional html2CanvasOptions object which you wish to pass it to html2Canvas
- exportComponentAsPDF also accepts an optional pdfOptions object with these optional fields {x, y, orientation}
```
x = 100 (width in pixels)
y = 50 (height in pixels)
orientation = 'p' (portrait) OR 'l' (landscape)
```

## How to Upgrade
The previous way of using an export looked like this: 
> exportComponentAsJPEG(node, fileName, type, backgroundColor, options)

The new way: pass node & an optional object with only the fields you need. 
- backgroundColor is no longer accepted in this main object, but is accepted in the "html2CanvasOptions" object, which is passed directly to html2canvas

> exportComponentAsJPEG(node, {fileName, type, html2CanvasOptions})

- exportComponentAsPDF also accepts an additional pdfOptions object (see introduction)

> exportComponentAsPDF(node, {fileName, type, html2CanvasOptions, pdfOptions})

## Code Samples

### Component
 ```jsx
import { exportComponentAsJPEG, exportComponentAsPDF, exportComponentAsPNG } from 'react-component-export-image';
import React from 'react';

class ComponentToPrint extends React.Component {
  render() {
    return <div>Hello World</div>;
  }
}
export default class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.componentRef = React.createRef();
  }

  render() {
    return (
      <React.Fragment>
        <ComponentToPrint ref={this.componentRef} />
        <button onClick={() => exportComponentAsJPEG(node: this.componentRef)}>
          Export As JPEG
        </button>
        <button onClick={() => exportComponentAsPDF(node: this.componentRef)}>
          Export As PDF
        </button>
        <button onClick={() => exportComponentAsPNG(node: this.componentRef)}>
          Export As PNG
        </button>
      </React.Fragment>
    );
  }
}
```
### Function component
```jsx
import { exportComponentAsJPEG, exportComponentAsPDF, exportComponentAsPNG } from 'react-component-export-image';
import React, { useRef } from 'react';

const ComponentToPrint = React.forwardRef((props, ref) => (
  <div ref={ref}>Hello World</div>
));

const MyComponent = () => {
  const componentRef = useRef();

  return (
    <React.Fragment>
      <ComponentToPrint ref={componentRef} />
      <button onClick={() => exportComponentAsJPEG(node: componentRef)}>
        Export As JPEG
      </button>
      <button onClick={() => exportComponentAsPDF(node: componentRef)}>
        Export As PDF
      </button>
      <button onClick={() => exportComponentAsPNG(node: componentRef)}>
        Export As PNG
      </button>
    </React.Fragment>
  );
};

export default MyComponent;
```

## Installation

```bash
npm i react-component-export-image
or
yarn add react-component-export-image
```
