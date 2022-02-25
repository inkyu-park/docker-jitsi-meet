## Jibri 세팅
````
# install the module
sudo apt update
sudo apt install linux-image-extra-virtual

# configure 5 capture/playback interfaces
sudo echo "options snd-aloop enable=1,1,1,1,1 index=0,1,2,3,4" > /etc/modprobe.d/alsa-loopback.conf

# setup autoload the module
sudo echo "snd-aloop" >> /etc/modules

# check that the module is loaded
sudo lsmod | grep snd_aloop
````

## docker 세팅
````
cp env.example .env

./gen-passwords.sh

mkdir -p ~/new-live-learning/docker-jitsi-meet/.jitsi-meet-cfg/{web/crontabs,web/letsencrypt,transcripts,prosody/config,prosody/prosody-plugins-custom,jicofo,jvb,jigasi,jibri}

# Jibri, etherpad 추가 기동
docker-compose -f docker-compose.yml -f etherpad.yml -f jibri.yml up -d
docker-compose -f docker-compose.yml -f etherpad.yml -f jibri.yml down

# Jitsi만 기동
docker-compose -f docker-compose.yml up -d
docker-compose -f docker-compose.yml down
````

## web 세팅
````
sudo docker cp dockerjitsimeet_web_1:/config/config.js ./config.js
sudo docker cp dockerjitsimeet_web_1:/config/interface_config.js ./interface_config.js

docker cp ~/new-live-learning/jitsi-meet/css/all.css dockerjitsimeet_web_1:/usr/share/jitsi-meet/css/all.css
docker cp ~/new-live-learning/jitsi-meet/css/all.bundle.css.map dockerjitsimeet_web_1:/usr/share/jitsi-meet/css/all.bundle.css.map
for f in ~/new-live-learning/jitsi-meet/libs/*; do docker cp $f dockerjitsimeet_web_1:/usr/share/jitsi-meet/libs/; done
````

