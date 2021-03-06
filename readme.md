Support hotkeys other keyboard layouts
----------------------------------------------------------------------
It is plugin for FM [ranger](https://github.com/ranger/ranger) ;).
It allows to enable support command hotkeys for other keyboard layouts.
By default, Russian and Ukrainian are supported enable.
You can add or replace support your keyboard layouts for ranger.
To do this, replace the following fields: `other_keys`, `en_keys` in a file:
`~/.config/ranger/plugins/ranger_multiple_keyboard.py`
You can use merge mode (usually for `S-[0-9]`): field `other_keys_mm`.
Simple to fill in the other_keys_mm (see examples in plugin).
It do not applied for a pager.


Installation plugin for your ranger
----------------------------------------------------------------------
multiple_keyboard.py must be copied to `~/.config/ranger/plugins`


version 2.0
----------------------------------------------------------------------
fix crash on some file names(preview lags input) with translate-keys navigation in list files:
```
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xd0 in position 4: unexpected end of data
```

How to fill other `other_keys`, `en_keys` and `other_keys_mm`
----------------------------------------------------------------------
1. You can open your favourite text editor (need support utf-8) and input all keys for your
   native keyboard layout. For example to do it for German witch more intricate than Cyrillic group.
   1. Your En-inputting for all symbols ***without pressed Shift*** and below DE-inputting:
      1. de: `qwertzuiopü+asdfghjklöäyxcvbnm,.-` and up-numerical `^1234567890ß´`
      2. en: `qwertyuiop[]asdfghjkl;'zxcvbnm,./` and up-numerical `ˋ1234567890-=` (`ˋ` is replaced)
   2. Your En-inputting for alphabetic symbols ***with pressed Shift*** and below DE-inputting:
      1. DE: `QWERTZUIOPÜ*ASDFGHJKLÖÄYXCVBNM;:_` and up-numerical `°!"§$%&/()=?ˋ` (`ˋ` is replaced)
      2. EN: `QWERTYUIOP{}ASDFGHJKL:"ZXCVBNM<>?` and up-numerical `~!@#$%^&*()_+`
2. You can see equals hotkeys in column inputting. Deleting it...
   1. de: `zü+öäy-` and up-numerical `^ß´`
   2. en: `y[];'z/` and up-numerical `ˋ-=` (`ˋ` is replaced)
   3. DE: `ZÜ*ÖÄY;:_` and up-numerical `°"§&/()=?ˋ` (`ˋ` is replaced)
   4. EN: `Y{}:"Z<>?` and up-numerical `~@#^&*()_+`
3. Union variables and there are next:
   1. de: `zü+öäy-` + `ZÜ*ÖÄY;:_` + `^ß´` + `°"§&/()=?ˋ` (`ˋ` is replaced)
   2. en: `y[];'z/` + `Y{}:"Z<>?` + `ˋ-=` + `~@#^&*()_+` (`ˋ` is replaced)
4. Arrange it for plugin:
   1. Grouping:
      ```
      de: "üÜä°§" + 'ö;Ö:' + 'Ä"' + 'ß-/&^`+' + '?_' + '´=)(*' + 'zZyY'
      en: "[{'~#" + ';<:>' + '"@' + '-/&^`+]' + '_?' + '=)(*}' + 'yYzZ'
      ```
   2. Part. Fill variable by symbols and utf-8, it will be translated in ascii:
      ```
      other_keys    = "üÜä°§" + "öÖ"  + 'Ä' + 'ß'
      en_keys       = "[{'~#" + ";:"  + '"' + '-'
      other_keys_mm = ''
      ```
   3. All. Adding merge and handling ascii (fallback):
      ```
      other_keys    = "üÜä°§" + "öÖ"  + 'Ä' + 'ß'
      en_keys       = "[{'~#" + ";:"  + '"' + '-' \
                      ';:"------_====zZ'
      other_keys_mm = '<>@/`^&+]?)(*}yY'
      ```
   4. Optimization:
      ```
      other_keys    = "üÜä°§öÖ" + 'Äß'
      en_keys       = "[{'~#;:" + '"-' \
                      ';:"------_====zZ'
      other_keys_mm = '<>@/`^&+]?)(*}yY'
      ```
5. Fill variables (copy/paste) in for plugin using text from 4.4.

So, `other_keys` and `en_keys` need for translate letters for utf-8 into ascii, where translated char is a pair map `other_keys`, `en_keys`.
`other_keys_mm` need for merge keys for two or more keyboards layout (usually for intersection). Too may been used to translate ascii chars (fallback).

## Example support Ukrainian and Russian keyboard layouts
```
other_keys    = "фисвуапршолдьтщзйкыіегмцчнябюхъїжэєё'" + 'ФИСВУАПРШОЛДЬТЩЗЙКЫІЕГМЦЧНЯБЮХЪЇЖЭЄЁʼ' + '№'
en_keys       = "abcdefghijklmnopqrsstuvwxyz,.[]];''``" + 'ABCDEFGHIJKLMNOPQRSSTUVWXYZ<>{}}:""~ʼ' + '#' \
                '@$^&/&'
other_keys_mm = '";:?.,'
```

## Example support for German keyboard layouts
```
other_keys    = "üÜä°§öÖ" + 'Äß'
en_keys       = "[{'~#;:" + '"-' \
                ';:"------_====zZ'
other_keys_mm = '<>@/`^&+]?)(*}yY'
```

## Example support German, Ukrainian and Russian keyboard layouts
```
other_keys    = "фисвуапршолдьтщзйкыіегмцчнябюхъїжэєё'" + 'ФИСВУАПРШОЛДЬТЩЗЙКЫІЕГМЦЧНЯБЮХЪЇЖЭЄЁʼ' + '№' + "üÜä°§öÖ" + 'Äß'
en_keys       = "abcdefghijklmnopqrsstuvwxyz,.[]];''``" + 'ABCDEFGHIJKLMNOPQRSSTUVWXYZ<>{}}:""~ʼ' + '#' + "[{'~#;:" + '"-' \
                '@$-&/&' + '$-"------&====zZ'
other_keys_mm = '";:?.,' + '<>@/`^&+]_)(*}yY'
```

## Example way to swap keys
```
other_keys    = ""
en_keys       = "" \
                "uj"
other_keys_mm = "ju"
```

Merge mode
----------------------------------------------------------------------
Unfortunately, in order to completely abandon the merge mode, we need to know the name of the keyboard layout when a key is pressed in a message for the program.
It is assumed that this requires a modification of the Linux kernel and keyboard modules. But this would forever solve the input issue for all future console applications in any languages.
