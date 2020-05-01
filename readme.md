Support hotkeys other keyboard layouts
----------------------------------------------------------------------
It is plugin for FM [ranger](https://github.com/ranger/ranger) ;).
It allows to enable support command hotkeys for other keyboard layouts.
By default, Russian and Ukrainian are supported.
You can add or replace support your keyboard layouts for ranger.
To do this, replace the following fields: `other_keys`, `en_keys` in a file:
`~/.config/ranger/plugins/ranger_multiple_keyboard.py`
You can use merge mode (usually for `S-[0-9]`): field `other_keys_mm`.
Simple to fill in the other_keys_mm (see examples in plugin).
For ranger pager commands used only simply Engligh hotkyes.


Installation plugin for your ranger
----------------------------------------------------------------------
multiple_keyboard.py must be copied to `~/.config/ranger/plugins`


Example for Ukrainian and Russian keyboard layouts
----------------------------------------------------------------------
```
|----------+---------------+----------------------------------------|
| KEYS     | VARIABLE      | PART OF VALUE                          |
|----------+---------------+----------------------------------------|
| keys     | en_keys       | abcdefghijklmnopqrsstuvwxyz,./[]];''`` |
| keys     | other_keys    | фисвуапршолдьтщзйкыіегмцчнябю.хъїжэєё' |
|          |               |                                        |
| S-keys   | en_keys       | ABCDEFGHIJKLMNOPQRSSTUVWXYZ<>?{}}:""~~ |
| S-keys   | other_keys    | ФИСВУАПРШОЛДЬТЩЗЙКЫІЕГМЦЧНЯБЮ,ХЪЇЖЭЄЁʼ |
|          |               | @#$%^&                                 |
|          |               |                                        |
| S-234567 | other_keys_mm | "№;%:?                                 |
|----------+---------------+----------------------------------------|
```
