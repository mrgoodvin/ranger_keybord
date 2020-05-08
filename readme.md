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


Example for Ukrainian and Russian keyboard layouts
----------------------------------------------------------------------
```
|----------+---------------+----------------------------------------|
| KEYS     | VARIABLE      | PART OF VALUE                          |
|----------+---------------+----------------------------------------|
| keys     | en_keys       | abcdefghijklmnopqrsstuvwxyz,.[]];''``# |
| keys     | other_keys    | фисвуапршолдьтщзйкыіегмцчнябюхъїжэєё'№ |
|          |               |                                        |
| S-keys   | en_keys       | ABCDEFGHIJKLMNOPQRSSTUVWXYZ<>{}}:""~~  |
| S-keys   | other_keys    | ФИСВУАПРШОЛДЬТЩЗЙКЫІЕГМЦЧНЯБЮХЪЇЖЭЄЁʼ  |
|          |               | @$^&/?                                 |
|          |               |                                        |
| S-23467  | other_keys_mm | ";:?.,                                 |
|----------+---------------+----------------------------------------|
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

```
Conversion German merge table
|----+---------+--------|
| KB | CHARS   | ACTION |
|----+---------+--------|
| EN | yYzZ    |        |
| DE | zZyY    | MERGE  |
| A  | ++++    | z      |
|----+---------+--------|
| EN | -/&^`+] |        |
| DE | ß-/&^`+ | MERGE  |
| A  | -++++++ | -      |
|----+---------+--------|
| EN | _?      |        |
| DE | ?_      | MERGE  |
| A  | ++      | _      |
|----+---------+--------|
| EN | =)(*}   |        |
| DE | ´=)(*   | MERGE  |
| A  | +++++   | =      |
|----+---------+--------|
| EN | ;<      |        |
| DE | ö;      | MERGE  |
| A  | -+      | ;      |
|----+---------+--------|
| EN | :>      |        |
| DE | Ö:      | MERGE  |
| A  | -+      | :      |
|----+---------+--------|
```
