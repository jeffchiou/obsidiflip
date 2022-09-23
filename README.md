
![Obsidiflip Banner Black Gold Neuron Flashcards](assets/black-gold-neuron-flashcards_stable-diffusion.png)[^1]

# Obsidiflip Readme

Interactive Obsidian-Anki flashcards that flip and fade using CSS and two plugins.
Current status: WIP - writing instructions and demo.

## Demo

## Prerequisites

Please have these apps and plugins installed and working.
- [Obsidian](https://obsidian.md/)
- [Anki](https://apps.ankiweb.net/)
- Obsidian Plugins
	- [Obsidian to Anki](https://github.com/Pseudonium/Obsidian_to_Anki)
		- Requires Anki plugin [Anki Connect](https://ankiweb.net/shared/info/2055492159)
	- [Obsidian Admonition](https://github.com/valentine195/obsidian-admonition)

## Installation and Usage

### Admonition Plugin Settings

In the admonition plugin settings, please add these 6 admonition types. Feel free to customize the title, title display option, copy button, icon, and color, but don't change the admonition type unless you plan to modify the CSS and regex.
![Obsidiflip Admonition Types](assets/obsidiflip_admonition-types.png)

| Flip Card    | Fade Card     |
| ------------ | ------------- |
| `anki`       | `cloze`       |
| `anki-front` | `cloze-front` |
| `anki-back`  | `cloze-back`  |


![Obsidiflip Admonition Type Settings](assets/obsidiflip_admonition-type-settings.png)

### CSS

1. Go to Settings -> Appearance -> CSS Snippets and open your CSS Snippet folder.
2. Click `obsidiflip.css` in this repository, right click raw, and save as
![Save Github Single File](assets/save-github-single-file.png)
3. Save `obsidiflip.css` to your snippets folder, refresh the CSS settings, and enable it.

### Obsidian to Anki Plugin Settings
#### Regex and corresponding sample flashcards
##### Revealed Context
I use this when I want to reveal context on the back of the card.
###### Markdown
``````
`````ad-anki
%%anki-revealed-context%%
````ad-anki-front
front
````
````ad-anki-back
back
***
revealed
````
`````
``````

###### Regex
```
`````ad-anki[\s\S]+?%%anki-revealed-context%%[\s\S]+?````ad-anki-front\n([\s\S]*?)````[\s\S]+?````ad-anki-back\n([\s\S]*?)(?:\*\*\*\n([\s\S]*?))?````
```

##### Complex

I don't actually use this card. It's for demo purposes to show the flexibility of the format. The last `***` is necessary to avoid keep the id within `ad-anki` and allow for flashcards next to each other.

###### Markdown

``````
`````ad-anki
title:Complex Flashcard
%%anki-complex%%

````ad-anki-front
this is the front of the card
***
this context should show up on the front of the card
````

````ad-anki-back
this is the back of the card
***
this context should show up on the back of the card
````
this shows up on both sides
***
`````

``````
###### Regex
```
`````ad-anki[\s\S]+?%%anki-complex%%[\s\S]+?````ad-anki-front\n([\s\S]*?)(?:\*\*\*\n([\s\S]*?))?````[\s\S]+?````ad-anki-back\n([\s\S]*?)(?:\*\*\*\n([\s\S]*?))?````\n([\s\S]*?)\*\*\*\n
```
##### Forward (Basic)
```
`````ad-anki[\s\S]+?%%anki-forward%%[\s\S]+?````ad-anki-front\n([\s\S]*?)````[\s\S]+?````ad-anki-back\n([\s\S]*?)````
```




`````ad-anki
%%anki-basic-anking%%
````ad-anki-front
front
````
````ad-anki-back
back
***
personal notes
***
missed questions
````
`````


#### Modding the plugin to support images

Unfortunately the Obsidian to Anki plugin hasn't seen any updates in a while, so we need to edit it to support images. [https://github.com/Pseudonium/Obsidian_to_Anki/issues/245](https://github.com/Pseudonium/Obsidian_to_Anki/issues/245) Open `main.js` in your favorite editor, and comment out the `getAndFormatMedias` function (as backup). Add this right under it:

```js
    getAndFormatMedias(note_text) {
      // By Jeff Chiou thanks to TobiasKlosek's code https://github.com/Pseudonium/Obsidian_to_Anki/issues/245
      // TODO: support image resize format (ex. ![[og-image.png|200]])
      // PLAN: create escaped regex pattern for images and audio to capture link and size separately. Add style tag to <img>.
      let hasAudio = AUDIO_EXTS.some(ext => note_text.includes(ext));
      let hasImage = IMAGE_EXTS.some(ext => note_text.includes(ext));

      if (hasAudio || hasImage) {
        let matches = note_text.match(/\!\[\[(.*)\]\]/g);
        matches.forEach(match => {          
          let link = match.substring(3, match.length - 2);

          this.detectedMedia.add(link);
          if (AUDIO_EXTS.includes(path.extname(link))) {
            note_text = note_text.replace(new RegExp(escapeRegex(match), "g"), "[sound:" + path.basename(link) + "]");
          }
          else if (IMAGE_EXTS.includes(path.extname(link))) {
            note_text = note_text.replace(new RegExp(escapeRegex(match), "g"), '<img src="' + path.basename(link) + '" alt="' + link + '">');
          }
          else {
            console.warn("Unsupported extension: ", path.extname(link));
          }
        });
      }
      return note_text;
    }
```

I have plans to mod the plugin further but it is GPL licensed and this repo is MIT, so I might make a new repo so I can include a `main.js` file.[^2]

## Troubleshooting

If your note type isn't showing under the obsidian to anki plugin settings, you have to either uninstall and reinstall the plugin, add the note types manually, or mod the plugin using [this commit](https://github.com/Pseudonium/Obsidian_to_Anki/pull/301). See [this issue](https://github.com/Pseudonium/Obsidian_to_Anki/issues/252) for details.

[^1]: Generated by Stable Diffusion locally on my laptop RTX 3080, which has 16gb of VRAM! Prompt was a variant of "thin shiny sharp black obsidian flashcards with shiny gold neurons on the front."

[^2]: I don't have the resources and knowledge to support a full fork yet.