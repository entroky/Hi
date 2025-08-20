# 
const chapterTitle = document.querySelector('h2')?.textContent.trim();
const baseurl = i.baseurl.replace(/[^\/]+\.m3u8$/, 'index.m3u8');
const hexstring = Array.prototype.map.call(f, e => ("0"+e.toString(16)).slice(-2)).join("");
copy(`./avmake.sh "${baseurl}" ${hexstring} "${chapterTitle}"`);
