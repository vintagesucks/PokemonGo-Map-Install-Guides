### PokemonGo-Map: DigitalOcean Ubuntu 14.04. Installation

> Install [PokemonGo-Map](https://github.com/AHAAAAAAA/PokemonGo-Map) from scratch on DigitalOcean

---

#### Prerequisites for this guide
- [ ] DigitalOcean Account ([reflink](https://m.do.co/c/5585c0623c5d), [non-reflink](https://digitalocean.com/))

---

### Step 1: Create Droplet
Go to [this link](https://cloud.digitalocean.com/droplets/new?size=512mb) and create a Droplet (smallest size, Ubuntu 14.04. x64)

### Step 2: Change root password

> You can find <YourDropletIP> and current root password in an email from DigitalOcean

`ssh root@<YourDropletIP>`

Follow the instructions to change your password.

### Step 3: Setup pip, git and some prerequisites

```
apt-get update
apt-get install python-pip
pip install pyopenssl ndg-httpsclient pyasn1
apt-get install git
```

### Step 4: Clone and install PokemonGo-Map

```
git clone https://github.com/AHAAAAAAA/PokemonGo-Map.git
cd PokemonGo-Map
pip install -r requirements.txt
```

### Step 5: Get your own Google Maps API Key

Go to [this page](https://console.developers.google.com/flows/enableapi?apiid=maps_backend,geocoding_backend,directions_backend,distance_matrix_backend,elevation_backend,places_backend&keyType=CLIENT_SIDE&reusekey=true) to get your own Google Maps API Key. If you do not get your own API Key, you'll very likely run into an error telling you that you reached the daily request limit.

If you got your own API Key, open the *credentials.json* file inside the *PokemonGo-Map* folder. Replace the API Key in line 6 with the one you got from that Google website. You can edit that file directly from your shell using `nano credentials.json`.

### Step 6: Start PokemonGo-Map

Now we are ready to start the map.

A full list of parameters you can use with the map and what they mean can be found [here](https://github.com/AHAAAAAAA/PokemonGo-Map#usage). This guide will only cover the important ones:

-a: Use either `ptc` or `google` for the login  
-u: Your Username  
-p: Your Password  
-l: The location you want to scan for Pokémon. You can try something like `La tour Eiffel, Paris`, your street or exact coordinates in this format: `47.6062100 -122.3320700`  
-st: The amount of steps to take (5 steps is approximately a 1.2km radius according to [this list](https://github.com/AHAAAAAAA/PokemonGo-Map#usage))  
-ar: Auto refresh interval (in seconds), so you don't have to refresh the map all the time
-H: The host IP Address (***use your Droplet's IP***)
-P: The port to use (***use 80***)

> **Note**: It's recommended that you create a dummy account to use this Map with in order to prevent your real account from getting (soft)banned.

The final command should look like this:

`python example.py -a ptc -u johndoe -p ilovemama -H <YourDropletIP> -P 80 -l "400 Broad St, Seattle, WA 98109, USA" -st 5 -ar 10`

![Final command](https://i.imgur.com/axKgvEI.png)

Hit enter and view your map in all it's glory at your droplet's IP Address. Done!

![Map](http://i.imgur.com/EBkRhvZ.png)

---

### Bonus: How to update PokemonGo-Map
Since PokemonGo-Map is under active development and gets a lot of updates, you probably want to get all the latest features and bug fixes. You can see the latest updates (called commits) [here](https://github.com/AHAAAAAAA/PokemonGo-Map/commits/master). To update your copy, cd to your PokemonGo-Map folder, paste this command and hit enter:

`git pull origin master`

Now repeat Step 6 to restart your map.
