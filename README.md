# Visualizing Hayabusa 2 Mission in OpenSpace

This is an additional file of Open Space that I created during my internship at the American Museum of Natural History.
アメリカ自然史博物館(AMNH) Computer Visualization Group 制作物

![Visualizing Hayabusa 2 Mission](https://github.com/payopayouhuh/Visualizing-Hayabusa-2-Mission-in-OpenSpace/assets/134220954/a1217937-79c8-47f5-9241-a775148a9a50)


## Configuration Files

To run this package, place each folder in the following location.
1. `mission.asset`: Contains data for mission panel and timeline.
2. `HAYABUSA2.profile`: `C:\OpenSpace\OpenSpace-0.19.0\user\data\profiles`
3. `Hayabusa2`: `C:\OpenSpace\OpenSpace-0.19.0\user\data\assets`
4. `hayabusa2_labels`: `C:\OpenSpace\OpenSpace-0.19.0\sync\http`
5. `slide_image`: `C:\OpenSpace\OpenSpace-0.19.0\sync\http`

## Data Source
This visualization is based on Hayabusa 2 SPICE data for the surveying and collection phase of the mission. 
- **Hayabusa 2**: 2014/12/03 to 2019/02/13
- **Target asteroid Ryugu**: 2014/01/01 to 2021/01/01

[**SPICE kernel data on JAXA**](https://data.darts.isas.jaxa.jp/pub/hayabusa2/spice_bundle/) (Last updated: 2020-03-11)

[Documentation](https://data.darts.isas.jaxa.jp/pub/hayabusa2/spice_bundle/document/spiceds_v001.html)

## How to Browse the Data
1. Visit [NAIF Utilities](https://naif.jpl.nasa.gov/naif/utilities.html) and download "brief.exe" suitable for your PC.
2. Search for "Edit the system environment variables" on your PC, and choose "Environment Variables".
3. Add a new System Variable named “CSPICE” as depicted in the referenced image.
4. Open Command Prompt and navigate to where your “brief.exe” file is located.
5. Execute commands as mentioned in the repository for accessing data.

## Visualization Process
Steps we undertook:
- Used a reference script (e.g., `venuslabel.asset`) to determine label properties.
- Adjusted properties like FontSize, Size, MinMaxSize, FadeUnit, FadeDistances, and FadeWidths for better visualization.
  
Details:
FontSize = 70.0
Size = 8.5
MinMaxSize = { 1, 40 }
FadeUnit = "au"
FadeDistances = { 1.5, 25.0 }
FadeWidths = { 1.0, 35.0 }


## Mission Panel
The Mission Panel contains:
- Overview of the mission
- Photos 
- Interactive timeline with milestones and mission phases
- Functional buttons like "Set Focus to Hayabusa 2", "Fly to Ryugu", and more.

## Mission.asset

This file contains the information displayed in the mission panel and mission timeline.
This file can be found in C:\OpenSpace\OpenSpace-0.19.0\user\data\assets\Hayabusa2\Hayabusa2
The variables present in this file are explained below.
Name: A short name for the phase or milestone.
- Date: Date and time the specific milestone took place
- TimeRange: Indicates the start and end dates and times when a particular phase took place
- Image: attach up to one photo that symbolizes the phase or milestone.
- Tips: “mission.asset” file only takes a URL to load images.So you can’t add photos locally.
- Description: Description of the phase or milestone
- Actions: The actions described here are added as buttons within the mission panel. Actions must be defined in other files.
- Link: This can be used when the Description alone is not sufficient.The link listed here will appear as buttons in the mission panel, and clicking the button will take you to the designated link.


## Mission Timeline
**Milestones**:
We highlighted five major events. Each milestone has a detailed description and associated image.

**Phases**:
Four phases of the mission are described in detail, each accompanied by a relevant image.

*For more details and sources, refer to: [JAXA Hayabusa 2 Mission Website] and [JAXA Hayabusa 2 Image Gallery]*

## slidedeck
This asset contains a set of screen space images related to the Hayabusa2 mission, including images of the return capsule, the Hayabusa2 spacecraft, the Crab Nebula, and various other related visual elements.

### Files
- **slide_image.asset**: Contains paths to slide images.
- **slidedeck.asset**: Contains details about slide decks.

### Images

- **Capsule Image**: An image showing the return capsule. File: `return_capsule_1.jpg`
- **Itokawa and Ryugu to Scale Image**: A comparative image of the two asteroids. File: `itokawa-and-ryugu-to-scale.png`
- **ONC Image**: File: `ONC.png`
- **MASCOT Image**: File: `MASCOT.png`
... etc ...

### Usage

To initialize and utilize this asset in OpenSpace:

```lua
asset.onInitialize(function()
  openspace.addScreenSpaceRenderable(CapsuleImage)
  ...etc
end)
To deinitialize:

asset.onDeinitialize(function()
  openspace.removeScreenSpaceRenderable(CapsuleImage)
  ... etc ...
end)

```
### How to add images to a slide deck
#### Add images
If you want to add images to your slide deck, use the helper.addSlide function.

example
```

  helper.addSlide(deck, slide_image.image .. "image1.png")
  helper.addSlide(deck, slide_image.image .. "image2.png")
  helper.addSlide(deck, slide_image.image .. "image3.png")
  helper.addSlide(deck, slide_image.image .. "etc.jpg")

```

This will add the specified image to your slidedeck.asset

#### Image reference destination
In the above code, slide_image.image is used as the base path for the image. I need to add the image at that file location

example
- C:\OpenSpace\OpenSpace-0.19.0\sync\http\slide_image\image1.png

This will load images from the specified location within your OpenSpace directory andasset display them as slides.

### Metadata
Name: Hayabusa2 Return Capsule
Version: 1.0
Author: NASA, ESA and Allison Loll/Jeff Hester (Arizona State University). Acknowledgement: Davide De Martin (ESA/Hubble)
URL: Hayabusa2 Details
License: CC BY 4.0
Dependencies
Util/Slide Deck Helper: A utility to handle slide decks in OpenSpace.
Controls

### slideaction
nextSlide(): Move to the next slide.
previousSlide(): Move to the previous slide.
toggleSlides(): Show or hide the slides.
go



## HAYABUSA2.profile
This profile is specialized in learning about and explaining HAYABUSA2

### Features:
- Addition of elements described on this page.
- Initial start at HAYABUSA2's position.
- Addition of various actions and shortcut keys.


### Examples:
```json
"keybindings": [
  {
    "action": "nextslide",
    "key": "CTRL+RIGHT"
  },
  {
    "action": "prevslide",
    "key": "CTRL+LEFT"
  },
  {
    "action": "slide_decktoggleslides",
    "key": "CTRL+DOWN"
  },
  {
    "action": "hayabusa2Focus",
    "key": "CTRL+V"
  },

]

```

## Additional Resources
- OpenSpace Wiki Pages
- Documentation found in local OpenSpace folder: `OpenSpace/OpenSpace-<your version>/documentation/index.html`

## References
- [Hayabusa 2 Data Archive, Planetary Data System (PDS) Small Bodies Node]
- [Hayabusa 2’s Data Management Plan]
- [Asteroid Explorer Hayabusa 2, Institute of Space and Astronautical Science]

![image](https://github.com/payopayouhuh/Visualizing-Hayabusa-2-Mission-in-OpenSpace/assets/134220954/2f60bd60-9cd3-434d-a7be-dfc0d04f0efb)

![image](https://github.com/payopayouhuh/Visualizing-Hayabusa-2-Mission-in-OpenSpace/assets/134220954/7fb90d0e-fedb-43ad-941b-fd192df92f20)

