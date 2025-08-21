# 
const chapterTitle = document.querySelector('h2')?.textContent.trim();
const baseurl = i.baseurl.replace(/[^\/]+\.m3u8$/, 'index.m3u8');
const hexstring = Array.prototype.map.call(f, e => ("0"+e.toString(16)).slice(-2)).join("");
copy(`./avmake.sh "${baseurl}" ${hexstring} "${chapterTitle}"`);

Incase only hls_video no audio in index then Change url to hls_500k whatever is available then you can run these commands
BASE="https://qcdn.spayee.in/spees/w/o/63690b5de4b097305ac9980a/v/665b012f6bd90b071bddc332/u/63f37b73e4b0a71a3a615ffc/t/5cd4fc6dd76f4b14814b378185c4a56a/p/assets/videos/63690b5de4b097305ac9980a/2024/06/01/665b012f6bd90b071bddc332/"
for i in $(seq -f "%03g" 1 3500); do
  echo "${BASE}hls_500k_${i}.ts"
done > segments.txt                               
  
aria2c --quiet=true --console-log-level=error -j 16 -x 16 -s 16 -i segments.txt > /dev/null 2>&1


KEY=65d109d047d0b50ce777f5b21788977a; IV=496daa1c6914000e408c65cead91fc29; ls *.ts | xargs -P$(sysctl -n hw.ncpu) -I{} openssl aes-128-cbc -d -nosalt -in "{}" -out "dec_{}" -K "$KEY" -iv "$IV"
cat $(ls dec_hls_500k_*.ts | sort -V) > video_all.ts                                  
ffmpeg -i video_all.ts -c:v libx264 -crf 18 -preset slow -c:a aac -b:a 192k output.mp4
