# Steam_Deck_Alyx_Boot_video
Gets the non-VR version of the Valve loading screen from HL: Alyx

`curl -o - https://raw.githubusercontent.com/kageurufu/steamdeck_startup_animations/main/install.sh | bash -`

`python3 -m ensurepip
~/.local/bin/pip install --user youtube-dl`

# Video in question for your viewing pleasure

https://www.youtube.com/watch?v=ZYq6VKw3XbA

# Run

`~/.local/bin/youtube-dl -f bestvideo -o ‘ALYX.%(ext)s' https://www.youtube.com/watch?v=ZYq6VKw3XbA`
`~/.local/bin/youtube-dl -f bestaudio -o ‘ALYX.%(ext)s' https://www.youtube.com/watch?v=ZYq6VKw3XbA`

# Convert the video from whatever input formats to a webm video in VP9 encoding, with vorbis encoded audio

`ffmpeg -i ALYX.webm -i ALYX.m4a \
       -map 0:v:0  -map 1:a:0 \
       -filter:v "scale='min(1280,iw)':min'(800,ih)':force_original_aspect_ratio=decrease,pad=1280:800:(ow-iw)/2:(oh-ih)/2" \
       -c:v vp9 \
       -c:a libvorbis \
       my_deck_startup_ALYX.webm`

# Make sure the generated file is less than 1840847B here. Mine was `389670`, plenty small enough

`stat -c '%s' my_deck_startup_ALYX.webm`

# Lastly: 
`truncate -s 1840847 my_deck_startup_ALYX.webm`
