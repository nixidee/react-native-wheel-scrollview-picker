<h1 align="center">react-native-wheel-scrollview-picker</h1>
 
 <p align="center">
   <img src="./demo.gif">
</p>
  
<p align="center">A pure js picker for React Native</h1>


> - Original repository by @veizz: [react-native-picker-scrollview](https://github.com/veizz/react-native-picker-scrollview).
> - Fork by @yasemincidem who added the real cross platform behavior and datepicker [react-native-wheel-scroll-picker](https://github.com/yasemincidem/react-native-picker-scrollview).
> - This is the third fork of repository, since it seems that @yasemincidem is no longer supporting [react-native-wheel-scroll-picker](https://github.com/yasemincidem/react-native-picker-scrollview).
> - This a fork of repository from rheng001, since some changes seem to broken this package

---

## Fixes
- added use of snapToOffsets as default instead of snapToInterval (useSnapToInterval=true can overwrite it)
- decelerationRate can be passed
- scrollToAnimated can be passed
- changed momentumStarted from state to ref

## Table of Contents

1. [Features](#features)
2. [Installation](#installation)
3. [Usage](#usage)
   - [Example](#usage)
4. [Props](#props)
5. [License](#license)

## Installation

```sh
yarn add react-native-wheel-scrollview-picker
# or
npm install react-native-wheel-scrollview-picker --save
```

## Usage

```jsx
import React, { Component } from "react";
import ScrollPicker from "react-native-wheel-scrollview-picker";

export default class SimpleExample extends Component {
  render() {
    return (
      <ScrollPicker
        dataSource={["1", "2", "3", "4", "5", "6"]}
        selectedIndex={1}
        renderItem={(data, index) => {
          //
        }}
        onValueChange={(data, selectedIndex) => {
          //
        }}
        wrapperHeight={180}
        wrapperBackground="#FFFFFF"
        itemHeight={60}
        highlightColor="#d8d8d8"
        highlightBorderWidth={2}
        decelerationRate="fast"    // optional: "fast" | "normal" | number (default: "normal")
        useSnapToInterval={false}  // optional: boolean (default: false)
        scrollToAnimated={true}    // optional: boolean (default: false)
      />
    );
  }
}
```

## Props

| Props                |           Description            |  Type  |   Default |
| -------------------- |:--------------------------------:| :----: |----------:|
| dataSource           |        Data of the picker        | Array  |           |
| selectedIndex        |    selected index of the item    | number |         1 |
| wrapperHeight        |       height of the picker       | number |           |
| wrapperBackground    |        picker background         | string |    '#FFF' |
| itemHeight           |       height of each item        | number |           |
| highlightColor       |   color of the indicator line    | number | "#d8d8d8" |
| highlightBorderWidth |      width of the indicator      | string |         1 |
| activeItemTextStyle  |  Active Item Text object style   | object |           |
| itemTextStyle        |      Item Text object style      | object |           |
| useSnapToInterval    |       Item snap behaviour        | object |     false |
| scrollToAnimated     |         smooth scrollTo          | object |     false |
| decelerationRate     | set decelerationRate of momentum | object |    normal |

## Extra

If you want to scroll to target index, you need the instance function, and that is exposed some functions to parent components by using `useImperativeHandle` ,you can use it。

```jsx
import React from "react";
import { Button } from 'react-native';
import ScrollPicker from "react-native-wheel-scrollview-picker";

const dataSource = ["1", "2", "3", "4", "5", "6"]
export const Demo = () => {
  const ref = React.useRef();
  const [index, setIndex] = React.useState(0);
  const onValueChange = (data, selectedIndex) => {
    setIndex(selectedIndex);
  };

  const onNext = () => {
    if (index === dataSource.length - 1) return;
    setIndex(index + 1);
    ref.current && ref.current.scrollToTargetIndex(index + 1);
  }
  return (
    <ScrollPicker
      ref={ref}
      dataSource={dataSource}
      selectedIndex={index}
    />
    <Button
      onPress={onNext}
      title="Next one"
    />
  );
};
```

## Author

- [Richard Heng](http://richardheng.me/)

## License

MIT
