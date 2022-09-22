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
![obsidiflip_admonition-types.png](assets/obsidiflip_admonition-types.png)

| Flip Card    | Fade Card     |
| ------------ | ------------- |
| `anki`       | `cloze`       |
| `anki-front` | `cloze-front` |
| `anki-back`  | `cloze-back`  |


![obsidiflip_admonition-type-settings.png](assets/obsidiflip_admonition-type-settings.png)

### CSS

1. Go to Settings -> Appearance -> CSS Snippets and open your CSS Snippet folder.
2. Click `obsidiflip.css` in this repository, right click raw, and save as
![save-github-single-file.png](assets/save-github-single-file.png)
3. Save `obsidiflip.css` to your snippets folder

### Obsidian to Anki Plugin Settings

#### Modding the plugin to support images

Unfortunately the Obsidian to Anki plugin hasn't seen any updates in a while, so we need to edit it to support images.

## Troubleshooting


If your note type isn't showing under the obsidian to anki plugin settings, you have to either uninstall and reinstall the plugin, add the note types manually, or mod the plugin using [this commit](https://github.com/Pseudonium/Obsidian_to_Anki/pull/301). See [this issue](https://github.com/Pseudonium/Obsidian_to_Anki/issues/252) for details.