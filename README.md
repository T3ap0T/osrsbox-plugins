# osrsbox-plugins

A selection of (very) basic RuneLite plugins for learning about plugin development. There are also some plugins for extracting data, such as player equipment and NPC locations. Also have been creating some new plugins to help gameplay on Ultimate Ironman mode.

## Plugins

All of the plugins in this repository have a brief summary in the subsections below. To use these plugins the following instructions should help. Note: these instructions are for Linux-based operating systems (specifically, Ubuntu 18.04), and you need the JDK and Maven installed.

```
# Install dependencies
sudo apt update
sudo apt install openjdk-11-jdk maven

# Move to a folder to download stuff
cd ~/Downloads

# Clone RuneLite development repository
git clone https://github.com/runelite/runelite.git

# Clone this repository
git clone https://github.com/osrsbox/osrsbox-plugins.git

# Copy all plugins to the RuneLite plugins folder
cp -R ~/Downloads/osrsbox-plugins/plugins/* ~/Downloads/runelite/runelite-client/src/main/java/net/runelite/client/plugins/

# Compile/build using Maven
cd ~/Downloads/runelite/ && mvn install -DskipTests

# Find the RuneLite JAR file and store in a variable
runeliteversion=$(ls -d ~/Downloads/runelite/runelite-client/target/* | grep 'shaded.jar')

# Run the compile RuneLite client (include dev tools and debugging output)
java -ea -cp net.runelite.client.RuneLite -jar $runeliteversion --debug --developer-mode
```

### plugins/bagspace

- Status: Current
- Issues: None
- Purpose: 
    - Simple overlay to display the current count of items in the player's inventory. 
    - Authored to help my UIM track bag space more easily. 
    - Might add support for the looting bag in the future.

```
plugins/bagspace
├── BagSpaceCounter.java
└── BagSpacePlugin.java
```

### plugins/currentworld

- Status: Current
- Issues: None
- Purpose: 
    - Simple overlay to show the player's current world number.

```
plugins/currentworld/
├── CurrentWorldConfig.java
├── CurrentWorldOverlay.java
└── CurrentWorldPlugin.java
```

### plugins/metadatadumper

- Status: Current
- Issues: None
- Purpose: 
    - Dump item metadata, NPC metadata and item icon images.
    - The data is the same information as contained in the ItemDefintion data that can be exported by most cache tools.

```
plugins/metadatadumper/
├── ItemMetadata.java
├── MetadataDumperConfig.java
├── MetadataDumperPlugin.java
└── NpcMetadata.java
```

### plugins/npclocations

- Status: Development
- Issues: None
- Purpose: 
    - Dump NPC world locations to JSON.
    - Needs updating and checking after attempting to plot on world map.

```
plugins/npclocations/
├── NpcLocation.java
├── NpcLocationsConfig.java
└── NpcLocationsPlugin.java
```

### plugins/itemscraper

- Status: Outdated
- Issues: 
    - Uses `org.json.simple` instead of `com.google.gson.Gson` for JSON output.
    - Is very slow compared to the new metadatadumper plugin. 
    - Needs the Simple JSON library dependency added to `runelite-client/pom.xml file`.
- Purpose: 
    - Dump item metadata and item icon images (replaced by metadatadumper).

```
plugins/itemscraper/
├── ItemScraperConfig.java
└── ItemScraperPlugin.java
```

### plugins/playerscraper

- Status: Outdated (but still works)
- Issues:
    - Uses `org.json.simple` instead of `com.google.gson.Gson` for JSON output.
    - Needs the Simple JSON library dependency added to `runelite-client/pom.xml file`.
- Purpose: 
    - Dump equipment data in JSON format of players in close location.
    - Option to dump either one player's equipment, or multiple.

```
plugins/playerscraper/
├── PlayerScraperConfig.java
├── PlayerScraperPlugin.java
└── TargetPlayer.java
```
