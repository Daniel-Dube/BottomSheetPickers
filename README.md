# BottomSheetPickers
[ ![Download](https://api.bintray.com/packages/philliphsu/maven/bottom-sheet-pickers/images/download.svg) ](https://bintray.com/philliphsu/maven/bottom-sheet-pickers/_latestVersion)

BottomSheetPickers is a set of new time pickers for Android that can be used in place of the stock
time picker. As seen in my [Clock+](https://github.com/philliphsu/ClockPlus) app.

**Number Pad**

<img src="screenshots/number-pad-12h-light.png" width="180" height="320">
<img src="screenshots/number-pad-24h-light.png" width="180" height="320">
<img src="screenshots/number-pad-12h-dark.png" width="180" height="320">
<img src="screenshots/number-pad-24h-dark.png" width="180" height="320">

**Grid Picker**

<img src="screenshots/12h-grid-light.png" width="180" height="320">
<img src="screenshots/minutes-grid-light.png" width="180" height="320">
<img src="screenshots/24h-grid-light.png" width="180" height="320">

<img src="screenshots/12h-grid-dark.png" width="180" height="320">
<img src="screenshots/minutes-grid-dark.png" width="180" height="320">
<img src="screenshots/24h-grid-dark.png" width="180" height="320">

Support for API level 14 and up. This library is based on code from the following AOSP repositories:
* https://android.googlesource.com/platform/frameworks/opt/datetimepicker
* https://android.googlesource.com/platform/packages/apps/Calculator

## Installation
Add the following dependency to your module's `build.gradle`:
```groovy
dependencies {
  compile 'com.philliphsu:bottomsheetpickers:1.0.1'
}
```

## Usage
**You must be using the support library version of `Activity` or `Fragment` to use this library
properly.** The pickers are indirect subclasses of `android.support.v4.app.DialogFragment`.

Implement `BottomSheetTimePickerDialog.OnTimeSetListener` in your `Activity` or `Fragment`:

```java
@Override
public void onTimeSet(ViewGroup viewGroup, int hourOfDay, int minute) {
    // Do something with the time.
}
```

Then create an instance of your desired time picker dialog and `show()` it.

```java
NumberPadTimePickerDialog dialog = NumberPadTimePickerDialog.newInstance(
    MainActivity.this  // your implementation of OnTimeSetListener
);
dialog.show(getSupportFragmentManager(), TAG);
```

```java
Calendar now = Calendar.getInstance();
GridTimePickerDialog dialog = GridTimePickerDialog.newInstance(
    MainActivity.this,  // your implementation of OnTimeSetListener
    now.get(Calendar.HOUR_OF_DAY),
    now.get(Calendar.MINUTE),
    DateFormat.is24HourFormat(MainActivity.this));
dialog.show(getSupportFragmentManager(), TAG);
```

### Theming
The pickers automatically use your current theme's `colorAccent` defined in your `styles.xml`.

You can specify whether to use a light (default) or dark theme:
* in code with the dialog's `setThemeDark(boolean dark)` method. **Call this before `show()`ing the dialog.**
* in `styles.xml` by specifying a boolean value for the attribute `themeDark` in your theme.

```xml
<item name="themeDark">true</item>
```

> **NOTE**: `setThemeDark(boolean dark)` takes precedence over the value specified in XML.

## FAQ
> Why is the library named **BottomSheetPickers** if it only has time pickers?
Will there be more pickers in the future other than for time (e.g. date picker)?

My original plan was to release only time pickers, but then I figured the library should have a
matching date picker. So I refactored the package structure to accommodate the addition, as well
as renamed the library to the more general **BottomSheetPickers**. However, as of October 2016,
a date picker is not a priority feature. Though in case of future developments, I left the
packages and library name as general as possible.

> Why isn't the date picker a priority feature?

In my opinion, there's not much to improve on the stock date picker; the interaction with a
bottom sheet date picker would feel almost the same as the stock date picker. Additionally,
I would want to retain the general look and feel of the stock date picker, but the latest style
seen in the [Material Design spec](https://material.google.com/components/pickers.html#pickers-date-pickers)
and introduced in Android 6.0 is not reflected in the AOSP `datetimepicker` repository.

## License
```
Copyright 2016 Phillip Hsu

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```