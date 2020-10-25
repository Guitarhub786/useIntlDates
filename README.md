# useIntlDates

This package provides a quick and easy way to work with dates by returning an object containing commonly used, helpful date related data. It can also be passed an [options object](#options) to further customize the way the date information comes back, such as language (locale). Currently the package exports a custom React hook that returns an object with helpful date related data.

## What can I get out of this package

The `useintldates` hook returns an object named `dates` with various date related information allowing you to simply grab it and arrange it as you need. ([see example further down](#examples))<br /> <br />
The `dates` object returned by the `useintldates` hook contains the following key/value pairs:

- `dateDMY`: <br /> &nbsp; String containing the current date in the following format: "DD-MM-YYYY"

- `dateMDY`: <br /> &nbsp; String containing the current date in the following format: "MM-DD-YYYY"

- `dateYMD`: <br /> &nbsp; String containing the current date in the following format: "YYYY-MM-DD"

- `dayOfMonth`: <br /> &nbsp; String containing the day of the month in numeric form, e.g. "24"

- `monthLong`: <br /> &nbsp;String containing the month expressed as it's full name, e.g. "October"

- `monthNumeric`: <br /> &nbsp; String containing the month expressed in numeric form, e.g. "10"

- `monthShort`: <br /> &nbsp; String containing the month expressed as a short name, e.g. "Oct"

- `weekEndDate`: ([see use case further down](#examples)) <br /> &nbsp; String containing the full date of the Saturday of the current week in the following format: "YYYY-MM-DD"

- `weekStartDate`: ([see use case further down](#examples)) <br /> &nbsp; String containing the full date of the Sunday of the current week in the following format: "YYYY-MM-DD"

- `weekdayLong`: <br /> &nbsp; String containing the full name of the current weekday, e.g. "Saturday"

- `weekdayShort`: <br /> &nbsp; String containing the short name of the current weekday, e.g. "Sat"

- `year`: <br /> &nbsp; String containing the year expressed in numeric form, e.g. "2020"

## Dependencies

Great news! This code uses the power of the [JavaScript Intl object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat) to derive date related data. _No outside libraries or code_ is needed by this package, so no alerts that a dependency of a dependency has a security issue!<br />

### There are only 2 requirements for using this hook:

1.  **React**: The hook will only run in a React app v16.8.0 and up (React with support for hooks) and must be called in a functional component (not class based) in accordance with the [React docs](https://reactjs.org/docs/hooks-intro.html).

2.  The browser must support **Intl.DateTimeFormat.formatToParts**. Check [caniuse.com](https://caniuse.com/?search=Intl%3A%20DateTimeFormat%3A%20formatToParts) to make sure your target browsers are supported (_92.77% at time of writing_)

## Options

This hook will accept an object of these options ([see example below](#examples)):

1. `locale` [_optional_]<br />
   - default: "default" &nbsp; [_defaults to the locale identified by the browser_]<br />
   - This option allows you to pass a specific locale in the call to the Intl constructor used inside the hook. Any valid [locale acceptable to Intl](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat/DateTimeFormat) will work.<br />
   - Examples: "en-US", "da-DK", "de", "es"

## Examples

1. <u>_Common use_</u> - get date related info and format it as you need. The date information is based on the current day. Consider the following if it were _Saturday October 24, 2020_.<br />

```
import useintldates from 'useintldates'; // Bring the hook into your component

const MyComponent = () => {
  const dates = useintldates();
  // Retrieve and destructure the dates object from the useintldates hook

  return(
    <div>
    'Today is ${dates.weekdayLong} ${dates.monthShort} ${dates.dayOfMonth}, ${dates.year}'
    </div>
  )
}

// Would return "Today is Saturday Oct 24, 2020"
```

2. <u>_Date Ranges_</u> - Say you need the date for the first and last day of the week (Sunday and Saturday) to request a range of data from an API for the current week. <br /> <br />
   The following would make the request with the date of Sunday in the current week as the weekStartDate and the date for Saturday as the weekEndDate in the format 'YYYY-MM-DD' <br />

```
    import React, { useEffect } from 'react';
    import useintldates from 'useintldates'; // Bring the hook into your component

    const MyComponent = () => {
      const dates = useintldates();
      // Retrieve and destructure the dates object from the useintldates hook

    useEffect(() => {
      fetch('<https://urlToYourAPI/getByDateRange?startDate=${dates.weekStartDate}&endDate=${dates.weekEndDate}>') })

    return(

    // Use the returned data

    ) }
```

## Feature List

This list includes current and planned features. Check the issues page for a more exhaustive look at what features are being added and where they stand in the development process.

- [x] No dependencies, pure JavaScript code running in the hook
- [x] Options object accepts locale property to specify a locale/language for Intl to use
- [ ] Options object will allow a 'date' property to get back data from a specified date instead of only from the current day.
