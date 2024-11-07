# Material Symbols Icons for Flutter

[![pub package](https://img.shields.io/pub/v/material_symbols_icons.svg)](https://pub.dev/packages/material_symbols_icons)

### Using Official Material Symbols Icons variable fonts version 2.791 released 10/17/2024 from [material font repo](https://github.com/google/material-design-icons) with 3736 icons.

The dart docs and vscode hover docs now include icon preview (if you install [the
three MaterialSymbols*.ttf fonts](https://github.com/google/material-design-icons/tree/master/variablefont) locally on your machine).

[Complete interactive icon map can be found here.](https://timmaffett.github.io/material_symbols_icons)

----------------------

[<img src="https://github.com/timmaffett/material_symbols_icons/raw/master/media/example.png" width="100%">](https://timmaffett.github.io/material_symbols_icons)

### (with full variation support and automatic code generation capability for updating icon definition files)

This package is intended to be COMPLETELY compatible with the future flutter 'native' implementation of Material Symbols Icons support
as defined in this [specification document](https://docs.google.com/document/d/1UHRKDl8-lzl_hW_K2AHnpMwvdPo0vGPbDI7mqACWXJY/edit).
Once flutter natively supports the Material Symbols icons all that should be needed is removal of the import statement for this package.

Icons are referenced using the [Symbols] class and the name of the desired icon.  For Example `Symbols.pedal_bike`, or you can access
the rounded version using `Symbols.pedal_bike_rounded` and the sharp version using `Symbols.pedal_bike_sharp`.

These icons also support the complete set of icon variation parameters defined for the Material Symbols Icons.  This includes setting fill/not filled, various weights, grades and optical sizes.

## [Live Flutter Web Example with Material Symbols Icons style and variation customization](https://timmaffett.github.io/material_symbols_icons)

Here is a [live example](https://timmaffett.github.io/material_symbols_icons) of the current version of this package where you can test any Material Symbols icon name to verify it's availability.  The example also allows playing with all of the font variation options to explore further customizing the look of our Material Symbols.

To use this package simply

```dart
import 'package:material_symbols_icons/symbols.dart';

final myIcon = Icon( Symbols.add_task);
final myRoundedIcon = Icon( Symbols.add_task_rounded);
final mySharpIcon = Icon( Symbols.add_task_sharp);

```

and then access the icons from the `Symbols` class.

This class contains outlined, rounded and sharp versions of every icon.  You access them using `Symbols.iconname` (for the outlined version),
and `Symbols.iconname_rounded` or `Symbols.iconname_sharp` for the rounded and sharp versions respectively.

Additionally the Material Symbols [specification](https://docs.google.com/document/d/1UHRKDl8-lzl_hW_K2AHnpMwvdPo0vGPbDI7mqACWXJY/) document also specifies
a Symbols.get(String name, SymbolStyle style) method that can be used to return the IconData for any icon using it's
icon name and style (SymbolStyle.outlined, SymbolStyle.rounded, or SymbolStyle.sharp).  The get() method is not included on
Symbols by default to avoid needlessly bringing in the large name->codepoint map, it can be included by using import 'package:material_symbols_icons/get.dart'.
When using the get() method *tree-shaking must be turned off* using
`--no-tree-shake-icons` as there is no way for the compiler to know what icons are being used.
`SymbolsGet.values` can be used to access an `Iterable<String>` of the icon names for each available icon.
`SymbolsGet.map` can be used to access a `Map<String,int>` of the icon names to unicode code points for each icon.
You can optionally `import 'package:material_symbols_icons/symbols_map.dart';` to force
references to every icon's IconData object and prevent all tree-shaking from occuring.
This is used by the example app to allow previewing of all icons.

```dart
// `import 'package:material_symbols_icons/symbols_map.dart';` or 
// optionally turn off icon tree-shaking when using the get() method!
// ( build with `--no-tree-shake-icons` )
import 'package:material_symbols_icons/symbols_map.dart';
import 'package:material_symbols_icons/get.dart';

final iconRounded = SymbolsGet.get('airplane',SymbolStyle.rounded);
final iconSharp = SymbolsGet.get('airplane',SymbolStyle.sharp);
final iconOutlined = SymbolsGet.get('airplane',SymbolStyle.outlined);

// access iconname->codepoint map
final unicodeCodePointAirplane = SymbolsGet.map['airplane'];

// iterate on and print all available icon names
for(var iconname in SymbolsGet.values) {
  print(iconname);
}

```

----------------------------------------------------------------

All icons share the same name they had in the Material Icons [Icons] class.
All icon names that start with a number (like `360` or `9mp`) but have their icon name changed so that the number is written out and may have
added `_` separating numbers.  For example `3d_rotation` becomes `threed_rotation`, `123` becomes `onetwothree`, `360` becomes `threesixty`,
`9mp` becomes `nine_mp`, `2d` becomes `twod`, `3d` becomes `threed`.
This is done to generate valid dart class member names.
For example if you want to access the icon with the name `360` you use `Symbols.threesixty` instead.

Additionally the iconnames `class`, `switch`, and `try` have also been renamed with a trailing `'_'` (`class_`, `switch_` and `try_`) as these are dart language
reserved words.  `door_back` and `door_front` have also been renamed `door_back_door` and `door_front_door` respectively.
`power_rounded` becomes `power_rounded_power` (and therefor `power_rounded_power_rounded` for the rounded version and
`power_rounded_power_sharp` for the sharp version.
(likewise `error_circle_rounded` becomes `error_circle_rounded_error`).

----------------------------------------------------------------

The middle 4 digit number (for example `2758`) of the version number corresponds to the version number of of the variable fonts used to generated the icon data (with the decimal point removed).  (`2758` corresponds to version number (`Version 2.758`)).  This is found in the `name` table of the variable font true type (.ttf)).  Thus it can be used to determine the variable source font TTF version numbers used to generate a given version of this package.  (The version number can also be found in the `fontRevision` property of the `head` table of the .ttf font files).

----------------------------------------------------------------

The Material Symbols Icon fonts are variable fonts, so it is possible to further modify (or animate!) the icons by specifying your own parameters for fill, weight, grade, and optical size when creating your icons.  The [live web example app](https://timmaffett.github.io/material_symbols_icons) will show you a preview of the `Icon(...)` statement required to accomplish the currently visible axis settings.  This takes into account the default configuration for each axis, wichi is weight at 400, optical size at 48, grade at 0 and fill also 0.  Any axis which differs from the default will be included in the shown `Icon(...)` example.

```dart
    
final myIcon = Icon( Symbols.settings,
                        fill: 1, weight: 700, grade: 0.25, opticalSize: 48 );

```

]You can also set application wide defaults using your `IconThemeData` within your Theme.

```dart
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    /*
      Set default IconThemeData() for ALL icons
    */
    return MaterialApp(
      title: 'Material Symbols Icons For Flutter',
      theme: ThemeData(
        primarySwatch: Colors.teal,
        useMaterial3: true,
        fontFamily: 'Roboto',
        iconTheme: const IconThemeData(color: Colors.black,
                                       fill: 0,
                                       weight: 100,
                                       opticalSize: 48),
      ),
      home: const MyHomePage(title: 'Material Symbols Icons For Flutter'),
    );
  }
}
```

---------------------------------------------------------------

This package includes an automatic generator program so that the user has the option of regenerating the package at any time with the most current Material Symbols Icons definitions.  This program downloads the latest Material Symbols fonts from the github repository [https://github.com/google/material-design-icons](https://github.com/google/material-design-icons), and their corresponding codepoint definition files.  It will then automatically create the material_symbols_icons.dart definition source file.    This automatic generations allows this package to use Github CI routines to ensure that it is always up to date and in-sync with the latet Material Symbols defintions.

(For users of the previous Flutter alternatives for Material Symbols Icons support - No more finding an icon on [google's material symbols icon browser](https://fonts.google.com/icons?icon.style=Outlined) and then trying to use it's name, and then discovering that it is missing, or worse yet having the incorrect icon appear!)

---------------------------------------------------------------

<img src="https://github.com/timmaffett/material_symbols_icons/raw/master/media/google_icon_fonts.png" width="100%">

---------------------------------------------------------------

## Material Symbols Icons - Google's replacement to the original material design icons

Following background information info from [google's material design icon repo](https://github.com/google/material-design-icons/raw/master/README.md).

These newer icons can be browsed in a more user-friendly way at [google's material symbols icon browser](https://fonts.google.com/icons?icon.style=Outlined). Use the popdown menu near top left to choose between the two sets; Material Symbols is the default.

These icons were built/designed as variable fonts first (based on the 24 px designs from Material Icons). There are three separate Material Symbols variable fonts, which also have static icons available (but those do not have all the variations available, as that would be hundreds of styles):

- Outlined
- Rounded
- Sharp
- Note that although there is no separate Filled font, the Fill axis allows access to filled styles—in all three fonts.

Each of the fonts has these design axes, which can be varied in CSS, or in many more modern design apps:

- Optical Size (opsz) from 20 to 48 px. The default is 24.
- Weight from 100 (Thin) to 700 (Bold). Regular is 400.
- Grade from -50 to 200. The default is 0 (zero).
- Fill from 0 to 100. The default is 0 (zero).

What is currently _not_ available in Material Symbols?
- only the 20 and 24 px versions are designed with perfect pixel-grid alignment
- the only pre-made fonts are the variable fonts
- there are no two-tone icons

---------------------------------------------------------------

NOTE: The following is specific to this material_symbols_icons package and will not be present in the future flutter native `Symbols` class,
although the code from this package could mimic this behavior in the future if desired.

If you find yourself using more than one of the styles simultaneously this package has a method of specifying default variations on a *per* style basis using:

```dart
    MaterialSymbolsBase.setOutlinedVariationDefaults(
        color: Colors.red,
        fill: 1,
        weight: 300,
        grade: 0,
        opticalSize: 40.0);
    MaterialSymbolsBase.setRoundedVariationDefaults(
        color: Colors.blue,
        fill: 0,
        weight: 400,
        grade: 200,
        opticalSize: 48.0);
    MaterialSymbolsBase.setSharpVariationDefaults(
        color: Colors.teal,
        fill: 0,
        weight: 600,
        grade: 0.25,
        opticalSize: 20.0);

    // then use VariedIcon.varied() to create your icons - instead of Icon() directly
    Icon example = VariedIcon.varied( Symbols.developer );

```

If the `setOutlinedVariationDefaults`, `setRoundedVariationDefaults` or `setSharpVariationDefaults`  methods are used then the icons need to be
created using `VariedIcon.varied()` call instead of `Icon()` directly.
