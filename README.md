# Vue-Date-Text

A date-text Vue component. Compatible with Vue 2.x

# Statement

Modify by vuejs-datepicker

## Install

``` bash
$ npm install vue-date-text --save
```
``` javascript
import DateText from 'vue-date-text';

Vue.component('my-component', {
    components: {
        DateText
    }
});
```


## Usage

``` html
<datetext></datetext>
```

*value* prop if passed should be a Date object

``` html
<script>
var state = {
    date: new Date(2016, 9,  16)
}
</script>
<datetext :value="state.date"></datetext>

```
Use `v-model` for two-way binding
``` html
<datetext v-model="state.date" name="uniquename"></datetext>
```
```
Use `dateText` only this date can select
``` html
<script>
var dateText: [
    {
      date: '2017-07-10',
      text: 'only 5 seat'
    },
    {
      date: '2017-07-11',
      text: 'only 6 seat'
    }
]
methods: {
    validate (day) {
      if (day.text && day.text.split(' ')[1] < 6) {
        console.log('not enough seat')
        return false
      }
      return true
    }
}
</script>
<datetext :dateText="dateText" :validate="validate"></datetext>
```

Emits events
``` html
<datetext v-on:selected="doSomethingInParentComponentFunction" v-on:opened="datepickerOpenedFunction" v-on:closed="datepickerClosedFunction"></datetext>
```
Inline always open version
``` html
<datetext :inline="true"></datetext>
```
## Available props

| Prop                  | Type          | Default     | Description                                             |
|-----------------------|---------------|-------------|---------------------------------------------------------|
| value                 | Date\|String  |             | Date value of the datepicker                            |
| id                    | String        |             | Input id                                                |
| format                | String        | dd MMM yyyy | Date formatting string                                  |
| language              | String        | en          | Translation for days and months                         |
| calendar-class        | String\|Object|             | CSS class applied to the calendar el                    |
| wrapper-class         | String\|Object|             | CSS class applied to the outer div                      |
| monday-first          | Boolean       | false       | To start the week on Monday                             |
| clear-button          | Boolean       | false       | Show an icon for clearing the date                      |
| clear-button-icon     | String        |             | Use icon for button (ex: fa fa-times)                   |
| calendar-button       | Boolean       | false       | Show an icon that that can be clicked                   |
| calendar-button-icon  | String        |             | Use icon for button (ex: fa fa-calendar)                |
| bootstrapStyling      | Boolean       | false       | Output bootstrap styling classes                        |
| initial-view          | String        | 'day'       | If 'month' or 'year', open on that view                 |
| dateText              | Array         |             | Sets text for date [{date: String|Date}, text: String]  |
| validate              | Function      | () => true  | validata the text for that date                         |

## Events

These events are emitted on actions in the datepicker

| Event         | Output     | Description                   |
|---------------|------------|-------------------------------|
| opened        |            | The picker is opened          |
| closed        |            | The picker is closed          |
| selected      | Date\|null | A date has been selected      |
| input         | Date\|null | Input value has been modified |
| cleared       |            | Selected date has been cleared|
| changedMonth  | Object     | Month page has been changed   |
| changedYear   | Object     | Year page has been changed    |
| changedDecade | Object     | Decade page has been changed  |


## Date formatting

NB. This is not very robust at all - use at your own risk! Needs a better implementation.

| Token | Desc                   | Example     |
|-------|------------------------|-------------|
| d     | day                    | 1           |
| dd    | 0 prefixed day         | 01          |
| D     | abbr day               | Mon         |
| su    | date suffix            | st, nd, rd  |
| M     | month number (1 based) | 1 (for Jan) |
| MM    | 0 prefixed month       | 01          |
| MMM   | abbreviated month name | Jan         |
| MMMM  | month name             | January     |
| yy    | two digit year         | 16          |
| yyyy  | four digit year        | 2016        |


#### Disabled Dates
Dates can disabled in a number of ways.

``` html
<script>
var state = {
    disabled: {
        to: new Date(2016, 0, 5), // Disable all dates up to specific date
        from: new Date(2016, 0, 26), // Disable all dates after specific date
        days: [6, 0], // Disable Saturday's and Sunday's
        dates: [ // Disable an array of dates
            new Date(2016, 9, 16),
            new Date(2016, 9, 17),
            new Date(2016, 9, 18)
        ]
    }
}
</script>
<datetext :disabled="state.disabled"></datetext>
```

#### Highlight Dates
Dates can be highlighted (e.g. for marking an appointment) in a number of ways. Important: You can only highlight dates, that aren't disabled.
Note: Both `to` and `from` properties are require to define a range of dates to highlight

``` html
<script>
var state = {
    highlighted: {
        to: new Date(2016, 0, 5), // Highlight all dates up to specific date
        from: new Date(2016, 0, 26), // Highlight all dates after specific date
        days: [6, 0], // Highlight Saturday's and Sunday's
        dates: [ // Highlight an array of dates
            new Date(2016, 9, 16),
            new Date(2016, 9, 17),
            new Date(2016, 9, 18)
        ]
    }
}
</script>
<datetext :highlighted="state.highlighted"></datetext>
```


#### Translations

Contributing guide - please use appropriate code from this [list](http://www.iana.org/assignments/language-subtag-registry/language-subtag-registry) as the translation property.

``` html
<datetext language="es"></datetext>
```
Available languages

| Abbr        | Language         |          |
| ----------- |------------------|----------|
| ar          | Arabic           |          |
| bg          | Bulgarian        |          |
| bs          | Bosnian          |          |
| cs          | Czech            |          |
| da          | Danish           |          |
| de          | German           |          |
| ee          | Estonian         |          |
| en          | English          | *Default*|
| es          | Spanish          |          |
| fi          | Finnish          |          |
| fr          | French           |          |
| he          | Hebrew           |          |
| hu          | Hungarian        |          |
| hr          | Croatian         |          |
| id          | Indonesian       |          |
| is          | Icelandic        |          |
| it          | Italian          |          |
| ja          | Japanese         |          |
| ko          | Korean           |          |
| lt          | Lithuanian       |          |
| nb-no       | Norwegian Bokmål |          |
| nl          | Dutch            |          |
| pl          | Polish           |          |
| pt-br       | Portuguese-Brazil|          |
| ro          | Romanian         |          |
| ru          | Russian          |          |
| sk          | Slovak           |          |
| sl-si       | Slovenian        |          |
| sv          | Swedish          |          |
| th          | Thai             |          |
| tr          | Turkish          |          |
| uk          | Ukrainian        |          |
| vi          | Vietnamese       |          |
| zh          | Chinese          |          |
