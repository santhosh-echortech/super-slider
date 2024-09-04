# Super Range Slider

The component is not re-rendered while user moves the thumb.<br/>
Even if there is a label, only the label component is re-rendered when values are changed.

RangeSlider uses React Native's Animated library to transform thumbs / label / selected rail.<br/>
These optimizations help to achieve as much native look & feel as possible using only the JS layer.



#### Version 1

The version 1 was using native Android and iOS views.<br/>

## Installation

- npm: `npm install --save react-native-super-slider`
- yarn: `yarn add react-native-super-slider`

## Usage

```
...

import RangeSlider from 'react-native-super-slider';

...

const renderThumb = useCallback(() => <Thumb/>, []);
const renderRail = useCallback(() => <Rail/>, []);
const renderRailSelected = useCallback(() => <RailSelected/>, []);
const renderLabel = useCallback(value => <Label text={value}/>, []);
const renderNotch = useCallback(() => <Notch/>, []);
const handleValueChange = useCallback((low, high) => {
  setLow(low);
  setHigh(high);
}, []);

...

<Slider
  style={styles.slider}
  min={0}
  max={100}
  step={1}
  floatingLabel
  renderThumb={renderThumb}
  renderRail={renderRail}
  renderRailSelected={renderRailSelected}
  renderLabel={renderLabel}
  renderNotch={renderNotch}
  onValueChanged={handleValueChange}
/>

...
```

### Properties

| Name                 | Description                                                                                                                                                                                                                                                                                          | Type                                                     |                   Default Value                   |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------- | :-----------------------------------------------: |
| `min`                | Minimum value of slider                                                                                                                                                                                                                                                                              | number                                                   |                  _**required**_                   |
| `max`                | Maximum value of slider                                                                                                                                                                                                                                                                              | number                                                   |                  _**required**_                   |
| `minRange`           | Minimum range of thumbs allowed to be selected **by the user**.<br/>**Note:** it is still possible to set values closer to each other than `minRange` programmatically.<br/>If `disableRange` is set to true, maximum value allowed for user will be `max` - `minRange`.                             | number                                                   |                        `0`                        |
| `step`               | Step of slider                                                                                                                                                                                                                                                                                       | number                                                   |                        `1`                        |
| `low`                | Low value of slider                                                                                                                                                                                                                                                                                  | number                                                   | Initially `min` value will be set if not provided |
| `high`               | High value of slider                                                                                                                                                                                                                                                                                 | number                                                   | Initially `max` value will be set if not provided |
| `floatingLabel`      | If set to `true`, labels will not take space in component tree. Instead they will be rendered over the content above the slider (like a small popup).                                                                                                                                                | boolean                                                  |                      `false`                      |
| `disableRange`       | Slider works as an ordinary slider with 1 control if `true`                                                                                                                                                                                                                                          | boolean                                                  |                      `false`                      |
| `disabled`           | Any user interactions will be ignored if `true`                                                                                                                                                                                                                                                      | boolean                                                  |                      `false`                      |
| `allowLabelOverflow` | If set to `true`, labels are allowed to be drawn outside of slider component's bounds.<br/>Otherwise label's edges will never get out of component's edges.                                                                                                                                          | boolean                                                  |                      `false`                      |
| `renderThumb`        | Should render the thumb. The `name` is the name of the thumb. This may be helpful if there is a need to render different thumbs for high and low values.                                                                                                                                             | `(name: 'high' &#124; 'low') => Node`                    |                  _**required**_                   |
| `renderRail`         | Should render the "rail" for thumbs.<br/>Rendered component **should** have `flex: 1` style so it won't fill up the whole space.                                                                                                                                                                     | `() => Node`                                             |                  _**required**_                   |
| `renderRailSelected` | Should render the selected part of "rail" for thumbs.<br/>Rendered component **should not** have `flex: 1` style so it fills up the whole space.                                                                                                                                                     | `() => Node`                                             |                  _**required**_                   |
| `renderLabel`        | Should render label above thumbs.<br/>If no function is passed, no label will be drawn.                                                                                                                                                                                                              | `(value: number) => Node`                                |                    `undefined`                    |
| `renderNotch`        | Should render the notch below the label (above the thumbs).<br/>Classic notch is a small triangle below the label.<br/>If `allowLabelOverflow` is not set to true, the notch will continue moving with thumb even if the label has already reached the edge of the component and can't move further. | `() => Node`                                             |                    `undefined`                    |
| `onValueChanged`     | Will be called when a value was changed.<br/>If `disableRange` is set to true, the second argument should be ignored.<br/>`fromUser` will be true if the value was changed by user's interaction.                                                                                                    | `(low: number, high: number, fromUser: boolean) => void` |                    `undefined`                    |
| `onSliderTouchStart` | Will be called when user starts interaction with slider.<br/>If `disableRange` is set to true, the second argument should be ignored.                                                                                                                                                                | `(low: number, high: number) => void`                    |                    `undefined`                    |
| `onSliderTouchEnd`   | Will be called when user ends interaction with slider.<br/>If `disableRange` is set to true, the second argument should be ignored.                                                                                                                                                                  | `(low: number, high: number) => void`                    |                    `undefined`                    |

All the other props (e.g. style) will be passed to root container component.


