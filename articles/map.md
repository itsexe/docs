# .map files

Map files are XML files with this architecture :

Name | Contains
--- | -----------
STAGE_HEADER   | Main informations
ALL_TRACK  | ?
ALL_BUMP  | grinds ?
ALL_PROP   | 3D items (nx3) placed
ALL_DIR   | ?
ALL_VIS   | ?
ALL_SOUNDOBJECT   | Placed sound objects
ALL_SOUNDENVOBJDATA   | ?
BGM_SOUND   | Background music for the map
ALL_PROP   | ?

## General

The root of the file is kept under :
```
<?xml version="1.0" ?>
    <ROOT>
        Here comes the content
    </ROOT>
```

## Stage Header

```
    <STAGE_HEADER>
        <STAGE nVersion="1" nLevel="3" szStageName="backstreet" />
    </STAGE_HEADER>
```
nVersion is "1" for all maps, nLevel is always one of {1,2,3}. This is the required licence to go (to confirm)

## ALL_TRACK

```
    <ALL_TRACK>
    </ALL_TRACK>
```

ALL_Track contains the list of tracks for the race. They are defined as this :
### Tracks
```
    <Track nTrack_ID="0" szTrackFileName="Halem_track01.nx3" vMin="-342,-802,-1" vMax="265,-88,20">
    </Track>
```

Tracks contains a list of items from the nx3 selected (i guess)

### Bumps

```
    <Bump type="BARRIER">
 115 116 117 118 119 120 121 122 123 124 125 126 127 128 143 144 145 146 147 148 149 150 155 156 157 158 159 160 161 162 163 164 366 367 370 371 372 373 396 397 412 413 414 415 416 417 818 819 820 821 822 823 824 825 826 827 828 829 
    </Bump>
```
> There is usually no new line after <Bump type="BARRIER>.

Most used BUMP types (you can have as much as you want (see later how it's defined)) :
- BARRIER
- BARRIER1
- TOP
- BOTTOM
- BOTTOM2 (Goes up to BOTTOM6)
- STAIR
- GRIND
- VERT
- VERT1
- VERT2
- RESPAWN

We can add our own types in map files, as they are defined below in the file, in ALL_BUMP

Bump then contains a lot of numbers that represents IDs.
> // IDs are linked with nIndex in nGroup ?

## ALL_BUMP

ALL_BUMP lists all bumps in the file
```
    <ALL_BUMP>
    </ALL_BUMP>
```

### BUMP
BUMP defines an item, with an nx3 filename and an id the file can refer to to add items.
```
<BUMP type="BOTTOM" szBumpFileName="Halem_bottom_polygon.nx3" />
```
> For example, the line
> <BUMP type="BOTTOM"></BUMP> (see previously)
> Will refer to the item in file Halem_bottom_polygon.nx3

## ALL_PROP

Here, again another container for a list of items.
```
<ALL_PROP>
</ALL_PROP>
```

### Items contained :
Opposed to ALL_BUMP, ALL_PROP contains multiple children type. There are not sorted by their name or content.

type | content
----|----
PROP | default element placed on the map
INDOORBOX | ?
ANIBOARD | "Advertisement panel"
Example of [Advertisement panel](http://img15.hostingpics.net/pics/12690803CFCE576EA520063F3125579D276D2B7198D2EBED559FA64Fpimgpshmobilesavedistr.jpg)

All of them store the same infos. I removed the decimal part because it was not relevant. They are separated by ".".
example : vMin="31.2,110.5,54.3"
```
<PROP szPropFileName="Halem_BillTree30_bill.nx3" vMin="36,-1107,-180" vMax="490,-652,159" />
```
```
<INDOORBOX szPropFileName="Halem_box01_indoorbox01_polygon.nx3" vMin="704,267,45" vMax="1189,623,178" />
```
```
<ANIBOARD szPropFileName="Halem_sign10_06.nx3" vMin="270,1322,98" vMax="327,1337,124" />
```

## ALL_DIR

Regroups a list of Dir and DirGroup

### Dir

// TODO : What is it exactly ?
isEnable is always set to "1"
Direction is always set to "0"
DirGroup is defined below.
```
<Dir nGroup="1" nIndex="0" IsEnable="1" Direction="0" fLength="10512" vStart="118,-389,15" vEnd="119,-349,15">
        <Prev>321 </Prev>
        <Next>1 </Next>
</Dir>
```

nIndex is unique
<Prev> and <Next> can contain multiple values, separated by a space. Than can be empty too. Still present under <Prev /> and </Next> form.

### DirGroup

???
```
<DirGroup nFrom="0" nTo="1" />
```
Each line is unique, but this is possible :
```
<DirGroup nFrom="1" nTo="2" />
<DirGroup nFrom="1" nTo="3" />
<DirGroup nFrom="1" nTo="4" />
```

## ALL_VIS

This can be empty on some maps (backstreet for example)

```
 <ALL_VIS>
 </ALL_VIS>
```
```
<ALL_VIS />
```

### VIS

// TODO : NO IDEA
```
<VIS nFrom="5" nTo="6" />
```

## BGM_SOUND

Background music for the map. No content, only one declaration line.
```
<BGM_SOUND strBGM="map_rand_bgm" />
```

## ALL_SOUNDGROUP

Contains a list of <SND_GROUP>
```
<ALL_SOUNDGROUP>
</ALL_SOUNDGROUP>
```

### SND_GROUP
```
<SND_GROUP strGroupName="noise" strGroupSoundFile="envi_noise.wav" />
```
A bit like Dump, but for sound, assigns strGroupName to strGroupSoundFile to access the second by referring the first.

## ALL_SOUNDOBJECT

Contains a list of <SND_OBJECT>
```
<ALL_SOUNDOBJECT>
</ALL_SOUNDOBJECT>
```

### SND_GROUP
```
<SND_OBJECT strObjectName="wind_curve" strObjectSoundFile="wind_curve.wav" />
```
A bit like Dump, but for sound, assigns strObjectName to StrObjectSoundFile to access the second by referring the first.

## ALL_SOUNDDIR
```
<ALL_SOUNDDIR>
</ALL_SOUNDDIR>
```

### SND_DIR
```
<SND_DIR vStart="-111,573,-36" nDirIndex="0" GroupA_VolLR="3:100,100" GroupB_VolLR="0:0,0" Reverb_DryWet="0:100,0" Road="asphalt" />
```

Name | Goal
----|----
vStart | Position of the sound
nDirIndex | ?
GroupA_VolLR | Sound volume ?
GroupB_VolLR | ?
Reverb_DryWet | ?
Road | sound to play depending on road

Road can be one of these : {asphalt, block, ground} 

SND_DIR can contain a sub-object of type SND_OBJ_DATA

#### SND_OBJ_DATA

```
<SND_OBJ_DATA nObjectID="0" nDist="50" vPos="-1076.433594,425.663239,46.561035" nLocation="2" bRate="1" />
```
Name | Goal
---- | ----
nObjectID | (int) Unique Identifier
nDist | ? (int)
vPos | ? (position)
nLocation | ? (int)
bRate | ? (int) (1 most of the time)

## ALL_SOUNDENVOBJDATA
This can be empty
```
<ALL_SOUNDENVOBJDATA>
</ALL_SOUNDENVOBJDATA>
```
```
<ALL_SOUNDENVOBJDATA />
```

> Empty most of the time

## ALL_SHADOWCOLOR
```
<ALL_SHADOWCOLOR>
</ALL_SHADOWCOLOR>
```
> This represents more than 50% of the ground_r.map file !!

> This contains SHADOWCOLOR or PVS_INFO. Those two are mutually exclusive !

### SHADOWCOLOR
> There is not multiple SHADOWCOLOR in a single file
```
<SHADOWCOLOR szShadowBoxFileName="IQ_shadowbox_polygon.nx3" Color="85,85,85" />
```
Name | Goal
---- | ----
szShadowBoxFileName | (filename) ?
Color | (rgb) Color of shadow ?

### PVS_INFO
> There is not multiple PVS_INFO in one single file
```
<PVS_INFO vtMin="-394,-973,-3" vtMax="1697,126,139" fCellSize="100.000000" numCellsInX="21" numCellsInY="11" numCellsInZ="2">
</PVS_INFO>
```

Name | Goal
---- | ----
vtMin | ? (pos)
vtMax | ? (pos)
fCellSize | ? (float)
numCellsInX | ? (int)
numCellsInY | ? (int)
numCellsInZ | ? (int)

> numCellsIn? probably refers to the resolution used to apply shadows to the render

PVS_INFO contains PVSCELL_INFO

#### PVSCELL_INFO

```
<PVSCELL_INFO nIndex="228" vtMin="1405,26,-3" vtMax="1505,126,96">
            <VisTracks>0 </VisTracks>
            <VisPropDiffs>-21 </VisPropDiffs>
        </PVSCELL_INFO>
```

Name | Goal
---- | ----
nIndex | (int) unique ID
vtMin | ? (pos)
vtMax | ? (pos)

VisTracks and VisPropDiffs can be empty, they'll be under this form : <VisTracks /> and <VisPropDiffs />
