# Nativefier

A fork from https://github.com/jiahaog/nativefier. I've just added a thing for myself where i can create a new menu item from a config.json in the root directory.

## config.json

the config.json contains basically this structure:

```json
{
    "Menutitle" : "The label that the menu item will get",
    "submenu" : [
    {..},
    {..},
    {..}
   ]
}
```

There are three types of entries to put in the root submenu:
### 1. normal entry 
Each single entry must have an unique id, a label and the corresponding url + their entry type.
```json
{
    "id": "yahoo",
    "label": "Yahoo",
    "url": "https://www.Yahoo.de",
    "type": "entry"
}
```
### 2. separator
separators just need their type specified:
```json
{
    "type": "separator"
}
```
### 3. submenus
A submenu needs a label, the type "submenu" and an array *submenu*. This array can contain more entries, separators or even more submenus.
```json

{
    "label": "Submenu 1",
    "type": "submenu",
    "submenu": [
        {
            "id": "google",
            "label": "Google",
            "url": "https://www.google.de",
            "type": "entry"
        },
        {
            "label": "Submenu in submenu",
            "type": "submenu",
            "submenu": [
                {
                    "id": "amazon",
                    "label": "Amazon",
                    "url": "https://www.amazon.de",
                    "type": "entry"
                }
            ]
        }

    ]
}
``` 

### 4. Example json.config

```
{
    "Menutitle" : "Bookmarks",
    "submenu" : [
        {
            "id": "github",
            "label": "Github",
            "url": "https://www.github.com",
            "type": "entry"
        },
        {
            "type": "separator"
        },
        {
            "id": "yahoo",
            "label": "Yahoo",
            "url": "https://www.Yahoo.de",
            "type": "entry"
        },
        {
            "label": "Submenu",
            "type": "submenu",
            "submenu": [
                {
                    "id": "google",
                    "label": "Google",
                    "url": "https://www.google.de",
                    "type": "entry"
                },
                {
                    "label": "Submenu in submenu",
                    "type": "submenu",
                    "submenu": [
                        {
                            "id": "amazon",
                            "label": "Amazon",
                            "url": "https://www.amazon.de",
                            "type": "entry"
                        }
                    ]
                }

            ]
        }
    ]
}
```

## how to use / install

open a terminal.
```mkdir temp
cd temp
git clone https://github.com/Sarimon/nativefier.git
cd ./nativefier
``` 
put now the config.json in exactly this folder.

```
npm install
npm run build
sudo npm link
cd ..
npm link "nativefier"
``` 

See the original github page for instructions. Basically for our purposes, the comman is like this:
```
nativefier -n <App name> -p linux -a x64 --show-menu-bar --internal-urls "<a regex defining what is an internal url>" <target URL to nativefy> <target path>
``` 
for example:

```
nativefier -n "Webex Hs-Mannheim" -p linux -a x64 --show-menu-bar --internal-urls ".*.webex.com.*|.*web.zoom.us.*" https://hs-mannheim.webex.com/ . 
```

now there should be a new folder like ``./<Appname>-linux-x64/``. Inside, there is an executable``<Appname>`` file. in our case:

```json
./WebexHs-Mannheim-linux-x64/WebexHs-Mannheim 
```

## License

[MIT](LICENSE.md)
