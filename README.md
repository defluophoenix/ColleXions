# ColleXions
ColleXions automates the process of pinning collections to your Plex home screen, making it easier to showcase your favorite content. With customizable features, it enhances your Plex experience by dynamically adjusting what is displayed, randomly.

## Key Features
- **Randomized Pinning:** ColleXions randomly selects collections to pin each cycle, ensuring that your home screen remains fresh and engaging. This randomness prevents the monotony of static collections, allowing users to discover new content easily.

- **Special Occasion Collections:** Automatically prioritizes collections linked to specific dates, making sure seasonal themes are highlighted when appropriate.

- **Exclusion List:** Users can specify collections to exclude from pinning, ensuring that collections you don't want to see on the home screen are never selected. This is also useful if you manually pin items to your homescreen and do not want this tool to interfere with those.

- **Inclusion List:** Users can specify collections to include from pinning, ensuring full control over the collections you see on your home screen.

- **Customizable Settings:** Users can easily adjust library names, pinning intervals, and the number of collections to pin, tailoring the experience to their preferences.

## Include & Exclude Collections

- **Exclude Collections:** The exclusion list allows you to specify collections that should never be pinned. These collections are "blacklisted," meaning that even if they are randomly selected or included in the special collections, they will be skipped, any collections you have manually pinned that are in this list will not be unpinned either.

- **Include Collections:** The inclusion list is the opposite of the exclusion list. It allows you to specify exactly which collections should be considered for pinning. This gives you control over which collections can be pinned, filtering the selection to only a few curated options. Make sure ```"use_inclusion_list": false,``` is set appropriately for your use case.

## How Include & Exclude Work Together 

- If the inclusion list is enabled (i.e., use_inclusion_list is set to True), the script only picks collections from the inclusion list. Special collections are added if they are active during the date range.

- If no inclusion list is provided, the script will attempt to pick collections randomly from the entire library while respecting the exclusion list. The exclusion list is always active and prevents specific collections from being pinned.

- If the inclusion list is turned off or not defined (use_inclusion_list is set to False or missing), the exclusion list will still be honored, ensuring that any collections in the exclusion list are never pinned.

## Special Collections Enforcement

- Special collections will only be pinned during their active dates. If a special collection is found outside its defined date range, it will be skipped.
This ensures that users can't pin special collections out of season (e.g., Halloween movies in December).


## Installation
Extract the files in the location you wish to run it from

Run ```pip install -r requirements.txt``` to install dependencies

Update the ```config.json``` file with your Plex URL, token, library names, and exclusion/inclusion lists. 

Run ```python3 ColleXions.py```

## Docker Run

Download the ```config.json``` and edit to your liking

https://github.com/jl94x4/ColleXions/blob/main/config.json

```
docker run -it --name ColleXions \
  -v /mnt/nvme/plexified/services/ColleXions/config.json:/app/config.json \
  -v /mnt/nvme/plexified/services/ColleXions/logs:/app/collexions.log \
  docker.io/jl94x4/collexions
```

## Docker Compose

```version: '3.8'

services:
  collexions:
    image: jl94x4/collexions
    container_name: collexions
    volumes:
      - /path/to/config.json:/app/config.json
      - /path/to/ColleXions/logs:/app/collexions.log
    restart: unless-stopped
```

Then run ```docker-compose up -d```

## Config Notes

**Pinning interval is in seconds, not minutes! In my example the field is set to 21600 which is 6 hours**

## Logging

After every run ```collexions.log``` will be created with a full log of the last successful run. It will be overwritten on each new run.

## Acknowledgments
Thanks to the PlexAPI library and the open-source community for their support.

## License
This project is licensed under the MIT License.
