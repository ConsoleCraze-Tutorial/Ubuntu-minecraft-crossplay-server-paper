## Ubuntu server minecraft crossplay server

1. Install Java – Minecraft 1.21.1 requires Java 21. On your Ubuntu server, run:

```
sudo apt update
```
```
sudo apt install openjdk-21-jre-headless -y
```

2.Create the Server Directory – It’s best to keep everything in one folder

```
mkdir ~/minecraft-server
```
```
cd ~/minecraft-server
```
3. Download Paper – let's grab the latest build of 1.21.1 and rename it to keep things simple:

```
wget https://api.papermc.io/v2/projects/paper/versions/1.21.1/builds/116/downloads/paper-1.21.1-116.jar -O paper.jar
```

4. First Run & EULA – Run the server for the first time to generate the configuration files:

```
java -Xmx2G -Xms2G -jar paper.jar nogui
```
It will fail and tell you to accept the EULA. Open the file

```
nano eula.txt
```
Change eula=false to eula=true, then press Ctrl+O, Enter, and Ctrl+X to save and exit

5. Add Geyser & Floodgate
Now that the plugins folder exists, we can add the bridge for Bedrock players

```
cd plugins
wget https://download.geysermc.org/v2/projects/geyser/versions/latest/builds/latest/downloads/spigot -O Geyser-Spigot.jar
wget https://download.geysermc.org/v2/projects/floodgate/versions/latest/builds/latest/downloads/spigot -O Floodgate-Spigot.jar
cd ..
```

6. Open the Ports
You need to open both the Java port (TCP) and the Bedrock port (UDP) on your Ubuntu firewall
```
sudo ufw allow 25565/tcp
```
```
sudo ufw allow 19132/udp
```

7.Start the Server
Now you can start your server. Use this command to give it 2GB of RAM (you can increase this if your server has more)
```
java -Xmx2G -Xms2G -jar paper.jar nogui
```

