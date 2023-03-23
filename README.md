# PdXR - turn your PureData patches into XR Metaverse expierences

PdXR is an open-source implementation of PureData for multiuser Metaverse environments. 
Use a PD patch with your VR or AR devices together with other people in a shared virtual environment. 


## Dependencies

PdXR is made for [A-Frame](https://github.com/aframevr/aframe)

Run this in a Networked-Aframe instance: [Networked-Aframe](https://github.com/networked-aframe/networked-aframe)

Forks of [Aframe-Super-Keyboard](https://github.com/supermedium/aframe-super-keyboard) and [Aframe-Resonance-Audio](https://github.com/mkungla/aframe-resonance-audio-component)
are added to this project

## Usage

### Add the Aframe PdXR object to your A-Frame scene to include the PdXR runtime environment:

```html
    <a-scene>
        <a-pdxr visualize="true" src="default.pd" position="0 1 0" ></a-pdxr>
    </a-scene>
```
###### Attributes:

| Property | Description | Default |
| ------------- | ------------- | ------------- |
| src | Path and filename to the PureData patch.  | default.pd  |
| visualize | Flag if PureData patch will be visualized. GUI objects are not affected by this | true |


### Add templates of the GUI objects to your A-Scene assets:

```html
    <a-assets>
        <template id="bang-template">
          <a-entity
            geometry="primitive: box"
            material="wireframe: false; color: white"
            bang
            animation="property: material.color; from: #FFFFFF; to: #000000; dur: 50; dir: reverse; startEvents: pdbng_glow"
            animation__2="property: bang.bang;from: 1; to: 0; delay: 50; dur: 1; startEvents: pdbng_false"
          >
          </a-entity>
        </template>
        <template id="num-template">
          <a-entity
            geometry="primitive: box"
            material="wireframe: true; color: white"
            num
          >
          </a-entity>
        </template>
        <template id="sym-template">
          <a-entity
            geometry="primitive: box"
            material="wireframe: true; color: white"
            sym
          >
          </a-entity>
        </template>
        <template id="toggle-template">
          <a-entity
            geometry="primitive: box"
            material="wireframe: true; color: white"
            toggle
          >
          </a-entity>
        </template>
        <template id="sld-template">
          <a-entity
            geometry="primitive: box; height:4"
            material="wireframe:true"
            scale="0.5 0.5 0.5"
          >
            <a-entity
              geometry="primitive: box; height:0.5"
              material="wireframe:false"
              position="0 2.25 0"
              slideup
              animation="property:material.color; from: #FFFFFF; to: #000000; dur:50; dir:reverse; startEvents: pdsldup_glow"
            ></a-entity>
            <a-entity
              geometry="primitive: box; height:0.1"
              material="wireframe:false"
              position="0 0 0"
              slider
            ></a-entity>
            <a-entity
              geometry="primitive: box; height:0.5"
              material="wireframe:false"
              position="0 -2.25 0"
              slidedwn
              animation="property:material.color; from: #FFFFFF; to: #000000; dur:50; dir:reverse; startEvents: pdslddwn_glow"
            ></a-entity>
          </a-entity>
        </template>
    </a-assets>
```


### Add templates the Networked-Aframe NAF.shemas: 


```javascript
        if (!NAF.schemas.hasTemplate("#bang-template")) {
          NAF.schemas.add({
            template: "#bang-template",
            components: [
              "position",
              {
                component: "bang",
                property: "bang",
              },
            ],
          });
        }
        if (!NAF.schemas.hasTemplate("#toggle-template")) {
          NAF.schemas.add({
            template: "#toggle-template",
            components: [
              "position",
              {
                component: "material",
                property: "wireframe",
              },
              {
                component: "toggle",
                property: "toggle",
              },
            ],
          });
        }
        if (!NAF.schemas.hasTemplate("#sld-template")) {
          NAF.schemas.add({
            template: "#sld-template",
            components: [
              "position",
              {
                component: "pdsld",
                property: "value",
              },
            ],
          });
        }
        if (!NAF.schemas.hasTemplate("#num-template")) {
          NAF.schemas.add({
            template: "#num-template",
            components: [
              "position",
              {
                component: "num",
                property: "value",
              },
            ],
          });
        }
        if (!NAF.schemas.hasTemplate("#sym-template")) {
          NAF.schemas.add({
            template: "#sym-template",
            components: [
              "position",
              {
                component: "sym",
                property: "value",
              },
            ],
          });
        }
```

## Develope compatible PD patches




## Run on Glitch

Run or remix Metabeat on Glitch: [PdXR Example](https://pdxr.glitch.me/)


## Acknowledgements

PdXR ist based on [PdWebParty](https://github.com/cuinjune/PdWebParty) by Zack Lee, integrating the [PureData](https://github.com/pure-data/) programming language.
